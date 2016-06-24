# Wide Color 宽域颜色

文档的原话说：大多数的 core字打头的图形框架 还有AVFoundation 都大大提高了对扩展像素和宽色域色彩空间的支持。通过图形堆栈扩展这种方式比以往支持广色域的显示设备更加容易。现在对UIKit扩展可以在sRGB的色彩空间下工作，性能更好，也可以在更广泛的色域来搭配sRGB颜色。 然后说了几个场景说建议你用sRGB吧，比如依赖于UIkit的clamp component values的应用程序，或是使用较低级别api执行自己图像处理的 都建议用sRGB吧。

然后看了下UIColor类里 到底什么是sRGB？ 发现多了两个iOS10新增的api。 

	+ (UIColor *)colorWithDisplayP3Red:(CGFloat)displayP3Red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha NS_AVAILABLE_IOS(10_0);
 
	- (UIColor *)initWithDisplayP3Red:(CGFloat)displayP3Red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha NS_AVAILABLE_IOS(10_0);



