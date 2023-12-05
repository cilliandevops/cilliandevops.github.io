## 2023年11月22日

如何解决Linux磁盘空间告急：详细解决方案

## 恢复Linux磁盘空间全面指南

运维告警里比较常见的就是磁盘空间超过告警阀值的情况，遇到这种情况是最常见的，只要不影响业务以及不是快速占满磁盘的情况下，就可以慢慢着手解决问题。以下是比较常用的步骤。


### 步骤1：检查磁盘空间

首先，你需要知道问题的所在。通过终端，你可以使用 `df` 命令查看磁盘空间使用情况。

```bash
df -h
```

这个命令会列出每个挂载点的可用空间，`-h` 参数让信息以易读的格式（如GB、MB）显示。

### 步骤2：找出占用空间最多的文件和目录

一旦你知道了空间资源紧张的分区，你可以使用 `du` 命令来找出哪些文件或目录占用了最多的空间。

```bash
du -sh /path/to/directory | sort -rh | head -20
```

这个命令将在指定目录下显示占用空间最大的前20个文件或目录。

使用ncdu工具

ncdu是一个用于查看磁盘使用情况的简单工具，提供了一个基于文本的用户界面。

安装ncdu（如果尚未安装）：

```bash
sudo apt-get install ncdu # Debian/Ubuntu系统
sudo yum install ncdu # CentOS系统
```
使用ncdu扫描文件系统：

```bash
ncdu /
```

### 步骤3：删除不必要的文件

检查列表中的项目，看看是否有不再需要的文件或者可以转移到其他存储设备的数据。使用 `rm` 命令来删除文件：

```bash
rm /path/to/unwanted/file
```

对于目录，你可以使用带有 `-r`（递归）标志的 `rm` 命令：

```bash
rm -r /path/to/unwanted/directory
```

**注意：** 使用 `rm` 命令时要非常小心，因为删除后无法恢复。

使用find命令删除旧文件

自动查找并删除一定时间前的文件：

```bash
find /path/to/directory -type f -mtime +30 -exec rm {} \;
```
这个命令会删除30天前的文件。

### 步骤4：清理缓存和临时文件

Linux系统经常存储临时文件和缓存，这些文件随着时间的推移可能会占用大量的空间。使用以下命令清理：

```bash
sudo apt-get clean       # 对于Debian系的系统
sudo yum clean all       # 对于RedHat系的系统
```

此外，你可以手动删除 `/tmp` 目录下的文件。
```bash
sudo rm -rf /tmp/*
```
### 步骤5：日志文件管理

日志文件是另一个可能占用大量空间的来源。查看 `/var/log` 目录，并考虑删除旧的或不必要的日志文件。你可以使用 `logrotate` 工具来帮助管理日志文件。

```bash
sudo find /var/log -type f -name "*.log" -mtime +30 -exec rm {} \;
```

### 步骤6：查找并删除重复文件

有时候，系统中可能会有不小心复制的重复文件。你可以使用 `fdupes` 或 `rdfind` 等工具来找到和删除这些文件。

```bash
sudo apt-get install fdupes # Debian/Ubuntu系统
sudo yum install fdupes # CentOS系统

fdupes -r /path/to/directory
```

### 步骤7：磁盘配额管理

如果是多用户系统，考虑设置磁盘配额来限制用户使用的空间量，这可以通过 `quotacheck`、`quotaon` 和 `edquota` 等命令完成。

### 步骤8：扩展磁盘空间

扩展硬盘空间最直接，这可能包括添加新的硬盘、调整分区大小或使用网络附加存储（NAS）。

### 步骤9：使用文件系统特性

如果文件系统支持，比如xfs可以通过启用压缩来节省空间。

### 步骤10：压缩文件

如果它们不是经常访问，可以使用压缩工具如tar和gzip来减少它们的大小：
```bash
tar -czvf name-of-archive.tar.gz /path/to/directory
```

磁盘空间的管理是Linux系统维护的重要组成部分。通过定期检查和清理，可以确保系统运行顺畅，并避免因磁盘空间不足导致的问题。始终在执行删除操作前备份重要数据，以防意外发生。





## 2023年11月20日

## 近日见闻

1. Pear Admin 4.x 迎来了正式的发布。

2. OpenAI 前CEO和总裁Sam Altman&Greg Brockman加入微软 --Microsoft

3. 近日，河南电视台都市频道节目报道称，河南周口联通为了强迫用户更换光猫，公司在后台停掉用户的宽带账号，导致用户无法上网，然后让工程师上门 “维修”，谎称光猫损坏，需要花 299 元换新。更换完后，联通再在后台恢复用户的网络。只能说牛！

4. Apache APISIX 3.7.0版本已经发布，带来了一系列新功能、Bug 修复和相关用户体验优化。快去体验一下！

## 如何查看k8s中pod所用的字体？

作为一位k8s操作手，这个过程需要我们深入Pod的内部环境，利用Linux系统的工具进行探查。

### 第一步：确定目标Pod

开启命令行终端，使用`kubectl`这个强大的工具列出当前命名空间下的所有Pod。这就像扫描我们的集群，找到那个正在运行我们应用的容器实例：

```sh
kubectl get pods -n xxx
```

细心观察返回的列表，确定你要检查的Pod名称。

### 第二步：进入Pod

接下来，我们需要进入Pod的Shell环境。使用`kubectl exec`命令，这相当于我们在远程通过SSH进入一个服务器：

```sh
kubectl exec -it <pod-name> -- /bin/sh
```

替换`<pod-name>`为实际的Pod名称。`/bin/sh`是我们用来和Pod进行交互的Shell环境，有些Pod可能需要你使用`/bin/bash`。

### 第三步：列出Pod中的字体

现在已经处于Pod的内部，可以使用`fc-list`命令来列出所有安装的字体。这就像用目录扫描工具来查看服务器上的文件：

```sh
fc-list
```

一般如果用到渲染字体值之类的需求，一般使用这个命令查看即可。
```
DejaVuSerif-Bold.ttf: DejaVu Serif粗体
DejaVuSansMono.ttf: DejaVu Sans Mono普通字体
DejaVuSans.ttf: DejaVu Sans普通字体
DejaVuSans-Bold.ttf: DejaVu Sans粗体
DejaVuSansMono-Bold.ttf: DejaVu Sans Mono粗体
DejaVuSerif.ttf: DejaVu Serif普通字体
```
这些字体文件位于/usr/share/fonts/truetype/dejavu/目录下。DejaVu系列字体是开源字体，常用于Linux和其他操作系统中。它们是DejaVu字体家族的一部分，提供了一系列字体风格和变体，包括正常、粗体、斜体等。


如果发现系统中没有`fc-list`命令，说明`fontconfig`包尚未安装。可以这么安装：

```sh
apt-get update && apt-get install -y fontconfig
```

注意，上述命令假设你的容器基于Debian或Ubuntu。如果是基于Alpine Linux的容器，你需要使用`apk add`来安装。

### 第四步：完成检查和退出

在完成字体的检查后，就像离开服务器前注销用户一样，我们通过输入`exit`命令安全退出Pod：

```sh
exit
```

要注意的是，这些操作需要Pod具有足够的权限，而且你的容器镜像中需要包含相关的工具。如果你发现在这个过程中出现任何问题，可能需要回到Dockerfile中去查看是否有必要添加额外的工具或者字体包。如果没有权限的话，安装也会受限制。


## 2023年11月18日

重大新闻！奥特曼被OpenAI开除了！


## 怎么就被开除了？

早上被刷圈了，先看看发生什么了。据新闻了解，11月17日，人工智能研究公司OpenAI首席执行官山姆·奥特曼（Sam Altman）突然离职。我们先上官网看看怎么个事？

![Alt text](image.png)

以下是结合工具翻译，原文大致内容如下：

开放人工智能（OpenAI）的董事会宣布，Sam Altman将离任首席执行官并离开董事会。同时，该公司的首席技术官Mira Murati将作为临时首席执行官领导OpenAI。

Mira在OpenAI担任领导团队成员已有五年时间，对于OpenAI发展成为全球人工智能领导者发挥了至关重要的作用。她拥有独特的技能组合，对公司的价值观、运营和业务有深刻理解，并且已经负责公司的研究、产品和安全职能。基于她长期的任职时间和与公司各个方面的密切合作，包括在人工智能治理和政策方面的经验，董事会认为她非常适合这个角色，并期待在进行正式搜索永久首席执行官的同时实现无缝过渡。

董事会经过审慎的审查流程后决定Altman先生离任，认为他在与董事会的沟通中缺乏一贯的坦诚，阻碍了董事会行使职责的能力。董事会不再对他继续领导OpenAI的能力表示信心。

董事会在一份声明中表示：“OpenAI旨在推动我们的使命：确保人工通用智能造福全人类。董事会始终致力于履行这一使命。我们对Sam在OpenAI的创立和发展中的许多贡献表示感谢。与此同时，我们相信在我们继续前进时需要新的领导力。作为公司研究、产品和安全职能的领导者，Mira非常有资格担任临时首席执行官。我们对她在这个过渡期内领导OpenAI的能力充满信心。”

OpenAI的董事会由OpenAI首席科学家Ilya Sutskever、独立董事Quora首席执行官Adam D’Angelo、技术企业家Tasha McCauley和乔治城大学安全与新兴技术中心的Helen Toner组成。

作为过渡的一部分，Greg Brockman将辞去董事会主席职务，但将继续担任公司内的职位，并向首席执行官汇报。

OpenAI成立于2015年，是一个非营利性机构，其核心使命是确保人工通用智能造福全人类。2019年，OpenAI进行了重组，以确保公司能够筹集资金追求这一使命，同时保留非营利机构的使命、治理和监督。董事会的大部分成员是独立的，独立董事在OpenAI没有股权。尽管公司经历了巨大的增长，但董事会始终承担着推进OpenAI使命和保护章程原则的基本治理责任。


对于业内人士来说可谓是震惊，毕竟奥特曼是很多人心中的英雄，前谷歌首席执行官就Eric Schmidt就是在社交媒体上这么说，认为奥特曼将openai从一无所有发展成价值将近千亿美金的企业，并做出了永久改变人类世界的事情。


咱再详细解下奥特曼

Sam Altman于1985年出生，从小在密苏里州圣路易斯长大，他从小就对计算机科学和技术表现出浓厚的兴趣，8岁就拥有了自己第一台电脑。儿时偶像是史蒂夫乔布斯。在上高中时，他开始学习编程，并在互联网初期就开始开发软件。

Altman进入斯坦福大学攻读计算机科学学位，但在一年级结束时辍学。他决定投身创业，并与一位朋友共同创立了一家名为Loopt的移动定位社交网络公司。这家公司于2005年成立，成为全球首批推出基于位置的社交网络应用的企业之一。

