# 网络摄像头RTSP视频流-WEB端实时播放实现方案

IPC视频流怎么实时在WEB浏览器播放，视频流格式是RTSP。
下面我整理了自己实现的方案以及网上看到的一些方案

一、FFmpeg + nginx 将转 hls 通过 video.js 在支持h5浏览器播放（我实现的）
参见：Nginx+FFmpeg实现rtsp流转hls流，在WEB通过H5 video实现视频播放

不足：hls延迟较rtmp、http-flv大

二、FFmpeg + nginx-rtmp-module + h5 video，rtsp转rtmp播放
https://blog.csdn.net/gui66497/article/details/78590190
https://blog.csdn.net/LLittleF/article/details/81111713

注：通过video.js播放rtmp流。需要将代码放到服务器，本地windows电脑无法播放

不足：需要浏览器开启flash

三、FFmpeg + nginx-http-flv-module + flv.js，rtsp转rtmp，直接播放flv格式
基于nginx-rtmp-module，通过配置将rtmp转为flv，最后通过flv.js播放。
https://github.com/winshining/nginx-http-flv-module/blob/master/README.CN.md
https://segmentfault.com/a/1190000016043297
https://blog.csdn.net/qq\_22633333/article/details/96288603\#comments

这种方式是最理想的，我目前找到的方案。当然单指不想花钱买收费方案的。

四、WebRTC
https://github.com/lulop-k/kurento-rtsp2webrtc
https://www.jianshu.com/p/1ddfa72de165

五、streamedian
https://github.com/Streamedian/html5\_rtsp\_player
https://streamedian.com/
https://streamedian.com/\#demo
https://blog.csdn.net/u011489205/article/details/79327275

六、h5stream
https://www.linkingvision.com/
https://github.com/liweilup/h5stream
https://blog.csdn.net/Dnison/article/details/81663137

七、liveqing
https://www.liveqing.com

其他参考：

JAVA实现大华摄像头WEB方式实时显示视频,H5界面展示方式思路。
浏览器播放rtsp视频流解决方案
javaCV开发详解之2：推流器实现，推本地摄像头视频到流媒体服务器以及摄像头录制视频功能实现(基于javaCV-FFMPEG、javaCV-openCV)
————————————————
版权声明：本文为CSDN博主「妙明元心」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/beihenanfei/article/details/126747340