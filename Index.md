
# Activity
## 一、Activit的生命周期
1. onCreate()
2. onStart()
3. onResume()
4. onPause()
5. onStop()
6. onDestroy()

### 知识点
1. 屏幕旋转

    >默认情况下，屏幕旋转会使Activity重建，当然这不是我们想看到的，我们可以通过设置android:configChanges=“keyboardHidden|orientation”（属性很多，可能因机型原因需更改属性） 来阻止activity重建，也可以通过android:screenOrientation 来固定屏幕方向（landscape横向、portrait竖向）。

    >如果调用android:configChanges=“keyboardHidden|orientation”属性，则avtivity会执行onConfigurationChanged()方法来实现activity的旋转，不设置这个属性，onConfigurationChanged()方法也会照常执行。

## 二、Activity的启动模式
1. standard（默认）

    >我们平时直接创建的Activity都是这种模式的Activity，这种模式的Activity的特点是：只要你创建了Activity实例，一旦激活该Activity，则会向任务栈中加入新创建的实例，退出Activity则会在任务栈中销毁该实例。


2. singleTop

	>这种模式会考虑当前要激活的Activity实例在任务栈中是否正处于栈顶，如果处于栈顶则无需重新创建新的实例，会重用已存在的实例，否则会在任务栈中创建新的实例。


3. singleTask

	>如果任务栈中存在该模式的Activity实例，则把栈中该实例以上的Activity实例全部移除，调用该实例的onNewIntent()方法重用该Activity，使该实例处於栈顶位置，否则就重新创建一个新的Activity实例。

4. singleInstance

	>该模式Activity实例会单独放在一个新的任务栈中，只要该实例还在任务栈中，即只要激活的是该类型的Activity，都会通过调用实例的onNewIntent()方法重用该Activity，此时使用的都是同一个Activity实例。此模式一般用于加载较慢的，比较耗性能且不需要每次都重新创建的Activity。


### 知识点：
1. onNewIntent()

    >当①位于栈顶的singleTop模式的Activity被再次打开，②栈中任意位置打开singleTask模式的Activity，③再次打开singleInstance模式的Activity，会调用 onNewIntent()方法。
2. startActivity() 和 startActivityForResult()

    >startActivityForResult的主要作用就是它可以回传数据。
    使用 startActivityForResult() 方法打开新的Activity，新的Activity 关闭后会向前面的Activity传回数据，为了得到传回的数据，必须在前面的Activity中重写 onActivityResult() 方法。
    

## 三、显式和隐式调用Activity

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