Loopt早期获得了多轮融资，并迅速发展壮大。2012年3月，Green Dot Corporation一家金融科技公司以4340万美元收购了Loopt。这次交易使Altman成为了一名年轻的企业家，并为他日后的创业生涯奠定了基础。

在Loopt被收购后，Altman成为了Y Combinator的创业伙伴。Y Combinator是一家知名的创业加速器和风险投资公司，帮助初创企业获得资金和资源，并提供指导和支持。Altman在Y Combinator的领导下推动了公司的发展，并为全球范围内的许多成功创业公司提供了支持和指导。

2014年2月，Altman 被 Y Combinator 联合创始人Paul Graham任命为总裁。在他的领导下，Y Combinator继续推动着创业公司的发展，并成为全球范围内最具影响力的创业加速器之一。

随着时间的推移，Altman对人工智能的发展产生了浓厚的兴趣，并相信这将对全人类产生重大影响。因此，他于2015年与其他合伙人共同创立了OpenAI，这是一个致力于推动人工通用智能发展的非营利组织。作为OpenAI的创始人之一，Altman在公司初期发挥了重要的领导作用。

除了OpenAI和Y Combinator，Altman还是许多知名科技公司的董事会成员，包括Reddit、Palantir Technologies和Coinbase等。他也积极投资和支持其他初创企业，并在科技界广泛发表演讲和写作，分享他对技术和创新的见解和观点。

2017 年，Altman因通过 Velocity 创业计划为企业提供支持而获得加拿大滑铁卢大学荣誉 工程博士学位。

看完以上，大家什么感受？这个开除不像咱一般人的开除，咱们被开除了，只能卷铺盖回家了。人家有能力，况且又投资了一堆公司，可能只是换个地方而已。好了今天的介绍就到这了。


## 聊点别的

1. 周末到了，铁铁们都在干嘛？没事的话可以来技术交流群闲聊哈，都是一群热爱技术的人，会分享一些技术干货和资料，等你加入哈。

2.  世纪难题，待会吃点啥？

参考资料：

[1]https://openai.com/blog/openai-announces-leadership-transition

[2]https://en.wikipedia.org/wiki/Sam_Altman

[3]https://web.archive.org/web/20140625021419/http://ycombinator.com/people.html



## 2023年11月17日



## 阿里云对象存储OSS

最近业务在用腾讯的oss，然后看阿里云在做活动，我这边看还可以使用，所以申请来试用下，特此分享给大家。

首先登录阿里云官网，在产品一栏找到对象存储OSS栏目，点进去就可以了。

我们可以看到侧面导航栏主要分为产品概述、快速入门、操作指南、开发参考、实践教程和服务支持六部分。我们就围绕这几部分简单介绍。

### 产品概述

阿里云对象存储OSS（Object Storage Service）具体介绍可以看官网，总之简单理解就是一个可自定义的网盘，我们可以使用这个东西存储和管理我们使用的各种类型的电子数据，包括文本、图片、视频、音频等等。可以实现存储备份、静态网站的备份、图片处理、文件分发等等功能。

然后就是了解下产品如何计费的，可以通过按量、资源包、预留空间等方式计费，一般使用资源包比较划算。目前个人用户可以免费试用20G容量3个月。

存储类型有：标准、低频访问、归档、冷归档和深度归档，就是从访问速度和频率依次降低的排序，全面覆盖从热到冷的数据存储场景。


### 快速入门

有几种方式，一种是web控制台、一种是命令行工具ossutil、还有图形化工具ossbrowser和sdk的方式实现快速入门。

这里介绍下通过控制台使用

- 注册阿里云账号并开通OSS服务。
- 创建存储空间（Bucket），用于存储数据。
- 根据需要设置存储空间的访问权限、生命周期规则等。
- 使用阿里云提供的SDK或API进行数据的上传、下载、删除等操作。
- 根据业务需求，使用OSS的其他功能如图片处理、视频转码等。
- 分享文件。

### 操作指南

这部分里面就比较详细了，包括实际使用的各种点都有介绍，这部分我这里只能挑一部分说，详细的大家可以上官网查看。包括访问域名、存储类型、存储空间、权限控制、数据安全、数据管理等等。

- 涉及oss访问域名的规则、地域
- 存储类型
- 存储空间
- 上传下载
- 权限控制
- 数据安全
- 数据管理
- 监控、日志
- 数据处理
- 加速设置等等

### 开发参考

这一部分就是开发人员用到的，可以使用接口进行增删改查、或者使用SDK进行自定义的处理和开发，感兴趣的可以看一下，基本包含主流语言。还有就是常用工具比如命令行、图形化、数据迁移等等。这里OSS是一个REST服务。可以使用REST API或封装了REST API的阿里云SDK向OSS发起请求。认证系统收到请求后，会通过凭证验证请求的发送者身份。身份验证成功后，就可以操作相应的OSS资源。

### 实践教程

这一部分主要介绍数据迁移、数据备份和容灾、数据直传OSS、数据处理与分析、音视频转码、使用Terraform管理 OSS等操作，帮助高效地使用OSS，满足业务需求。


好了，到这里关于阿里云oss大致的都介绍完了，心动不如行动，实践出真知，实际去体验下，才会有自己的评价！我也先去用用，后期3个月以内分享实际操作给大家！

## 聊点别的

- 各位铁铁（不再说读者了，搞得和大家距离好远的感觉）对于自己的职业怎么看呢？是否有职业生涯的规划呢？在职业发展或者技术道路上是否有困惑或遇到瓶颈呢？打算后期通过访谈或者直播的方式请一些行业大佬来和大家聊一聊，一起探讨下，感兴趣的铁铁可以关注下或者加一下交流群，或者提前后台留言给我。

- 天冷了，咳嗽的多了，各位铁铁注意保暖！

- 好了，今天那就这些，待会吃点啥？



## 2023年11月16日

## 近日见闻

1. nodejs-21.2.0版本发布，更新速度真的快。

2. 俄罗斯操作系统 Aurora OS 5.0 全新UI亮相。

3. 小米澎湃OS刚刚在微博宣布，Xiaomi Vela采用Apache 2.0 License 面向全球软硬件开发者正式开源。

4. 开源中国将在年末推出大模型托管平台，大量人才招募中


## 腾讯云轻量数据库

这两天腾讯在搞活动，就申请免费体验了一个月的轻量数据库，感觉很不错，分享给大家。

首先说说什么是轻量应用服务器，官方解释就是新一代开箱即用、面向轻量应用场景的云服务器产品，可以建站、小程序、电商、云盘、图床等各类开发测试和学习环境，相比普通云服务器更加简单易用。

轻量服务器是自带模板的，就是说包含预置的操作系统和软件，镜像就是装机盘，通过镜像创建一台或者多台轻量应用服务器。


包含五部分镜像：应用、系统、docker基础、自定义和共享镜像

### 应用镜像

- 宝塔 Linux 面板腾讯云专享版
- WordPress
- SRS 音视频服务器
- 互动直播房间服务
- Typecho
- Cloudreve
- Matomo
- LAMP
- Node.js
- Theia IDE
- Docker CE
- K3s
- 长安链 ChainMaker
- 宝塔 Windows 面板腾讯云专享版
- ASP.NET
- Cloud Studio 1.0.1
- OpenFaaS

### 系统

- Windows Server 2022
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- CentOS 7.6
- CentOS Stream 8
- Ubuntu 18.04.1 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Debian 10.2
- Debian 11.1
- OpenCloudOS 8.6

### Docker基础

- CentOS 8.2 - Docker 20
- CentOS 7.6 - Docker 20
- Ubuntu 20.04 - Docker 20

然后和CVM有什么区别，轻量适合中小企业和开发者、CVM适合中大型企业用户，适合更轻量的业务场景，价格也更优惠、无需自己动手管理。

那我们快速使用一下轻量云数据库

登录免费专区，申请试用

然后登录控制台选择轻量应用服务器中的数据库，点击创建

选择合适的版本，创建即可。如果需要外网访问，开启即可

登录后可以查看详细的数据库情况，可以一键备份与回滚。



## 2023年11月15日

## 近日见闻

1. 铁铁们，这两天成都气温一下子就下降了，你们哪里怎么样，注意保暖。

2. 看新闻，最近各大厂商开始研制自己的系统且朝着不兼容安卓系统的方向发展，这个事大家怎么看?

3. ChatGPT Plus临时暂停新用户注册，CEO奥特曼称服务器扛不住了，你们都用上plus了吗？


## tssh客户端管理工具

之前一直想自己实现一个比较轻量而且有管理功能终端工具，尝试前端用xterm，通过websocket和后端服务器连接，实现web终端功能。最近逛github发现一个项目，挺有意思，分享给大家，这里涉及两个项目，一个是luanruisong/tssh，另一个项目应该是tssh的plus版本Trzsz-ssh。

下面一块来看看tssh，这个tssh开发作者叫anwu安伍，是个golang开发工程师，这里是关于tssh的心路历程，看了博客发现作者是一个具有非常有趣的灵魂的人<https://luanruisong.com/post/golang/tssh/>，光是各种贴图就把人逗笑了。

tssh定位是一个轻量ssh管理工具，联想到实际工作中，如果有一款直接可以在命令行中连接服务器的工具是极好的，因为比如我在开发过程中，不用再额外打开另一个终端连接工具。虽然有微软自带的，但是需要多开窗口才能实现管理功能。

这里作者分成立需求、开搞、支撑需求、基础需求、整合需求、一键安装几个部分，实现了ssh登录、tab不全、密码和秘钥登录等功能。并解决了在windows终端大小获取的问题，看完之后确实收获不少。而且作者的讲解方式非常有趣，令人印象深刻。

安装方式：

$ brew install tssh

以下是使用效果图：


## Trzsz-ssh管理工具

发现tssh虽然日常使用足够，但是这个版本的tssh支持了上传下载功能，官网地址如下：
<https://trzsz.github.io/cn/ssh>

简介中说，支持选择和搜索服务器、支持vim操作习惯、一次选择多台服务器，批量登录而且
支持 trzsz (trz / tsz) 文件传输工具。

这里安装方式很多，基本覆盖常用平台，根据自己平台选择安装即可。具体的试用还需大家多多研究。

以下是官方录屏演示：


## 2023年11月14日

Axios曝高危漏洞，私人信息还安全吗？


Axios，作为广泛应用于前端开发中的一个流行的HTTP客户端库，因其简洁的API和承诺（promise）基础的异步处理方式，而得到了众多开发者的青睐。然而，近期在安全社区中，Axios被报告存在一个重要漏洞，该漏洞涉及其对跨站请求伪造（CSRF）保护机制的处理。

## 描述

