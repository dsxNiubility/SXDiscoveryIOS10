# Proactive Suggestions 系统预先建议

背景就是iOS9的时候系统给予的主动建议会通过：Spolight搜索，Safari搜索，Handoff，或者siri建议。 在iOS10之后新增了，键盘QuickType建议，地图，车载娱乐，应用切换，siri交互，锁屏播放。 比如你正在一个应用里看一个酒店，可以使用mapitem属性保存正在查看的这个酒店的位置，然后你切换旅行或地图App时这个位置可以自动提供使用。  如果你需要这样利用系统来共享一个位置，那你需要指定这个位置的经纬度，地名,电话等属性 来便于siri的直接调起。

文档中还列出了几种场景

1.在输入框（UITextFiled）输入时，可以指定一下这个输入框的类型，以便系统可以分析出用户的语义。 是电话类型就建议一些电话，是地址类型就建议一些地址。看下头文件（#import <UIKit/UITextInputTraits.h>）可指定的类型 就是这个新增的textContentType字段，里面有很多种类型可选。

	UIKIT_EXTERN NSString *const UITextContentTypeName                      NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeNamePrefix                NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeGivenName                 NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeMiddleName                NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeFamilyName                NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeNameSuffix                NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeNickname                  NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeJobTitle                  NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeOrganizationName          NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeLocation                  NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeFullStreetAddress         NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeStreetAddressLine1        NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeStreetAddressLine2        NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeAddressCity               NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeAddressState              NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeAddressCityAndState       NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeSublocality               NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeCountryName               NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypePostalCode                NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeTelephoneNumber           NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeEmailAddress              NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeURL                       NS_AVAILABLE_IOS(10_0);
	UIKIT_EXTERN NSString *const UITextContentTypeCreditCardNumber          NS_AVAILABLE_IOS(10_0);
	
2.如果是视频类App可以使用MPPlayableContentManager （#import <MediaPlayer/MPPlayableContentManager.h>）看了下，新增了一个属性nowPlayingIdentifiers，苹果的意思应该是只要你以前是用这个多媒体类播放音乐的我就可以让你在锁屏页面交互，需要配置在这个数组里。  

3.如果是出行类app可以使用MKDirectionsRequest。 （#import <MapKit/MKDirectionsRequest.h>  ）这个类里几乎没有新增api，iOS10就新增了一个枚举，而且看上去就是个默认值。如果要使用此功能，需要配置在info.plist文件里 新增key - value ，MKDirectionsApplicationSupportedModes - MKDirectionsModeRideShare。