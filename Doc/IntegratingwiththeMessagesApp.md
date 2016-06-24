# Integrating with the Messages App 与系统短信 app交互

<img src="https://github.com/dsxNiubility/SXDiscoveryIOS10/raw/master/Images/Messages.png" alt="Drawing" width="500px" />

####1.MSMessagesAppViewController.h

这个类应该就是苹果自己的消息界面，你可以继承他写你自己自定义的界面。 属性有：activeConversation 指的是当前的会话对象，是上面“2”这个类型，具体详细可以看下面的第“2”点、还有个是presentationStyle（外观样式，枚举类型，紧缩？扩张？）。 接下来就是方法了：requestPresentationStyle（请求消息过渡到指定的样式），dismiss消除方法。 然后就是一波生命周期方法了，每一类都有will和did，会话信息将要（已经）活跃时，将要（已经）解除活跃，将要（已经）选择信息，将要（已经）收到信息，将要（已经）开始发送，将要（已经）取消发送，将要（已经）开始过渡。

####2.MSConversation.h

属性有localParticipantIdentifier（当前会话参与者生成的标识，他说只有删了App才会变 姑且理解成id是不会变的），remoteParticipantIdentifiers（远端的标识符数组），selectedMessage（选中的信息），以及4个对象方法 插入一条信息，插入一个标签，插入一段文本，插入一个附件。 这四个方法都有成功的回调。

####3.MSSession.h

这个类里面是空的，解释说是用session来处理消息序列间的关系。可能就是占个位，以后估计会添加东西。 这个MSSession是后面很多参数的类型，应该就是区分消息类似于标识符的作用。 

####4.MSMessage.h

初始化方法是initWithSession ，没错就是上面那个MSSession。 除了初始化方法剩下的就全是属性了：session，senderParticipantIdentifier（发送者的标识符），layout布局这个是“5”这个类型，URL，shouldExpire（选yes会自动消失，用户手动选择为这条消息续命），accessibilityLabel（残疾人模式支持），error。

####5.MSMessageLayout.h

这个是抽象类，里面是空的，就是个布局文件，继承自NSObject。

####6.MSMessageTemplateLayout.h

继承上面那个类，看名字是模板布局后面应该会用的挺多的，里面的属性有，标题，子标题，尾部标题，尾部子标题，图片，多媒体URL，图片标题，图片子标题。 

####7.MSSticker.h

应该是消息上的表情包。 里面就有两个属性imageFileURL ，localizedDescription 图片和局部描述。然后是带上这两个属性的初始化方法 initWithContentsOfFileURL: localizedDescription: 。

####8.MSStickerView.h

这个类就是一个view，里面包着一个sticker，也就是包裹着上面那个装饰品的view。 提供了带上sticker的初始化方法，一个常规属性animationDuration，和三个方法startAnimating，stopAnimating，isAnimating。

####9.MSStickerBrowserViewDataSource.h

细思极恐，这个类不就是wwdc2016上说的那个可以在消息下面添加自定义表情的地方么。 符合datasource的风格，里面就两个方法，numberOfStickersInStickerBrowserView: （返回一个总数），stickerBrowserView：stickerAtIndex：（返回这个索引下的内容）。

####10.MSStickerBrowserView.h

上面那个是datasource，那这个就是用了上面数据源的view呗。 除了初始化方法，有两个属性 stickerSize（枚举，小，中，大），dataSource（就是上面的“9”），还有个人reloadData方法。

####11.MSStickerBrowserViewController.h

上面是个view， 这个就是承载上面那个view的viewcontroller。肯定得有这个属性stickerBrowserView 和初始化方法。

 

这个message模块还有UI相关的api   #import <MessageUI/MessageUI.h>

就是两个VC ,MFMailComposeViewController,MFMessageComposeViewController。 这两个都是继承自UINavigationController.   觉得这两个就是发邮件的编辑页面，和发消息的编辑页面。  发邮件的页面里有 canSendMail （Bool方法），set主题，set发件人，set收件人，set内容，set附件。 然后有一个代理，和代理方法，猜也能猜到 就是成功失败回调。mailComposeController:didFinishWithResult: error:  。 那另一个消息和这差不多了就不说了。