在 Axios 1.5.1中发现的一个问无意中泄露了存储在cookie中的机密 XSRF-TOKEN，方法是将其包含在向任何主机发出的每个请求的 HTTP 标头 X-XSRF-TOKEN 中，从而允许攻击者查看敏感信息。当XSRF-TOKEN cookie可用且withCredentials设置已启用时，该库会在对任何服务器的所有请求中使用秘密的XSRF-TOKEN cookie值插入X-XSRF-TOKEN头。如果恶意用户设法获取这个值，它可能会导致绕过XSRF防御机制。

NVD发布日期： 2023-11-08

CVE字典条目： CVE-2023-45857

漏洞类型： CWE-359 将私人信息暴露给未经授权的行为者

严重性： 高

影响度： 广泛


## 什么是CWE0359

详细可以查看官网介绍：```https://cwe.mitre.org/data/definitions/359.html```

CWE-359:将私人个人信息暴露给未经授权的行为者,是 Common Weakness Enumeration（共同弱点枚举）中的一个条目，代表 "Exposure of Private Information ('Privacy Violation')"，即 "暴露私人信息（隐私违规）"。这个弱点描述了一个安全问题，其中应用程序未能充分保护用户的敏感数据，导致未经授权的第三方可以访问或泄露这些信息。

在CWE-359的情景下，可能发生的是：

- 应用程序可能会在没有适当加密的情况下传输敏感信息。
- 存储敏感信息的数据库可能未能正确配置访问控制，导致未授权访问。
- 应用程序日志可能会记录敏感信息，如果没有得到适当保护，可能会被泄露。
- 错误消息或页面上可能会显示敏感信息，没有经过适当处理，导致在用户界面上泄露。

CWE-359 违反了用户隐私权，可以导致个人数据泄露，这对个人和组织都可能产生严重后果。为了避免此类弱点，开发者和组织应实施严格的数据处理和存储政策，定期进行安全审计，并确保使用最佳实践来保护个人数据。对于开发人员而言，理解CWE-359并采取预防措施对于创建安全软件来说至关重要。

## 什么是CSRF、XSRF

跨站请求伪造（CSRF）是一种网络攻击，它允许攻击者利用用户的登录状态在另一个网站上对目标应用程序发起恶意请求。这种攻击的危险之处在于，它可以在用户毫不知情的情况下，以用户的身份在目标网站上进行操作，例如更改密码、转账等。

`XSRF-TOKEN` 是一种常用的防御措施，它涉及到在客户端生成一个令牌（Token），这个令牌会在进行敏感操作时由服务器进行验证。该令牌通常在用户打开表单时由服务器生成，并作为表单数据的一部分发送回服务器。服务器将验证提交的表单中的`XSRF-TOKEN`是否与用户的会话中存储的令牌相匹配，以确认请求是合法的。

漏洞出现的情况可以是：

1. **服务器配置不当**：如果服务器没有正确设置或验证`XSRF-TOKEN`，那么即使在客户端设置了令牌，攻击者也可能绕过这种保护机制。例如，如果服务器不验证所有敏感请求的令牌，或者验证逻辑存在缺陷，那么攻击者可以发送未经授权的请求。

2. **客户端实现错误**：客户端代码，比如JavaScript或Web框架，可能没有正确地在每个请求中发送`XSRF-TOKEN`，或者在处理cookies时出现错误，导致令牌不被包含在请求中。

3. **安全策略缺失**：如果网站不使用`XSRF-TOKEN`或类似的防御机制，或者没有将其纳入全面的安全策略中，就可能容易受到CSRF攻击。

查看相关文章：
```https://portswigger.net/web-security/csrf/preventing```
```https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html```

为了保护应用程序不受CSRF攻击，你应该：

- 为所有敏感操作使用CSRF令牌。
- 确保服务器端对所有需要的地方进行令牌验证。
- 设置和强制执行内容安全策略（Content Security Policy，CSP）以减少跨站脚本（XSS）攻击的风险，XSS攻击可以用来窃取`XSRF-TOKEN`。
- 确保使用HTTPS来防止中间人攻击，中间人攻击可能会截取令牌。
- 定期更新和修补所有软件依赖项，包括客户端库和服务器端框架。


## 再现

复现步骤

通过运行以下命令使用Next.js的最新版本开始一个新项目：npx create-next-app@latest。然后，使用这个命令安装最新版本的Axios库：npm i axios
创建一个Axios实例，配置如下，启用跨站点请求伪造（CSRF）保护，通过在请求中包括凭据：
```javascript
  const instance = axios.create({
    withCredentials: true,
  });
```
用特定属性安装XSRF-TOKEN cookie。将cookie值设置为"whatever"，并为"localhost"域配置严格的同站策略：
```javascript
    const cookies = new Cookies();
    cookies.set("XSRF-TOKEN", "whatever", {
      domain: "localhost",
      sameSite: "strict",
    });
```
使用你的Axios实例发起跨域请求。在这个例子中，我们向"https://www.com/"发出GET请求，并处理响应及潜在错误：
```javascript
    instance
      .get("https://www.com")
      .then((res) => console.log(res.data))
      .catch((err) => console.error(err.message));
```
运行你的项目，并打开浏览器的网络标签进行调试和监控网络活动。
验证对"https://www.com/"的跨域请求是否包含值为"whatever"的"X-XSRF-TOKEN"头。
确认在使用Axios实例发送请求时，"XSRF-TOKEN" cookie的值会泄露给任何第三方主机。这对于安全至关重要，因为你不希望将CSRF令牌泄漏给未授权的实体。
代码片段
lib/adapters/xhr.js:191
```javascript
const xsrfValue = (config.withCredentials || isURLSameOrigin(fullPath))
```
预期行为
预期结果：XSRF-TOKEN不会泄露给第三方主机
实际结果：XSRF-TOKEN在每个使用Axios实例发出的请求中泄露

Axios 版本
[v0.8.1] - [v1.5.1]


参考资料：

[1] https://portswigger.net/web-security/csrf/preventing

[2] https://github.com/axios/axios/issues/6006

[3] https://nvd.nist.gov/vuln/detail/CVE-2023-45857

[4] https://cwe.mitre.org/data/definitions/359.html



## 2023年11月13日

## 近日见闻

1. tssh 发布 v0.1.13，支持 Warp终端，支持了更多 ssh功能。支持trzsz的ssh客户端，支持搜索和选择服务器进行批量登录，支持记住密码。  --trzsz-ssh

2. 近日，网易、美团等多家互联网公司发布和鸿蒙系统有关岗位招聘，加快推进鸿蒙原生应用开发转型。数据显示，截至今年 8 月，鸿蒙生态设备数已超过 7 亿，220 万开发者投入到鸿蒙生态的开发。 --oschina

3. Axios有漏洞，在Axios受影响版本中，当 XSRF-TOKEN cookie可用且 withCredentials设置打开时，该库会在对任何服务器的所有请求中将 XSRF-TOKEN cookie 值插入 X-XSRF-TOKEN 标头。攻击者可以通过构造链接、页面等方式诱导受害者点击，以受害者的身份执行未经授权的操作，可能导致账户被接管、数据泄露等安全问题。修复方案：将组件 axios 到 1.6.0 或更高版本。--axios社区

## k8s基础术语词汇表
```
- API Group (API 组)
Kubernetes API 中的一组相关路径。

- API 服务器 (kube-apiserver)
API 服务器是 Kubernetes 控制平面的组件，它公开了 Kubernetes API，并负责处理接收请求的工作。API 服务器是 Kubernetes 控制平面的前端。Kubernetes API 服务器的主要实现是 kube-apiserver，它设计上考虑了水平扩缩，即可以通过部署多个实例进行扩展。

- CustomResourceDefinition
通过定制化的代码增加资源对象给你的 Kubernetes API 服务器，而无需编译完整的定制 API 服务器。

- DaemonSet
确保 Pod 的副本在集群中的一组节点上运行。

- Deployment
管理多副本应用的一种 API 对象，通常通过运行没有本地状态的 Pod 来完成工作。

- Docker (Docker Engine)
一种提供操作系统级别虚拟化（也称作容器）的软件技术。

- Dockershim
Kubernetes v1.23 及之前版本中的一个组件，使得 kubelet 能够与 Docker Engine 通信。

- Finalizer
带有命名空间的键，告诉 Kubernetes 在特定条件满足后再完全删除被标记为删除的资源。

- Init 容器
应用容器运行前必须先运行完成的一个或多个 Init 容器。

- Job
需要运行完成的确定性的或批量的任务。

- kube-controller-manager
控制平面的组件，负责运行控制器进程。

- kube-proxy
集群中每个节点上运行的网络代理，实现 Kubernetes 服务概念的一部分。

- Kubectl
Kubernetes API 与 Kubernetes 集群的控制面进行通信的命令行工具。

- Kubelet
会在集群中每个节点上运行，确保容器运行在 Pod 中。

- Kubernetes API
通过 RESTful 接口提供 Kubernetes 功能服务并负责集群状态存储的应用程序。

- LimitRange
提供约束，限制命名空间中每个容器或 Pod 的资源消耗。

- Master
遗留术语，作为运行控制平面的节点的同义词使用。

- Minikube
用来在本地运行 Kubernetes 的工具。

- Pod
Kubernetes 的原子对象，表示集群上一组正在运行的容器。

- Pod 安全策略
为 Pod 的创建和更新操作启用细粒度的授权。

- Pod 生命周期
关于 Pod 在其生命周期中的不同阶段的高层次概述。

- QoS 类 (Quality of Service Class)
为 Kubernetes 提供了一种分类集群中的 Pod 并做出有关调度和驱逐决策的方法。

- ReplicaSet
下一代副本控制器。

- ServiceAccount
为在 Pod 中运行的进程提供标识。

- StatefulSet
用于管理一组 Pod 的部署和扩缩，并为这些 Pod 提供持久存储和持久标识符。

- UID
Kubernetes 系统生成的字符串，唯一标识对象。

- 标签 (Label)
用来为对象设置可标识的属性标记，对用户有意义且重要。

- 对象 (Object)
Kubernetes 系统中的实体，用于表示集群的状态。

- 服务 (Service)
将运行在一个或一组 Pod 上的应用程序作为网络服务公开的方法。

- 干扰 (Disruption)
导致一个或多个 Pod 服务停止的事件，影响依赖于受影响 Pod 的资源，例如 Deployment。

- 工作负载 (Workload)
在 Kubernetes 上运行的应用程序。

- 混排切片 (Shuffle Sharding)
一种请求指派给队列的技术，其隔离性优于哈希取模的方式。

- 基于角色的访问控制 (RBAC)
管理授权决策，允许管理员通过 Kubernetes API 动态配置访问策略。

- 集群 (Cluster)
一组运行容器化应用程序的工作机器，称为节点。

- 节点 (Node)
Kubernetes 中的工作机器。

- 静态 Pod (Static Pod)
由节点上的 kubelet 守护进程直接管理的 Pod。API 服务器不了解其存在。

- 镜像 (Image)
保存的容器实例，包含了应用运行所需的软件。

- 卷 (Volume)
包含可被 Pod 中容器访问的数据的目录。

- 控制平面 (Control Plane)
指容器编排层，暴露 API 和接口定义、部署容器和管理容器生命周期。

- 控制器 (Controller)
通过监控集群的公共状态，并努力将当前状态转变为期望的状态。

- 控制组 (cgroup; control group)
一组具有可选资源隔离、审计和限制的 Linux 进程。

- 扩展组件 (Extensions)
扩展并与 Kubernetes 深度集成支持新型硬件的软件组件。

- 垃圾收集 (Garbage Collection)
Kubernetes 用于清理集群资源的各种机制的统称。

- 临时容器 (Ephemeral Container)
可以在 Pod 中临时运行的容器类型。

- 名称 (Name)
客户端提供的字符串，引用资源 URL 中的对象。

- 名字空间 (Namespace)
Kubernetes 用来支持集群中资源组隔离的抽象。

- 亲和性 (Affinity)
一组规则，提供给调度程序在何处放置 Pod 的提示信息。

- 清单 (Manifest)
JSON 或 YAML 格式的 Kubernetes API 对象规范。

- 日志 (Logging)
集群或应用程序记录的事件列表。

- 容器 (Container)
可移植、可执行的轻量级镜像，包含软件及其相关依赖。

- 容器环境变量 (Container Environment Variables)
以 name=value 形式提供的，在 Pod 中运行的容器所必须的信息。

- 容器运行时 (Container Runtime)
基础组件，使 Kubernetes 能够有效运行容器。

- 容器运行时接口 (Container Runtime Interface; CRI)
一组让容器运行时与节点上 kubelet 集成的 API。

- 容忍度 (Toleration)
核心对象，包含三个必需的属性：key、value 和 effect。允许将 Pod 调度到具有对应污点的节点或节点组上。

- 设备插件 (Device Plugin)
在工作节点上运行并为 Pod 提供访问资源的能力，例如需要特定供应商初始化或安装步骤的本地硬件资源。

- 事件 (Event)
描述系统状态变化及需要注意的事项的 Kubernetes 对象。

- 数据平面 (Data Plane)
提供诸如 CPU、内存、网络和存储的能力，以便容器运行并连接到网络。

- 特性门控 (Feature gate)
一组键，用于控制集群中启用哪些 Kubernetes 特性。

- 污点 (Taint)
核心对象，包含三个必需的属性：key、value 和 effect。阻止节点或节点组调度 Pod。

- 选择算符 (Selector)
允许用户通过标签对资源对象进行筛选过滤。

- 应用 (Applications)
各种容器化应用运行所在的层。

- 注解 (Annotation)
以键值对形式给资源对象附加随机的、无法标识的元数据。

- 资源配额 (Resource Quotas)
限制每个命名空间资源消耗总和的约束。
```





