Android
##http://blog.csdn.net/a296777513/article/details/73610719

1、本地广播和全局广播有什么差别



2、Android进程优先级

  进程分为五个常用的等级：
   1、前台进程（Foreground process）
   杀死前台进程需要与用户交互，应为前台进程的优先级是最高的。
   2、可见进程（Visable process）
   可见进程也被认为是很重要的，一般不会销毁，除非是为了保证所有前台进程的运行而不得不杀死前台进程对的时候。
   3、服务进程（Service process）
   尽管服务进程没有和用户可以看到的东西，但是它们一般在做的事情是用户关心的，比如播放音乐，后台下载数据等。所以系统会尽量维持他们的运行，除非系统内存不足以维持前台进程和可见进程的运行需要。
   4、后台进程（Background process）
   后台进程不直接影响用户体验，系统为了前台进程，可见进程，服务进程而任意杀死后台进程。
   通常会有很多个后台进程的存在，它们会保存在一个LRU（least recently used）列表中，这样就可以确认用户最近使用的activity最后被销毁，即先销毁时间最远的activity。
   5、空进程
   如果一个进程不包含任何活跃的组件，则认为是空进程。
   保存这种进程唯一的理由是为了缓存需要，为了加快下次要启动这个进程中的组件时需要的启动时间。系统为了平衡进程缓存和底层内存缓存的资源，经常杀死空进程。


   保活策略：

   尽可能保证service不是常用技巧
   1、在Androidmanidest.xml文件中对于intent-filter可以通过android：priority="1000"这个属性设置最高优先级，1000是最高值，如果数字越小，优先级最低，同时适用于广播。
   2、在onStartCommand里面调用startForeground方法把service优先级提升为前台进程级别，然后在onDestory()里面记得调用stopForeground()方法。
   3、onStartCommand方法，返回START_STICKY.
   4、在onDestory方法里发广播重启service.
   5、监听系统广播判断service状态。
   6、Application加上Persistent属性。
   7、类似监听锁屏方法
   QQ采取在锁屏的时候启动一个1像素的activity,用户解锁以后将这个activityo结束掉（顺便同时把自己的核心服务在重启一次）
   8、双进程守护+JobScheduler调度
   双进程守护，可以防止单个进程被杀死，同事可以防止第三方的360清理掉。
   一个进程被杀死，另外一个进程又被他启动。相互监听启动。A<--->B
   杀进程是一个个杀的，本质上是和时间再赛跑。

   JobScheduler
   JobScheduler来执行一些满足特定条件但不紧急的后台任务，把任务加到系统调度队列中，当到达任务窗口期的时候就会执行，我们可以在这个里面启动我们的进程。
   这样可以做到将近杀不死的进程。



   ####
   http://blog.csdn.net/chenliguan/article/details/54603611
   http://blog.csdn.net/wuseyukui/article/details/48004687
   http://blog.csdn.net/fhy_2008/article/details/7328967
