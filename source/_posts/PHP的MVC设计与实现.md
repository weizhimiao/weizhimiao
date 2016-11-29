---
title: PHP魔术方法小结
date: 2016-10-12 22:30:00
tags:
- MVC
categories:
- PHP
---

MVC模式，即模型-试图-控制器模式，是将应用程序划分成不同层次的一种方式。

即，

C | Control |控制器层  |负责业务逻辑的处理。根据用户的请求确定用户可以做什么。之后，调用模型执行操作获得数据。最后调用视图将操作结果呈现给用户。
--|---------|---------|------
M | Model   |模型层    |负责加工处理数据 返回结果。
V | View    |视图层    |负责接收信息和显示信息。

一个典型MVC应用程序流程图

![典型MVC应用程序流程图](http://n.sinaimg.cn/games/3ece443e/20161013/mvcYingYongChengXuLiuChengTu.png)

<!-- more -->

## 简单实现：

### 文件结构：
```
$ tree shop         
shop
├── Control
│   ├── FlinkControl.class.php
│   ├── GoodsControl.class.php
│   ├── IndexControl.class.php
│   ├── NewsControl.class.php
│   ├── OrderControl.class.php
│   └── UserControl.class.php
├── Model
│   ├── MemcacheModel.class.php
│   └── MysqlModel.class.php
├── Org
│   └── Vcode.class.php
├── Views
├── index.php
└── readme

4 directories, 11 files
```

### 说明：
```
Model  文件夹    模型层的Model类（操作数据 MYSQL、Memcached...）
Org    文件夹	  模型层的其他类(不操作数据 分页/验证码...)
Controls文件夹	  控制器层的类
Views  文件夹	  视图层(html页面)
```

### 主要文件内容：
index.php

```php
<?php
	//类的自动加载
	function __autoload($className){

		//包含控制器的类
		if(strtolower(substr($className,-7))=='control'){
			include 'Control/'.$className.'.class.php';
		}elseif(strtolower(substr($className,-5))=='model'){
			include 'Model/'.$className.'.class.php';
		}else{
			include 'Org/'.$className.'.class.php';
		}
	}

	//如何调用控制器
	//index.php?m=user&a=add      表示调用用户类中的添加用户方法
	//index.php?m=goods&a=drop    表示调用商品类中的删除商品方法

	//index.php?m=user&a=add  

	//m=user ->调用UserControl类
	$class=!empty($_GET['m'])?strtolower($_GET['m']):'Index';//$class=user;
	$class=ucfirst($class);//$class=User;
	$class.='Control';//$class=UserControl

	//a=add -> add
	$method=!empty($_GET['a'])?strtolower($_GET['a']):'index';
	$one=new $class;
	$one->$method();
?>
```

Control/UserControl.class.php

```php
<?php
	class UserControl{
		//控制器不需用属性！！！1

		//默认的方法index
		function index(){
      //实例化一个模型层的扩展类
			echo new Vcode;
			echo '显示用户列表';
		}

		//添加用户
		function add(){
      //调用Model 查询友情连接信息
			$mysql=new MysqlModel;
			//调用Model类的方法
			$mysql->insert();

			echo '添加用户操作';
		}

		//删除用户
		function drop(){
			echo '删除用户操作';
		}

		//修改用户
		function mod(){
			echo '修改用户操作';
		}

		//查询用户
		function show(){
			echo '查询用户操作';
		}

	}

```
Model/MysqlModel.class.php

```php
<?php

	class MysqlModel{

		//连接数据库的方法
		function __construct(){
			echo '连接数据库中<br>';
		}

		//使用数据库进行查询操作
		function select(){
			echo '使用数据库进行查询操作<br>';
		}

		//使用数据库进行删除操作
		function delete(){
			echo '使用数据库进行删除操作<br>';
		}

		//使用数据库进行修改操作
		function update(){
			echo '使用数据库进行修改操作<br>';
		}

		//使用数据库进行添加操作
		function insert(){
			echo '使用数据库进行添加操作<br>';
		}

		function __destruct(){
			echo '断开数据库连接';
		}

	}
```

Org/Vcode.class.php

```php
<?php
	class  Vcode {
		private $width;                               //验证码图片的宽度
		private $height;                              //验证码图片的高度
		private $codeNum;                             //验证码字符的个数
		private $disturbColorNum;                     //干扰元素数量
		private $checkCode;                           //验证码字符
		private $image;                               //验证码资源

		/**
		 * 构造方法用来实例化验证码对象，并为一些成员属性初使化       
		 * @param	int	$width		设置验证码图片的宽度，默认宽度值为80像素        
		 * @param	int	$height		设置验证码图片的高度，默认高度值为20像素       
		 * @param	int	$codeNum	设置验证码中字母和数字的个数，默认个数为4个  
		 */
		function __construct($width=80, $height=20, $codeNum=4) {
			$this->width=$width;                     //为成员属性width初使化
			$this->height=$height;                     //为成员属性height初使化
			$this->codeNum=$codeNum;               //为成员属性codeNum初使化
			$number=floor($height*$width/15);
			if($number > 240-$codeNum)
				$this->disturbColorNum=240-$codeNum;
			else
				$this->disturbColorNum=$number;
			$this->checkCode=$this->createCheckCode();  //为成员属性checkCode初使化
		}
		/**
		 * 用于输出验证码图片，也向服务器的SESSION中保存了验证码
		 * 使用echo 输出对象即可
		 * @return string	验证码
		 */

		function __toString(){
			$_SESSION["code"]=strtoupper($this->checkCode);  //加到session中
			$this->outImg();              //输出验证码
			return '';
		}

		private function outImg(){                       //通过访问该方法向浏览器中输出图像
			$this->getCreateImage();                 //调用内部方法创建画布并对其进行初使化
			$this->setDisturbColor();                 //向图像中设置一些干扰像素
			$this->outputText();                     //向图像中输出随机的字符串
			$this->outputImage();                    //生成相应格式的图像并输出
		}


		private function getCreateImage(){              //用来创建图像资源，并初使化背影
			$this->image=imagecreatetruecolor($this->width,$this->height);

			$backColor = imagecolorallocate($this->image, rand(225,255),rand(225,255),rand(225,255));    //背景色（随机）
			 @imagefill($this->image, 0, 0, $backColor);

			$border=imageColorAllocate($this->image, 0, 0, 0);
			imageRectangle($this->image,0,0,$this->width-1,$this->height-1,$border);
		}
		private function createCheckCode(){           
			//随机生成用户指定个数的字符串,去掉了容易混淆的字符oOLlz和数字012
			$code="3456789abcdefghijkmnpqrstuvwxyABCDEFGHIJKMNPQRSTUVWXY";
			for($i=0;$i<$this->codeNum;$i++) {
				$char=$code{rand(0,strlen($code)-1)};

				$ascii.=$char;
			}
			return $ascii;

		}
		private function setDisturbColor() {    
			//设置干扰像素，向图像中输出不同颜色的100个点
			for($i=0; $i<=$this->disturbColorNum; $i++) {
				$color = imagecolorallocate($this->image, rand(0,255), rand(0,255), rand(0,255));
   				imagesetpixel($this->image,rand(1,$this->width-2),rand(1,$this->height-2),$color);
			}

			for($i=0; $i<10; $i++){
				$color=imagecolorallocate($this->image,rand(0,255),rand(0,255),rand(0,255));
				imagearc($this->image,rand(-10,$this->width),rand(-10,$this->height),rand(30,300),rand(20,200),55,44,$color);
			}  
		}


		private function outputText() {       
			//随机颜色、随机摆放、随机字符串向图像中输出
			for ($i=0;$i<=$this->codeNum;$i++) {
				$fontcolor = imagecolorallocate($this->image, rand(0,128), rand(0,128), rand(0,128));
				$fontSize=rand(3,5);
				$x = floor($this->width/$this->codeNum)*$i+3;
   				$y = rand(0,$this->height-imagefontheight($fontSize));
				imagechar($this->image, $fontSize, $x, $y, $this->checkCode{$i}, $fontcolor);
 			  }
		}

		private function outputImage(){              
			//自动检测GD支持的图像类型，并输出图像
			if(imagetypes() & IMG_GIF){          //判断生成GIF格式图像的函数是否存在
				header("Content-type: image/gif");  //发送标头信息设置MIME类型为image/gif
				imagegif($this->image);           //以GIF格式将图像输出到浏览器
			}elseif(imagetypes() & IMG_JPG){      //判断生成JPG格式图像的函数是否存在
				header("Content-type: image/jpeg"); //发送标头信息设置MIME类型为image/jpeg
				imagejpeg($this->image, "", 0.5);   //以JPEN格式将图像输出到浏览器
			}elseif(imagetypes() & IMG_PNG){     //判断生成PNG格式图像的函数是否存在
				header("Content-type: image/png");  //发送标头信息设置MIME类型为image/png
				imagepng($this->image);          //以PNG格式将图像输出到浏览器
			}elseif(imagetypes() & IMG_WBMP){   //判断生成WBMP格式图像的函数是否存在
				 header("Content-type: image/vnd.wap.wbmp");   //发送标头为image/wbmp
				 imagewbmp($this->image);       //以WBMP格式将图像输出到浏览器
			}else{                              //如果没有支持的图像类型
				die("PHP不支持图像创建！");    //不输出图像，输出一错误消息，并退出程序
			}
		}
		function __destruct(){                      //当对象结束之前销毁图像资源释放内存
 			imagedestroy($this->image);            //调用GD库中的方法销毁图像资源
		}
	}
```
