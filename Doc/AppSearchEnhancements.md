# App Search Enhancements 应用搜索增强

iOS10的搜索功能做了一定增强：应用程序内搜索，搜索传递，考虑私人差异，结果可视化。 使用CSSearchQuery类，调用Core Spotlight的api，可以让你不必自己维护自己的搜索索引，关于对搜索关键字的处理，还有考虑到不同类别差异导致搜索结果的排序都是苹果帮你处理。

并且搜索结果可以继续往下传递，假设你用Core Spotlight搜索火车站，提示的是地图类app搜索火车站的结果，你点进去后，这个地图类app会接收到“火车站”这个字段在应用内也完成搜索。支持此功能也是需要配置plist文件:key-value  CoreSpotlightContinuation-YES，然后设置CSQueryContinuationActionType（#import<CoreSpotlight/CSSearchableItem.h>）。最后传递的搜索字符串用continueUserActivity：restorationHandler：方法接收。

然后现在看一下#import <CoreSpotlight/CSSearchQuery.h>头文件里面的结构。

看上去这个CSSearchQuery像是一个查询语句操作，有创建，查询成功和错误等。初始化方法是initWithQueryString: attributes:。 有isCanceled属性 和 cancel 和 start方法。 还有foundItemCount属性，看上去是能够得到搜索的结果个数。protectionClasses(数组)，看上去像是隐私相关受保护的文件。 还有两个block，一个是搜索结束后回调，参数是NSError；一个是查询到结果时回调，参数是items数组。这个items数组都是CSSearchableItem类型，这里面有个attributeSet属性，里面可以传入以下类型

<img src="https://github.com/dsxNiubility/SXDiscoveryIOS10/raw/master/Images/Search.png" alt="Drawing" width="500px" />