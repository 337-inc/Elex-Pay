Elex-Pay
========

#Elex PayCenter Document#

## ׼������ ##

�������ڽ���payelex֧��ƽ̨֮ǰ������ϵhuchao@elex-tech.com����ȡϵͳΪ�������APPID���������Ʊ��棬�⽫�ǿ����߽���֧��ƽ̨����Ҫƾ֤��

ͬʱ����������Ҫ��payelex�ṩ�ص���ַ(URL)��������֧����ɺ��֪������֧������ɡ�

## ֧��ԭ��ͼ ##
![֧��ԭ��ͼ](http://payment.eleximg.com/payment/pay/v3/paydocument01.png)

## ֧������ ##

1. �̼�����֧������
2. ��ת��payelex֧��ƽ̨����֧��ҳ��
3. ѡ��֧����ʽ����ת��������֧����������֧��
4. ������֧�������ص�֧��ƽ̨��֪ͨ�������
5. Payelex֧��ƽ̨�ص��̼ң�֪ͨ�������
6. �̼Ҹ�֪�̳��û��������

## ֧������ ##

#####�Զ�������ѡ��ҳ��#####

1. ����URL��ַ

	�����ѡ���Լ���������ѡ��ҳ�棬������Ҫpayelex֧��ƽ̨�ṩ��ҳ	�棬����ѡ������URL��Ϊ֧�������ַ:

	http://pay.337.com/v2/index.php?mod=do_payment&act=mall

2. HTTP����ʽ

	GET/POST

3. �������˵��


	�̼ҿ���ͨ�����½ӿڻ�ȡ����������Ϣ��

	`https://pay.337.com/v2/index.php?mod=listchannel&act=list`

	���ʴ˽ӿ�ʱ����Ҫ����Ĳ����У�
	* app_id:�����ǻ�ȡ��APPID

	����ʾ������app_id=1ʱ���˽ӿ�URLΪ��

	`https://pay.337.com/v2/index.php?mod=listchannel&act=list&app_id=1`

	�˽ӿڷ��صĸ�ʽΪjson�ַ�����

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

	statusΪ����״̬����ֵΪOKʱ��˵������������ȷ��

	data�г���app_idΪ1ʱ�����õ�channel��Ϣ����ʾ���п���������paypal��moneybookers��

	���������ݣ�
	* name��������
	* img��������logo
	* url��ѡ��������󣬷��������URL

	ȡ��������Ϣ����url��������²�������ͬ��������֧������,�������£�
	* item	����Ʒ���������룩
	* order_id	�������ţ��뱣֤���ֶε�Ψһ�ԣ����룩
	* gross	����Ҫ֧���ľ�������룩
	* currency	��֧�����õĻ��ҵ�λ��Ŀǰ֧�ֵĻ����У�USD(American Dollar)�����룩
	* custom_data	�������߷���֧��ʱ�Զ����ֶΣ��Ǳ��룩
	* activityid	������ͬһӦ�������ֲ�ͬ�Ļص���ַ���Ǳ��룩
	* return_url	��֧����ɻ�ʧ�ܺ����ת��ַ���Ǳ��룩

	���裬����app_idΪ1����ȡ��������Ϣ�У�����paypal��moneybookers���������������ѡ����paypal��Ϊ֧������������Եõ�����URL��

	`https://pay.337.com/v2/index.php?mod=do_payment&act=mall&app_id=1&channel=paypal`

	��Ҫ֧������Ʒ����Ϊexample2�����������ɵ�ORDERIDΪ20120102��֧�����Ϊ0.02�����ҵ�λΪUSD�������ɵĵ���ʾ�����£�

	`http://pay.337.com/v2/index.php?mod=do_payment&act=mall&app_id=1&item=example&order_id=20120101&gross=0.01&currency=USD&channel=paypal&paymentmethod=paypal`

	֮���ֱ����ת��������֧��������֧��ҳ�档

##### ʹ��payelex֧��ƽ̨������ѡ��ҳ�� #####

1. ����URL��ַ

	����ѡ��ʹ��payelex֧��ƽ̨�ṩ��֧������ѡ��ҳ��ʱ�������ѡ������URL��Ϊ֧�������ַ
	
	`http://pay.337.com/v2/index.php?mod=show_payment&act=mall`

2. HTTP����ʽ

	GET/POST

3. �������˵��
	* app_id	:����ʱ��ȡ��APPID�����룩
	* item	����Ʒ���������룩
	* order_id	�������ţ��뱣֤���ֶε�Ψһ�ԣ����룩
	* gross	����Ҫ֧���ľ�������룩
	* currency	��֧�����õĻ��ҵ�λ��Ŀǰ֧�ֵĻ����У�USD(American Dollar)�����룩
	* activityid	������ͬһӦ�������ֲ�ͬ�Ļص���ַ���Ǳ��룩
	* return_url	��֧����ɻ�ʧ�ܺ����ת��ַ���Ǳ��룩

	���裬�����߱������APPIDΪ1����Ҫ֧������Ʒ����Ϊexample�����������ɵ�ORDERIDΪ20120101��֧�����Ϊ0.01�����ҵ�λΪUSD�������ɵĵ���ʾ�����£�

	`http://pay.337.com/v2/index.php?mod=show_payment&act=mall&app_id=1&item=example&order_id=20120101&gross=0.01&currency=USD`

	�˽ӿڷ���HTML���ڷ��ص�ҳ���У�����ʾ��payelex֧��ƽ̨֧�ֵ�֧����ʽ������paypal��moneybookers�ȣ����������ͼ��ʾ��

	![֧��ԭ��ͼ](http://payment.eleximg.com/payment/pay/v3/paydocument02.png)

## �ص� ##

##### ����ӿڻص�URL #####

֧���ɹ����۳���Ӧ�˻��Ľ���payelex֧��ƽ̨ͨ��������ָ���Ļص���ַ(URL)�������ص��������ߡ�

������Ӧȷ���ص���ַ(URL)�ǿ����ڻ�������ֱ�ӱ����ʵģ�������ӵ�¼��֤�ȹ��ܣ�Ҳ����ʹ�ñ��ػ�������ڲ��ĵ�ַ��

##### �ӿڻص�����˵�� #####

* trans_id	:��payelex֧��ƽ̨���ɵĽ��׼�¼id
* user_id	�������߷���֧������ʱ��order_id
* timestamp	�����ν��׼�¼������ʱ���
* currency	��֧�����õĻ��ҵ�λ
* gross	��֧��������
* channel	:�����߾���ѡ���֧������������paypal��moneybooker��
* item	:����֧������ʱ���ݵ�item��ֵ
* custom_data	:�����߷���֧��ʱ�Զ����ֶΣ���֮ǰδ������Ϊ����֧������ʱ��order_id��
* status :����״̬��SUCCESS���ɹ���IN_CASE�����飬CANCEL_REVERSAL��ȡ�����飬APP_REVERSE���˿
* channel_data :������һЩ������Ϣ��json��ʽ����ͬ��������һ������Ŀǰֻ���paypal���ظ����û����䣩

##### �ӿڻص�������Ϣ #####

�ص���ַ�յ����ݺ�����payelex֧��ƽ̨���ؽ���״̬����ȷ�ķ��ظ�ʽΪ��3��USER_ID����

���磬�ڷ���֧������ʱ��order_idΪ20120101�����ص�������user_idΪ20120101���򵱿�������ȷ����ص�֮��Ӧ��payelex֧��ƽ̨���ء�3��20120101����

���֧��ƽ̨δ���յ���ȷ�ķ���ֵ��Payelex֧��ƽ̨���ظ���ص���ַ�������ݣ�����ʹ���Ϊ3��

##### �ص������֤ #####

��������ص�����֮ǰ��Ӧ�öԽ��յ��Ļص����ݽ�����֤��

Ϊ����֤���յ���������payelex֧��ƽ̨�Ļص���Ϣ��������������α�����ݣ�����ͨ�����·�ʽ���лص���֤��

1. �ص���֤����URL 

	�ڽ��յ��ص����ݺ󣬿�������ص���֤�������ַΪ��

	`http://pay.337.com/v2/index.php?mod=verify`

2. �ص���֤����ʽ 

	GET/POST

3. �ص���֤����˵��

	����ص���֤ʱ����Ĳ������£�
* trans_id	����payelex֧��ƽ̨���ɵĽ��׼�¼id
* user_id	��Payelex֧��ƽ̨�ص������е�user_id(�������߷���֧������ʱ��order_id)
* currency	��֧�����õĻ��ҵ�λ
* gross	��֧��������
* channel	�������߾���ѡ���֧������������paypal��moneybooker��

4. �ص���֤������Ϣ

	�ڽ��յ��ص���֤�����payelex֧��ƽ̨�������Ӧ�����ݻص���֤�������᷵�ز�ͬ����Ϣ�������ߣ�������Ϣ���뼰�������£�
* unkonwn transaction	������Ľ��׼�¼
* params error	���ص������д���
* system error	������ϵͳ������
* OK	����ȷ��������payelex֧��ƽ̨�Ļص�

## ����˵�� ##

�������ڽ���payelexƽ̨ʱ�����ṩ�����˺ţ�������������ʵС����ҽ��в��ԡ�

�ڿ��������У������������⣬��ӭ��ѯ�����ͷ�֧�֡�

