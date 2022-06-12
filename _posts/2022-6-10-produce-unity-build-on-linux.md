---
layout: post
title: "在Ubuntu上Unity构建持续集成的随笔"
author: "Kong Weihang"
categories: produce
tags: [review,produce]
image: unity-build-on-linux.png
---

# 一些小提示
- Ubuntu是大小写敏感的文件系统，Windows不是，文件重命名的时候 `docker` 和 `Docker` 在windows的SVN下是不认为发生改变的。这会在Linux上造成严重的问题。

- 使用root账户下载了基于python软件，是没有办法在Jenkins中使用的，因为用户是不同的。使用sudo -H pip3 install [software name]来解决，放到bin中让所有用户都能够使用

- Linux文件名字中不要使用`:`

- 出于某些无法解释的原因，如果Unity中设置了default cursor，会导致在Linux上的编译失败，具体表现为
```
ALSA lib confmisc.c:767:(parse_card) cannot find card '0'
ALSA lib conf.c:4732:(_snd_config_evaluate) function snd_func_card_driver returned error: No such file or directory
ALSA lib confmisc.c:392:(snd_func_concat) error evaluating strings
ALSA lib conf.c:4732:(_snd_config_evaluate) function snd_func_concat returned error: No such file or directory
ALSA lib confmisc.c:1246:(snd_func_refer) error evaluating name
ALSA lib conf.c:4732:(_snd_config_evaluate) function snd_func_refer returned error: No such file or directory
ALSA lib conf.c:5220:(snd_config_expand) Evaluate error: No such file or directory
ALSA lib pcm.c:2642:(snd_pcm_open_noupdate) Unknown PCM default
FMOD failed to initialize the output device.: "Error initializing output device. " (60)
Forced to initialize FMOD to to the device driver's system output rate 48000, this may impact performance and/or give inconsistent experiences compared to selected sample rate 48000
ALSA lib confmisc.c:767:(parse_card) cannot find card '0'
ALSA lib conf.c:4732:(_snd_config_evaluate) function snd_func_card_driver returned error: No such file or directory
ALSA lib confmisc.c:392:(snd_func_concat) error evaluating strings
ALSA lib conf.c:4732:(_snd_config_evaluate) function snd_func_concat returned error: No such file or directory
ALSA lib confmisc.c:1246:(snd_func_refer) error evaluating name
ALSA lib conf.c:4732:(_snd_config_evaluate) function snd_func_refer returned error: No such file or directory
ALSA lib conf.c:5220:(snd_config_expand) Evaluate error: No such file or directory
ALSA lib pcm.c:2642:(snd_pcm_open_noupdate) Unknown PCM default
FMOD failed to initialize the output device.: "Error initializing output device. " (60)
FMOD initialized on nosound output
[Subsystems] No new subsystems found in resolved package list.
Package Manager log level set to [2]
[Package Manager] Done registering packages in 0.06s seconds
Refreshing native plugins compatible for Editor in 20.39 ms, found 2 plugins.
Preloading 0 native plugins for Editor in 0.00 ms.
Initialize engine version: 2021.3.4f1 (cb45f9cae8b7)
[Subsystems] Discovering subsystems at path /home/wei-hang/Unity/Hub/Editor/2021.3.4f1/Editor/Data/Resources/UnitySubsystems
[Subsystems] Discovering subsystems at path /var/lib/jenkins/workspace/Prison Island/Assets
Forcing GfxDevice: Null
GfxDevice: creating device client; threaded=0; jobified=0
NullGfxDevice:
    Version:  NULL 1.0 [1.0]
    Renderer: Null Device
    Vendor:   Unity Technologies
Segmentation fault (core dumped)
```
这里会直接显示一个`Segmentation fault (core dumped)`，目前没有找到合适的解决方案，暂时把Cursor去掉了。


# Unity License

近日由于有远程打包的需求，希望提供给策划和美术人员一个简单轻松看到结果的方案，因此开始尝试配置远程服务器进行打包服务。也因此遇到了诸多问题，由于中文互联网上对于这一块的介绍相当有限，在此做一些记录以供参考。

- 在Ubuntu上，除非你购买了Pro或者Plus版本的unity，否则无法通过-username -password -serialnumber通过headless模式登录。
> 对此我并不确定，你可以参试拷贝license，并使用账号密码登录
```
Unity -quit -batchmode -nographics -serial xxxx -username "xxxx" -password "xxxx" -logfile /dev/stdout
```



- 需要通过手动激活本机的license。
首先输入：

```bash
Unity -batchmode -createManualActivationFile -logfile /dev/stdout
```
生成激活文件 `Unity_xxxx.alf`

打开 https://license.unity3d.com/manual 上传`Unity_xxxx.alf` 得到 `Unity_.x.ulf` ，把 `Unity_.x.ulf` 放在  ~.local/share/unity3d/Unity/ 里

然后激活它

```
Unity -batchmode -logfile /dev/stdout -manualLicenseFile /home/[User Name]/.local/share/unity3d/Unity/Unity_xxxx.x.ulf

```

之后就可以使用其他的命令了。


# Jenkins配置
- 在最新版本的Email Extension Plugin 2.88中，不再支持通过账号密码登录的功能，必须使用Credentials，通过邮箱生成的密码来登录。
