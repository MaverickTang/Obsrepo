---
title: ffmpeg
date: 2021-01-01 20:01:01
tags:
- 工具
categories: 技术
---

2021年开年第一个博客

正好剪这个[视频](https://www.bilibili.com/video/BV1ni4y1F79U)的时候

需要转码（从mkv到mov）

在网上找了好多解决方案，最后就选择了这个最“程序员的”

写一篇关于这个ffmpeg小工具的吧

<!--more-->

# 简述

## PRO

**FFmpeg：Fast Forward Moving Picture Experts Group**

`FFmpeg`是一套可以用来`记录`、`转换数字音频`、`视频`，并能将其转化为`流`的开源计算机`程序`。采用LGPL或GPL许可证。它提供了录制、转换以及流化音视频的完整解决方案。它包含了非常先进的音频/视频编解码库libavcodec，为了保证高可移植性和编解码质量，libavcodec里很多codec都是从头开发的。 ffmpeg项目由以下几部分组成: 1.ffmpeg 视频文件转换命令行工具,也支持经过实时电视卡抓取和编码成视频文件. 2.ffserver 基于HTTP、RTSP用于实时广播的多媒体服务器.也支持时间平移 3.ffplay 用 SDL和FFmpeg库开发的一个简单的媒体播放器 4.libavcodec 一个包含了所有FFmpeg音视频编解码器的库.为了保证最优性能和高可复用性,大多数编解码器从头开发的. 5.libavformat 一个包含了所有的普通音视格式的解析器和产生器的库

<!--more-->

## 说人话：

一个完整的，跨平台的音视频记录，转换，流传输的解决方案

具体就是帮你转换**媒体的格式**，**播放视频**，**拼接视频**，**转换gif**等

太多了不一一枚举

详细的可以跳到功能实践去看

![ffmpeg1](https://s3.ax1x.com/2021/01/02/sSGdlF.md.png)

# 安装

这里以Macos系统为主进行介绍

点击上面图片的Download![ffmpeg2](https://s3.ax1x.com/2021/01/02/sSGwy4.png)

找到苹果的图标，下载这个Static builds for macOS 64-bit（Source Code我们用不着

下载下来减压后是一个exe文件

点击运行后会打开终端，然后自行就安装完了

![ffmpeg3](https://s3.ax1x.com/2021/01/02/sSG0OJ.png)

# 使用

~~不要听我瞎逼逼~~，英语好的建议直接去[官网](https://ffmpeg.org/ffmpeg.html#toc-Synopsis)

在前面我会介绍案例让程序员之外的人能够理解，后面就是程序内容了

希望大家各取所需

## 大纲（Synopsis)

ffmpeg [global_options] {[input_file_options] -i input_url} ... {[output_file_options] output_url} ...

## 参数设置

### 主要参数，不必强记，结合后面的示例理解

`-i`——设置输入档名。
` -f`——设置输出格式。
` -y`——若输出文件已存在时则覆盖文件。
` -fs`——超过指定的文件大小时则结束转换。
 `-ss`——从指定时间开始转换。
 `-t`从-ss时间开始转换（如-ss 00:00:01.00 -t 00:00:10.00即从00:00:01.00开始到00:00:11.00）。
` -title`——设置标题。
` -timestamp`——设置时间戳。
 `-vsync`——增减Frame使影音同步。

### 视频参数
 `-b:v`——设置视频流量，默认为200Kbit/秒。（单位请引用下方注意事项）
 `-r`——设置帧率值，默认为25。
 `-s`——设置画面的宽与高。
 `-aspect`——设置画面的比例。
` -vn`——不处理视频，于仅针对声音做处理时使用。
 `-vcodec( -c:v )`——设置视频视频编解码器，未设置时则使用与输入文件相同之编解码器。

### 声音参数
 `-b:a`——设置每Channel（最近的SVN版为所有Channel的总合）的流量。（单位请引用下方注意事项）
` -ar`——设置采样率。
 `-ac`——设置声音的Channel数。
` -acodec ( -c:a ) `——设置声音编解码器，未设置时与视频相同，使用与输入文件相同之编解码器。
 `-an`——不处理声音，于仅针对视频做处理时使用。
 `-vol`——设置音量大小，256为标准音量。（要设置成两倍音量时则输入512，依此类推。）

### 注意事项
 以-b:v及-b:a首选项流量时，根据使用的ffmpeg版本，须注意单位会有kbits/sec与bits/sec的不同。（可用ffmpeg -h显示说明来确认单位。）
 例如，单位为bits/sec的情况时，欲指定流量64kbps时需输入 -b:a 64k；单位为kbits/sec的情况时则需输入 -b:a 64。
 以-acodec及-vcodec所指定的编解码器名称，会根据使用的ffmpeg版本而有所不同。例如使用AAC编解码器时，会有输入aac与libfaac的情况。此外，编解码器有分为仅供解码时使用与仅供编码时使用，因此一定要利用ffmpeg -formats确认输入的编解码器是否能运作。

## 示例

在这里假设输入文件都为 input.avi，并且默认路径已经在要转换的文件上

### 直接转换视频格式

这里直接在后面写转化后的格式以及名字就好

可以通过这个将视频转化为gif

```
ffmpeg -i input.avi output.mp4
```

### 将视频中一部分转化为gif

```
// 从视频中第二秒开始，截取时长为3秒的片段转化为 gif
ffmpeg -t 3 -ss 00:00:02 -i small.mp4 small-clip.gif
// 默认转化是中等质量模式，若要转化出高质量的 gif，可以修改比特率
ffmpeg -i small.mp4 -b 2048k small.gif
```

### 加倍速播放视频

```
ffmpeg -i input.mov -filter:v "setpts=0.5*PTS" output.mov
//慢速就是2.0
```

### 定义帧率 16fps:

```
ffmpeg -i input.mov -r 16 -filter:v "setpts=0.125*PTS" -an output.mov
```

### 静音视频（移除视频中的音频）

-an 就是禁止音频输出

```
ffmpeg -i input.mov -an mute-output.mov
```

### 视频提取帧

```cpp
// 将视频提取10帧
ffmpeg -i index.mp4 -r 10 %03d.jpg;
```

### 将输出文件的视频比特率设置为64 kbit / s:

```
ffmpeg -i input.avi -b:v 64k -bufsize 64k output.avi
```

### 将输出文件的帧速率强制为24 fps:

```
ffmpeg -i input.avi -r 24 output.avi
```

### 将输入文件的帧速率（仅对原始格式有效）强制为1 fps，将输出文件的帧速率强制为24 fps:

```
ffmpeg -r 1 -i input.m2v -r 24 output.avi
```

### 两路/多路视频拼接，同时播放

```
ffmpeg -i input1.avi -i input2.avi -filter_complex "[0:v]pad=iw*2:ih[a];[a][1:v]overlay=w:0" -pix_fmt yuv420p -y output_result.mp4
```

`-filter_complex "[0:v]pad=iw*2:ih[a];[a][1:v]overlay=w:0"`指的是复杂滤波器的设置。其中`[0:v] [1:v]`表示输入的第一个和第二个编号。`pad `用于边界扩充，iw/ih分别是输入视频的宽度和高度。`[0:v]pad=iw*2:ih[a] `表示将第一个输入视频边界扩充，并将扩充好的命名为 [a]，方便后续操作。`[a][1:v]overlay=w*1` 中的` [a][1:v] `表示将 [1:v] 叠加到 [a] 上去，并且位置从 w 开始，默认是 `width=w` 处，h 未写表示 0。

### 从输入视频中裁剪一部分输出

利用 ffmpeg 中的 video filter功能，设置指定的裁剪开始位置和裁剪的宽度和高度即可

```
ffmpeg -i ffmpeg_test.mp4 -vf "crop=w:h:x:y" -y ffmpeg_test_out.mp4
```

其中 -i 指定输入视频数据

`-vf` 是` -filter:v `的缩略形式告诉 ffmpeg 使用视频滤波器进行次操作

`crop=w:h:x:y` 中 `w` 是输出视频的宽，`h `是输出视频的高，`x `和` y `是裁剪开始的坐标值，以左上为坐标原点，向右为 x 方向，向下为 y 方向

### 在给定视频指定位置添加水印

```
ffmpeg -i ctest.mp4 -vf "drawtext=fontfile=simhei.ttf: text='Original':x=620:y=500:fontsize=72:fontcolor=blue:shadowy=2" -y test_dst.mp4
```

其中：

`fontfile `表示字体类型，要确保存在对应的字体库

`text `表示要添加的字符串形式的文字内容

`fontsize `用来设置字体大小，默认大小为 16

`fontcolor `用来设置字体颜色，默认为 Black

`x=620:y=1920` 表示文字水印放置的位置

效果如下

![show](https://s3.ax1x.com/2021/01/02/sSU0aj.gif)

### 将视频拆分成图像序列

直接输入需要分解的视频名，并指定输出图像的格式即可

```
ffmpeg -i video.mpg image%d.jpg
ffmpeg -i scene2frame1.mov frame%d.png
ffmpeg -i src.mp4 -vframes 200 bmp_images/camera_01/%04d.bmp
ffmpeg -i src.mp4 -vf scale=1920:1080 -vframes 200 bmp_resize/camera_01/%04d.bmp
//vframes 用于设置提取的帧数。
//vf scale 用于设置提取帧之后输出的分辨率，可用于对提取帧进行 resize 处理。
```

# 源码结构

## 主要组成

这部分直接引用自雷神的博客：[FFMPEG中最关键的结构体之间的关系](https://blog.csdn.net/leixiaohua1020/article/details/11693997)

FFMPEG中结构体很多。最关键的结构体可以分成以下几类：

a) 解协议（http,rtsp,rtmp,mms）

AVIOContext，URLProtocol，URLContext主要存储视音频使用的协议的类型以及状态。URLProtocol存储输入视音频使用的封装格式。每种协议都对应一个URLProtocol结构。（注意：FFMPEG中文件也被当做一种协议“file”）

b) 解封装（flv,avi,rmvb,mp4）

AVFormatContext主要存储视音频封装格式中包含的信息；AVInputFormat存储输入视音频使用的封装格式。每种视音频封装格式都对应一个AVInputFormat 结构。

c) 解码（h264,mpeg2,aac,mp3）

每个AVStream存储一个视频/音频流的相关数据；每个AVStream对应一个AVCodecContext，存储该视频/音频流使用解码方式的相关数据；每个AVCodecContext中对应一个AVCodec，包含该视频/音频对应的解码器。每种解码器都对应一个AVCodec结构。

d) 存数据

视频的话，一般每个 AVPacket 是一帧；音频可能有好几帧

解码前数据：AVPacket(h264, aac)
解码后数据：AVFrame(yuv, pcm)

## 模块简介

AVUtil：核心工具库，最基础的模块之一，其它模块经常依赖该库做一些基本的音视频处理操作，比如 av_image_fill_arrays（填充原始图像数据到 AVFrame）、av_image_get_buffer_size（根据图像宽高、格式获取填充该图像需要的字节数）、av_get_pix_fmt_name（获取像素格式的名称） 等等。

AVFormat：文件格式和协议库，最重要的模块之一，封装了 Protocol 层和 Demuxer、Muxer 层。常用于读写文件及文件信息，比如 avformat_write_header（写文件头）、av_write_trailer（写文件尾）、av_read_frame （从文件中读取一帧编码后的图像/音频数据）、av_write_frame（往文件中写一帧编码后的图像/音频数据）、av_seek_frame（给定一个时间戳，移动读指针到对应位置）等等。

AVCodec：编解码库，最重要的模块之一。FFmpeg 默认不会添加 libx264、FDK-AAC 等库，但 FFmpeg 可以像一个平台一样，将其它第三方的 Codec 以插件的形式添加进来，并为开发者提供统一的接口。编解码需要用到的函数基本都在该库中，比如 avcodec_find_decoder（找到对应的第三方解码器）、avcodec_decode_video2（使用对应的解码器解码一帧图像/音频数据）。

AVFilter：滤镜库。该模块提供了包括音频特效和视频特效的处理，比如把 “drawbox=10:20:200:60:red@0.5” 这条命令，传递给函数 avfilter_graph_parse() 解析，并传递原始图像数据到该 filter 中，就能在图像坐标为 (10, 20) 的点上生成一个宽高为 (200, 60) 、透明度为 0.5 的红色矩形。

以上是 FFmpeg 最常用的四个库，此外还有 AVDevice（输入输出设备库）、SwrResample（音频重采样，可转换音频的声道数、数据格式、采样率等格式）、SWScale（可用于处理像素格式转换的库）等就不一一介绍了，实际上，到对应的 FFmpeg 源代码对应的头文件看看都提供了什么函数，就大致能了解该库的作用了。

在 FFmpeg 中，还有一个类型的 filter 为 bit stream filter，顾名思义，该 filter 处理的是流数据，主要用于某些格式的封装转换行为。比如 AAC 编码，常见的有两种封装格式，一种是 ADTS 的流，一种是封装在 MPEG4 里面的格式，这种格式会在每一帧前面拼接一个由声道、采样率等信息组成的头，该 filter 中的一个类型，名为 aac_adtstoasc，可以很方便地把 ADTS 转换为另一种格式，常用于编码过程中。与之相对应的，H264 也有两种封装格式，一种是 MP4 封装的格式，一种是裸的 H264 格式（一般称为 annexb 封装格式），用于转换的 filter 名为 h264_mp4toannexb。若要使用这两个 filter，需要在编译 ffmpeg 的时候开启：

```
--enable-bsf=aac_adtstoasc
--enable-bsf=h264_mp4toannexb
12
```

## 常用 API 分析

### 通用 API

1. av_register_all

编译配置（–enable、–disable） FFmpeg 的时候，会生成两个文件：[config.mk](http://config.mk/)、config.h。[config.mk](http://config.mk/) 会实际上就是 makefile 文件需要包含进去的子模块，会作用在编译阶段，帮助开发者编译出正确的库；而 config.h 是作用在运行阶段，这一阶段将确保需要注册哪些容器以及编解码格式到 FFmpeg 框架中。所以该函数的内部实现会先调用 avcodec_register_all 来注册所有 config.h 里面开放的编解码器，然后会注册所有的 Muxer 和 Demuxer，最后注册所有的 Protocol。如此，在 config 的过程中，enable、disable 的选项就作用到了运行时，该函数的源码分析涉及的源文件包括 url.c、alformats.c、mux.c、format.c 等文件。

1. av_find_codec

在 avcodec_register_all 函数里面已经把编码器和解码器都存放到了一个链表中，因此都是从该链表进行遍历查找

1. avcodec_open2 分析

打开编解码其的时候就会用到该函数，参数有三个，第一个是 AVCodecContext，如果想要传入私有参数，比如 preset、tune、profile，则可以为设置到 priv_data 参数中。具体到函数实现时，它会找到对应的实现文件，比如，如果打开的是 libx264 编码器，那么实际上的 Codec 为 libx264.c 中的 ff_libx264_encoder，Codec 的生命周期方法就会委托给该结构体对应的函数指针所指向的函数。open 对应的就是 init 函数指针所指向的函数，该函数会调用具体的编码库的 API，并以对应的 AVCodecContext 中的 priv_data 来填充对应第三方库所需要的私有参数。

1. av_codec_close 分析

和 open 类似，找到对应的实现文件中的 close 函数指针所指向的函数，然后该函数会调用对应第三方库的 API 来关闭掉对应编码库。

其实 FFmpeg 所做的事情就是透明化所有的编码库，用自己的封装来为开发者提供统一的接口，开发者只需要在打开编解码库时指定编解码器的 ID 即可，之后编码、解码、关闭资源都会找到对应的实现文件去做具体的事情。

### 解码时用到的 API

1. avformat_open_input

该函数会根据提供的的文件路径判断文件的格式，继而决定使用哪一个 Demuxer。比如，如果是 flv 文件，那么 Demuxer 就会使用对应的 ff_flv_demuxer，之后关键的生命周期方法 read_header、read_packet、read_seek、read_close 都会使用 ff_flv_demuxer 中函数指针指定的函数。read_header 函数会将 AVStream 结构体构造好。

1. avformat_find_stream_info

这个函数非常重要，该方法的作用是将所有 Stream 的 MetaData 信息填充好，方法内部会先查找对应的解码器，并打开，紧接着利用 Demuxer 中的 read_packet 函数读取一段数据进行解码，解码数据越多，分析出的流数据就会越准确，本地资源会比较快，网络资源则较慢。该函数提供了几个参数可以控制读取数据的长度，分别为：probe_size、max_analyze、fps_probe_size，这几个参数的值越小，读取速度越快，信息则相对不够准确。

1. av_read_frame

该方法读取出来的数据是 AVPacket，该函数的实现首先会委托到 Demuxer 的 read_packet 方法，然后在该函数中把未处理完的压缩数据进行缓存处理。

1. avcodec_decode

如果要解码 H264，会找到 ff_h264_decoder，其中最重要的三个声明周期方法为 init、decode、close。

### 编码时用到的 API

1. avformat_alloc_output_context

和 avformat_open_input 类似，该函数最终会找到对应的格式复制给 AVFormatContext 中的 oformat。

1. avio_open2

该方法首先调用函数 ffurl_open，构造除 URLContext，这个结构体包含了 URLProtocol，接着调用 avio_alloc_context 方法，分配除 AVIOContext 结构体，并将上一步构造出来的 URLProtocol 传递进来，然后复制给 AVFormatContext 的属性。

编码步骤其实是解码的一个逆过程，解码过程中的 av_find_stream_info 对应到编码就是 avformat_new_stream 和 av_format_write_header，该步骤会将音频流或视频流的信息填充好，分配出 AVStream 结构体。read_header 则对应于 av_write_header，再之后是 av_write_frame、av_write_tailer，注意，av_write_header 和 av_write_tailer 必须成对出现。avcodec_encode 等函数就不一一介绍了。

## 一些概念

1. PTS 和 DTS

DTS（Decoding Time Stamp）：解码时间戳，这个时间戳的意义在于告诉播放器该在什么时候解码这一帧图像

PTS（Presentation Time Stamp）：显示时间戳，这个时间戳用来告诉播放器该在什么时候显示这一帧图像

DTS、PTS 是在编码的时候由编码器生成的，当视频流中没有 B 帧时，通常 DTS 和 PTS 的顺序一致。但如果有 B 帧时，解码顺序和播放顺序就有区别了。

比如一个视频中，帧的显示顺序是：I B B P，现在我们需要在解码 B 帧时知道 P 帧中信息，因此这几帧在视频流中的顺序可能是：I P B B，这时候就体现出 DTS 和 PTS 的作用了。DTS 告诉我们该按什么顺序解码这几帧图像，PTS 告诉我们该按什么顺序显示这几帧图像。顺序大概如下：

```
PTS: 1 4 2 3
DTS: 1 2 3 4
Stream: I P B B
123
```

1. time_base

时间单位，比如帧率为 30帧/s 的视频，time_base 就等于 1/30，此时 pts * time_base 就等于当前帧显示的时间

1. 音视频的同步

音频也有 DTS、PTS 的概念，但是音频没有 B 帧，不需要双向预测，所以音频帧的 DTS、PTS 顺序是一致的。

音视频同步的方式一般有三种：同步视频到音频、同步音频到视频、同步音频和视频到外部时钟。 因为音频帧的 DTS、PTS 顺序一致，因此一般情况下，都采用同步视频到音频的方式。

1. gop

group of picture，可以认为是两个 I 帧之间的间隔，通常设置为帧率的两倍即可

1. 参考帧

最多可以设置为 16 个， 通常，该值越大，压缩率越高，但大于6后对压缩率的贡献很低，推荐默认值 6。

1. align

很多图像相关的函数中都有这个参数，是 YUV 通道对齐时的字节单位，如果不确定，可以设为 1，但效率可能不太高。

参考：[what is ‘linesize alignment’ meaning?](https://stackoverflow.com/questions/35678041/what-is-linesize-alignment-meaning)

## 码率控制

主要参考：[H.264 Video Encoding Guide](https://trac.ffmpeg.org/wiki/Encode/H.264)

在 x264 中，码率控制方式主要有（通常只推荐 CRF、Two-Pass ABR 两种）：

1. CQP（Constant Quantization Parameter ）。值越大，压缩率越大，质量越低。使用方法（虽然这里使用的是命令行的形式，但在编写代码时也有参考价值）：

```
ffmpeg -i <input> -c:v libx264 -qp 23 <output>
ffmpeg -i <input> -c:v libx265 -x265-params qp=23 <output>
12
```

仅适用于视频编码研究，除非确切知道自己在做什么，否则不要使用这种模式。

1. ABR（Average Bitrate）。使用方法：

```
fmpeg -i <input> -c:v libx264 -b:v 1M <output>
ffmpeg -i <input> -c:v libx265 -b:v 1M <output>
ffmpeg -i <input> -c:v libvpx-vp9 -b:v 1M <output>
123
```

避免使用这种模式！x264 开发者甚至说永远不要用它，因为质量不可控。

1. CBR（Constant BitRate）。

使用：

```
ffmpeg -i <input> -c:v libx264 -x264-params "nal-hrd=cbr:force-cfr=1" -b:v 1M -minrate 1M -maxrate 1M -bufsize 2M <output>
// VP9
ffmpeg -i <input> -c:v libvpx-vp9 -b:v 1M -maxrate 1M -minrate 1M <output>
123
```

输出文件需要是 .ts 文件，因为 MP4 不支持 NAL 填充，如果输入文件易于编码，使用这种方式会浪费带宽，适用于视频直播。

1. CRF（Constant Rate Factor）。

使用方法：

```
ffmpeg -i <input> -c:v libx264 -crf 23 <output>
ffmpeg -i <input> -c:v libx265 -crf 28 <output>
ffmpeg -i <input> -c:v libvpx-vp9 -crf 30 -b:v 0 <output>
123
```

x264 默认值是 23（推荐 17 ~ 28），x265 是28（推荐 24 ~ 34），可用值是 0 到 51。值越小编码质量越好，码率越高（每 -6，比特率加倍），值等于 0 时则为无损编码。注意：如果不是基于 ffmpeg 的播放器，可能无法解码无损压缩的视频。

很方便，但比特率、文件大小不好控制 ，适用于文件存储或需要实现最好的质量的场景；不适用于流媒体。

在代码中使用时，通过 av_dict_set 设置到 AVDictionary 中，并作为参数传递给 avcodec_open2 即可

1. Two-Pass ABR

用于限制输出文件的大小，比如预期视频文件有 10min(600s)，200 MB：

```
200 * 8192 / 600 = ~2730 Kb
2730 - 128(音频常用的比特率) = 2602 kb
12
```

那么：

```
ffmpeg -y -i input -c:v libx264 -b:v 2600k -pass 1 -c:a aac -b:a 128k -f mp4 /dev/null && \
ffmpeg -i input -c:v libx264 -b:v 2600k -pass 2 -c:a aac -b:a 128k output.mp4
12
```

如果是 Windows 环境， /dev/null 换为 NUL，\ 换为 ^

但我一直不知道在代码中应该怎么使用这种模式，如果有了解的请指教。

1. VBV（Video Buffer Verifier）

可以确保最大码率限制在一个范围里，对于流式传输非常有用，可以配合到 （2-Pass）ABR 或 CRF 模式一起使用，使用方法：

```
// crf & vbv
ffmpeg -i <input> -c:v libx264 -crf 23 -maxrate 1M -bufsize 2M <output>
ffmpeg -i <input> -c:v libx265 -crf 28 -x265-params vbv-maxrate=1000:vbv-bufsize=2000 <output>

ffmpeg -i <input> -c:v libvpx-vp9 -crf 30 -b:v 2M <output>

// 2-pass abr & vbv
ffmpeg -i <input> -c:v libx264 -b:v 1M -maxrate 1M -bufsize 2M -pass 1 -f mp4 /dev/null
ffmpeg -i <input> -c:v libx264 -b:v 1M -maxrate 1M -bufsize 2M -pass 2 <output>



ffmpeg -i <input> -c:v libx265 -b:v 1M -x265-params pass=1:vbv-maxrate=1000:vbv-bufsize=2000 -f mp4 /dev/null
ffmpeg -i <input> -c:v libx265 -b:v 1M -x265-params pass=2:vbv-maxrate=1000:vbv-bufsize=2000 <output>


ffmpeg -i <input> -c:v libvpx-vp9 -b:v 1M -maxrate 1M -bufsize 2M -pass 1 -f webm /dev/null
ffmpeg -i <input> -c:v libvpx-vp9 -b:v 1M -maxrate 1M -bufsize 2M -pass 2 <output>
123456789101112131415161718
```

编写代码的话，指定 AVCodecContext 的 rc_max_rate 和 rc_buffer_size 即可。bufsize 根据你希望比特率获得多大的可变性而设置，默认为 maxrate 的两倍，如果想限制流的比特率，可以设置为 maxrate 的一半。

配合 CRF 模式使用的时候，如果设置的 crf 值过低，视频码率可能超出 -maxrate 的时候，编码器会自动调整 crf，避免出现较大的码率波动。然而，x264 不会严格控制你指定的最大码率，除非使用 2 pass 模式。

1. preset、tune

如果参数的设置有些复杂，可以使用 preset、tune 参数（编写代码时可以通过 av_dict_set 设置），preset 是一个用于控制编码速度压缩比的选项集合，编码速度越慢，压缩率越高。可选值有：

```
ultrafast
superfast
veryfast
faster
fast
medium – default preset
slow
slower
veryslow
123456789
```

编码速度对比：

![preset 编码速度对比](https://s3.ax1x.com/2021/01/02/sStw6S.png)

tune 可根据输入情况（不同的视频类型等）调整设置（比如对画面作出一些优化），可选值有：

```
film        – use for high quality movie content; lowers deblocking
animation   – good for cartoons; uses higher deblocking and more reference frames
grain       – preserves the grain structure in old, grainy film material（纹理调整）
stillimage  – good for slideshow-like content（适用于 ppt 等内容）
fastdecode  – allows faster decoding by disabling certain filters
zerolatency – good for fast encoding and low-latency streaming（适用于快速编码及低延迟流）
```

# 参考资料

1.https://www.cnblogs.com/phillee/p/12244970.html

2.https://ffmpeg.org/ffmpeg.html#toc-Synopsis

3.https://blog.csdn.net/u011330638/article/details/82392268?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_baidulandingword-2&spm=1001.2101.3001.4242