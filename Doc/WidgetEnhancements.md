# Widget Enhancements 锁屏部件增强

现在锁屏界面有了新的设计，建议我们废弃以前的notificationCenterVibrancyEffect 改用widgetPrimaryVibrancyEffect或者widgetSecondaryVibrancyEffect，并且窗口的小部件可以让你描述有多少东西可用，支持紧凑和扩展两种形态。

这些新旧的Effect效果在这个类下，可能是之前锁屏玩不出什么花样所以大家没怎么关注这里。

import <NotificationCenter/NotificationCenter.h> 里面有三个头文件

<img src="https://github.com/dsxNiubility/SXDiscoveryIOS10/raw/master/Images/Widget.png" alt="Drawing" width="500px" />


####1.NCWidgetProviding.h

先来两个方法 

	- (void)widgetPerformUpdateWithCompletionHandler:(void (^)(NCUpdateResult result))completionHandler;
这个方法如果实现了，系统将在适当的时候召唤部件更新形态，无论是在通知中心还是后台。 需要启用后台更新功能，部件会在异步工作主线程更新，调用参数块的工作完成后会得到相应的结果。

	- (void)widgetActiveDisplayModeDidChange:(NCWidgetDisplayMode)activeDisplayMode withMaximumSize:(CGSize)maxSize;
这个方法应该是部件变化时调用，参数是最大有多大。

这里声明了一个分类UIVibrancyEffect (NCWidgetAdditions)，里面就是本章节说的iOS10新增API

	+ (UIVibrancyEffect *)widgetPrimaryVibrancyEffect NS_AVAILABLE_IOS(10_0);
	 
	+ (UIVibrancyEffect *)widgetSecondaryVibrancyEffect NS_AVAILABLE_IOS(10_0);
这两个方法名字上是老大和老二，有什么区别？ 都是用在选择的文字或图形上，默认用上面，如果开启了further diminution（应该是类似于上面压缩模式）就用下面的。

下面又声明了一个分类NSExtensionContext (NCWidgetAdditions)，里面也是iOS10的新增API

里面有两个属性 widgetLargestAvailableDisplayMode ，widgetActiveDisplayMode 。 是两种显示模式是NCWidgetDisplayMode枚举类型，有紧缩和扩张两种。 ，估计假如是新闻通知一个是一般大小，一个是点开详情的大小。 然后就是一个方法widgetMaximumSizeForDisplayMode ，返回值是CGSize取到播放模式的最大尺寸。

####2.NCWidgetController.h

里面除了个初始化方法，还有一个方法

	- (void)setHasContent:(BOOL)flag forWidgetWithBundleIdentifier:(NSString *)bundleID;
第一个参数默认为yes，就是该展示
时就展示，这个方法可以跨小组件间通讯，以及和providing app交互。

####3.NCWidgetTypes.h

里面就一个枚举类型NCWidgetDisplayMode ，前面第1点说过了。