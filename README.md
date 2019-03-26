# about-multimedia
## 有关多媒体与直播

![](./doc/有关多媒体与直播.png)

## 多媒体知识
### 基本概念
- 媒体文件和编码的区别

	文件是既包括视频又包括音频、甚至还带有脚本的一个集合，也可以叫容器；文件当中的视频和音频的压缩算法才是具体的编码。

- <details><summary>常见的音频视频编码</summary>

	- MPEG 系列：（由ISO[国际标准组织机构]下属的MPEG[运动图象专家组]开发）
		- 视频编码方面主要是Mpeg1（vcd 用的就是它）、Mpeg2（DVD 使用）、Mpeg4（现在的DVDRIP 使用的都是它的变种，如：divx，xvid 等）、Mpeg4 AVC（现在正热门）；
		- 音频编码方面主要是MPEG Audio Layer 1/2、MPEG Audio Layer 3（大名鼎鼎的mp3）、MPEG-2 AAC 、MPEG-4 AAC等等。注意：DVD音频没有采用Mpeg
	- H.26X系列（由ITU[国际电传视讯联盟]主导，侧重网络传输，注意：只是视频编码）
		- 包括H261、H262、H263、H263+、H263++、H264（就是MPEG4 AVC-合作的结晶）
	- 微软windows media系列
		- 视频编码有Mpeg-4 v1/v2/v3（基于MPEG4）、Windows Media Video 7/8/9/10
		- 音频编码有Windows Media audeo v1/v2/7/8/9
	- Real Media系列
		- 视频编码有RealVideo G2（早期）、RealVideo 8/9/10
		- 音频编码有RealAudio cook/sipro（早期）、RealAudio AAC/AACPlus等
	- QuickTime系列
		- 视频编码有Sorenson Video 3（用于QT5，成标准了）、Apple MPEG-4、Apple H.264
		- 音频编码有QDesign Music 2、Apple MPEG-4 AAC

</details>

- <details><summary>常见的文件格式（容器）</summary>

	- AVI，音视频交互存储，最常见的音频视频容器。支持的视频音频编码也是最多的；
	- MPG，MPEG编码采用的音频视频容器，具有流的特性，里面又分为PS，TS 等，PS主要用于DVD存储，TS主要用于HDTV；
	- VOB，DVD采用的音频视频容器格式（即视频MPEG-2，音频用AC3 或者DTS），支持多视频多音轨多字幕章节等；
	- MP4，MPEG-4 编码采用的音频视频容器，基于QuickTime MOV开发，具有许多先进特性；
	- 3GP，3GPP 视频采用的格式，主要用于流媒体传送；
	- ASF，Windows Media 采用的音频视频容器，能够用于流传送，还能包容脚本等；
	- RM，RealMedia 采用的音频视频容器，用于流传送；RMVB，是视频编码部分采用可变码率压缩的文件格式（容器）；
	- MOV，QuickTime 的音频视频容器；
	- MKV，它能把Windows Media Video，RealVideo，MPEG-4 等视频音频融为一个文件，而且支持多音轨，支持章节字幕等；
	- WAV，一种音频容器（注意：只是音频），大家常说的WAV就是没有压缩的PCM编码，其实WAV里面还可以包括MP3等其他ACM压缩编码；
	- MP3，MPEG Audio Layer 3（Mpeg 1 的音频编码的一种）文件转换（实际上也是编码转换）；

</details>

### RTSP协议
- RTSP+(RTCP/RTP)三者关系
  - ![](./doc/rtsp_rtcp_rtp2.png)

### 案例一：vlc播放动画片，rtsp://184.72.239.149/vod/mp4:BigBuckBunny_115k.mov

- Wireshark抓取RTSP流+(RTCP/RTP基于UDP)过程

  - ![](./doc/rtsp_rtcp_rtp.png)

