# User Notifications 用户通知
总体的意思就是支持了很多用户定义的通知，并且可以捕捉到各个通知状态的回调。以往通知的概念是：大家想接收的都提前做好准备，然后一下全量分发，没收到也不管了，也不关心发送者。现在用户通知做成了和网络请求有点像 一个先发request再得到response的流程，甚至封装了error，可以在各个状态的方法中做一些额外操作，并且也能取到一些字段，如发送者等。

此功能的头文件入口在#import <UserNotifications/UserNotifications.h><br />

<img src="https://github.com/dsxNiubility/SXDiscoveryIOS10/raw/master/Images/Notification.png" alt="Drawing" width="500px" />


####1.NSString+UserNotifications.h

有一个方法 localizedUserNotificationStringForKey: arguments: （提供该通知被呈现时的本地化字符串），猜测下面的类有很多initWithIdentifier的，他们的indentifier就是这个。

####2.UNError.h

有一个属性UNErrorDomain 和一个枚举 UNErrorCode，顾名思义。

####3.UNNotification.h

里面有两个属性，date日期 和 request，这个request是上面“8”的类型UNNotificationRequest，点进去看了下比较清晰，有identifier标识，content内容，trigger触发条件， 和带上这三个东西的初始化方法。 其中内容 和 触发条件这两个属性，分别是上面“7” 和 “12”的类型，这个下面再谈。

####4.UNNotificationAction.h

这个类突出的是一个通知的动作，有identifier，title，options（枚举，就是通知当前的权限，允许？拒绝？前台时允许？）属性。然后就是带上这三个东西的初始化方法。 然后比较费解的就是下面有一个子类UNTextInputNotificationAction ，这个子类有两个额外属性， 按钮title，和文本框placeholder， 为什么会是这两个属性？ 莫非是点击通知后下拉出的快速回复，有一个输入框和一个按钮。

####5.UNNotificationAttachment.h

这个里面就是URL（资源url属性），type（附件类型）。 然后是带上这两个属性的初始化方法。 下面声明了几个字符串常量，暂时还不知道具体用在哪里，typeHint，hiddenKey，clippingRectKey，TimeKey。

####6.UNNotificationCategory.h

有indentifier属性，actions（里面是数组），minimalActions（最重要的数组，就是只能给你两个位置显示你显示哪两个，这么个意思），intentIdentifiers属性（应该是和上面的动作数组关联的吧），options（权限相关，无？允许自定义关闭？允许车载系统交互？）。最后就是把这些都带上的init方法。  猜测这个类之所以取名叫category应该是，在某个地方展示通知的时候会把所有通知一一分类， 然后每个类别的通知可能最多只能让你展示几个，如果不做限制应该会展示全部通知，如果权限设置的是允许自定义关闭那可能就是支持类似一键清除的操作。

####7.UNNotificationContent.h

消息的内容，一看就能知道应该是一个类似于Entity的东西，里面装有大量的属性：attachments（可选的附件集合），badge（小红点数量），body，categoryIndentifier，launchImageName（从消息里点开的应用程序应该能看到启动图对吧），subtitle，threadIdentifier（与request关联），title，userInfo，sound这个是“11”的类型，应该是同时来时的声音，点开“11”看一下 ，就俩方法，defaultSound，soundNamed: 自定义声音，都在~/Library/Sounds 目录下。 恩再回到刚才那个content类里面有个子类UNMutableNotificationContent，属性和父类相同，只不过是子类的属性都可以修改了，父类的那些属性都是readonly的。

####8.UNNotificationRequest.h 上面第3条说过了

####9.UNNotificationResponse.h 

有action，也有request，那也就有response，这里面有两个属性，notification，actionIdentifier  响应里就这俩破玩意。 然后有个子类UNTextInputNotificationResponse， 这里面就一个属性userText ，看命名很好猜，应该就是前面说的那个有输入框里输入的内容。

####10.UNNotificationSettings.h

这个类里就是一些设置了，有一个枚举说的是有没有权限，一个枚举说的是不支持？禁用？启用？。 然后下面一大波属性，小红点设置，声音设置，弹窗设置等等 都是这个枚举类型， 最后还有个alertStyle属性（枚举，None？Banner？alert？）。

####11.sound前面第7条说过了

####12.UNNotificationTrigger.h

有一个属性 repeats（是否重复发通知）。 下面有四个子类，push通知触发， 时间通知触发，日历通知触发，地区通知触发， 时间的有timeInterval属性， 日历的有dateComponents属性。 然后时间和日历的子类都有nextTriggerDate 方法。

####13.UNUserNotificationCenter.h

这里面东西多到吐了，同学你记得NSNotificationCenter么？ 需要提一点的就是以前的通知中心有个方法[NSNotificationCenter defaultCenter]， 这里是[UNUserNotificationCenter currentNotificationCenter]， 提醒一下到时候别说敲不出来。 方法大多是一些remove，add，get等操作， 还有2个代理方法：通知将要发出去时调用，收到通知的response后调用。

####14.UNNotificationServiceExtension.h

里面有两个方法，收到通知的请求后调用， 系统将要销毁时调用。

 

通知里面有UI相关的类 #import <UserNotificationsUI/UserNotificationsUI.h>

这个类里面就一个文件， 而且方法比较单一，就是收到通知调用，和收到通知的响应调用。 其他方法也就是mediaPlay 和 mediaPause 。和一些多媒体播放的按钮frame，color等， 这里面的作用难道仅仅就是通知来了后播放的音乐暂时暂停下，响一声通知，再播放？ 具体WWDC2016上说的锁屏页面的通知样式处理的api是在下面的部件增强章节中。

