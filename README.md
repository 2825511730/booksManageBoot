@文章目录[toc]


![微信扫码关注这个有温度的程序猿](https://img-blog.csdnimg.cn/c5b40e17bc614f5d99a5d6e179a0447b.png)


源码下载：微信搜索公众号【`IT学长`】，回复关键词“`20220927`”下载图书管理系统（booksManageBoot）源码


开发文档：[《SpringBoot+MySQL+HTML图书管理系统设计与实现（附源码下载地址）》](https://mp.weixin.qq.com/s/JLrUlo7eTJccvGs0BOOSvw)

运行教程：[《SpringBoot+MySQL+HTML图书管理系统运行教程》](https://mp.weixin.qq.com/s/y5TytE8Y3Y1UfxAJ0JHrvw)

演示截图：[《SpringBoot+MySQL+HTML图书管理系统演示截图》](https://blog.csdn.net/m0_73470247/article/details/127530001)


毕设项目源码大全：[毕业设计、课程设计项目源码领取](https://mp.weixin.qq.com/mp/homepage?__biz=MzkyMDAxNTQ4NQ==&hid=5&sn=097a81acff1e1971604ea1b571c13b9e&scene=18)


## 01 系统概述

图书管理系统有着手工管理无法比拟的优点，如检索迅速、查找方便、可靠性高、存储量大、保密性好、成本低等，这些优点能够极大地提高图书管理的效率。因此，开发一套能够为用户提供充足的信息和快捷的查询手段的图书管理系统是非常必要的。


本系统实现了图书管理、借阅管理、用户管理、公告管理、个人中心等功能，界面友好、操作容易、维护简单，同时具备数据的完整性和安全性，符合高校图书管理系统的要求。


![](https://img-blog.csdnimg.cn/63d09b99d2084f8baf0ae8f3faacf63c.png)


## 02 开发工具及技术选型

- 数据表现层：Html+JavaScript+CSS+JavaEx+JQuery 
- 业务逻辑层：Java+Spring+SpringMVC
- 数据持久层：MySQL+MyBatis
- 开发工具：IDEA / Eclipse


## 03 运行环境

```
JDK1.8 + Maven3 + MySQL5.7
```

## 04 用户分析

本系统主要用于高校图书管理，使用人群为系统管理员、普通读者。

- 系统管理员：管理整个系统的各项功能，如：公告信息、图书信息、用户信息更新维护。
- 普通读者：借阅图书、归还图书、阅览公告信息、查询编辑个人信息等。

## 05 功能分析

**系统管理员：**

 1. 首页
 	- 名片方式展示系统管理员拥有的权限
 2. 图书管理
 	-	图书列表：显示已上架的图书信息，可对已上架图书进行搜索、修改、删除操作
 	-	图书上架：录入图书信息，输入图书名称、作者、图书分类，页数，定价等数据进行图书录入
 3. 借阅管理
 	- 借阅图书：根据图书名称、作者名称，图书分类等搜索、查看、借阅图书
	- 归还图书：对已经借阅的图书进行归还操作
 4. 用户管理
 	- 用户列表：显示已注册的用户，可以对已注册的用户信息进行搜索、修改、删除操作
	- 用户添加：录入用户的昵称、用户名、密码、生日、电话、邮箱等信息添加新用户
 5. 公告管理
 	- 公告列表：显示已发布的公告信息，可以对已发布的公告进行搜索、修改、删除等操作
	- 公告发布：输入公告标题，发布时间，公告内容等要素发布公告
 6. 个人管理
 	- 个人信息详情：查看个人信息
	- 个人信息修改：修改个人信息


![](https://img-blog.csdnimg.cn/f74ff29a6dee4ad892930337cefec958.png)


**普通读者：**

1. 首页
	- 名片方式展示普通读者拥有的权限
2. 借阅管理
	- 借阅图书：根据图书名称、作者名称，图书分类等搜索、查看、借阅图书
	- 归还图书：对已借阅的图书进行归还操作
3. 公告管理
	- 公告列表：查看已发布的公告信息
4. 个人管理
	- 个人信息详情：查看个人信息
	- 个人信息修改：修改个人信息

![](https://img-blog.csdnimg.cn/0013de69873f452e91a37351f4c66e41.png)


## 06 数据库设计

**users：** 存储用户信息

|	字段名称	|	类型	|	是否为null	|	是否主键	|	说明	|
|--|--|--|--|--|
| id	| int	| 否  | 是 | ID主键| 
| address	| varchar	 | 是  | 否	 | 地址	 | 	
| avatar	| varchar	 |  是 | 否 |  头像	 | 	
| birthday	| datetime | 是 | 否 | 	生日	 | 	
| email	| varchar	 |  是  | 否	 | 	邮箱	 | 	
| is_admin	| int	 | 是 | 否 | 	是否为管理员（0 管理员 1 普通用户） | 	
| nickname	| varchar	| 是  | 否 | 	昵称	 | 	
| password	| varchar	| 是 | 否 | 密码	 | 	
| size	| int	 | 是 | 否 | 	可借数量	 | 	
| tel	| varchar	 | 是 | 否 | 	电话	 | 	
| username	| varchar | 是 | 否  | 	用户名	 | 	

**book：** 存储图书信息

|	字段名称	|	类型	|	是否为null	|	是否主键	|	说明	|
|--|--|--|--|--|
|	id	|	int| 否 |  是 |	ID主键	|
|	author	|	varchar|	是|否	|	图书作者	|
|	isbn	|	varchar| 是	|	否|	图书ISBN编码	|
|	name	|	varchar| 是	|否	|	图书名称	|
|	pages	|	int| 是	|	否|	图书页数 |
|	price	|	double| 是 |	否|	单价	|
|	publish 	|	varchar| 是 |否	|	出版社	|
|	publish_time|	datetime|	是 |否	|	出版时间	|
|	size	|	int| 是 |否	|	库存	|
|	translate	|	varchar| 是	|否	|	翻译	|
|	type	|	varchar| 是 	|否	|	分类	|


**borrow：** 存储借阅信息

|	字段名称	|	类型	|	是否为null	|	是否主键	|	说明	|
|--|--|--|--|--|
|	id	|	int | 否 | 是 |ID主键	|
|	book_id	|	int | 是 | 否 |图书ID		|
|	create_time	|	datetime | 是 | 否 |借阅时间	|
|	update_time	|	datetime | 是 | 否 |实际归还时间	|
|	user_id	|	int | 是 | 否 |用户ID	|
|	end_time	|	datetime | 是 | 否 |归还时间	|
|	ret	|	int | 是 | 否 |是否归还（0 已归还 1 未归还）	|

**notice：** 存储公告信息

|	字段名称	|	类型	|	是否为null	|	是否主键	|	说明	|
|--|--|--|--|--|
|	id	|	int| 否 | 是 |ID主键|
|	title	|	varchar| 是 | 否 |标题|
|	date	|	datetime	| 是 | 否 |发布时间|
|	content	|	text| 是 | 否 |内容|

##  07 接口示例

由于后台接口较多，没办法在此逐个列举，详情请阅读“`图书管理系统设计与实现（SpringBoot+Mysql+HTML）`”源码包中 `图书管理后台Swagger UI.html` 文件。

**注：“图书管理系统设计与实现（SpringBoot+Mysql+HTML）”源码包在本文`第10章节`下载**


![](https://img-blog.csdnimg.cn/4a378bcf7d4c4cdfa47bd8f20a63b671.png)


### 7.1 图书管理--添加图书

**接口描述**:

**接口地址**:`/booksManageBoot/book/add`

**请求方式**：`POST`

**consumes**:`["application/json"]`

**produces**:`["*/*"]`

**请求示例**：

```json
{
	"author": "",
	"id": 0,
	"isbn": "",
	"name": "",
	"pages": 0,
	"price": 0,
	"publish": "",
	"publishTime": "",
	"size": 0,
	"translate": "",
	"type": ""
}
```

**请求参数**：

| 参数名称 | 参数说明 | in   | 是否必须 | 数据类型 | schema |
| -------- | -------- | ---- | -------- | -------- | ------ |
| book     | book     | body | true     | Book     | Book   |

**schema属性说明**

**Book**

| 参数名称    | 参数说明     | in   | 是否必须 | 数据类型          | schema |
| ----------- | ------------ | ---- | -------- | ----------------- | ------ |
| author      | 图书作者     | body | false    | string            |        |
| id          | ID主键       | body | false    | integer(int32)    |        |
| isbn        | 图书ISBN编码 | body | false    | string            |        |
| name        | 图书名称     | body | false    | string            |        |
| pages       | 图书页数     | body | false    | integer(int32)    |        |
| price       | 单价         | body | false    | number(double)    |        |
| publish     | 出版社       | body | false    | string            |        |
| publishTime | 出版时间     | body | false    | string(date-time) |        |
| size        | 库存         | body | false    | integer(int32)    |        |
| translate   | 翻译         | body | false    | string            |        |
| type        | 分类         | body | false    | string            |        |

**响应示例**:

```json
{
	"code": 0,
	"data": {},
	"msg": ""
}
```

**响应参数**:

| 参数名称 | 参数说明 | 类型           | schema         |
| -------- | -------- | -------------- | -------------- |
| code     | 响应码   | integer(int32) | integer(int32) |
| data     | 响应数据 | object         |                |
| msg      | 响应信息 | string         |                |

**响应状态**:

| 状态码 | 说明         | schema |
| ------ | ------------ | ------ |
| 200    | OK           | R      |
| 201    | Created      |        |
| 401    | Unauthorized |        |
| 403    | Forbidden    |        |
| 404    | Not Found    |        |

### 7.2 借阅管理--借阅图书

**接口描述**:

**接口地址**:`/booksManageBoot/borrow/add`

**请求方式**：`POST`

**consumes**:`["application/json"]`

**produces**:`["*/*"]`

**请求示例**：
```json
{
	"bookId": 0,
	"createTime": "",
	"endTime": "",
	"id": 0,
	"ret": 0,
	"updateTime": "",
	"userId": 0
}
```

**请求参数**：

| 参数名称 | 参数说明 | in   | 是否必须 | 数据类型 | schema |
| -------- | -------- | ---- | -------- | -------- | ------ |
| borrow   | borrow   | body | true     | Borrow   | Borrow |

**schema属性说明**

**Borrow**

| 参数名称   | 参数说明                      | in   | 是否必须 | 数据类型          | schema |
| ---------- | ----------------------------- | ---- | -------- | ----------------- | ------ |
| bookId     | 图书ID                        | body | false    | integer(int32)    |        |
| createTime | 借阅时间                      | body | false    | string(date-time) |        |
| endTime    | 归还时间                      | body | false    | string(date-time) |        |
| id         | ID主键                        | body | false    | integer(int32)    |        |
| ret        | 是否归还（0 已归还 1 未归还） | body | false    | integer(int32)    |        |
| updateTime | 实际归还时间                  | body | false    | string(date-time) |        |
| userId     | 用户ID                        | body | false    | integer(int32)    |        |

**响应示例**:

```json
{
	"code": 0,
	"data": {},
	"msg": ""
}
```

**响应参数**:

| 参数名称 | 参数说明 | 类型           | schema         |
| -------- | -------- | -------------- | -------------- |
| code     | 响应码   | integer(int32) | integer(int32) |
| data     | 响应数据 | object         |                |
| msg      | 响应信息 | string         |                |

**响应状态**:

| 状态码 | 说明         | schema |
| ------ | ------------ | ------ |
| 200    | OK           | R      |
| 201    | Created      |        |
| 401    | Unauthorized |        |
| 403    | Forbidden    |        |
| 404    | Not Found    |        |


### 7.3 用户管理--用户列表

**接口描述**:

**接口地址**:`/booksManageBoot/user/list`

**请求方式**：`POST`

**consumes**:`["application/json"]`

**produces**:`["*/*"]`

**请求示例**：
```json
{
	"currPage": 0,
	"keyword": "",
	"pageSize": 0
}
```

**请求参数**：

| 参数名称 | 参数说明 | in   | 是否必须 | 数据类型 | schema |
| -------- | -------- | ---- | -------- | -------- | ------ |
| pageIn   | pageIn   | body | true     | PageIn   | PageIn |

**schema属性说明**

**PageIn**

| 参数名称 | 参数说明   | in   | 是否必须 | 数据类型       | schema |
| -------- | ---------- | ---- | -------- | -------------- | ------ |
| currPage | 当前页     | body | false    | integer(int32) |        |
| keyword  | 搜索关键字 | body | false    | string         |        |
| pageSize | 每页数量   | body | false    | integer(int32) |        |

**响应示例**:

```json
{
	"code": 0,
	"data": {},
	"msg": ""
}
```

**响应参数**:

| 参数名称 | 参数说明 | 类型           | schema         |
| -------- | -------- | -------------- | -------------- |
| code     | 响应码   | integer(int32) | integer(int32) |
| data     | 响应数据 | object         |                |
| msg      | 响应信息 | string         |                |

**响应状态**:

| 状态码 | 说明         | schema |
| ------ | ------------ | ------ |
| 200    | OK           | R      |
| 201    | Created      |        |
| 401    | Unauthorized |        |
| 403    | Forbidden    |        |
| 404    | Not Found    |        |


### 7.4 公告管理--编辑公告

**接口描述**:

**接口地址**:`/booksManageBoot/notice/update`

**请求方式**：`POST`

**consumes**:`["application/json"]`

**produces**:`["*/*"]`

**请求示例**：
```json
{
	"content": "",
	"date": "",
	"id": 0,
	"title": ""
}
```

**请求参数**：

| 参数名称 | 参数说明 | in   | 是否必须 | 数据类型 | schema |
| -------- | -------- | ---- | -------- | -------- | ------ |
| notice   | notice   | body | true     | Notice   | Notice |

**schema属性说明**

**Notice**

| 参数名称 | 参数说明 | in   | 是否必须 | 数据类型          | schema |
| -------- | -------- | ---- | -------- | ----------------- | ------ |
| content  | 公告内容 | body | false    | string            |        |
| date     | 发布时间 | body | false    | string(date-time) |        |
| id       | ID主键   | body | false    | integer(int32)    |        |
| title    | 公告标题 | body | false    | string            |        |

**响应示例**:

```json
{
	"code": 0,
	"data": {},
	"msg": ""
}
```

**响应参数**:

| 参数名称 | 参数说明 | 类型           | schema         |
| -------- | -------- | -------------- | -------------- |
| code     | 响应码   | integer(int32) | integer(int32) |
| data     | 响应数据 | object         |                |
| msg      | 响应信息 | string         |                |

**响应状态**:

| 状态码 | 说明         | schema |
| ------ | ------------ | ------ |
| 200    | OK           | R      |
| 201    | Created      |        |
| 401    | Unauthorized |        |
| 403    | Forbidden    |        |
| 404    | Not Found    |        |

## 08 项目工程结构及说明

下载本项目源码并导入到开发工具后（下图为导入到IDEA中的目录结构），项目的目录结构如下图所示：


![](https://img-blog.csdnimg.cn/5c38e4dbb2194ad3bfc1819dbb53c084.png)


|包名| 说明  |
|--|--|
| com.cya.config | 存放基础配置类，如：拦截器配置类、管理后台Swagger配置类、Spring Security安全配置类等 |
| com.cya.controller  |  用于存放接收请求的Controller类，前后端交互的“桥梁”   |
| com.cya.service |  存放业务逻辑层代码  |
| com.cya.dao | 存放数据持久层代码 |
| com.cya.entity | 存放实体类 |
| com.cya.util | 存放工具类 |
| com.cya.interceptor |  登录拦截器 |
| resources/mapper |  mybatis mapper文件 |
| resources/staitc|  存放静态文件，如：JavaScript、CSS、img |
| resources/templates|  存放html文件 |
|  application.yml |  SpringBoot框架配置文件，如：项目启动端口、项目路径、数据库配置等 |
| ManagerApplication.java|  项目启动类 |



## 09 部分功能展示及源码

### 9.1 首页

![](https://img-blog.csdnimg.cn/9c1434ef0e9048e4847fa3459a33082b.png)


**部分代码：**

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta charset="utf-8">
<!--字体图标-->
<link href="javaex/pc/css/icomoon.css" rel="stylesheet" />
<!--动画-->
<link href="javaex/pc/css/animate.css" rel="stylesheet" />
<!--骨架样式-->
<link href="javaex/pc/css/common.css" rel="stylesheet" />
<!--皮肤（缇娜）-->
<link href="javaex/pc/css/skin/tina.css" rel="stylesheet" />
<!--jquery，不可修改版本-->
<script src="javaex/pc/lib/jquery-1.7.2.min.js"></script>
<!--全局动态修改-->
<script src="javaex/pc/js/common.js"></script>
<!--核心组件-->
<script src="javaex/pc/js/javaex.min.js"></script>
<!--表单验证-->
<script src="javaex/pc/js/javaex-formVerify.js"></script>
<title>图书管理系统-首页</title>
<style>
</style>
</head>
<body>
	<!--顶部导航-->
	<div class="admin-navbar">
		<div class="admin-container-fluid clear">
			<!--logo名称-->
			<div class="admin-logo">图书管理系统</div>

			<!--右侧-->
			<ul class="admin-navbar-nav fr">
				<li><input id="index_role" hidden /> <a href="javascript:;">欢迎您，<span
						id="login_user"></span></a>
					<ul class="dropdown-menu" style="right: 10px;">
						<li><a href="logout">退出当前账号</a></li>
					</ul></li>
			</ul>
		</div>
	</div>

	<!--主题内容-->
	<div class="admin-mian" style="margin-bottom: 50px;">
		<!--左侧菜单-->
		<div class="admin-aside admin-aside-fixed">
			<!-- 应用标题  -->
			<div id="admin-toc" class="admin-toc">
				<div class="menu-box">
					<div id="menu" class="menu">
						<ul id="adminMenu" style="display: none;">
							<li class="menu-item hover"><a
								href="javascript:page('welcome');"><i class="icon-home2"></i>首页</a>
							</li>

							<li class="menu-item"><a href="javascript:;">图书管理<i
									class="icon-keyboard_arrow_left"></i></a>
								<ul>
									<li><a href="javascript:page('book/book-list');">图书列表</a></li>
									<li><a href="javascript:page('book/book-add');">图书上架</a></li>
								</ul></li>

							<li class="menu-item"><a href="javascript:;">借阅管理<i
									class="icon-keyboard_arrow_left"></i></a>
								<ul>
									<li><a href="javascript:page('borrow/book-list');">借阅图书</a></li>
									<li><a href="javascript:page('borrow/back');">归还图书</a></li>
								</ul></li>

							<li class="menu-item"><a href="javascript:;">用户管理<i
									class="icon-keyboard_arrow_left"></i></a>
								<ul>
									<li><a href="javascript:page('user/user-list');">用户列表</a></li>
									<li><a href="javascript:page('user/user-add');">用户添加</a></li>
								</ul></li>

							<li class="menu-item"><a href="javascript:;">公告管理<i
									class="icon-keyboard_arrow_left"></i></a>
								<ul>
									<li><a href="javascript:page('notice/notice-list');">公告列表</a></li>
									<li><a href="javascript:page('notice/notice-add');">公告发布</a></li>
								</ul></li>

							<li class="menu-item"><a href="javascript:;">个人中心<i
									class="icon-keyboard_arrow_left"></i></a>
								<ul>
									<li><a href="javascript:page('my/my-info');">个人信息详情</a></li>
									<li><a href="javascript:page('my/my-update');">个人信息修改</a></li>
								</ul></li>
						</ul>
						<ul id="userMenu" style="display: none;">
							<li class="menu-item hover"><a
								href="javascript:page('welcome');"><i class="icon-home2"></i>首页</a>
							</li>

							<li class="menu-item"><a href="javascript:;">借阅管理<i
									class="icon-keyboard_arrow_left"></i></a>
								<ul>
									<li><a href="javascript:page('borrow/book-list');">借阅图书</a></li>
									<li><a href="javascript:page('borrow/back');">归还图书</a></li>
								</ul></li>

							<li class="menu-item"><a href="javascript:;">公告管理<i
									class="icon-keyboard_arrow_left"></i></a>
								<ul>
									<li><a href="javascript:page('notice/notice-list');">公告列表</a></li>
								</ul></li>

							<li class="menu-item"><a href="javascript:;">个人中心<i
									class="icon-keyboard_arrow_left"></i></a>
								<ul>
									<li><a href="javascript:page('my/my-info');">个人信息详情</a></li>
									<li><a href="javascript:page('my/my-update');">个人信息修改</a></li>
								</ul></li>
						</ul>
					</div>
				</div>
			</div>
		</div>

		<!--iframe载入内容-->
		<div class="admin-markdown">
			<iframe id="page" src="welcome"></iframe>
		</div>
	</div>

	<!-- foot -->
	<div class="admin-footer" style="position: fixed; bottom: 0;">
		<div class="admin-container-fluid clear"
			style="line-height: 50px; text-align: center;">公众号【IT学长】</div>
	</div>
	<!-- foot -->
</body>
<script>

	var hightUrl = "xxxx";
	javaex.menu({
		id : "menu",
		isAutoSelected : true,
		key : "",
		url : hightUrl
	});
	
	$(function() {
		// 设置左侧菜单高度
		setMenuHeight();
	});
	
	/**
	 * 设置左侧菜单高度
	 */
	function setMenuHeight() {
		var height = document.documentElement.clientHeight - $("#admin-toc").offset().top;
		height = height - 10;
		$("#admin-toc").css("height", height+"px");
	}
	
	// 控制页面载入
	function page(url) {
		$("#page").attr("src", url);
	}

    $(document).ready(function(){
        // 页面一加载, 读取登录用户信息
    	  $.get("user/currUser", function(data){
  			var user = data.data;
  			var userId = user.id;
  			console.log("user",user);
              if (userId >0) {
                $("#login_user").text(user.username+"["+user.ident+"]");
                $("#index_role").val(user.isAdmin);
                if(user.isAdmin==0){
                	$("#adminMenu").css("display",'block');
                	$("#userMenu").css("display",'none');
                	
                }
                else{
                	$("#adminMenu").css("display",'none');
                	$("#userMenu").css("display",'block');
                }
                
              }else {
                  // 找不到用户, 不可进行借阅操作
                  javaex.message({
                      content : "登录信息已失效, 请登录后借阅",
                      type : "error"
                  });
              }
          });

    });
</script>
</html>
```

### 9.2 图书管理

**图书上架：**


![](https://img-blog.csdnimg.cn/194cbeba84af4f68a225de4ef4ebf9d2.png#pic_center)


**图书修改：**

![](https://img-blog.csdnimg.cn/25a1593d5f324f0ca331ca67f9bd054c.png)

**部分源码：**

```java
package com.book.manager.controller;

import com.book.manager.entity.Book;
import com.book.manager.service.BookService;
import com.book.manager.service.BorrowService;
import com.book.manager.util.R;
import com.book.manager.util.http.CodeEnum;
import com.book.manager.util.ro.PageIn;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;

/**
 * @Description 用户管理
 * @Date 2022/9/4 16:35
 * @Author by 公众号【IT学长】
 */
@Api(tags = "图书管理")
@RestController
@RequestMapping("/book")
public class BookController {

    @Autowired
    private BookService bookService;
    
    @Autowired
    private BorrowService borrowService;

    @ApiOperation("图书搜索列表")
    @PostMapping("/list")
    public R getBookList(@RequestBody PageIn pageIn) {
        if (pageIn == null) {
            return R.fail(CodeEnum.PARAM_ERROR);
        }

        return R.success(CodeEnum.SUCCESS,bookService.getBookList(pageIn));
    }

    @ApiOperation("添加图书")
    @PostMapping("/add")
    public R addBook(@RequestBody Book book) {
        return R.success(CodeEnum.SUCCESS,bookService.addBook(book));
    }

    @ApiOperation("编辑图书")
    @PostMapping("/update")
    public R modifyBook(@RequestBody Book book) {
        return R.success(CodeEnum.SUCCESS,bookService.updateBook(book));
    }


    @ApiOperation("图书详情")
    @GetMapping("/detail")
    public R bookDetail(Integer id) {
        return R.success(CodeEnum.SUCCESS,bookService.findBookById(id));
    }

    @ApiOperation("图书详情 根据ISBN获取")
    @GetMapping("/detailByIsbn")
    public R bookDetailByIsbn(String isbn) {
        return R.success(CodeEnum.SUCCESS,bookService.findBookByIsbn(isbn));
    }

    @ApiOperation("删除图书")
    @GetMapping("/delete")
    public R delBook(Integer id) {
        bookService.deleteBook(id);
        borrowService.deleteBorrowByBookId(id);
        return R.success(CodeEnum.SUCCESS);
    }

}
```


### 9.3 借阅管理

**借阅图书：**

![](https://img-blog.csdnimg.cn/f7df11ea33e04601beca99b1a8b47a85.png)

![](https://img-blog.csdnimg.cn/ada312b1ca8b4e7d840f874317654b00.png)

**归还图书：**

![](https://img-blog.csdnimg.cn/60fcdae65fc344ed8db26c5452c2118b.png)

**部分源码：**

```java
package com.book.manager.service;

import cn.hutool.core.bean.BeanUtil;
import com.book.manager.dao.BookMapper;
import com.book.manager.dao.BorrowMapper;
import com.book.manager.dao.UsersMapper;
import com.book.manager.entity.Book;
import com.book.manager.entity.Borrow;
import com.book.manager.entity.Users;
import com.book.manager.repos.BookRepository;
import com.book.manager.repos.BorrowRepository;
import com.book.manager.util.consts.Constants;
import com.book.manager.util.vo.BookOut;
import org.springframework.beans.BeanUtils;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.Date;
import java.util.List;
import java.util.Optional;

/**
 * @Description 借阅管理
 * @Date 2022/9/4 16:35
 * @Author by 公众号【IT学长】
 */
@Service
public class BorrowService {

    @Autowired
    private BorrowRepository borrowRepository;

    @Autowired
    private BorrowMapper borrowMapper;

    @Autowired
    private BookService bookService;

    @Autowired
    private UserService userService;

    /**
     * 添加
     */
    @Transactional
    public Integer addBorrow(Borrow borrow) {
        Book book = bookService.findBook(borrow.getBookId());
        Users users = userService.findUserById(borrow.getUserId());

        // 查询是否已经借阅过该图书
        Borrow bor = findBorrowByUserIdAndBookId(users.getId(),book.getId());
        if (bor!=null) {
            Integer ret = bor.getRet();
            if (ret!=null) {
                // 已借阅, 未归还 不可再借
                if (ret == Constants.NO) {
                    return Constants.BOOK_BORROWED;
                }
            }
        }

        // 库存数量减一
        int size = book.getSize();
        if (size>0) {
            size--;
            book.setSize(size);
            bookService.updateBook(book);
        }else {
            return Constants.BOOK_SIZE_NOT_ENOUGH;
        }

        // 用户可借数量减一
        int userSize = users.getSize();
        if (userSize>0) {
            userSize --;
            users.setSize(userSize);
            userService.updateUser(users);
        }else {
            return Constants.USER_SIZE_NOT_ENOUGH;
        }


        // 添加借阅信息, 借阅默认为未归还状态
        borrow.setRet(Constants.NO);
        borrowRepository.saveAndFlush(borrow);

        // 一切正常
        return Constants.OK;
    }

    /**
     * user id查询所有借阅信息
     */
    public List<Borrow> findAllBorrowByUserId(Integer userId) {
        return borrowRepository.findBorrowByUserId(userId);
    }

    /**
     * user id查询所有 已借阅信息
     */
    public List<Borrow> findBorrowsByUserIdAndRet(Integer userId, Integer ret) {
        return borrowRepository.findBorrowsByUserIdAndRet(userId,ret);
    }


    /**
     * 详情
     */
    public Borrow findById(Integer id) {
        Optional<Borrow> optional = borrowRepository.findById(id);
        if (optional.isPresent()) {
            return optional.get();
        }
        return null;
    }

    /**
     * 编辑
     */
    public boolean updateBorrow(Borrow borrow) {
        return borrowMapper.updateBorrow(borrow)>0;
    }


    /**
     * 编辑
     */
    public Borrow updateBorrowByRepo(Borrow borrow) {
        return borrowRepository.saveAndFlush(borrow);
    }

    /**
     * 根据ID删除
     */
    public void deleteBorrow(Integer id) {
        borrowRepository.deleteById(id);
    }
    
    /**
     * 根据book_id删除
     */
    public void deleteBorrowByBookId(Integer bookId) {
    	borrowMapper.deleteBorrowByBookId(bookId);
    }
    

    /**
     * 查询用户某一条借阅信息
     * @param userId 用户id
     * @param bookId 图书id
     */
    public Borrow findBorrowByUserIdAndBookId(int userId,int bookId) {
        return borrowMapper.findBorrowByUserIdAndBookId(userId,bookId);
    }

    /**
     * 归还书籍,
     * @param userId 用户Id
     * @param bookId 书籍id
     */
    @Transactional(rollbackFor = Exception.class)
    public void retBook(int userId,int bookId) {
        // 用户可借数量加1
        Users user = userService.findUserById(userId);
        Integer size = user.getSize();
        size++;
        user.setSize(size);
        userService.updateUser(user);


        // 书籍库存加1
        Book book = bookService.findBook(bookId);
        Integer bookSize = book.getSize();
        bookSize++;
        book.setSize(bookSize);
        bookService.updateBook(book);
        // 借阅记录改为已归还,删除记录
        Borrow borrow = this.findBorrowByUserIdAndBookId(userId, bookId);
        this.deleteBorrow(borrow.getId());
    }
}
```

### 9.4 用户管理

**用户列表：**

![](https://img-blog.csdnimg.cn/a12fad394eea4aa48080c83b4d673b44.png)

**用户添加：**

![](https://img-blog.csdnimg.cn/ac034a2e236b4a3e81284ed43d3a181c.png)


**部分源码：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.book.manager.dao.UsersMapper">
	<resultMap id="BaseResultMap"
		type="com.book.manager.entity.Users">
		<id column="id" property="id" jdbcType="INTEGER" />
		<result column="avatar" property="avatar" jdbcType="VARCHAR" />
		<result column="nickname" property="nickname"
			jdbcType="VARCHAR" />
		<result column="username" property="username"
			jdbcType="VARCHAR" />
		<result column="password" property="password"
			jdbcType="VARCHAR" />
		<result column="birthday" property="birthday"
			jdbcType="TIMESTAMP" />
		<result column="is_admin" property="isAdmin" jdbcType="INTEGER" />
		<result column="tel" property="tel" jdbcType="VARCHAR" />
		<result column="email" property="email" jdbcType="VARCHAR" />
		<result column="address" property="address" jdbcType="VARCHAR" />
		<result column="size" property="size" jdbcType="INTEGER" />
	</resultMap>

	<!-- 模糊查询 -->
	<select id="findListByLike" resultMap="BaseResultMap">
		select * from users
		<where>
			<if test="_parameter != null and _parameter != ''">
				and `username` like CONCAT('%',#{_parameter},'%') or `nickname` like
				CONCAT('%',#{_parameter},'%')
			</if>
		</where>
	</select>

	<update id="updateUsers" parameterType="map">
		update users
		<set>
			<if test="avatar != null and avatar != ''">
				avatar = #{avatar},
			</if>
			<if test="nickname != null and nickname != ''">
				nickname = #{nickname},
			</if>
			<if test="username != null and username != ''">
				username = #{username},
			</if>
			<if test="password != null and password != ''">
				password = #{password},
			</if>
			<if test="birthday != null">
				birthday = #{birthday},
			</if>
			<if test="isAdmin != null">
				is_admin = #{isAdmin},
			</if>
			<if test="tel != null and tel != ''">
				tel = #{tel},
			</if>
			<if test="email != null and email != ''">
				email = #{email},
			</if>
			<if test="address != null and address != ''">
				address = #{address},
			</if>
			<if test="size != null">
				`size` = #{size},
			</if>
		</set>
		where id = #{id}
	</update>
</mapper>
```

### 9.5 公告管理

**公告列表：**

![](https://img-blog.csdnimg.cn/db85fd978db744298f224bb067d97430.png)

**公告详情：**

![](https://img-blog.csdnimg.cn/f77e20ef69924622932db52c6f48bd10.png)

**部分源码：**

```java
package com.book.manager.controller;

import cn.hutool.core.bean.BeanUtil;
import cn.hutool.core.date.DateUtil;
import cn.hutool.core.util.StrUtil;

import com.book.manager.entity.Notice;
import com.book.manager.entity.Users;
import com.book.manager.service.NoticeService;
import com.book.manager.util.R;
import com.book.manager.util.consts.Constants;
import com.book.manager.util.consts.ConvertUtil;
import com.book.manager.util.http.CodeEnum;
import com.book.manager.util.vo.NoticeOut;
import com.book.manager.util.vo.PageOut;
import com.book.manager.util.vo.UserOut;
import com.book.manager.util.ro.PageIn;
import com.github.pagehelper.PageInfo;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import org.springframework.beans.BeanUtils;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;

/**
 * @Description 公告管理
 * @Date 2022/9/4 16:35
 * @Author by 公众号【IT学长】
 */
@Api(tags = "公告管理")
@RestController
@RequestMapping("/notice")
public class NoticeController {

    @Autowired
    private NoticeService noticeService;

    @ApiOperation("公告列表")
    @PostMapping("/list")
    public R getNotices(@RequestBody PageIn pageIn) {
        if (pageIn == null) {
            return R.fail(CodeEnum.PARAM_ERROR);
        }
        // 封装分页出参对象
        PageInfo<Notice> noticeList = noticeService.getNoticeList(pageIn);
        PageOut pageOut = new PageOut();
        pageOut.setCurrPage(noticeList.getPageNum());
        pageOut.setPageSize(noticeList.getPageSize());
        pageOut.setTotal((int) noticeList.getTotal());
        List<Notice> outs = new ArrayList<>();
        for (Notice notice : noticeList.getList()) {
            NoticeOut out = new NoticeOut();
            BeanUtils.copyProperties(notice,out);
            out.setDate1(DateUtil.format(notice.getDate(),Constants.DATE_FORMAT));
            outs.add(out);
        }
        pageOut.setList(outs);

        return R.success(CodeEnum.SUCCESS,pageOut);
    }

    @ApiOperation("添加公告")
    @PostMapping("/addNoticer")
    public R addNoticer(@RequestBody Notice notice) {
        if (notice == null) {
            return R.fail(CodeEnum.PARAM_ERROR);
        }
        return R.success(CodeEnum.SUCCESS,noticeService.addNotice(notice));
    }


    @ApiOperation("编辑公告")
    @PostMapping("/update")
    public R modifyNotice(@RequestBody Notice notice) {
        return R.success(CodeEnum.SUCCESS,noticeService.updateNotice(notice));
    }


    @ApiOperation("公告详情")
    @GetMapping("/detail")
    public R noticeDetail(Integer id) {
        Notice notice = noticeService.findNoticeById(id);
        if (notice!=null) {
        	NoticeOut out = new NoticeOut();
            BeanUtils.copyProperties(notice,out);
            out.setDate1(DateUtil.format(notice.getDate(),Constants.DATE_FORMAT));
            return R.success(CodeEnum.SUCCESS,out);
        }

        return R.fail(CodeEnum.NOT_FOUND);
    }

    @ApiOperation("删除公告")
    @GetMapping("/delete")
    public R delNotice(Integer id) {
    	noticeService.deleteNotice(id);
        return R.success(CodeEnum.SUCCESS);
    }

}
```

### 9.6 个人中心

**个人信息详情：**

![](https://img-blog.csdnimg.cn/d2b6afb052d04fefa80474bbf7a2bb08.png)


**部分源码：**

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta charset="utf-8">
<!--字体图标-->
<link href="../javaex/pc/css/icomoon.css" rel="stylesheet" />
<!--动画-->
<link href="../javaex/pc/css/animate.css" rel="stylesheet" />
<!--骨架样式-->
<link href="../javaex/pc/css/common.css" rel="stylesheet" />
<!--皮肤（缇娜）-->
<link href="../javaex/pc/css/skin/tina.css" rel="stylesheet" />
<!--jquery，不可修改版本-->
<script src="../javaex/pc/lib/jquery-1.7.2.min.js"></script>
<!--全局动态修改-->
<script src="../javaex/pc/js/common.js"></script>
<!--核心组件-->
<script src="../javaex/pc/js/javaex.min.js"></script>
<!--表单验证-->
<script src="../javaex/pc/js/javaex-formVerify.js"></script>
<title>图书管理系统-查询个人信息</title>
</head>
<style>
</style>

<body>
	<!--全部主体内容-->
	<div class="list-content">
		<!--块元素-->
		<div class="block">
			<!--修饰块元素名称-->
			<div class="banner">
				<p class="tab fixed">个人信息</p>
			</div>

			<!--正文内容-->
			<div class="main">
				<form id="form">
					<!--文本框-->
					<div class="unit clear">
						<div class="left">
							<span class="required">*</span>
							<p class="subtitle">昵称</p>
						</div>
						<div class="right">
							<input type="text" class="text" id="nickname" name="nickname"
								readonly="readonly" />
						</div>
					</div>

					<div class="unit clear">
						<div class="left">
							<span class="required">*</span>
							<p class="subtitle">用户名</p>
						</div>
						<div class="right">
							<input type="text" class="text" id="username" name="username"
								readonly="readonly" />
						</div>
					</div>

					<div class="unit clear">
						<div class="left">
							<span class="required">*</span>
							<p class="subtitle">密码</p>
						</div>
						<div class="right">
							<input type="password" class="text" id="password" name="password"
								readonly="readonly" />
						</div>
					</div>

					<div class="unit clear">
						<div class="left">
							<span class="required"></span>
							<p class="subtitle">生日</p>
						</div>
						<div class="right">
							<input type="text" class="text" id="birthday" name="birthday"
								readonly="readonly" />
						</div>
					</div>

					<div class="unit clear">
						<div class="left">
							<span class="required"></span>
							<p class="subtitle">电话</p>
						</div>
						<div class="right">
							<input type="text" class="text" id="tel" name="tel"
								readonly="readonly" />
						</div>
					</div>

					<!--下拉选择框-->
					<div class="unit clear">
						<div class="left">
							<span class="required"></span>
							<p class="subtitle">身份</p>
						</div>
						<div class="right">
							<input type="text" class="text" id="ident" name="ident"
								readonly="readonly" />
						</div>
					</div>

					<div class="unit clear">
						<div class="left">
							<span class="required"></span>
							<p class="subtitle">邮箱</p>
						</div>
						<div class="right">
							<input type="text" class="text" id="email" name="email"
								readonly="readonly" />
						</div>
					</div>

					<div class="unit clear">
						<div class="left">
							<span class="required"></span>
							<p class="subtitle">地址</p>
						</div>
						<div class="right">
							<input type="text" class="text" id="address" name="address"
								readonly="readonly" />
						</div>
					</div>

					<div class="unit clear">
						<div class="left">
							<span class="required"></span>
							<p class="subtitle">可借数量</p>
						</div>
						<div class="right">
							<input type="text" class="text" id="size" name="size"
								readonly="readonly" />
						</div>
					</div>
					<br> <br>

				</form>
			</div>
		</div>
	</div>

	<script>
		javaex.select({
			id : "select",
			isSearch : false
		});

		// 页面加载执行
		$(document).ready(function() {
			// get读取参数
			$.get("../user/currUser", function(data) {
				var user = data.data;
				$("#nickname").val(user.nickname);
				$("#username").val(user.username);
				$("#password").val(user.password);
				$("#birthday").val(user.birth);
				$("#tel").val(user.tel);
				$("#email").val(user.email);
				$("#address").val(user.address);
				$("#size").val(user.size);
				$("#ident").val(user.ident);

				return false;
			});
		});
	</script>
</body>
</html>
```

## 10 完整源码下载

微信搜索公众号【`IT学长`】，回复关键词“`20220927`”下载图书管理系统（booksManageBoot）源码。
   


## 11 运行教程

详细运行步骤及常见问题解答请看“`图书管理系统设计与实现（SpringBoot+Mysql+HTML）`”源码包中 `README.md` 文件。

通过`第10章节`下载源码包并解压后如下图所示：

![](https://img-blog.csdnimg.cn/d468ccb7b51e4880ad77fcc42092ed75.png)

本期内容就到这里，感谢你的阅读。


## 12 相关说明

 1. 制作不易，记得点赞+收藏+转发
 3. 本人技术有限，若有错误欢迎指正
 4. 本系统和文章均属于【IT学长】原创，转载请注明出处
