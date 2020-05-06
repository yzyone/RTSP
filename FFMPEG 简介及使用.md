ffmpeg 简介及使用

简介

    ffmpeg [global_options] {[input_file_options] -i input_url} ... {[output_file_options] output_url} ...

ffmpeg 是一款非常快速的视频和音频转换器, 是开源项目 FFmpeg (Fast Forward moving pictures expert group) 的命令行程序。 它可以在任意采样率之间转换，并通过高质量的多相滤波器实时调整视频大小。

ffmpeg 程序的转码流程,如下所示

```
 _______              ______________
|       |            |              |
| input |  demuxer   | encoded data |   decoder
| file  | ---------> | packets      | -----+
|_______|            |______________|      |
                                           v
                                       _________
                                      |         |
                                      | decoded |
                                      | frames  |
                                      |_________|
 ________             ______________       |
|        |           |              |      |
| output | <-------- | encoded data | <----+
| file   |   muxer   | packets      |   encoder
|________|           |______________|

```


其中, demuxer 为解复用器, muxer 为复用器; decoder 为解码器, encoder 为编码器 

 
具体使用示例
假定 PCM 音频格式 s16le (signed 16 bits little endian, 有符号 16 位小端) , 更多格式参见"补充内容 - 1. PCM格式".

1. PCM 音频转换为 WAV 格式

```
ffmpeg -y -f s16le -ar 16k -ac 1 -i input.raw output.wav
```

其中, -y 表示无需询问,直接覆盖输出文件; -f s16le 用于设置文件格式为 s16le ; -ar 16k 用于设置音频采样频率为 16k; -ac 1 用于设置通道数为 1; -i input.raw 用于设置输入文件为 input.raw; output.wav 为输出文件.

2. PCM 音频转换为 MP3 格式

```
ffmpeg -y -f s16le -ar 16k -ac 1 -i input.raw output.mp3
```


注: 与PCM音频转换为WAV命令相比, 只有输出文件不同, 其他相同.

3. WAV 音频转换为 PCM 格式

```
ffmpeg -y  -i input.wav  -acodec pcm_s16le -f s16le -ac 1 -ar 16k output.pcm
```

其中, -acodec 用于设置音频的编码器和解码器(codec, 即 coder-decoder 的混成词). 也是参数 -codec:a 的别名, 其中a表示 audio. 

4. MP3 音频转换为 PCM 格式

```
ffmpeg -y  -i input.mp3  -acodec pcm_s16le -f s16le -ac 1 -ar 16k output.pcm
```

5. WAV 音频转换为 MP3 格式
6. 
```
ffmpeg -y  -i input.wav  input.mp3
```

6. MP3 音频转换为 WAV 格式

```
ffmpeg -y  -i input.mp3  input.wav
```

补充内容
1. PCM 格式
PCM, 英文全称为 pulse-code modulation, 中文名为脉冲编码调制, 是用于数字化表示采样后的模拟信号的一种方法. 其也是数字音频的标准形式. 更多内容参见 Pulse-code modulation, Wikipedia. 由于 PCM 音频只包含数据, 没有数据头指定采样率, 通道数, 数据位数等, 所以需要在转码(transcoding)前, 指定这些参数. 在 ffmpeg 程序中, 支持多种格式的 PCM 数据, 如下所示:

```
$ ffmpeg -formats | grep PCM
 DE alaw            PCM A-law
 DE f32be           PCM 32-bit floating-point big-endian
 DE f32le           PCM 32-bit floating-point little-endian
 DE f64be           PCM 64-bit floating-point big-endian
 DE f64le           PCM 64-bit floating-point little-endian
 DE mulaw           PCM mu-law
 DE s16be           PCM signed 16-bit big-endian
 DE s16le           PCM signed 16-bit little-endian
 DE s24be           PCM signed 24-bit big-endian
 DE s24le           PCM signed 24-bit little-endian
 DE s32be           PCM signed 32-bit big-endian
 DE s32le           PCM signed 32-bit little-endian
 DE s8              PCM signed 8-bit
 DE u16be           PCM unsigned 16-bit big-endian
 DE u16le           PCM unsigned 16-bit little-endian
 DE u24be           PCM unsigned 24-bit big-endian
 DE u24le           PCM unsigned 24-bit little-endian
 DE u32be           PCM unsigned 32-bit big-endian
 DE u32le           PCM unsigned 32-bit little-endian
 DE u8              PCM unsigned 8-bit
```

其中,  A-law 和 mu-law 都是压缩和扩展算法 (companding algorithm). 在 8 位 PCM 数字通信系统中, 用于优化模拟信号数字化的动态范围. A-law 算法主要应用在欧洲, 而 mu-law 算法主要应用在北美和日本. 更多内容,参见 A-law algorithm, Wikipedia 和 μ-law algorithm, Wikipedia .

2. 使用 ffplay 播放音频

```
$ ffplay [options] [input_url]
```

ffplay 是一款使用 FFmpeg 库(用于转换视频和音频文件, 官方网址为 https://ffmpeg.org) 和 SDL 库(Simple DirectMedia Layer, 一个跨平台的开发库, 用于通过 OpenGL 和 Direct3D, 提供对音频, 鼠标, 操纵杆和图形硬件的低层访问, 官方网址为 https://www.libsdl.org), 主要用于各种 FFmpeg API 的测试平台.

注意: 播放PCM文件时, 同样需要指定具体参数信息.

具体播放命令, 示例如下: 

1). 播放 s16le 格式的 PCM 文件 input.raw

```
$ ffplay -f s16le -ac 1 -ar 16k -i input.raw
```

其中, -i 参数可以省略

2). 播放 wav 格式文件

```
$ ffplay -i input.wav
```

3). 播放 mp3 格式文件

```
$ ffplay -i input.mp3
```

参考资料
1. ffmpeg Documentation. https://ffmpeg.org/ffmpeg.html

2. Can ffmpeg convert audio to raw PCM? If so, how? https://stackoverflow.com/questions/4854513/can-ffmpeg-convert-audio-to-raw-pcm-if-so-how

3. FFmpeg wiki: audio types. https://trac.ffmpeg.org/wiki/audio%20types

4. ffplay Documentation. https://ffmpeg.org/ffplay.html

5. FFmpeg - Wikipedia. https://en.wikipedia.org/wiki/FFmpeg