- <details><summary>RTSP协议交互过程</summary>

	OPTIONS rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov RTSP/1.0
	CSeq: 2
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	
	RTSP/1.0 200 OK
	CSeq: 2
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Public: DESCRIBE, SETUP, TEARDOWN, PLAY, PAUSE, OPTIONS, ANNOUNCE, RECORD, GET_PARAMETER
	Supported: play.basic, con.persistent
	
	DESCRIBE rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov RTSP/1.0
	CSeq: 3
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Accept: application/sdp
	
	RTSP/1.0 200 OK
	CSeq: 3
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Expires: Tue, 26 Mar 2019 02:22:23 UTC
	Content-Length: 587
	Content-Base: rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/
	Date: Tue, 26 Mar 2019 02:22:23 UTC
	Content-Type: application/sdp
	Session: 310018309;timeout=60
	
	v=0
	o=- 310018309 310018309 IN IP4 184.72.239.149
	s=BigBuckBunny_115k.mov
	c=IN IP4 184.72.239.149
	t=0 0
	a=sdplang:en
	a=range:npt=0- 596.48
	a=control:*
	m=audio 0 RTP/AVP 96
	a=rtpmap:96 mpeg4-generic/12000/2
	a=fmtp:96 profile-level-id=1;mode=AAC-hbr;sizelength=13;indexlength=3;indexdeltalength=3;config=1490
	a=control:trackID=1
	m=video 0 RTP/AVP 97
	a=rtpmap:97 H264/90000
	a=fmtp:97 packetization-mode=1;profile-level-id=42C01E;sprop-parameter-sets=Z0LAHtkDxWhAAAADAEAAAAwDxYuS,aMuMsg==
	a=cliprect:0,0,160,240
	a=framesize:97 240-160
	a=framerate:24.0
	a=control:trackID=2
	SETUP rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=1 RTSP/1.0
	CSeq: 4
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Transport: RTP/AVP;unicast;client_port=54286-54287
	
	RTSP/1.0 200 OK
	CSeq: 4
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Expires: Tue, 26 Mar 2019 02:22:23 UTC
	Transport: RTP/AVP;unicast;client_port=54286-54287;source=184.72.239.149;server_port=8432-8433;ssrc=389A31E5
	Date: Tue, 26 Mar 2019 02:22:23 UTC
	Session: 310018309;timeout=60
	
	SETUP rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=2 RTSP/1.0
	CSeq: 5
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Transport: RTP/AVP;unicast;client_port=54288-54289
	Session: 310018309
	
	RTSP/1.0 200 OK
	CSeq: 5
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Expires: Tue, 26 Mar 2019 02:22:23 UTC
	Transport: RTP/AVP;unicast;client_port=54288-54289;source=184.72.239.149;server_port=16626-16627;ssrc=4B70664B
	Date: Tue, 26 Mar 2019 02:22:23 UTC
	Session: 310018309;timeout=60
	
	PLAY rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/ RTSP/1.0
	CSeq: 6
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Session: 310018309
	Range: npt=0.000-
	
	RTSP/1.0 200 OK
	RTP-Info: url=rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=1;seq=1;rtptime=0,url=rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=2;seq=1;rtptime=0
	CSeq: 6
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Range: npt=0.0-596.48
	Session: 310018309;timeout=60
	
	PAUSE rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/ RTSP/1.0
	CSeq: 7
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Session: 310018309
	
	RTSP/1.0 200 OK
	CSeq: 7
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Session: 310018309;timeout=60
	
	PLAY rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/ RTSP/1.0
	CSeq: 8
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Session: 310018309
	Range: npt=37.220-
	
	RTSP/1.0 200 OK
	RTP-Info: url=rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=1;seq=113;rtptime=445440,url=rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=2;seq=296;rtptime=3340800
	CSeq: 8
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Range: npt=37.22-596.48
	Session: 310018309;timeout=60
	
	PAUSE rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/ RTSP/1.0
	CSeq: 9
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Session: 310018309
	
	RTSP/1.0 200 OK
	CSeq: 9
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Session: 310018309;timeout=60
	
	PLAY rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/ RTSP/1.0
	CSeq: 10
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Session: 310018309
	Range: npt=121.921-
	
	RTSP/1.0 200 OK
	RTP-Info: url=rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=1;seq=119;rtptime=1464324,url=rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=2;seq=316;rtptime=10982430
	CSeq: 10
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Range: npt=121.921-596.48
	Session: 310018309;timeout=60
	
	PAUSE rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/ RTSP/1.0
	CSeq: 11
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Session: 310018309
	
	RTSP/1.0 200 OK
	CSeq: 11
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Session: 310018309;timeout=60
	
	PLAY rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/ RTSP/1.0
	CSeq: 12
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Session: 310018309
	Range: npt=197.793-
	
	RTSP/1.0 200 OK
	RTP-Info: url=rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=1;seq=143;rtptime=2363388,url=rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/trackID=2;seq=388;rtptime=17725410
	CSeq: 12
	Server: Wowza Streaming Engine 4.7.5.01 build21752
	Cache-Control: no-cache
	Range: npt=197.793-596.48
	Session: 310018309;timeout=60
	
	TEARDOWN rtsp://184.72.239.149:554/vod/mp4:BigBuckBunny_115k.mov/ RTSP/1.0
	CSeq: 13
	User-Agent: LibVLC/3.0.6 (LIVE555 Streaming Media v2016.11.28)
	Session: 310018309