## 2023年11月12日

## 近日见闻

1. IntelliJ IDEA 2023.3 Beta 版本现已发布，此版本包括抢先体验计划期间引入的所有重要更新。--java社区

2. 苹果副总裁回应 “黄金内存”：「统一内存架构」的 8GB 近似于其它系统的 16GB。 --B站

3. UNIX时间即将进入17亿纪元，再过两天，北京时间2023/11/15 06:13:20，UNIX时间将进入 1700000000纪元。 --UNIX社区

## 阿里系产品崩了？

今天下午，淘宝、咸鱼、钉钉、语雀崩了，上了热搜，阿里云也登不上去了，到底是怎么回事？官方回复说故障原因与某个底层服务组件有关，工程师正在紧急处理。由于该故障为全域故障。所有部署于阿里云且高度依赖阿里云 API 的平台均出现故障情况，包括淘宝、钉钉、咸鱼、阿里云盘、不背单词等。

其实出现故障在运维工作中是正常不过的。但是提前发现问题，让故障消失，未来不复发是着重要关注的。最怕的是影响客户正常使用，而且是大面积故障，造成全国用户受影响，算是严重故障了。在阿里云拥有大规模运维团队的维护下，也会出现不可避免的问题，侧面表明999可用率的服务也是一种理论情况，实践才是检验真理的唯一标准。所以平时的所谓的运维救火演练、混沌平台的建设都是需要着重关注的。作为运维团队中的一员，每次大平台出现故障，我都会心里一惊，时长提醒自己，平时的运维预警以及故障演练是必不可少的。

好了，周末已经过去啦，保持好心态迎接明天！



## 2023年11月9日

## 近日见闻

1. Fedora 39 已正式发布。此版本采用 Linux 6.5 内核，更新的版本将作为稳定版更新发布。 --Fedora社区

2. binlog4j 1.9.0发布，Java轻量级binary log客户端。 --oschina

3. 魅族为Flyme征集中文名，入选者将获赠「华小魅」手机组合包。 --魅族

4. vivo 已在Hugging Face上正式开源蓝心大模型BlueLM-7B。 --vivo

## CentOS中实用的文件删除和备份脚本

在实际工作中，避免不了需要批量删除某一些文件，或者备份一些文件，所以这就交给脚本完成就好，但是使用中一定要谨慎使用。

### 删除文件

首先准备好你要删除的文件目录到一个list.txt中

例如：

```bash
ls -1 > list.txt
```

这个命令会将当前目录下的文件和目录名（不包括子目录）输出到 `list.txt` 文件中。

- `ls` 是列出目录内容的命令。
- `-1` 选项让 `ls` 每行只输出一个文件名，这使得输出更适合被脚本读取。
- `>` 是重定向操作符，它会将 `ls` 的输出写入到 `list.txt` 文件中。如果 `list.txt` 文件已经存在，这个操作会覆盖原有的文件内容。

如果你只希望列出文件，而非目录，你可以使用 `ls -1p | grep -v /` 命令：

```bash
ls -1p | grep -v / > list.txt
```

- `ls -1p` 命令会在目录名后添加 `/` 符号。
- `grep -v /` 命令会过滤掉包含 `/` 的行，也就是目录名。
- 最后结果重定向到 `list.txt` 文件中。


然后你可以使用 bash 脚本来实现删除文件。以下是一个示例脚本

```bash
#!/bin/bash

# 假设你的 txt 文件名为 filelist.txt
while IFS= read -r line
do
    if [ -f "$line" ]; then
        rm "$line"
        echo "$line 文件已被删除"
    else
        echo "$line 文件不存在"
    fi
done < "filelist.txt"
```
`IFS= read -r line` 是一种安全的读取文本文件的方式，它可以处理文件名中的特殊字符。

`[ -f "$line" ]` 会检查一个名为 `$line` 的文件是否存在。

`rm "$line"` 会删除指定的文件。

`echo "$line 文件已被删除"` 或 `"$line 文件不存在"` 是一个简单的确认消息，它不是必需的，但有助于你知道脚本在做什么。

另外，对于文件删除操作，一定要小心，因为删除的文件无法恢复。对于需要删除的文件，最好先确认一下，避免误删。

那如果使用python呢，可以使用 `os` 模块，它提供了许多处理文件和目录的功能。下面是一个示例脚本：

```python
import os

# 假设你的 txt 文件名为 filelist.txt
with open('filelist.txt', 'r') as f:
    for line in f.readlines():
        line = line.strip()  # 移除行尾的换行符
        if os.path.isfile(line):
            try:
                os.remove(line)
                print(f'文件 {line} 已被删除')
            except OSError as e:
                print(f'删除文件 {line} 发生错误: {e.strerror}')
        else:
            print(f'文件 {line} 不存在')
```

这个脚本使用了 `os.path.isfile(line)` 来检查一个名为 `line` 的文件是否存在，`os.remove(line)` 来删除指定的文件。

使用 `try/except` 结构是为了处理可能发生的错误，例如权限问题或其它文件系统错误。当删除文件发生错误时，我们打印出错误信息。 删除文件操作要特别小心，先在一些不重要的文件上测试。确认没有问题后，再在你要删除的文件上执行。

### 备份文件

用python备份可以使用 `shutil` 和 `os` 库来复制文件和管理路径。以下是一个示例脚本：

```python
import os
import shutil
from datetime import datetime

# 创建一个带日期的备份目录
backup_dir = "/path/to/your/backup/directory/backup_" + datetime.now().strftime("%Y%m%d%H%M%S")
os.makedirs(backup_dir, exist_ok=True)

# 从 list.txt 读取文件名
with open('list.txt', 'r') as f:
    for line in f.readlines():
        line = line.strip()  # 移除行尾的换行符
        if os.path.isfile(line):
            # 复制文件到备份目录
            shutil.copy(line, backup_dir)
```

这个脚本会创建一个带时间戳的备份目录，并从 `list.txt` 中读取文件名，将存在的文件复制到备份目录。

要定时执行这个脚本，你依然需要使用 cron 任务。你可以使用 `crontab -e` 命令打开你的用户的 cron 配置，并添加类似如下的配置：

```
0 0 * * * /usr/bin/python3 /path/to/your/script.py
```

这行配置表示每天午夜执行脚本 `/path/to/your/script.py`，`/usr/bin/python3` 是 Python 3 的常见路径，你需要根据你的环境替换为正确的 Python 路径。

注意：在给定的路径中，`/path/to/your/backup/directory/` 和 `/path/to/your/script.py` 你需要替换为你自己的路径。

## 2023年11月7日

## 近日见闻

1. 2023年11月6日，DataEase 开源数据可视化分析平台正式发布 v2.0 版本。DataEase 开源项目创立于2021年1月，于2021年6月发布v1.0版本。 --DataEase

2. DALL・E3绘图来啦，开源AI聊天、绘图软件AIdea现已支持 DALL・E3。 --mylxsw

3. OpenAI开发者大会：GPT-4 Turbo、GPTs商店、128k上下文窗口、大降价。 --奥特曼

4. 龙芯 3A6000 国产桌面处理器本月底发布，对标英特尔10代酷睿。 --龙芯

5. 李开复旗下AI公司发布Yi系列开源大模型，估值超 10 亿美元 --零一万物

## 一种框架，一次代码，多平台使用

### Flutter

有没有一种语言或者一种框架，只需编写一次代码，就可以在多种平台运行，没错它来了，它就是Flutter。

Flutter是一种前端框架。它是Google开发的一套用户界面（UI）开发工具，可以用一套代码库来构建在iOS、Android、Web、和桌面环境下运行的应用。Flutter的主要优势在于它的高度可定制性，以及其跨平台的能力。

Flutter使用Dart语言进行编程。Dart是由Google开发的一种计算机编程语言，它旨在为开发者提供一种简单、强大的方式来开发高效的、高质量的应用程序，特别是对于UI开发而言。Dart的语法风格相对简洁，同时它的性能强大、效率高，是Flutter的理想选择。

### Dart

