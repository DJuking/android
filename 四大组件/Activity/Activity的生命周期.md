## Activit的生命周期
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