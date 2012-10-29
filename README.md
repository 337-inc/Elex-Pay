Elex-Pay
========

#Elex PayCenter Document#

## 准备工作 ##

开发者在接入payelex支付平台之前，请联系huchao@elex-tech.com，获取系统为您分配的APPID，并且妥善保存，这将是开发者接入支付平台的重要凭证。

同时，开发者需要向payelex提供回调地址(URL)，用于在支付完成后告知开发者支付已完成。

## 支付原理图 ##
![支付原理图](http://payment.eleximg.com/payment/pay/v3/paydocument01.png)

## 支付流程 ##

1. 商家请求支付操作
2. 跳转到payelex支付平台，打开支付页面
3. 选择支付方式，跳转到第三方支付渠道进行支付
4. 第三方支付渠道回调支付平台，通知付费完成
5. Payelex支付平台回调商家，通知付费完成
6. 商家告知商城用户付费完成

## 支付接入 ##

#####自定义渠道选择页面#####

1. 请求URL地址

	如果您选择自己设置渠道选择页面，而不需要payelex支付平台提供此页	面，可以选择以下URL作为支付请求地址:

	http://pay.337.com/v2/index.php?mod=do_payment&act=mall

2. HTTP请求方式

	GET/POST

3. 请求参数说明


	商家可以通过以下接口获取可用渠道信息：

	`https://pay.337.com/v2/index.php?mod=listchannel&act=list`

	访问此接口时，需要传入的参数有：
	* app_id:申请是获取的APPID

	调用示例：当app_id=1时，此接口URL为：

	`https://pay.337.com/v2/index.php?mod=listchannel&act=list&app_id=1`

	此接口返回的格式为json字符串：

		{"status":"OK",
			"data":	{	
				"paypal":{
					"name":"paypal",
					"img":"https:\/\/elex_img_ak337-f.akamaihd.net\/payment\/pay\/paypal.png",
					"url":"https:\/\/pay.337.com\/v2\/index.php?mod=do_payment&act=mall&app_id=1&channel=paypal"
				},
				"moneybookers":{
					"name":"moneybookers",
					"img":"https:\/\/elex_img_ak337-f.akamaihd.net\/payment\/pay\/mb_ewallet.png",
					"url":"https:\/\/pay.337.com\/v2\/index.php?mod=do_payment&act=mall&app_id=1&channel=moneybookers"
				}
			}
		}

	status为请求状态，当值为OK时，说明请求数据正确。

	data列出了app_id为1时，可用的channel信息，此示例中可用渠道有paypal、moneybookers。

	渠道内数据：
	* name：渠道名
	* img：此渠道logo
	* url：选择该渠道后，发起请求的URL

	取得以上信息后，在url后添加以下参数，向不同渠道发送支付请求,参数如下：
	* item	：商品描述（必须）
	* order_id	：订单号，请保证此字段的唯一性（必须）
	* gross	：需要支付的具体金额（必须）
	* currency	：支付所用的货币单位，目前支持的货币有：USD(American Dollar)（必须）
	* custom_data	：开发者发起支付时自定义字段（非必须）
	* activityid	：用于同一应用下区分不同的回调地址（非必须）
	* return_url	：支付完成或失败后的跳转地址（非必须）

	假设，您的app_id为1，获取的渠道信息中，包括paypal及moneybookers两个渠道，如果您选择了paypal作为支付渠道，则可以得到以下URL：

	`https://pay.337.com/v2/index.php?mod=do_payment&act=mall&app_id=1&channel=paypal`

	需要支付的商品名称为example2，开发者生成的ORDERID为20120102，支付金额为0.02，货币单位为USD，则生成的调用示例如下：

	`http://pay.337.com/v2/index.php?mod=do_payment&act=mall&app_id=1&item=example&order_id=20120101&gross=0.01&currency=USD&channel=paypal&paymentmethod=paypal`

	之后会直接跳转到第三方支付渠道的支付页面。

##### 使用payelex支付平台的渠道选择页面 #####

1. 请求URL地址

	当您选择使用payelex支付平台提供的支付渠道选择页面时，则可以选择以下URL作为支付请求地址
	
	`http://pay.337.com/v2/index.php?mod=show_payment&act=mall`

2. HTTP请求方式

	GET/POST

3. 请求参数说明
	* app_id	:申请时获取的APPID（必须）
	* item	：商品描述（必须）
	* order_id	：订单号，请保证此字段的唯一性（必须）
	* gross	：需要支付的具体金额（必须）
	* currency	：支付所用的货币单位，目前支持的货币有：USD(American Dollar)（必须）
	* activityid	：用于同一应用下区分不同的回调地址（非必须）
	* return_url	：支付完成或失败后的跳转地址（非必须）

	假设，开发者被分配的APPID为1，需要支付的商品名称为example，开发者生成的ORDERID为20120101，支付金额为0.01，货币单位为USD，则生成的调用示例如下：

	`http://pay.337.com/v2/index.php?mod=show_payment&act=mall&app_id=1&item=example&order_id=20120101&gross=0.01&currency=USD`

	此接口返回HTML，在返回的页面中，会显示出payelex支付平台支持的支付方式，例如paypal、moneybookers等，具体界面如图所示。

	![支付原理图](http://payment.eleximg.com/payment/pay/v3/paydocument02.png)

## 回调 ##

##### 定义接口回调URL #####

支付成功，扣除相应账户的金额后，payelex支付平台通过开发者指定的回调地址(URL)将参数回调给开发者。

开发者应确保回调地址(URL)是可以在互联网上直接被访问的，切勿添加登录验证等功能，也不能使用本地或局域网内部的地址。

##### 接口回调参数说明 #####

* trans_id	:由payelex支付平台生成的交易记录id
* user_id	：开发者发起支付请求时的order_id
* timestamp	：本次交易记录产生的时间戳
* currency	：支付所用的货币单位
* gross	：支付具体金额
* channel	:开发者具体选择的支付渠道：例如paypal、moneybooker等
* item	:发起支付请求时传递的item的值
* custom_data	:开发者发起支付时自定义字段（若之前未传，则为发起支付请求时的order_id）
* status :交易状态（SUCCESS：成功，IN_CASE：争议，CANCEL_REVERSAL：取消争议，APP_REVERSE：退款）
* channel_data :渠道的一些额外信息，json格式，不同的渠道不一样。（目前只针对paypal返回付款用户邮箱）

##### 接口回调返回信息 #####

回调地址收到数据后请向payelex支付平台返回接收状态，正确的返回格式为”3，USER_ID”。

例如，在发起支付请求时的order_id为20120101，即回调参数中user_id为20120101，则当开发者正确处理回调之后，应向payelex支付平台返回”3，20120101”。

如果支付平台未接收到正确的返回值，Payelex支付平台会重复向回调地址发送数据，最大发送次数为3。

##### 回调结果验证 #####

在您处理回调数据之前，应该对接收到的回调数据进行验证。

为了验证您收到的是来自payelex支付平台的回调信息，而不是其他的伪造数据，可以通过以下方式进行回调验证。

1. 回调验证请求URL 

	在接收到回调数据后，可以请求回调验证，请求地址为：

	`http://pay.337.com/v2/index.php?mod=verify`

2. 回调验证请求方式 

	GET/POST

3. 回调验证参数说明

	请求回调验证时所需的参数如下：
* trans_id	：由payelex支付平台生成的交易记录id
* user_id	：Payelex支付平台回调参数中的user_id(即开发者发起支付请求时的order_id)
* currency	：支付所用的货币单位
* gross	：支付具体金额
* channel	：开发者具体选择的支付渠道：例如paypal、moneybooker等

4. 回调验证返回信息

	在接收到回调验证请求后，payelex支付平台会给出回应，根据回调验证结果，则会返回不同的信息给开发者，返回消息代码及含义如下：
* unkonwn transaction	：不详的交易记录
* params error	：回调参数有错误
* system error	：发生系统级错误
* OK	：正确的来自于payelex支付平台的回调

## 其他说明 ##

开发者在接入payelex平台时，不提供测试账号，开发者需用真实小额货币进行测试。

在开发过程中，如有其它问题，欢迎咨询技术客服支持。