Dart是由Google开发和维护的一种通用编程语言。它在2011年首次亮相，最初设计的目标主要是用于开发现代web应用程序。随着时间的推移，Dart已经发展成为一种多用途、简单易用、高效率、面向对象的语言。

以下是关于Dart的一些主要特性：

1. **易于学习和使用**：Dart与许多现有的语言有着相似的语法，特别是C语言和JavaScript，这使得开发者可以轻易地上手。同时，Dart也提供了一些现代化语言特性，提升开发效率和可读性。

2. **面向对象**：Dart是一种基于类的、面向对象的语言，所有的值都是对象，所有的对象都是类的实例。它还支持mixin式的继承。

3. **强类型**：虽然Dart在早期版本中是弱类型的，但现在它已经实现了强类型。这使得开发者可以在编译时捕获更多的错误，从而提高代码质量。

4. **垃圾回收**：Dart使用垃圾回收技术来自动管理内存，无需开发者手动释放不再使用的内存。

5. **支持并发**：Dart通过Isolates（一种类似于线程的实体，但不共享内存）来实现并发处理。

6. **用于多平台开发**：通过Google的Flutter框架，Dart可以用于开发跨平台的移动、Web和桌面应用程序。

Dart语言的一个简单示例：

```dart
void main() {
  var name = 'World';
  print('Hello, $name!');
}
```
这段代码会输出 "Hello, World!"。其中的`$name`是一个字符串插值的例子，可以在字符串中直接插入变量或表达式的值。

###  开发一个Flutter应用程序的步骤

1. **安装Flutter**: 下载最新稳定版本的Flutter SDK，然后添加flutter/bin到环境变量中。

2. **安装编辑器**: 尽管您可以使用任何文本编辑器来写Flutter应用，但建议使用支持Flutter开发的编辑器，例如Android Studio，VS Code，或IntelliJ IDEA。这些编辑器都有Flutter插件，可以提供代码补全、语法高亮、widget编辑等功能。

3. **创建新的Flutter应用**: 在命令行中，您可以通过以下命令来创建一个新的Flutter应用：
    ```
    flutter create my_app
    ```
    这将在当前目录下创建一个新的文件夹，文件夹名为my_app，里面包含了一个简单Flutter应用的初始代码。

4. **运行Flutter应用**: 在my_app目录下，用以下命令来启动您的应用：
    ```
    cd my_app
    flutter run
    ```
    如果您已经连接了Android设备，或者已经启动了Android模拟器，您的应用应该会在设备或模拟器上运行起来。

5. **编辑Flutter应用**: 打开my_app/lib/main.dart，这是应用程序的主入口文件。在这里，您可以开始编写自己的应用代码。以下是一个简单的示例，展示了一个包含“Hello World”文本的页面：
    ```dart
    import 'package:flutter/material.dart';

    void main() {
      runApp(MyApp());
    }

    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          home: Scaffold(
            appBar: AppBar(
              title: Text('My First Flutter App'),
            ),
            body: Center(
              child: Text('Hello World'),
            ),
          ),
        );
      }
    }
    ```
    保存文件后，Flutter的热重载功能会立即在设备或模拟器上更新应用。

