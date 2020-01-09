
# 最新海康摄像机、NVR、流媒体服务器、回放取流RTSP地址规则说明

原文链接：https://blog.csdn.net/xiaole0313/article/details/94785643

---

本文档主要介绍海康威视设备预览、回放、流媒体取流的RTSP URL和IE直接预览、回放的HTTP URL。

RTSP为取流协议，取到码流后需要解码显示，可以通过VLC播放器进行测试，IE等浏览器网页不支持RTSP协议直接取流预览或者回放。

网页上需要跳过登录界面直接访问我们设备的预览或者回放画面，可以使用文档中所述的HTTP的URL实现。

注：

1）URL中“:”“?”“&”等符号均为英文半角。

2）RTSP取流和HTTP 访问URL都需要设备支持，如下所示两种控件的设备均可支持。

1      RTSP取流URL
1.1     预览取流
设备预览取流的RTSP URL有新老版本，2012年之前的设备（比如V2.0版本的Netra设备）支持老的取流格式，之后的设备新老取流格式都支持。

【老版本】

URL规定：

rtsp://username:password@<ipaddress>/<videotype>/ch<number>/<streamtype>

注：VLC可以支持解析URL里的用户名密码，实际发给设备的RTSP请求不支持带用户名密码。

详细描述：

![hikvision-1(./images/hikvision-1.png)]

举例说明：

DS-9016HF-ST的IP通道01主码流：

rtsp://admin:12345@172.6.22.106:554/h264/ch33/main/av_stream

DS-9016HF-ST的模拟通道01子码流：

rtsp://admin:12345@172.6.22.106:554/h264/ch1/sub/av_stream

DS-9016HF-ST的零通道主码流（零通道无子码流）：

rtsp://admin:12345@172.6.22.106:554/h264/ch0/main/av_stream

DS-2DF7274-A的第三码流：

 rtsp://admin:12345@172.6.10.11:554/h264/ch1/stream3/av_stream

【新版本】

URL规定：

rtsp://username:password@<address>:<port>/Streaming/Channels/<id>(?parm1=value1&parm2-=value2…)

注：VLC可以支持解析URL里的用户名密码，实际发给设备的RTSP请求不支持带用户名密码。

详细描述：

![hikvision-2(./images/hikvision-2.png)]

举例说明：

DS-9632N-ST的IP通道01主码流：

rtsp://admin:12345@172.6.22.234:554/Streaming/Channels/101?transportmode=unicast

DS-9016HF-ST的IP通道01主码流：

rtsp://admin:12345@172.6.22.106:554/Streaming/Channels/1701?transportmode=unicast

DS-9016HF-ST的模拟通道01子码流：

rtsp://admin:12345@172.6.22.106:554/Streaming/Channels/102?transportmode=unicast  (单播)

rtsp://admin:12345@172.6.22.106:554/Streaming/Channels/102?transportmode=multicast (多播)

rtsp://admin:12345@172.6.22.106:554/Streaming/Channels/102 (?后面可省略，默认单播)

DS-9016HF-ST的零通道主码流（零通道无子码流）：

rtsp://admin:12345@172.6.22.106:554/Streaming/Channels/001

DS-2DF7274-A的第三码流：

rtsp://admin:12345@172.6.10.11:554/Streaming/Channels/103

注：前面老URL，NVR（>=64路的除外）的IP通道从33开始；新URL，通道号全部按顺序从1开始。

1.2     回放取流
URL规定：

rtsp://username:password@<address>:<port>/Streaming/tracks/<id>(?parm1=value1&parm2-=value2…)

注：VLC可以支持解析URL里的用户名密码，实际发给设备的RTSP请求不支持带用户名密码。

详细描述：

![hikvision-3(./images/hikvision-3.png)]

举例说明：

DS-9016HF-ST的模拟通道01：

rtsp://admin:12345@172.6.22.106:554/Streaming/tracks/101?starttime=20120802t063812z&endtime=20120802t064816z

DS-9016HF-ST的IP通道01：

rtsp://admin:12345@172.6.22.106:554/Streaming/tracks/1701?starttime=20131013t093812z&endtime=20131013t104816z

表示以单播形式回放指定设备的通道中的录像文件，时间范围是starttime到endtime，其中starttime和endtime的格式要符合ISO 8601。具体格式是YYYYMMDD”T”HHmmSS.fraction”Z”，Y是年，M是月，D是日，T是时间分格符，H是小时，M是分，S是秒，Z是可选的、表示Zulu(GMT) 时间。

1.3     流媒体取流
【流媒体V4.0】iVMS-4200 V2.0配套流媒体服务器

URL描述：

![hikvision-4(./images/hikvision-4.png)]

注：Devicehc8为固定字符，不可更改。

举例说明：

通过流媒体服务器172.6.24.15从设备172.6.22.106取通道01主码流：

rtsp://172.6.24.15:554/Devicehc8://172.6.22.106:8000:0:0?username=admin&password=12345

【流媒体V2.0】

URL描述：

![hikvision-5(./images/hikvision-5.png)]

举例说明：

rtsp://172.6.24.15:554/172.6.22.106:8000:HIK-DS8000HC:2:0:admin:12345/av_stream

注：流媒体2.0的取流URL不是标准的RTSP协议，必须使用流媒体SDK（客户端）才支持取流的，放在这里只是为了给流媒体4.0做参照的。
