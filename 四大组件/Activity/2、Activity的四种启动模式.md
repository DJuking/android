Activity的启动模式
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