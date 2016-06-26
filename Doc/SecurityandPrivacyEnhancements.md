# Security and Privacy Enhancements 安全和保密性增强

安全方面在iOS10中引入了更多修改和补充，具体有以下几点：

1.在info.plist文件新增了一个key，NSAllowsArbitraryLoadsInWebContent，允许任意web页面加载，同时苹果会用ATS保护你的app。

2.使用改进后的SecKey API 而不是过时的 CDSA API。

3.安全传输API中不再支持SSLv3， 建议你们尽快停用SHA1和3DES加密算法。

4.剪贴板的扩展，因为wwdc2016演示了可以跨设备复制粘贴啊，那肯定要做一些限制可见（#import <UIKit/UIPasteboard.h>）

5.这点最重要的，建议尽快适配， 所有和用户权限相关的地方必须在info.plist里配置里面包括

	NSBluetoothPeripheralUsageDescription
	NSCalendarsUsageDescription
	NSCameraUsageDescription
	NSContactsUsageDescription
	NSHealthShareUsageDescription
	NSHealthUpdateUsageDescription
	NSHomeKitUsageDescription
	NSLocationAlwaysUsageDescription
	NSLocationWhenInUseUsageDescription
	NSMicrophoneUsageDescription
	NSMotionUsageDescription
	NSPhotoLibraryUsageDescription
	NSRemindersUsageDescription
	NSSiriUsageDescription
	NSSpeechRecognitionUsageDescription
	NSVideoSubscriberAccountUsageDescription
	NSVoIPUsageDescription

虽然现在还没有iOS10系统的手机，但是我用模拟器试了下，亲测如果我想唤起通讯录但是没有配置NSContactsUsageDescription，刚启动时不会崩溃，但是在唤起操作发生时会直接崩溃。 在info.plist设置之后就可以正常使用了。
<img src="https://github.com/dsxNiubility/SXDiscoveryIOS10/raw/master/Images/Security.png" alt="Drawing" width="500px" />
