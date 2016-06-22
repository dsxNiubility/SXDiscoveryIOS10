# Speech Recognition 语音识别转文字


<img src="https://github.com/dsxNiubility/SXDiscoveryIOS10/raw/master/Images/SpeechRecognition.png" alt="Drawing" width="500px" />

####1.SFSpeechRecognitionResult.h

这个类里有三个属性：bestTranscription 就是最优的转化结果咯，是上面的“7”这个类型的。然后再看下这个SFTranscription.h ，果然不出所料 有两个属性 一个是字符串类型formattedString 一个是数组类型的segments ，恩 前者就是转化后的字符串，后者是分割后的一个个小结果集合。 然后这个分割的一个个小结果呢又是上面“6”这个类型。那再看一下“6” 里面的属性就是 substring， 时间戳，duration，准确性，备选答案数组，这些很清晰的东西了。

####2.SFSpeechRecognitionRequest.h

这个类里东西有点多，属性taskHint，是上面“4”这个类型，点开一看就是一个枚举，用来区分你这个语音识别的请求是哪一类的 查找？确认？听写？无法识别？。 接下来是两个BOOL类型的，shouldReportPartialResults（是否语音局部的一块一块也要处理？默认选false就是一句话全说完了再上传吧），detectMultipleUtterances（假如你说了10秒钟，只有后5秒匹配到了结果，那你前面删了还是保留？默认不删），然后是分析到的关键字数组，和标识符什么的。 然后这个request有两个子类，一个是从本地URL读取 一个声音文件去识别， 一个是默认做法用话筒和AVFoundation库接收到声音去识别，然后有几个拼接声音的API。

####3.SFSpeechRecognitionTask.h

从名字就能看出来这是语音识别最重要的一个类了，里面的属性有：state这是一个枚举，说明当前状态是进行中？已完成？被取消？等等。 接下来是三个常见的 isFinishing ，isCancelled ，error 。 接下来是 isPowerAvailable （是否开启说话声音大小的监测？），peakPower（最大声音），averagePower（平均声音）。 属性就这些了，接下来就是一个协议和一波代理方法：刚刚识别出话语调用，猜测话语时调用，话说完了调用，取消时调用，等等等，你能想到的回调方法苹果应该都有的。

####4.上面第2条里面说过了

####5.SFSpeechRecognizer.h

和系统的那些相机权限，通讯录权限有点像， 就是现在的状态是什么？同意？拒绝？还是未选择过？ 然后提供了方法让用户去选择。 然后有些属性：NSSet类型的supportedLocales（支持地区方言的集合），

available是否可用，locale当前地区 ，defaultTaskHint默认类别，request（就是上面说的请求），队列，代理。 然后有个协议和代理方法：发现用户给与的权限发生改变时调用。

####6和7. 上面第1条里说过了 