### 创建一个显示用户信息的Flutter应用

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('User Info')),
        body: DataTable(
          columns: const <DataColumn>[
            DataColumn(
              label: Text(
                'Name',
              ),
            ),
            DataColumn(
              label: Text(
                'Age',
              ),
            ),
            DataColumn(
              label: Text(
                'Address',
              ),
            ),
          ],
          rows: const <DataRow>[
            DataRow(
              cells: <DataCell>[
                DataCell(Text('John')),
                DataCell(Text('30')),
                DataCell(Text('New York')),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```



## 2023年11月6日

## 近日见闻

1. 马斯克旗下公司 xAI 的第一款AI模型曝光！名为：Grōk ，有望成为ChatGPT最强竞品！--马斯克

2. Rickrack焰火十二卷 v2.8.41更新，开源调色板软件。--rickrack

3. Ant Design 5.11.0 发布，企业级 UI 设计语言和 React 实现。 --AntDesign

4. 谷歌 Chrome 开发者博客官宣：Chrome 已默认启用 WebAssembly 垃圾回收 (WasmGC) 功能 —— 能够将具有 GC 的编程语言编译为 WebAssembly (Wasm)。 --google


## next.js快速创建一个示例应用


首先，我们使用create-next-app创建一个新的Next.js应用：

```bash
npx create-next-app@latest my-app
```

注意：
```js
Need to install the following packages:
create-next-app@14.0.1
Ok to proceed? (y) y
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: 'create-next-app@14.0.1',
npm WARN EBADENGINE   required: { node: '>=18.17.0' },
npm WARN EBADENGINE   current: { node: 'v18.16.0', npm: '9.8.1' }
```
最新版本，需要node版本大于等于18.17.0，需要注意下。

然后，进入新创建的应用目录：

```bash
cd my-app
```

在`pages`目录下，你会发现一个名为`index.js`的文件，这个文件对应的是应用的主页。

```jsx
import React from 'react';
import Link from 'next/link';

function HomePage() {
  return (
    <div>
      <h1>Welcome to Next.js!</h1>
      <p>This is the home page of our Next.js application.</p>
      <p>
        <Link href="/about">
          <a>About</a>
        </Link>
      </p>
    </div>
  );
}

export default HomePage;
```

然后，我们要创建一个关于页面。在`pages`目录下，创建一个新的文件`about.js`：

```jsx
import React from 'react';
import Link from 'next/link';

function AboutPage() {
  return (
    <div>
      <h1>About</h1>
      <p>This is the about page of our Next.js application.</p>
      <p>
        <Link href="/">
          <a>Home</a>
        </Link>
      </p>
    </div>
  );
}

export default AboutPage;
```

现在，启动应用：

```bash
npm run dev
```

在浏览器中访问http://localhost:3000，看到主页可以点击"About"链接到关于页面，然后在关于页面点击"Home"链接返回主页。

这只是一个非常基础的Next.js应用，而Next.js的功能远不止这些，想要深入学习，需要不断的实践和联系。








## 2023年11月3日17:05:09

## 近日见闻

1. Transformers.js 2.7.0 发布，Transformers.js 支持在浏览器中实现最先进的机器学习 —— 无需服务器。它提供预训练模型和熟悉的 API，支持自然语言处理、计算机视觉、音频和多模态领域的任务。借助 Transformers.js，开发者可以直接在浏览器中运行文本分类、图像分类、语音识别等任务，这使其成为 ML 从业者和研究人员的强大工具。最近发布的 Transformers.js 2.7.0 添加了一项重要功能：文本转语音。 --Transformer

2. SQLite 3.44.0发布,SQLite 是一个C语言库，实现了一个小型、快速、独立、高可靠性、全功能的 SQL数据库引擎。SQLite 是世界上使用最多的数据库引擎。SQLite的源代码属于公共领域，每个人都可以免费使用，用于任何目的。--SQLite

3. Redis 创始人用 C 语言编写最小聊天服务器：Smallchat,详情查看github。--redis社区

4. 阿里云推出了一款基于通义大模型的智能编码辅助工具 —— 通义灵码。 --阿里云

## python调用chatgp3.5接口

以下是使用Python调用ChatGPT接口的示例代码。在使用此代码之前，请确保已安装`requests`库。在命令行中运行以下命令以安装：

```bash
pip install requests
```

然后，使用以下示例代码来调用ChatGPT API。请记住将`your_openai_api_key`替换为您的实际API密钥，并根据需要修改输入文本和API参数。

```python
import requests
import json

# 替换为您的API密钥
api_key = 'your_openai_api_key'

# 设置请求头
headers = {
    'Content-Type': 'application/json',
    'Authorization': f'Bearer {api_key}'
}

# 设置请求的URL
url = 'https://api.openai.com/v1/engines/davinci-codex/completions'

# 设置请求参数
prompt = 'Translate the following English text to chinese: "{Hello, how are you?}"'
max_tokens = 50
n = 1
temperature = 0.5

payload = {
    'prompt': prompt,
    'max_tokens': max_tokens,
    'n': n,
    'temperature': temperature
}

# 发送POST请求并获取响应
response = requests.post(url, headers=headers, data=json.dumps(payload))

# 解析响应内容
data = response.json()

if 'choices' in data:
    for choice in data['choices']:
        print(choice['text'])
else:
    print("Error:", data)
```





## 2023年11月2日

## 近日见闻

1. Kotlin 1.9.20 版本已发布，适用于所有目标的 K2 编译器已进入 Beta 阶段，Kotlin Multiplatform 已进入稳定阶段。 --Kotlin

2. vivo 发布自研操作系统蓝河 (BlueOS)，系统框架采用 Rust 编写. --vivo

3. 新款 MacBook Pro “减配”：内存带宽缩水、14寸M3入门款2个USB-C接口 --oschina

4. youlai-mall v2.4.1 已经发布，全栈开源商城项目。 --youlai

## async/await和promise链

`async/await` 和 Promise 链都是 JavaScript 中处理异步操作的方法，但它们的编写方式和可读性有所不同。让我们分别了解一下它们的区别和作用。

### Promise 链

Promise 是一种编程范式，用于处理异步操作。它是一个表示异步操作结果的对象，可以是成功（resolved）或失败（rejected）的状态。Promise 的出现解决了回调地狱（callback hell）的问题，使得异步代码更容易处理和组织。

Promise 链是一种使用 Promise 的编程模式。在 Promise 链中，你可以通过 `.then()` 和 `.catch()` 方法链接多个异步操作。这样做的好处是，可以按顺序执行异步操作，并在前一个操作完成后传递结果给下一个操作。

下面是一个使用 Promise 链的示例：

```javascript
fetchData()
  .then((data) => processData(data))
  .then((processedData) => saveData(processedData))
  .catch((error) => handleError(error));
```

在这个示例中，我们首先调用 `fetchData()` 获取数据，然后使用 `.then()` 对数据进行处理，接着将处理后的数据保存，最后使用 `.catch()` 捕获并处理错误。

### async/await

`async/await` 是一种基于 Promise 的异步编程语法糖，引入于 ECMAScript 2017 标准。它使得异步代码看起来和同步代码类似，从而更容易阅读和理解。

`async` 关键字用于声明异步函数，这样的函数将返回一个 Promise。`await` 关键字用于等待一个 Promise 的结果，它只能在 `async` 函数内部使用。

下面是一个使用 `async/await` 的示例：

```javascript
async function handleData() {
  try {
    const data = await fetchData();
    const processedData = await processData(data);
    await saveData(processedData);
  } catch (error) {
    handleError(error);
  }
}

handleData();
```

在这个示例中，我们使用 `await` 关键字等待异步操作完成，使得代码看起来像同步代码。这样可以提高代码的可读性。

### 区别与作用

1. 语法和可读性：`async/await` 使得异步代码看起来像同步代码，提高了可读性。而 Promise 链使用了 `.then()` 和 `.catch()` 方法，导致代码嵌套，可读性略差。
2. 错误处理：`async/await` 允许你使用 `try/catch` 块处理异步错误，这与同步代码的错误处理方式相同。而 Promise 链需要使用 `.catch()` 方法捕获错误。
3. 返回值：`async` 函数总是返回一个 Promise，这使得你可以将多个 `async` 函数组合在一起。Promise 链的返回值也是一个 Promise。

尽管 `async/await` 和 Promise 链在功能上没有本质区别，但它们在语法和可读性上有所不同。你可以根据个人喜好和项目需求选择使用哪种方式处理异步代码。


## 同步代码、异步代码

同步代码和异步代码是编程中两种重要的执行方式，它们主要的区别在于是否需要等待操作完成后才进行下一步操作。

1. **同步代码**：在执行同步代码时，每一步操作都会按照代码的书写顺序依次执行，只有当当前的操作完成后，才会执行下一步操作。也就是说，每一步操作都会阻塞后面的代码，直到这一步操作完成。例如：

```javascript
let result = database.query("SELECT * FROM posts");
console.log(result); 
console.log("Done");
```

在这个例子中，首先执行数据库查询，然后等待查询结果返回，查询完成后才会执行后面的打印操作。如果数据库查询需要花费很长时间，那么后面的打印操作就需要等待相应的时间。

2. **异步代码**：不同于同步代码，异步代码不会等待当前操作完成后才执行下一步操作。也就是说，如果一步操作需要花费很长时间，异步代码不会阻塞，而是继续执行下面的代码。当这步操作完成后（通常通过回调函数、Promise 或 async/await 来通知），再处理这步操作的结果。例如：

```javascript
database.query("SELECT * FROM posts", function(result) {
    console.log(result);
});
console.log("Done");
```

在这个例子中，数据库查询的操作是异步的。执行到数据库查询这步时，代码不会等待查询结果，而是直接执行后面的打印操作。当数据库查询完成后，会调用提供的回调函数来处理查询结果。

异步编程是 JavaScript 中非常重要的部分，因为它允许处理耗时的操作，比如网络请求、文件读写等，而不阻塞代码的执行。这是 JavaScript 能够在浏览器中提供流畅用户体验的关键原因之一。





## 2023年11月1日

## 近日见闻

1. AMH7.1发布，安全稳定纯净轻巧高效的主机面板。AMH 国内首款开源的主机面板，目前已持续不中断更新12年。 --AMH

2. 开源物联网平台 ThingsPanel 0.5.4 发布，新增看板，美观快速。--ThingsPanel

3. 微软推送 Windows 11 23H2 更新。考虑到微软计划在 2024 年发布下一代 Windows（可能是 Windows 12），因此 23H2 会成为 Windows 11 的最后一个重大更新。 --windows

4. 百度上线「文心一言」会员，开通可解锁文心大模型 4.0。 --百度


## springboot+vue3快速启动应用

为了方便测试运维开发流程中会产生的各种问题，有一个测试应用是至关重要的。所以花了半天时间写好了前后端，但目前不够完善，先把大致流程分享给大家。


仓库地址如下。记得点个小星星哦：

https://github.com/cilliandevops/aops

### 1.准备好开发环境

- node16+
- jdk1.8+
- idea、vscode
- mysql5.7/mysql8
- api测试工具

### 2. 前端开发

- 使用官方vite创建vue项目即可
- 安装elmentplus或其他ui框架
- 安装vue-router
- 安装axios

直接给出依赖：

```js
{
  "name": "aops-fe",
  "private": true,
  "version": "0.1.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "@element-plus/icons-vue": "^2.1.0",
    "axios": "^1.6.0",
    "element-plus": "^2.4.1",
    "vue": "^3.3.7",
    "vue-router": "^4.2.5"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^4.4.0",
    "vite": "^4.5.0"
  }
}
```

- 编写功能组件，比如说这里编写一个用户信息增删改查的user.vue组件，具体代码可以关注仓库。有问题可以私信留言。

### 3. 后端开发

- springboot2.7初始化项目
- mybaitplus安装
- 代码生成
- 创建一个实体类，定义用户信息字段
- 创建controller类，处理用户表增删改查操作
- 创建一个 UserService 接口和其实现类，定义用户表的增删改查操作：
- 运行


### 4.测试部署

- 测试前后端接口连通
- 前后端打包部署至服务器
- 详细情况后期分享



Vue3和Spring Boot的结合可以让我们更加高效地进行全栈开发。其中，Vue3的灵活性和Spring Boot的便利性使得开发过程更加流畅，而用户信息增删改查应用的开发则让我们更好地理解了全栈开发的全过程。若有疑问或需要其他技术栈的全栈开发教程，欢迎大家留言交流！

## AI绘图

今天试用了下AI绘图，不得不说，MJ真的很强大，这是生成的图，分享给大家看看！只是使用中文生成还不太准确，最好用英文调试！












## 2023年10月30日

## 近日见闻

1. KubeSphere社区已经在深圳、杭州、上海三个城市各组织了一场线下 Meetup。11月4日，云原生+AI Meetup成都站将正式开启！--kubesphere社区

2. 澎湃OS发布前，不少人都争论，它不是小米自研的系统，对此雷军还特意表示，确实不是。小米的澎湃OS由两部分组成：一部分是基于安卓系统进行深度进化的，这使得澎湃OS可以与安卓系统保持同步，并且能够使用安卓软件。另一部分则是小米自研发的Vela系统，主要用于实现小米产品之间的互联互通。这种系统架构使得澎湃OS能够兼顾兼容性和自主性，既满足了用户对丰富应用的需求，又能够提供更好的硬件软件一体化体验。--小米社区

3. 身体第一位，身体好才能工作好！

## mysql主从复制

MySQL主从复制是一种数据库复制技术，允许将一个MySQL数据库的数据和变更同步到一个或多个其他MySQL数据库，其中一个被称为"主数据库"，而其他的被称为"从数据库"。主从复制有多种应用场景，包括数据备份、负载均衡、故障恢复和分布式数据处理。

1. 主数据库：主数据库包含数据和执行写操作（INSERT、UPDATE、DELETE）的操作。这是数据库的源头，数据的变更都从这里开始。主数据库维护一个二进制日志（Binary Log），该日志记录了数据库的所有写操作。

2. 从数据库：从数据库是主数据库的副本，它包含与主数据库相同的数据。但是，从数据库只能执行读操作，不允许对数据进行写操作。从数据库维护一个复制事件队列，通过复制事件队列来接收主数据库的数据变更。

主从复制的工作原理如下：

1. 主数据库将所有的写操作（增加、修改、删除数据）记录到二进制日志（Binary Log）中。这个日志以二进制的方式记录，因此效率更高，并且可以容纳大量的写操作。

2. 从数据库连接到主数据库，并请求复制权限。主数据库会为从数据库创建一个用于复制的账户，授权它可以读取二进制日志。

3. 从数据库启动一个I/O线程，它的任务是连接到主数据库，获取二进制日志中的事件。主数据库会将新的事件追加到二进制日志中，并I/O线程会将这些事件传输给从数据库。

4. 从数据库接收到事件后，会将这些事件写入到复制事件队列中，这个队列存储了即将被应用到从数据库上的事件。

5. 从数据库启动一个SQL线程，它会从复制事件队列中读取事件，并在从数据库上执行这些事件，以确保从数据库的数据与主数据库同步。

6. 从数据库周期性地将执行的事件信息反馈给主数据库，主数据库会记录从数据库的同步状态，以确保数据一致性。

7. 如果从数据库中的某个表需要读取数据，它会从本地数据获取，因为数据是只读的，不需要请求主数据库。这降低了主数据库的读负载，实现了负载均衡。

主从复制的好处包括：

- 数据冗余：通过创建一个或多个从数据库，可以实现数据冗余，提高了数据的可用性和容错性。如果主数据库发生故障，从数据库仍然可以提供读服务。

- 负载均衡：读操作可以分布到从数据库上，从而减轻主数据库的负载，提高了性能。

- 数据备份：从数据库可以用于数据备份，而不会影响主数据库的性能。备份可以从从数据库进行，而不必干扰主数据库的正常运行。


MySQL主从复制是一种有用的数据库复制技术，但它也存在一些潜在的缺点和导致延时的点。

1. 数据复制延时：
   - 网络延迟：如果主数据库和从数据库之间的网络连接速度较慢，数据传输可能会导致较大的延迟。
   - 大量写操作：如果主数据库上的写操作非常频繁，从数据库可能需要一定时间来追赶主数据库的数据变更。
   - 大事务：如果主数据库上执行了大规模的事务，这些事务可能需要更长的时间来复制到从数据库上，导致延时。

2. 数据不一致：
   - 数据冲突：如果在主数据库和从数据库上同时对同一数据进行写操作，可能导致数据不一致。主从复制无法解决这种冲突，需要应用层或数据库管理员手动解决。
   - 误删数据：如果在主数据库上执行了删除操作，这个操作也会在从数据库上执行，导致数据被永久删除。

3. 单点故障：主从复制通常依赖于主数据库，如果主数据库发生故障，整个复制架构可能会受到影响。因此，需要采取适当的故障恢复和高可用性措施。

4. 配置和管理复杂性：维护主从复制系统需要一定的配置和管理工作，包括设置、监控、维护、备份和性能调优。如果不小心配置错误，可能会导致数据不一致或性能问题。

5. 安全性问题：从数据库需要连接到主数据库，因此需要配置适当的安全措施来防止未经授权的访问。

6. 版本兼容性：主数据库和从数据库之间的MySQL版本必须兼容，否则可能会出现复制问题。

7. 故障检测和恢复：如果从数据库发生故障，需要手动或自动进行恢复，以确保主从复制能够继续正常工作。

8. 增加复杂性：主从复制引入了额外的复杂性，需要额外的硬件和维护成本，包括存储和网络资源。




## 2023年10月26日

### 近日见闻

1. Protect AI一手打造了开源软件（OSS）漏洞赏金平台Huntr，如今，这家公司更进一步，按Apache 2.0许可条款开源其三款AI/ML安全工具。NB Defense、ModelScan、Rebuff。 --https://github.com/protectai/nbdefense

2. EA 悄悄地搞了个大事件，把《命令与征服》系列中的 2 个游戏的部分源码开源了！这两个游戏分别是：Tiberian Dawn（泰伯利亚的黎明） 和 Red Alert（红色警戒）。--https://github.com/electronicarts/CnC_Remastered_Collection

3. 10月26日11时14分，搭载神舟十七号载人飞船的长征二号F遥十七运载火箭在酒泉卫星发射中心点火发射，约10分钟后，神舟十七号载人飞船与火箭成功分离，进入预定轨道，航天员乘组状态良好，发射取得圆满成功。--新闻

### MyBatis-Plus代码生成器

MyBatis-Plus 官方文档：

https://baomidou.com/

- 前提条件： 准备测试数据库、创建一个springboot项目

- 在 pom.xml 中导入相关依赖
```js
<!--mybatis-plus-->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.4.3.4</version>
</dependency>
<!--mybatis-plus-generator 生成器-->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-generator</artifactId>
    <version>3.5.1</version>
</dependency>
```

- 编写一个mian方法，加上框架
```js
public static void main(String[] args) {
    //1、配置数据源
    FastAutoGenerator.create("url", "username", "password")
        //2、全局配置
        .globalConfig(...)
        //3、包配置
        .packageConfig(...)
        //4、策略配置
        .strategyConfig(...)
        //5、模板引擎配置
        .templateEngine(...)
        //6、执行
        .execute();
}
```
- 附：快速生成样例代码

```js

public static void main(String[] args) {
    //1、配置数据源
    FastAutoGenerator.create("jdbc:mysql://localhost:3306/mybatisplus", "root", "123456")
        //2、全局配置
        .globalConfig(builder -> {
            builder.author("cillian") // 设置作者名
                .outputDir(System.getProperty("user.dir") + "/src/main/java")   //设置输出路径：项目的 java 目录下
                .commentDate("yyyy-MM-dd hh:mm:ss")   //注释日期
                .dateType(DateType.ONLY_DATE)   //定义生成的实体类中日期的类型 TIME_PACK=LocalDateTime;ONLY_DATE=Date;
                .fileOverride()   //覆盖之前的文件
                .enableSwagger()   //开启 swagger 模式
                .disableOpenDir();   //禁止打开输出目录，默认打开
        })
        //3、包配置
        .packageConfig(builder -> {
            builder.parent("com") // 设置父包名
                .moduleName("mp")   //设置模块包名
                .entity("entity")   //pojo 实体类包名
                .service("service") //Service 包名
                .serviceImpl("serviceImpl") // ***ServiceImpl 包名
                .mapper("mapper")   //Mapper 包名
                .xml("mapper")  //Mapper XML 包名
                .controller("controller") //Controller 包名
                .other("utils") //自定义文件包名
                .pathInfo(Collections.singletonMap(OutputFile.mapperXml, System.getProperty("user.dir")+"/src/main/resources/mapper"))    //配置 mapper.xml 路径信息：项目的 resources 目录下
        })
        //4、策略配置
        .strategyConfig(builder -> {
            builder.addInclude("user", "student") // 设置需要生成的数据表名
                .addTablePrefix("t_", "c_") // 设置过滤表前缀

                //4.1、Mapper策略配置
                .mapperBuilder()
                .superClass(BaseMapper.class)   //设置父类
                .formatMapperFileName("%sMapper")   //格式化 mapper 文件名称
                .enableMapperAnnotation()       //开启 @Mapper 注解
                .formatXmlFileName("%sXml"); //格式化 Xml 文件名称

            	//4.2、service 策略配置
            	.serviceBuilder()
                .formatServiceFileName("%sService") //格式化 service 接口文件名称，%s进行匹配表名，如 UserService
                .formatServiceImplFileName("%sServiceImpl") //格式化 service 实现类文件名称，%s进行匹配表名，如 UserServiceImpl

                //4.3、实体类策略配置
                .entityBuilder()
                .enableLombok() //开启 Lombok
                .disableSerialVersionUID()  //不实现 Serializable 接口，不生产 SerialVersionUID
                .logicDeleteColumnName("deleted")   //逻辑删除字段名
                .naming(NamingStrategy.underline_to_camel)  //数据库表映射到实体的命名策略：下划线转驼峰命
                .columnNaming(NamingStrategy.underline_to_camel)    //数据库表字段映射到实体的命名策略：下划线转驼峰命
                .addTableFills(
                new Column("create_time", FieldFill.INSERT),
                new Column("modify_time", FieldFill.INSERT_UPDATE)
            )   //添加表字段填充，"create_time"字段自动填充为插入时间，"modify_time"字段自动填充为插入修改时间
                .enableTableFieldAnnotation()       // 开启生成实体时生成字段注解

                //4.4、Controller策略配置
                .controllerBuilder()
                .formatFileName("%sController") //格式化 Controller 类文件名称，%s进行匹配表名，如 UserController
                .enableRestStyle()  //开启生成 @RestController 控制器
        })
        //5、模板
        .templateEngine(new VelocityTemplateEngine())
        /*
                .templateEngine(new FreemarkerTemplateEngine())
                .templateEngine(new BeetlTemplateEngine())
                */
        //6、执行
        .execute();
}
```

报错：
```bash
[main] WARN com.baomidou.mybatisplus.generator.config.GlobalConfig - 全局覆盖已有文件的配置已失效，已迁移到策略配置中
Exception in thread "main" java.lang.NoClassDefFoundError: org/apache/velocity/context/Context
	at website.cillian.aops.CodeGenerator.main(CodeGenerator.java:43)
Caused by: java.lang.ClassNotFoundException: org.apache.velocity.context.Context
	at java.net.URLClassLoader.findClass(URLClassLoader.java:382)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:349)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	... 1 more
```

添加生成模版引擎即可

```js
<dependency>
  <groupId>org.apache.velocity</groupId>
  <artifactId>velocity-engine-core</artifactId>
  <version>2.3</version>
</dependency>
```



## 2023年10月25日

### 近日见闻

1. 语雀宕机超过7小时，影响用户正常使用，已经发公告解释了原因和赔偿方案，给与用户半年会员。 --语雀

2. GOPS 全球运维大会2023 · 上海站，10月26日-27日上海站即将正式举行 --GOPS社区

3. 青云科技近日发布 KubeSphere 企业版 3.5.0（以下简称 KSE v3.5.0），致力于为企业提供更优质、更高效的容器应用体验。 --Kubesphere

4. 文档网站上线，历史文章各位可查看docs.cillian.website --希里安

### java常用注解

当使用Spring Boot进行应用程序开发时，常常需要使用各种注解来简化配置、处理依赖注入以及定义特定行为。以下是更详细的介绍和示例，以帮助您更好地了解Spring Boot中一些常用的注解：

1. `@SpringBootApplication`:
   - 用途：这个注解是Spring Boot应用程序的主要入口点。它结合了`@Configuration`、`@EnableAutoConfiguration`和`@ComponentScan`，自动配置应用程序并扫描包中的组件。
   - 示例：
     ```java
     @SpringBootApplication
     public class MyApplication {
         public static void main(String[] args) {
             SpringApplication.run(MyApplication.class, args);
         }
     }
     ```

2. `@RestController`:
   - 用途：标识一个类为RESTful控制器，它用于处理HTTP请求并返回数据，通常以JSON格式。
   - 示例：
     ```java
     @RestController
     public class MyController {
         @GetMapping("/hello")
         public String hello() {
             return "Hello, World!";
         }
     }
     ```

3. `@RequestMapping`:
   - 用途：用于映射HTTP请求到处理方法，并可以指定请求路径和HTTP方法。
   - 示例：
     ```java
     @RestController
     @RequestMapping("/api")
     public class MyController {
         @GetMapping("/hello")
         public String hello() {
             return "Hello, World!";
         }
     }
     ```

4. `@Autowired`:
   - 用途：自动装配依赖对象，通常用于注入Spring Bean。它可以用在字段、构造函数、或setter方法上。
   - 示例：
     ```java
     @Service
     public class MyService {
         @Autowired
         private MyRepository repository;
     }
     ```

5. `@Service`, `@Repository`, `@Component`:
   - 用途：这些注解用于将类标识为Spring管理的组件。`@Service`通常用于业务逻辑层，`@Repository`用于数据访问层，而`@Component`是一个通用的组件标识。
   - 示例：
     ```java
     @Service
     public class MyService {
         // ...
     }

     @Repository
     public class MyRepository {
         // ...
     }
     ```

6. `@Configuration`:
   - 用途：标识一个类为Spring配置类，通常用于定义Bean和配置。这对于将第三方组件集成到应用程序中非常有用。
   - 示例：
     ```java
     @Configuration
     public class MyConfig {
         @Bean
         public DataSource dataSource() {
             // 配置数据源并返回
         }
     }
     ```

7. `@Value`:
   - 用途：通过该注解可以将外部属性值注入到Spring Bean中。
   - 示例：
     ```java
     @Component
     public class MyComponent {
         @Value("${my.property}")
         private String myProperty;
     }
     ```

8. `@EnableAutoConfiguration`:
   - 用途：开启Spring Boot的自动配置功能，根据应用程序的依赖自动配置应用程序。
   - 示例：通常由`@SpringBootApplication`自动包含。

9. `@Entity`:
   - 用途：用于JPA实体类的标识。它指示该类将映射到数据库表。
   - 示例：
     ```java
     @Entity
     public class User {
         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id;
         private String username;
         // ...
     }
     ```

这些注解代表了Spring Boot应用程序中的常见构建块，它们帮助简化配置、依赖注入和处理HTTP请求等任务。根据您的应用程序需求，还可以使用其他Spring Boot注解来实现更多特定功能。这些注解是Spring Boot框架的核心，使开发变得更加高效且易于维护。


## 2023年10月24日

### 近日见闻

1. 1024程序员节快乐！

2. NGINX 推出 Plus Release 30 (R30) 版本。NGINX Plus 基于 NGINX 开源版构建而成，是唯一一款将软件 Web 服务器、负载均衡器、反向代理、内容缓存和 API 网关集于一身的多合一产品。 --Nginx社区

3. OpenTiny Vue 3.11.0 发布：增加富文本、ColorPicker等4个新组件，迎来了贡献者大爆发！ --前端开源星球

4. 有读者朋友建议我分享运维工作经验或者日常问题解决经验，我尽快总结分享，欢迎关注文档网站：docs.cillian.website



### Java21创建一个Springboot应用


**步骤 1：设置开发环境**

首先，安装Java Development Kit（JDK），可以从Oracle或OpenJDK下载并安装。Java版本要兼容Spring Boot。比如springboot3最低要求java17。我们直接下载安装openjdk21，并设置好环境变量。

**步骤 2：创建Spring Boot项目**

使用Spring Initializer（https://start.spring.io/）或在IDE中创建新的Spring Boot项目。

1. 打开浏览器，访问Spring Initializer网站。
2. 在该网站上，选择项目的基本设置，包括项目名称、描述、包名、Java版本等，选择spring web依赖。
3. 点击"Generate"按钮生成项目。
4. 下载生成的项目文件，通常是一个zip压缩包。
5. 解压缩项目文件，并导入到您的IDE中。

**步骤 3：编写Spring Boot应用程序**

在项目中，可以开始编写Spring Boot应用程序代码。比如创建一个RESTful Web服务：

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
public class MySpringBootApplication {

    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}

@RestController
class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot!";
    }
}
```

这个示例创建了一个Spring Boot应用程序，其中包含一个HelloController，用于处理HTTP GET请求并返回"Hello, Spring Boot!"。

**步骤 4：运行应用程序**

在IDE中运行应用程序，或者使用以下命令行命令来运行：

```
./mvnw spring-boot:run
```

**步骤 5：测试应用程序**

也可以使用浏览器或工具如curl或Postman来测试应用程序。在浏览器中输入`http://localhost:8080/hello`，应该能够看到"Hello, Spring Boot!"的响应。

**步骤 6：打包应用程序**

使用以下命令将应用程序打包成可执行的JAR文件：

```
./mvnw clean package
```

打包后的JAR文件通常会位于`target`目录下。

**步骤 7：部署应用程序**

将打包好的JAR文件部署到目标服务器或云平台上。通常，可以使用`java -jar your-app.jar`来运行应用程序。

**步骤 8：配置应用程序**

Spring Boot允许您在`application.properties`或`application.yml`文件中配置应用程序属性，例如端口号、数据库连接等。以下是一个`application.properties`文件的示例：

```properties
# 应用程序端口号
server.port=8080

# 数据库连接配置
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=username
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

这只是一个简单的示例，Spring Boot支持更多功能和配置选项，具体取决于项目需求。可以根据需求进一步扩展和定制应用程序。






## 2023年10月20日

### 近日见闻

1. 微软最近宣布，Azure Database 将放弃对 MariaDB 的支持。在接下来的几个月里，用户将不能通过控制台或 CLI 创建新的 MariaDB 数据库，现有的实例计划在 2025 年到期。--https://www.infoq.com/news/2023/09/azure-database-mariadb/

2. 2023年10月16日，vivo在官方微博宣布，将于11月1日举办开发者大会，并将发布vivo自研AI大模型，引领手机智慧体验变革。--vivo社区

3. 国考报名四天人数超63万！单日将近20万！ --新闻

### 日常sidecar运用


在Kubernetes（通常简称为K8s）中，"Sidecar" 是指一种容器模式，其中一个容器（主容器）与一个或多个辅助容器（Sidecar容器）一起运行在同一个Pod中。这种模式允许在一个Pod中同时运行多个容器，每个容器可以独立执行不同的任务，但它们共享相同的网络和存储命名空间，可以相互通信和协同工作。

以下是一个示例，假设您正在运行一个Web应用程序，需要记录应用程序日志。您可以使用一个主容器来运行您的Web应用程序，同时使用一个Sidecar容器来记录应用程序的日志。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app-pod
spec:
  containers:
    - name: web-app
      image: my-web-app:1.0
      ports:
        - containerPort: 80
    - name: log-sidecar
      image: log-processor:1.0
```

在上面的示例中，我们定义了一个Pod，其中包含两个容器：`web-app` 和 `log-sidecar`。`web-app` 容器运行您的Web应用程序，而 `log-sidecar` 容器运行一个用于处理和记录日志的服务。这两个容器在同一个Pod中运行，它们可以共享相同的网络和存储，以便 `web-app` 可以将日志发送给 `log-sidecar` 进行处理，然后 `log-sidecar` 负责将日志保存到适当的位置。

这种模式的好处包括了解耦、易于管理和维护。您可以根据需要添加或删除Sidecar容器，而无需对主应用程序进行修改。


### 怎么维护sidecar

在Kubernetes中，维护Sidecar容器的数量可能会涉及到一些管理和运维任务，特别是在多个Sidecar容器之间需要协同工作，以确保应用程序的稳定性和性能。以下是关于维护Sidecar容器的一些建议：

1. **监控和日志记录**：确保在整个Pod中监控主容器和所有Sidecar容器的性能和日志记录。使用适当的监控和日志记录工具，以便及时检测问题并采取必要的纠正措施。

2. **版本管理**：Sidecar容器的镜像版本应该与主应用程序的镜像版本保持一致，以防止不兼容或冲突的问题。在部署新版本时，确保所有容器都更新为最新版本。

3. **资源管理**：管理Pod的资源请求和限制，以确保Pod中的所有容器都有足够的资源来运行。不同容器可能需要不同的资源配置，因此需要根据各容器的需求来调整。

4. **容器间通信**：确保Sidecar容器能够与主容器进行正确的通信，以便执行协同工作。这可能需要适当的网络策略和服务发现机制。

5. **容器健康检查**：配置适当的健康检查以确保主容器和Sidecar容器都正常运行。这有助于自动故障恢复和替代。

6. **自动扩展**：如果需要，使用Kubernetes的自动扩展功能来动态调整Pod的副本数量，以满足应用程序的需求。这可以确保Sidecar容器能够处理负载的增加。

7. **升级策略**：定义升级策略，以确保在进行主容器或Sidecar容器的更新时不会导致应用程序中断。可以使用滚动升级或蓝绿部署等策略来管理更新。

8. **文档和标准**：为团队创建清晰的文档和标准，以规范化Sidecar容器的使用和维护。这有助于确保一致性和可维护性。

9. **灾难恢复计划**：制定灾难恢复计划，以应对主容器或Sidecar容器中的故障。这可以包括备份和恢复策略。

10. **安全性**：确保所有容器都受到适当的安全措施的保护，以防止潜在的威胁。

维护多个Sidecar容器需要仔细的计划和管理，以确保整个应用程序在长期运行中保持稳定和高效。这涉及到监控、调整资源、升级管理、文档化和灾难恢复计划等多个方面。在实践中，根据具体应用的需求来制定和实施维护策略。



## 2023年10月20日

1. 安全内参10月18日消息，今年5月至9月期间，有官方背景的俄罗斯黑客组织“沙虫”（Sandworm）已经成功侵入11家乌克兰电信公司。 --安全内参

2. Tekton 是一个用于创建持续集成和持续交付（CI/CD）系统的 Kubernetes 原生开源框架。通过对底层实施细节的抽象，它还可以帮助你在多个云供应商或企业内部系统中进行端到端（构建、测试、部署）应用开发。 --Linux社区

3. 「RTE 2023 第九届实时互联网大会」定档 10.24-10.25 --RTE

### TS与JS

当比较TypeScript（TS）和JavaScript（JS）时，以下是详细的区别：

1. **类型系统**：
   - **JavaScript**：JavaScript是一种动态类型语言，这意味着变量的类型在运行时确定，你可以随时改变一个变量的类型。
   - **TypeScript**：TypeScript是一种静态类型语言，你需要在编码阶段为变量、函数参数和返回值等显式定义类型注解。类型注解可以帮助编译器检测潜在的类型错误，提高代码的可靠性和可维护性。

2. **编译**：
   - **JavaScript**：JavaScript代码可以直接在浏览器或Node.js中运行，无需编译过程。
   - **TypeScript**：TypeScript代码需要经过编译，编译器将TypeScript代码转换为JavaScript代码。这个过程会去除类型注解，并将TypeScript特有的语法转换为标准的JavaScript，以便在浏览器或Node.js中执行。

3. **语法**：
   - **JavaScript**：JavaScript的语法相对灵活，可以在不严格遵循规范的情况下编写代码。
   - **TypeScript**：TypeScript引入了一些新的语法，如类型注解、接口、枚举、泛型等，以增强代码的可读性和可维护性。这些语法在编译时进行类型检查，并提供更多的开发工具支持。

4. **工具支持**：
   - **JavaScript**：JavaScript的开发工具有很多，但它们主要专注于语法高亮和基本的错误检查。
   - **TypeScript**：TypeScript拥有更强大的开发工具支持，如自动完成、智能重构、类型检查、导航等，这些功能可以提高开发效率和代码质量。

5. **生态系统**：
   - **JavaScript**：JavaScript拥有巨大而成熟的生态系统，有大量的第三方库和框架可供选择，用于前端和后端开发，以及各种其他应用。
   - **TypeScript**：TypeScript可以无缝与JavaScript生态系统集成，同时还有一个类型声明文件（.d.ts文件）生态系统，用于描述第三方JavaScript库的类型信息。这使得使用TypeScript开发时能够享受类型安全，同时仍然能够利用广泛的JavaScript库。

TypeScript是JavaScript的一个超集，它添加了类型系统和其他功能，旨在提高代码的可维护性和可读性。选择使用哪种语言取决于项目需求、开发团队的偏好以及个人偏好。较大、复杂的项目通常更容易受益于TypeScript的类型检查和工具支持，而小型项目可能更适合使用JavaScript的灵活性。

---
## 2023年10月19日

1. 10 月 17 日，Node.js 21 正式发布，其取代了 Node.js 20 成为当前版本，而 Node.js 20 则被推广为长期支持版本（LTS）。 --NodeJS

2. 10月17日，拜登政府决定停止向中国输送高性能的人工智能芯片，其中包括GPU A100、H100、A800、H800、L40、L40S 以及 RTX4090。 --新闻

3. 11月4日，云原生+ AI Meetup成都站即将开启！--CNCF

4. 大厂离职就打低绩效，已成常规操作？--招聘社区


### 静态、动态路由的使用

当你构建一个Vue.js应用时，你需要考虑如何管理和配置路由，以便导航到不同的页面或视图。路由可以分为两种主要类型：静态路由和动态路由，下面我将进一步详细解释它们。

#### 静态路由（Static Routes）

1. **定义方式**：静态路由是在应用的路由配置中提前定义的路由规则。这些规则在应用启动时就被确定，通常在路由配置文件中硬编码。

2. **用途**：静态路由通常用于表示应用中的一些常规页面，如主页、关于页面、联系页面等。这些页面的路由规则在开发时就已经确定，不会发生变化。

3. **示例**：以下是一些静态路由的示例，它们都是在路由配置文件中提前定义的：

```javascript
const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About },
  { path: '/contact', component: Contact }
];
```

#### 动态路由（Dynamic Routes）

1. **定义方式**：动态路由是在应用运行时根据数据或其他条件来动态生成的路由规则。这种路由通常用于处理具有可变参数的页面。

2. **用途**：动态路由通常用于处理需要根据不同参数显示不同内容的页面，例如博客文章详情页面，每篇文章都有不同的标识，或用户个人资料页面，每个用户都有不同的标识。

3. **示例**：以下是一些动态路由的示例，它们包含了动态参数，参数的值是根据实际路由匹配而变化的：

```javascript
const routes = [
  { path: '/blog/:id', component: BlogPost },
  { path: '/profile/:username', component: UserProfile }
];
```

在动态路由中，`:id`和`:username`都是动态参数，它们的值会根据实际路由匹配而变化。你可以在组件中使用这些参数来获取相应的数据并呈现在页面上。

静态路由是在开发时定义的固定路由规则，而动态路由是在运行时根据数据或用户输入动态生成的路由规则。你可以根据应用的需求和路由配置来选择使用静态路由、动态路由或两者结合，以构建你的Vue.js应用。