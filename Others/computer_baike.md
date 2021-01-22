[TOC]


# 序列 （被排成一列的对象）
数学上，序列是被排成一列的对象（或事件）；这样每个元素不是在其他元素之前，就是在其他元素之后。这里，元素之间的顺序非常重要。

# 数据流
数据流（data stream）是一组有序，有起点和终点的字节的数据序列。包括输入流和输出流。
数据流最初是通信领域使用的概念，代表传输中所使用的信息的数字编码信号序列。这个概念最初在1998年由Henzinger在文献87中提出，他将数据流定义为“只能以事先规定好的顺序被读取一次的数据的一个序列”。

总结：流stream是序列，则只有一列，并有顺序

# 流数据
流数据是一组顺序、大量、快速、连续到达的数据序列,一般情况下,数据流可被视为一个随时间延续而无限增长的动态数据集合。应用于网络监控、传感器网络、航空航天、气象测控和金融服务等领域。

# 序列化
序列化 (Serialization)是将对象的状态信息转换为可以存储或传输的形式的过程。在序列化期间，对象将其当前状态写入到临时或持久性存储区。以后，可以通过从存储区中读取或反序列化对象的状态，重新创建该对象。
序列化使其他代码可以查看或修改，那些不序列化便无法访问的对象实例数据。确切地说，代码执行序列化需要特殊的权限：即指定了 SerializationFormatter 标志的 SecurityPermission。在默认策略下，通过 Internet 下载的代码或 Internet 代码不会授予该权限；只有本地计算机上的代码才被授予该权限。
通常，对象实例的所有字段都会被序列化，这意味着数据会被表示为实例的序列化数据。这样，能够解释该格式的代码有可能能够确定这些数据的值，而不依赖于该成员的可访问性。类似地，反序列化从序列化的表示形式中提取数据，并直接设置对象状态，这也与可访问性规则无关。
对于任何可能包含重要的安全性数据的对象，如果可能，应该使该对象不可序列化。如果它必须为可序列化的，请尝试生成特定字段来保存不可序列化的重要数据。如果无法实现这一点，则应注意该数据会被公开给任何拥有序列化权限的代码，并确保不让任何恶意代码获得该权限。

# 一体式电脑
一体式电脑是将主机部分、显示器部分、甚至键盘鼠标整合到一起的新形态电脑。这种产品的创新在于内部元件的高度集成。有些厂商称之为 All In One、AIO电脑或屏式电脑。

# ukey 
UKey是一种通过USB (通用串行总线接口)直接与计算机相连、具有密码验证功能、可靠高速的小型存储设备。ukey 是对现行的网络安全体系是一个极为有力的补充，通过中国信息安全测评认证中心认证的网络安全产品。基于可信计算机及智能卡技术把易用性，便携性和最高级别的安全性带给了使用Microsoft IE或Netscape Navigator进行Web访问，在线交易（购物，付款）,收发电子邮件，在线聊天交友及表单签名，文件数字签名等操作的用户，保证用户在ukey下的操作不可篡改，抵赖。ukey最大的特点就是安全性高，技术规范一致性强，操作系统兼容性好，携带使用灵活。

# perl6 
Perl 6拥有丰富的现代语言特征，作者计划用重新定义正规表达式和增加函数式编程语言的特征，使之成为可演化的语言。
尽管提供了同Perl 5的兼容模式，由于Perl 6语言语法同Perl 5不同，因此，可以把她看作一种新的计算机程序语言。
Perl 6拥有丰富的现代语言特征，作者计划用重新定义正规表达式和增加函数式编程语言的特征，使之成为可演化的语言。为保证Perl 6和Perl社区的持续稳定发展，Perl 6编译器需要使用Perl 6来重写，为保证Perl语言原有函式库的重用，编译器还计划提供同Perl 5语言的兼容模式。
由于Perl 6语言的语法特征和要求，Perl 6编译器实现非常复杂，同时，开源社区的资源相对贫乏。因此，Perl 6编译器的开发显得相当缓慢。
有可能改名位raku。

# 防御式编程
防御式编程是提高软件质量技术的有益辅助手段。防御式编程的主要思想是：子程序应该不因传入错误数据而被破坏，哪怕是由其他子程序产生的错误数据。这种思想是将可能出现的错误造成的影响控制在有限的范围内。

# 802.11ac 
IEEE 802.11ac是802.11家族的一项无线网上标准，由IEEE标准协会制定，透过5GHz频带提供高通量的无线局域网（WLAN），俗称5G WiFi （5th Generation of Wi-Fi）。理论上它能够提供最少1Gbps带宽进行多站式无线局域网通信，或是最少500Mbps的单一连线传输带宽。 2008年年底，IEEE 802标准组织成立新小组，目的是在于创建新标准来改善802.11-2007标准。包括创建提高无线传输的速度的标准，使无线网上的能够提供与有线网上相当的传输性能。
802.11ac是802.11n的继承者。它采用并扩展了源自802.11n的空中接口（air interface）概念，包括：更宽的RF带宽（提升至160MHz），更多的MIMO空间流（spatial streams）（增加到 8），下行多用户的 MIMO (最多至4个)，以及高密度的调变（modulation）（达到 256QAM）。
2013年推出的第一批802.11ac产品称为Wave 1，2016年推出的较新的高带宽产品称为Wave 2。

# wiki （多人协作的写作系统） 
Wiki是一种在网络上开放且可供多人协同创作的超文本系统，由沃德·坎宁安于1995年首先开发，这种超文本系统支持面向社群的协作式写作，同时也包括一组支持这种写作。沃德·坎宁安将wiki定义为“一种允许一群用户用简单的描述来创建和连接一组网页的社会计算系统”。 Wiki站点可以有多人（甚至任何访问者）维护，每个人都可以发表自己的意见，或者对共同的主题进行扩展与探讨。

不能误以为就是百科。

# busybox 
BusyBox 是一个集成了三百多个最常用Linux命令和工具的软件。BusyBox 包含了一些简单的工具，例如ls、cat和echo等等，还包含了一些更大、更复杂的工具，例grep、find、mount以及telnet。有些人将 BusyBox 称为 Linux 工具里的瑞士军刀。简单的说BusyBox就好像是个大工具箱，它集成压缩了 Linux 的许多工具和命令，也包含了 Android 系统的自带的shell。













