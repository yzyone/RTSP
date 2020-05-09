1、查看RTSP参数

    ffmpeg -h demuxer=RTSP


```
Demuxer rtsp [RTSP input]:
RTSP demuxer AVOptions:
  -initial_pause     <boolean>    .D....... do not start playing the stream immediately (default false)
  -rtsp_transport    <flags>      ED....... set RTSP transport protocols (default 0)
     udp                          ED....... UDP
     tcp                          ED....... TCP
     udp_multicast                .D....... UDP multicast
     http                         .D....... HTTP tunneling
  -rtsp_flags        <flags>      .D....... set RTSP flags (default 0)
     filter_src                   .D....... only receive packets from the negotiated peer IP
     listen                       .D....... wait for incoming connections
     prefer_tcp                   ED....... try RTP via TCP first, if available
  -allowed_media_types <flags>      .D....... set media types to accept from the server (default video+audio+data+subtitle)
     video                        .D....... Video
     audio                        .D....... Audio
     data                         .D....... Data
     subtitle                     .D....... Subtitle
  -min_port          <int>        ED....... set minimum local UDP port (from 0 to 65535) (default 5000)
  -max_port          <int>        ED....... set maximum local UDP port (from 0 to 65535) (default 65000)
  -listen_timeout    <int>        .D....... set maximum timeout (in seconds) to wait for incoming connections (-1 is infinite, imply flag listen) (from INT_MIN to INT_MAX) (default -1)
  -timeout           <int>        .D....... set maximum timeout (in seconds) to wait for incoming connections (-1 is infinite, imply flag listen) (deprecated, use listen_timeout) (from INT_MIN to INT_MAX) (default -1)
  -stimeout          <int>        .D....... set timeout (in microseconds) of socket TCP I/O operations (from INT_MIN to INT_MAX) (default 0)
  -reorder_queue_size <int>        .D....... set number of packets to buffer for handling of reordered packets (from -1 to INT_MAX) (default -1)
  -buffer_size       <int>        ED....... Underlying protocol send/receive buffer size (from -1 to INT_MAX) (default -1)
  -user_agent        <string>     .D....... override User-Agent header (default "Lavf58.20.100")
  -user-agent        <string>     .D....... override User-Agent header (deprecated, use user_agent) (default "Lavf58.20.100")
```

2、TCP方式录制RTSP直播流

    ffmpeg -rtsp_transport tcp -i rtsp://47.90.47.25/test.ts -c copy -f mp4 output.mp4

如上，使用TCP方式拉流并保存为MP4。

    ffmpeg -user-agent "ChinaFFmpeg-Player" -i rtsp://input:554/live/1/stream.sdp -c copy -f mp4 -y output.mp4

如上，使用User-Agent设置标识区分是否为自己访问的流。

---

作者：Goning

链接：https://www.jianshu.com/p/d58a9b8ade1a

来源：简书

著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。