显式和隐式调用Activity

1、这是隐式调用系统短信应用的方法：

	/**
	 * 隐式意图的方法启动系统短信
	 * 
	 * 简单概括就是： 意图包括：Action（动作），Category（附加信息），Data（数据，具体内容），Tpye(类型)等等，举个例子，
	 * 说白了意图就是启动一个组件的的完整的动作信息
	 * ，就像打人，打就是Action动作，人就是Data内容，而Type就是类型，打什么人呢？打坏人，type就是坏指的类型
	 * ，只有这些信息全了才能执行一个完整的意图
	 * ，当然还有一些信息，比如scheme就是URI类型的数据的前缀，就像这个例子当中的sms:，还有host主机名，path路径等
	 * 
	 * @param view
	 */
	public void startOne(View view) {
		Intent intent = new Intent();
		intent.setAction("android.intent.action.SENDTO");// 发送信息的动作
		intent.addCategory("android.intent.category.DEFAULT");// 附加信息
		intent.setData(Uri.parse("sms:10086"));// 具体的数据，发送给10086
		startActivity(intent);
	}

2、这个是自己写的隐式意图方法：

	public void startTwo(View view) {  
        Intent intent = new Intent();  
        intent.setAction("net.loonggg.xxx");  
        intent.addCategory("android.intent.category.DEFAULT");  
        intent.setDataAndType(Uri.parse("loonggg://www.baidu.com/person"),  
                "person/people");  
        startActivity(intent);  
    }  

同时还要写册信息：

	 <activity android:name="net.loonggg.intent.SecondActivity" >
            <intent-filter>

                <!-- 自定义的动作 -->
                <action android:name="net.loonggg.xxx" />
                <!-- 自定义的scheme和host -->
                <data
                    android:host="www.baidu.com"
                    android:path="/person"
                    android:scheme="loonggg" />
                <!-- 自定义的类型 -->
                <data android:mimeType="person/people" />
                <!-- 附加信息 -->
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>