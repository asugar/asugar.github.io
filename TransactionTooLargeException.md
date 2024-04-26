# 问题报错：TransactionTooLargeException
```
04-25 15:10:08.654  2129  2129 E JavaBinder: !!! FAILED BINDER TRANSACTION !!!  (parcel size = 550048)
04-25 15:10:08.656  2129  2129 W ActivityThread: Bundle stats:
04-25 15:10:08.656  2129  2129 W ActivityThread:   android:viewHierarchyState [size=1124]
04-25 15:10:08.657  2129  2129 W ActivityThread:     android:views [size=1076]
04-25 15:10:08.660  2129  2129 W ActivityThread:   androidx.lifecycle.BundlableSavedStateRegistry.key [size=548212]
04-25 15:10:08.661  2129  2129 W ActivityThread:     android:support:activity-result [size=2404]
04-25 15:10:08.662  2129  2129 W ActivityThread:       KEY_COMPONENT_ACTIVITY_REGISTERED_KEYS [size=1712]
04-25 15:10:08.664  2129  2129 W ActivityThread:     android:support:fragments [size=545616]
04-25 15:10:08.666  2129  2129 W ActivityThread:       android:support:fragments [size=545544]
04-25 15:10:08.667  2129  2129 W ActivityThread: PersistableBundle stats:
04-25 15:10:08.667  2129  2129 W ActivityThread:   [null]
04-25 15:10:08.669  2129  2129 E AndroidRuntime: FATAL EXCEPTION: main
04-25 15:10:08.669  2129  2129 E AndroidRuntime: Process: com.youdao.pocket, PID: 2129
04-25 15:10:08.669  2129  2129 E AndroidRuntime: java.lang.RuntimeException: android.os.TransactionTooLargeException: data parcel size 550048 bytes
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at android.app.ActivityThread$StopInfo.run(ActivityThread.java:3991)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at android.os.Handler.handleCallback(Handler.java:790)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at android.os.Handler.dispatchMessage(Handler.java:99)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at android.os.Looper.loop(Looper.java:164)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at android.app.ActivityThread.main(ActivityThread.java:6548)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at java.lang.reflect.Method.invoke(Native Method)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:438)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:857)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: Caused by: android.os.TransactionTooLargeException: data parcel size 550048 bytes
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at android.os.BinderProxy.transactNative(Native Method)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at android.os.BinderProxy.transact(Binder.java:764)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at android.app.IActivityManager$Stub$Proxy.activityStopped(IActivityManager.java:4658)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	at android.app.ActivityThread$StopInfo.run(ActivityThread.java:3975)
04-25 15:10:08.669  2129  2129 E AndroidRuntime: 	... 7 more
04-25 15:10:08.670  2129  2129 I LogUtilsKt: pocket handleException java.lang.RuntimeException: android.os.TransactionTooLargeException: data parcel size 550048 bytes
```

# Bundle 存储1M得限制是在哪里？



## 问题原因
1) activity / fragment 跳转时传递的bundle携带了过大的数据
2）Activity.onSaveInstanceState()保存了过大的数据
3）FragmentStatePagerAdapter的saveState保存了过多的历史Fragment实例的状态数据，重写saveState
4）NavHostFragment
onSaveInstanceState  -> 
5）ViewPager2



https://github.com/guardian/toolargetool
```
public class TransactionTooLargeException extends RemoteException {
    public TransactionTooLargeException() {
        super();
    }

    public TransactionTooLargeException(String msg) {
        super(msg);
    }
}
```