</details>


## 直播技术和SRS开源直播平台

![](./doc/推流和拉流.jpg)

![](./doc/HLS方案模拟.jpg)

![](./doc/RTMPvsHLSvsHTTPFLV.png)

![](./doc/产品比较.png)

![](./doc/核心功能对比.png)

![](./doc/网络协议对比.png)

![](./doc/体系结构对比.png)

![](./doc/安装部署对比.png)

![](./doc/code对比.png)

![](./doc/cdn友好性对比.png)

## 有关Nginx高性能服务器

![](./doc/有关Nginx.png)


## 资料汇总
1. [rfc2326 - Real Time Streaming Protocol (RTSP)](https://tools.ietf.org/html/rfc2326)
2. [rfc3550 - RTP: A Transport Protocol for Real-Time Applications](https://tools.ietf.org/html/rfc3550)
3. [rfc3551 - RTP Profile for Audio and Video Conferences with Minimal Control](https://tools.ietf.org/html/rfc3551)
4. [rfc3611 - RTP Control Protocol Extended Reports (RTCP XR)](https://tools.ietf.org/html/rfc3611)
5. [rfc3711 - The Secure Real-time Transport Protocol (SRTP)](https://tools.ietf.org/html/rfc3711)
6. [rfc4585 - Extended RTP Profile for Real-time Transport Control Protocol (RTCP)-Based Feedback (RTP/AVPF)](https://tools.ietf.org/html/rfc4585)
7. [rfc4566 - SDP: Session Description Protocol](https://tools.ietf.org/html/rfc4566)
8. [rfc5104 - Codec Control Messages in the RTP Audio-Visual Profile with Feedback (AVPF)](https://tools.ietf.org/html/rfc5104)
9. [rfc5124 - Extended Secure RTP Profile for Real-time Transport Control Protocol (RTCP)-Based Feedback (RTP/SAVPF)](https://tools.ietf.org/html/rfc5124)
10. [rfc5450 - Transmission Time Offsets in RTP Streams](https://tools.ietf.org/html/rfc5450)
11. [rfc6184 - RTP Payload Format for H.264 Video](https://tools.ietf.org/html/rfc6184)
12. [rfc7741 - RTP Payload Format for VP8 Video](https://tools.ietf.org/html/rfc7741)
13. [rfc8216 - HTTP Live Streaming](https://tools.ietf.org/html/rfc8216)
14. [RTMP WIKI](https://en.wikipedia.org/wiki/Real-Time_Messaging_Protocol)
15. [rtmp specification v1.0](http://wwwimages.adobe.com/www.adobe.com/content/dam/acom/en/devnet/rtmp/pdf/rtmp_specification_1.0.pdf)
16. [HLS WIKI](https://en.wikipedia.org/wiki/HTTP_Live_Streaming)
17. [北京大学，视频编码算法研究室](http://vcl.idm.pku.edu.cn/articlesList.html?tag=research&page=0)
18. [流媒体加密](https://github.com/gwuhaolin/blog/issues/10)
19. [使用flv.js做直播](https://github.com/gwuhaolin/blog/issues/3)
20. [雷霄骅 - RGB、YUV像素数据处理](https://blog.csdn.net/leixiaohua1020/article/details/50534150)
21. [雷霄骅 - H.264视频码流解析](https://blog.csdn.net/leixiaohua1020/article/details/50534369) 
22. [雷霄骅 - h264_analysis](https://github.com/leixiaohua1020/h264_analysis)
23. [雷霄骅 - PCM音频采样数据处理](https://blog.csdn.net/leixiaohua1020/article/details/50534316)
24. [雷霄骅 - AAC音频码流解析](https://blog.csdn.net/leixiaohua1020/article/details/50535042)
25. [雷霄骅 - FLV封装格式解析](https://blog.csdn.net/leixiaohua1020/article/details/50535082)
26. [雷霄骅 - UDP-RTP协议解析](https://blog.csdn.net/leixiaohua1020/article/details/50535230)
