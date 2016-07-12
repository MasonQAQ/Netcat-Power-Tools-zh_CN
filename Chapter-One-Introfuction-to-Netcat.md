
目录
====

[TOC]




#导读

   Netcat最早是在1996年发行，作为一个网络管理程序，目的是可以读取和写入在TCP/IP协议栈上传输的TCP/UDP数据。Netcat常常被称为“瑞士军刀(Swiss Army knife)”，这当然有一定的理由的。就像瑞士军刀的多用途一样，Netcat的功能是很有用的，作为一个独立运行的程序和后端工具得到了广泛的应用。Netcat的用途包含：端口扫描，文件传输，获取banner，端口监听和重定向，还有一个比较邪恶的作用——后门程序。

   关于Netcat的名字来源有些争议，但是其中一个最常见（比较让人信服的）的是Netcat是网络版的cat程序。Netcat从网络连接中读取信息，就像cat从文件中读写信息一样。更深层次的原因是，Netcat是特意要设计成像cat那样操作的。

   最初的程序是在unix上，尽管没有按照一个规则来定期维护，但是Netcat已经被改写成一系列版本，它已经被移植到了很多的操作系统上，最常见的还是Linux的各种发行版和windows。



NOTE



   为了学习本章，我们会在windows和Linux上使用Netcat。Windwos是本身是一类操作系统;UNIX和Linux发行版在本质上是一样的，归为一类。此外，Linux的各个发行版的差距是很小的。另外要知道，还有至少两个略微不同的差别：在Unix发行版上的Netcat和最新版的GNU Netcat。

好像这个note是废话。。



   在2006年的nmap黑客的邮件讨论组(Nmap-hackers mailing list)的调查中，在总体评分中，Netcat排名第4。实际上，在三次连续的调查(2000,2003,2006)中，尽管有大量的先进的强大的工具，Netcat仍然名列前茅，分别排名第2和第4和第4。在目前这个时代，当用户寻找最新的最强大的利器(edge tools),Netcat仍然深入人心(Netcat’s long reign continues)。



   本章的目的是为您提供关于Netcat的基本了解。为此(To that end),我们将开始进行安装和配置(Windows和UNIX/Linux),并跟进各个选项的注释和Netcat的基本操作的理解。在探讨Netcat的一些操作的时候，我们会介绍这本书的各章，涵盖更详细的操作。为此，把这个介绍性的章节作为出发点，开始你的旅程。enjoy！



#安装



   Netcat是一个小而简单的程序，怪不得(no wonder)安装那么简单(straightward),不管你使用的是什么操作系统。对于windows，Netcat已经有编译好了二进制形式的软件包，所以没有真正安装的必要(no true installation required)。就像前面的note，有两种常用的UNIX/Linux的安装方式( implementations)：原始的UNIX版本和GNU版本。几乎(Virtually)所有的UNIX/Linux自带了其对应的已经编译好的版本;然而，学习怎么安装还是有必要的。此外，如果想要达到你的特定要求，你可能需要重新编译netcat来实现。



##在Windows上安装



   windows上的安装真的是不能在简单了。只需要从  [download](http://www.vulnwatch.org/netcat/nc111nt.zip) 下（已失效）现在为http://joncraton.org/files/nc111nt.zip（from：http://www.securityfocus.com/tools/139   ）下载zip文件。解压到你想要的目录，就搞定啦。(具体看图1.1)。还有一些重要的文件需要查看一下：hobbit.txt是原始文档，readme.txt是版本1.10-1.11安全修订的注释，还有license.txt是指GPL许可(GNU General Public License).



NOTE



   netcat是一个命令行工具。双击nc.exe，只是简单的运行netcat，没有指定参数，然后会显示一个命令提示符(prompt)。你要在这里运行netcat，但是当实例完成以后，窗口就会马上关闭。嘛。就什么都没有看到。这没用(helpful)啊，你要看到反馈啊。一个简单的方式，直接从命令行启动。开始-运行-cmd.exe nc -h，你就会看到帮助界面进行进一步的引导。








我的杀毒软件(anti-virus)说Netcat是一个木马程序(trojan)！



   Netcat的强力(potent)通信能力不受限于网络管理员。渗透测试(Penetration testers)使用Netcat来测试目标系统的安全性(举个例子，Netcat被包括在Metasploit框架里)。恶意(Malicious)用户用Netcat(或者它的变种中的一个)作为获取远程访问系统的途径。在这种方面，可以理解为什么很多杀毒软件把Netcat标记(label)为"木马"或者"黑客工具(hacktool)".

   一些杀毒软件可能会试图阻止(prevent..from)你安装Netcat，或者甚至试图阻止你下载Netcat或是其他包含Netcat的程序。与几乎所有的工具，没有道德规范要限制它的使用仅用于合法的目的。你的想法就简单的决定了Netcat是否是由你下载并安装的(这样就不会是威胁)，或是暗中(surreotitiously)被恶意用户用于恶意(nefatious)用途安装的。

   你可以考虑配置你的杀毒软件，当它扫描或自动防御的时候，排除安装了Netcat的特定目录。当然啦，你需要了解与此相关的危险。



##在Linux上安装



   很多主流(mainstream)Linux发行版自带了已经编译和安装好的Netcat。其他的(非主流？)系统也至少有一个或者多个Netcat的版本作为预编译(pre-compiled)的软件包可供下载(available)。要确定(determine这个词用的好)Netcat的版本，只需要输入`nc -h`或者`netcat -h`，最初的UNIX版本会返回[v1.10]的一个版本行，而GNU版本会返回GNU Netcat 0.7.1,这是一份网络工具的重写版本。即使Netcat已经预装在你的系统上，你可能也不希望跳过这一节吧。许多在Linux发行版上，预装(pre-installed)、预编译(pre-compiled)或者软件包版本的Netcat，编译是没有包含所谓的GAPING_SECURITY_HOEL选项(这允许Netcat用-e参数来执行程序)。这些通常是从Netcat的源代码中'安全'的编译出来的。GNU版本的Netcat自动编译了启用-e选项，因此这个版本的安装无需额外的必要配置。尽管如此，最初的Netcat的所有其他功能都保持不变(remains intact).当然啦，能够执行程序使Netcat成为了一个强大的工具。在这本书中，很多示范(demonstrations)都很好的利用了-e选项，所以如果你想照着学习(follow along)，你可能要考虑重新编译Netcat。



TIP

   如果您已经安装了Netcat，但是不确定它是否编译了-e选项，直接(simplely)运行netcat -h显示帮助信息(help screen)。如果包含-e选项，那么Netcat就有。如果没有-e选项，那么你就需要重新编译Netcat，或者使用GNU版本。





###从软件包安装



   绝大多数发行版都把Netcat预编译成一个软件包(package)。有一些发行版可能有多于一个的版本，或者多个有个不同功能的安装程序(implementations)。记住(note),就像我们上面做的那样(as we did above),这些软件包也许没有执行程序的选项(一般都是因为一个什么原因)。比如，在Debian系统上，要从一个预编译的包安装Netcat，输入apt-get install netcat







TIP



   确保你的软件源是最新的，虽然说这个超出(beyond)了本书的范围(scope)。比如说，Debian和APT，软件源列在/etc/apt/sources.list文件中。此外，一定要保持你的列表里的软件也是更新了的，用apt-get update来更新。对于其他发行版，查看你的文档，然后个呢更新软件包列表。

(尼玛这个tip又来了 真哆嗦





   图1.2显示了简单的Netcat软件包安装的过程。注意，在这种情况下(notice that in this case),Netcat没有与其他软件包的依赖关系(dependecies),即使是在Debian的最小化安装(minimalist install)中.还要注意下包名netcat_1.10-32_i386.deb。这里的关键是1.10,这代表版本信息。这就证实(comfirms)了这个包实际上是从最初的UNIX Netcat编译的，而不是(as opposed to)GNU Netcat。还有就是(Furthermore),nc -h表明(reveals)这个包是预编译了万能(all-powerful) -e 选项。



NOTE

   要通过(via)软件包的方式安装到另类的(other flavors)Linux发行版上，请参考(consult)你的文档上安装预编译包的具体方法。



###从源码安装



   如果你想要编译源代码，你有两个版本可供选择，这两个大致(more or less)都是一样的，但是有一点重要的不同(exception)。第一个选择是原始的UNIX Netcat版本，在此处查看 www.vulnwatch.org/netcat 。第二个选择是GNU Netcat版本，在这里 netcat.sourceforge.net 。Netcat的这两个版本的关键区别在于，原始的Netcat需要手动(manual)配置来编译-e选项，而GNU Netcat自动就编译好了。手动配置也不复杂，但是如果你不习惯看源代码的话，就会非常棘手(tricky).

   如果你对于Linux还比较(relatively)小白(new)，从源码编译一个程序让你感觉害怕(daunting)，放心(rest easy).整个(entire)安装过程是简单容易的，只需要花费几分钟。为了达到安装的目的(sake)，所以我们安装没有手动配置-e选项的Netcat，我们会下载GNU版本的Netcat，并且配置和编译。



快速安装nc

```shell
wget http://sourceforge.net/projects/netcat/files/netcat/0.7.1/netcat-0.7.1.tar.gz
tar –xzf netcat-0.7.1.tar.gz
cd netcat-0.7.1
./configure
make
make install

```



原文wget给的链接已经失效了，不过我已修正为可用的地址了。



   第一步是下载源码。你可以选择简单的wget命令行工具(utility)，也可以用浏览器或者其他下载方式。









   接着，解压(un-tar)文件(archive)并放到一个新创建的Netcat目录。然后，配置Netcat。这个configure脚本会创建一个叫makefile的配置文件。







   make命令会从上步骤的Makefile里面建立二进制文件(Netcat的可执行文件)。使用make install命令会把Netcat安装到你的系统中。注意，运行make install需要root权限(privileges).对的!(That's it)你会发现，往往来说(more often than not)，这就是个比较普通的，在Linux上的源代码安装软件的过程。



NOTE



   如果你在安装过程中遇到(encounter)任何错误，这可能是发生在最后两步。如果是，可能是你没有安装正确的软件包来编译。最有可能是你使用了最小化安装。一定要检查软件包的来源(references)，以确保安装正确 (proper)。



   你安装的可执行二进制文件可能是叫nc或者是netcat，这取决于netcat的版本。为了一致性，在本章，我们将使用nc。





##确认安装成功



   无论(Regardless of)你用的是Windows版本的Netcat还是Linux版本的，需要确认Netcat是否正确安装，输入nc -h或者netcat -h来显示帮助信息。注意，有些选项是存在差异的。比如，在windows版本，-L选项表示开启持久(persistent)的监听(listening)模式(以后会讲)，而在Linux版本表示隧道模式(我的根本没有-L选项呢)。

   还有就是，Linux版本包括-V选项(注意是大写字母)，用来显示版本信息(这个也没有)。而Windows版本没有(lacks)这个选项。最后，Linux版本包括-x(hexdump incoming and outgoing traffic 显示进出流量的十六进制)选项，但Windows没有-x，取而代之的是-o。







windows版的版本v1.11 NT









linux(bt)版的版本是GNU netcat0.7.1,a rewrite of the networking tool

而我的是1.10-41



确实多了很多选项 先前没有的如下 还有一些kali上nc有的GNU版没有的 不列举了

-L,--tunnel=ADDRESS:PORT forward local port to remote address

-V,--version output version information and exit

-x,--hexdump hexdump incoming and outgoing traffic



然后我安装了GNU版的nc了。。

果然，如果只输入netcat或者nc，就进入命令行模式了。

显示cmd line:





#Netcat的命令选项

   在本节中，我们将讨论Netcat的两种不用的操作模式，以及(as well as)一些最常用的选项。



##操作模式



   Netcat有两种主要的操作模式，要么作为客户端，要么作为服务端。在帮助页面上，开始的两行(在版本信息下面)说明了对于每种模式的正确语法(syntax):

连接到某处: ```nc [-options] hostname port[s] [ports] ...```

监听入口流量(inbound): ```nc –l –p port [options] [hostname] [port] ```

   连接到某处表示客户端模式的语法。通常(Typically)，你在你的电脑上把nc作为客户端来获取(obtain)另一台电脑上的信息。监听入口流量表示服务端模式的语法。注意使用-l让nc处于监听模式。此时，你将nc设置为了监听传入的连接。Netcat并不在意你使用是什么模式，但是不管你在什么模式下，都会按照你的命令去执行。



##常用命令选项



   在本节中，我们将会讨论，你可能会看到的最常用的用于nc的选项。这些选项在windows和Linux下都是一样的，除了少数例外(会预先在文中说明)。你可以在这本书中单独的章节参考(refer)Netcat更高级的用法，来完成(accomplish)你的任务。请记住，-l选项将会确定Netcat的操作模式。nc -l这个命令会将nc置于服务端/监听模式，而nc这个命令会将自身置于客户端。(command nc –l will put Netcat into server or listening mode, and nc by itself will run Netcat in client mode.尼玛这句话，看了三遍才看懂)



   第一个可用的选项，-c，命令netcat在标准输入(stdin)的结尾处(EOF)关闭。此选项仅用于Linux的各种版本。

   接下来是，-d，使Netcat从控制界面分开，在后台运行。如果你不希望运行Netcat的时候有个控制台窗口，这就特别有用(特别是如果有人可能会窥屏)(哈哈哈，真周到)。注意这个选项仅适用于Windwos版本。

   Netcat最强大(powerful)的选项，毫无悬念(undoubtedly)，-e prog。这个选项，只能在服务端模式使用，可以指定一个程序，当有客户端来连接的时候，让Netcat来执行。注意以下命令：

`nc -l -p 12345 -e cmd.exe`(windows)

`nc -l -p 12345 -e /bin/bash`(Linux)



   这两个命令是在做同样的事情，但是是在不同的系统上。第一个命令是在本地的12345端口运行netcat作为服务端模式，并会在有客户端连接的时候执行cmd.exe(windows的shell)。第二条命令也是(precisely)一样的，不一样的就是在Linux上执行了一个bash shell。为了测试这个选项，我们来启动Netcat的服务端模式。



c:\netcat>nc -l -p 12345 -e cmd.exe





另开一个窗口，然后让netcat作为客户端。



c:\netcat>nc localhost 12345







当你敲下(hit) enter，你就会看到(are greeted with)Microsoft的banner信息和一个新的命令提示符。



Microsoft Windows XP [Version 5.1.2600]

(C) Copyright 1985-2001 Microsoft Corp.

c:\netcat>_







   这可能看起来有些震惊(underwhelming)，但是这就是毫无疑问(make no mistake about it)：你的确是通过Netcat来运行这个命令提示符。如果你是在一个网络里运行Netcat，而不是在同一台计算机上，你就直接有这台服务器的shell访问权限了。在命令提示符中输入exit，你会看到在第一个窗口的netcat的服务端关闭了。



   在Linux上开启服务端的netcat，在终端(box)输入nc -l -p 12345 -e /bin/bash.现在，我们在Windows上打开命令提示符，然后把nc运行为客户端模式。







   不像(unlike)先前连接到windows那样，Linux的bash shell不会返回字符到你的屏幕上。所以要用uname -a来显示系统信息。此时，这就证明(confirms)我们连接到了一台Linux机器(box),因为它接受了Linux的命令。另外(furthermore)，它返回了相关(relevant)系统信息:内核(kernel)名称和版本，处理器(processor)信息，等等(so forth)。



C:\netcat>nc -v 192.168.1.10 12345

192.168.1.10: inverse host lookup failed:h_errno 11004: NO_DATA

(UNKNOWN) [192.168.1.10] 12345(?) open

uname -a

Linux bt 2.6.21.5 #2 SMP Sat Aug 25 19:01:21 GMT 2007 i686 AMD Turion(tm) 64 Mobile Technology ML-34 AuthenticAMD GNU/Linux





warning

   这还不能足够的突出(stressed)出netcat的-e选项是多么强大。通过允许一个客户端来连入netcat，你可以给予他shell的访问权限。还有，这不需要用户认证或者是与此相关联的接入认证过程。重要的是，虽然你可能有正当的理由这样做，但无疑还有很多违法的用途。第五章：netcat的黑暗，将更详细的探讨这个选项。





`-g`和`-G`，可以让你配置netcat使用源站路由(source routing).使用源路由的方式，在一个网络中，发送方(the sender)指定路由让数据包通过。由于(since)大多数路由都阻止(block)源路由的数据包，所以这个选项多多少少有些过时(obsolete)。



`-h`,显示帮助信息，你懂的。



`-i`，设置延迟间隔(delay interval)(在发送数据和端口扫描之间)。在扫描端口时有速率限制非常有用。



`-l`，将netcat置于监听模式，或者像我们这章中说的，服务端模式。一般情况下(normally)，Netcat是一种一次性使用(single-use)的程序。或者说，一旦连接被关闭，Netcat也就关闭，不能再用了(no longer available)。然而，-L，在原来的连接关闭后，会用先前的命令打开nc：



`nc -l -p 12345 -e cmd.exe -L`



连接到这个实例(instance)的netcat会打开一个命令行到客户端。退出了命令行会关闭这个连接，但是-L会再次打开。



NOTE

   `-L`持久选项仅在Windows版本的netcat可用.(Linux版本的 `-L, --tunnel=ADDRESS:PORT  forward local port to remote address`)。不过，在Linux上用一些脚本程序就能克服(overcome)这个限制.为了解决某些问题，GNU版本的Netcat用-L来运行隧道链接(tunneling)。-L可以将本地端口转发(forward)到远程地址。





`-n`，使用只有数字(numeric-only)的ip地址，而且不做反向查找(reverse lookup)。如果你不加上`-n`，netcat就会做域名解析。但是(假设你加上了`-v` 用于显示更多的信息)，netcat会显示正向和反向的名称，还会用地址查找指定主机。我们来看下面这个例子。


```
C:\netcat>nc -v -n 64.233.169.103 80

(UNKNOWN) [64.233.169.103] 80 (?) open
```






加上了`-n`，netcat会接受一个数字的ip地址，并且不做反向查询(rDNS)。比较一下下面这个没有`-n`的。


```
C:\netcat>nc -v 64.233.169.103 80

yo-in-f103.google.com [64.233.169.103] 80 (http) open
```






没有`-n`，netcat就会执行反向查询(rDNS)，然后告诉我们，指定的ip属于google。当做一个正向或者反向的dns查询Netcat显示警告，这并非罕见。这些警告往往涉及(relate)不匹配的dns记录的可能。



`-o filename`，可以将netcat的流量的16进制dump存到一个文件里。



`-p port`，指定netcat监听本机某个端口(服务端):

`nc -l -p 12345`



本例中，netcat作为服务端运行，并且在12345端口监听传入连接。



在客户端模式下，Netcat还可以扫描端口。你可以指定多个端口(以逗号分割)，范围(全部也可以)，甚至是常见端口的名称。当在客户端模式下指定了端口，可以不用-p选项。只需要列出主机名，后面跟着端口号或者是端口范围。如果你是指定了一个范围的端口，Netcat会在范围里的高端口(top)的向低端口(bottom)扫描。因此，如果你让Netcat扫描20-30端口，它会从30开始扫描到20。



`-r`，随机扫描端口。如果你用netcat来扫描端口，-r会让netcat以相对随机的方式(manner)从标准的大到小来扫描。此外，-r也可以用在当服务端模式下时随机打开你本地的源端口。



`-s`，改变数据包的源地址，可以用于源地址的欺骗(spoofing)。这又是一个过时的命令，由于智能路由器会丢弃这些数据包，所以其有效性(usefulness)已经随着时间的推移(over time)而退化(degraded)。还有一个明显的限制就是，回复会发送到伪造(spoofed)的地址，而不是真实的地址。



`-T,--telnet`，设置netcat来回应telnet的协商(negotiation)。换句话说，Netcat可以设置为一个简单的Telnet服务器。注意下面的命令:

nc -l -p 12345 -e cmd.exe -T      这里有错哦 原来是-t -t是tcp



需要注意的是，上面的(previous)命令是运行在windows的netcat服务端。如果你是运行netcat在linux的服务器上，你需要把cmd.exe换成/bin/bash。

使用Netcat，telnet，或者其他的像PUTTY这类的客户端链接到服务器，通过telnet你就会拥有shell的权限。



warning

你要记住(Recall)，Netcat的通信没有加密。而且，telnet是明文协议(clear-text protocol).同样(likewise)，在这条链路上的所有通信都可以被监听。



`-u`，使用UDP代替(rather than)默认的TCP。因为UDP是不需要建立连接(connectionless)的协议，因此建议你使用超时(-w)和此选项搭配使用。



`-v`，和很多常见的命令行工具一样，调节唠叨(verbosity)程度，或者说是显示给用户的信息量。没有这个选项，netcat一样可以完美运行，但是netcat将会静默运行，并且只有当发生了错误时，才会显示信息。同样，和其他大多数程序都一样，你可以使用多个v来增加显示信息的等级(`-v` `-v`或者`-vv`都可以)。



TIP

强烈建议(highly recommended)每次用netcat的时候都加上`-v`，以便于直观的看到它正在做的事。很多用户还可以结合`-v`和`-w`一起使用。



`-V`，在GNU版本下，显示版本信息，然后退出。



`-w secs`，设置网络闲置(network inactivity,或者idle)的超时。用于本应断开连接，但你的服务器没有自动断开，还可以加快你的请求速度。一般时间为3秒。

`-z`，不显示输入/输出，用于端口扫描。当使用-z时，Netcat不会在TCP连接中发送数据，而是在UDP连接中发送有限的数据。(ps:嘛。。。我也不知道这什么意思。。。所以要慢慢看咯)



TIP

Netcat的选项(switches)可以单独(individually)使用，也可以连用。比如说，你要启动Netcat的服务端模式，在12345端口监听，并且要显示详细信息(verbose)。这样的命令是`nc -v -l -p 12345`。然而，你还可以把多个(multiple)选项放在一起，就像这样`nc -vlp 12345`。(ps:其实Linux本身也支持的。。。



##重定向工具



最后，还有一些基本的UNIX重定向与netcat兼容。

其中最有帮助的是>,>>,<和管道(|).



   单"大于(greater than)"重定向符号会直接输出:

nc -l -p 12345 > dumpfile

   这个命令会将所有收到的信息重定向(redirect...into...)到一个文件。收到的信息可能是对方输入的文字，或者甚至是发送一个文件。换句话说，不管是向服务端发送了什么东西，都会被重定向到dumpfile这个文件里。





   双"大于"重定向符号会将重定向输出，但是是追加(append rather than replace)到文件：

nc -l -p 12345 >> dumpfile



warning

单">" 重定向是要重定向输出到一个指定(specified)位置或者文件。但是要记住(keep in mind)，如果你使用的是相同的文件名，单">"重定向符号会覆盖(overwrite)原来的文件。如果你想要保留你的源文件，更安全的选择是使用双">"重定向来追加内容。如果指定文件不存在，双">"重定向也会自己创建一个。



"小于(less than)"重定向会冲将输入重定向:

nc -l -p 12345 < dumpfile



   当客户端连接到这台服务器，Netcat会发送dumpfile给客户端。或者说是，Netcat的客户端会从服务器上拉取(pull，ps:或者说是下载)文件。



   还有一个有用的重定向工具，管道(|),可以让一个命令的输出，作为第二个命令的输入(等等)。这些过程共同构成(constitute)了"管道行(pipeline)"。一些常用命令也可以和Netcat一起协作(in concert with)：cat(发送文件)，echo，tar(压缩并发送一个目录)。你甚至可以将Netcat运行两次，以建立一个中继(relay)。这些都可以。



#基本运用

在本章的剩余部分，我们将探讨一些基本的运用。



##简易的聊天界面



我们在一开始(at the outset)就说Netcat是一个网络工具，被用于在网络中读取数据和写入。也许，最简单的办法来理解它是如何工作的，就是简单地建立一个服务器和客户端。你可以把这两个设置在同一台计算机上，也可以使用两台计算机。为了本次演示(demonstration)，我们在一台计算机上设置服务端和客户端。

  先打开一个终端窗口，启动服务端:
```
nc -l -p 12345
```
  在第二个终端，连接到服务端:
```
nc localhost 12345
```
   结果就是这样一个非常基础的聊天界面。在一端输入文字，敲下enter，文字会被发送另一端。需要注意的是，没有任何标志来表明(indicate)文本的来源，只会有输出显示。



Figure 1.12 Sending Data Across a Connection









##端口扫描



虽然Netcat不一定是端口扫描的最佳选择(Nmap是受到广泛认可的最佳工具(the cream of the crop))，但是是有做一些基础(rudimentary)扫描的能力。就像Backtrak的开发人员Mati Aharoni曾经说的,"这不是它所擅长的方面，但是如果我只能用一个工具，我会带上Netcat(It’s not always

the best tool for the job, but if I was stranded on an island, I’d take Netcat with me)."我猜，很多人如果只能选一个工具，他们也会选择Netcat。



   端口扫描用在客户端模式。语法如下:
```
nc -[options] hostname [ports]
```


-w(网络超时)和-z，是用于端口扫描时最常用的选项，这两个都可能帮助加快你的扫描。其他的，还有，-i(设置间隔时间)，-n(禁用DNS查找)，-r(扫描随机端口)。参见图1.13的例子。



TIP

端口扫描的时候，记得加上-v(详细)选项，或者是将输出重定向到一个文件。如果你不这样，Netcat也会正常扫描，但是不会给你任何显示。一般情况，常常加上-v是很好的选择。



当你列端口的时候，你可以加上一些选项。你可以列出一个单独的端口数字，或者一系列由逗号分割的端口，或者是一个范围(包含)。你甚至可以列出端口对应的服务名称。以下都可以:


```
nc –v 192.168.1.4 21, 80, 443

nc –v 192.168.1.4 1-200

nc –v 192.168.1.4 http
```


ps:
```
root@kali:~# nc -v 192.168.1.7 80

192.168.1.7 80 (http) open

^CExiting.

root@kali:~# nc -v 192.168.1.7 ssh

192.168.1.7 22 (ssh) open

SSH-2.0-OpenSSH_6.7p1 Raspbian-5

^CExiting.
```




   其中的常用端口，Netcat会告诉你那个端口和与其对应服务名称。在Windows中，常用的服务位于/WINDOWS/system32/drivers/etc/services。在Linux中，是在/etc/services文件。这些文件可以用于参考服务名称，以此来代替端口号。



图1.13
```
C:\netcat>nc -v -n -r -w3 -z 192.168.1.4 21-25

(UNKNOWN) [192.168.1.4] 25 (?): TIMEOUT

(UNKNOWN) [192.168.1.4] 24 (?): TIMEOUT

(UNKNOWN) [192.168.1.4] 22 (?): TIMEOUT

(UNKNOWN) [192.168.1.4] 21 (?)open

(UNKNOWN) [192.168.1.4] 23 (?): TIMEOUT
```






在图1.13,Netcat运行在客户端模式在，并且含有以下选项:

显示详细信息，无DNS查询，随机端口顺序扫描，网络闲置超时3秒，关闭输入\输出。主机是192.168.1.4,端口扫描是21-25.Netcat返回了的信息是21端口开启，这很可能是用于FTP。有关端口扫描和Netcat的更多信息，请参见第10章，用Netcat来审计(audit)。



NOTE

你也可以使用-u来扫描UDP端口，但是要知道(be aware)，即使端口开放，也可能"不会回复"。当然，这是有可能的，但并非大多数情况(circumstances)。



##传输文件



Netcat的一个常见的用途就是传输文件。Netcat有上传和下载(pull and push)的功能。注意下面的例子：
```
nc -l -p 12345 < textfile
```


此时，Netcat开始在本地端口12345运行在服务端，并且主动提供了textfile文件。一旦有客户端连接到这台服务器，就会开始从服务器上拉取textfile文件并接收：
```
nc 192.168.1.4 12345 > textfile
```




Notes from the Underground ...

使用Netcat下载文件

   你可能会带着一个很充分的理由来怀疑，为什么要使用Netcat来传输文件，而不是使用更常见的文件传输协议(FTP,File Transfer Protocol).其实，在很多情况下，FTP可能是比较好的选择。但是，考虑到潜在威胁的情况，就是你有shell访问权限的目标计算机是在防火墙内。你要传输一些文件到目标，但是防火墙会阻止入站(inbound)流量。

   在这种情况下，你可以在本地运行Netcat的服务端模式，提供要传输的文件。然后，在目标计算机上运行Netcat的客户端。在多数情况下，防火墙会允许常见的出口(outbound)流量，所以你还可以在常用端口隐藏你的文件传输，比如80(HTTP).要获取更多的信息，请参见第5章，Netcat的黑暗，和第6章，用Netcat传输文件。



Netcat也能被用于发送(push)文件。如果你正在目的地(就是你想要收到文件的地方)运行Netcat，把Netcat置于服务器模式:

nc -l -p 12345 > textfile     >表示收

在源文件的计算机上，通过Netcat的客户端模式发送文件:

nc 192.168.1.4 12345 < textfile     <表示发



   然而，所有使用了Netcat的连接都不加密，包括文件传输咯。如果你在意用netcat传输的数据的隐私，可以考虑使用Cryptcat，Netcat的一个使用集成加密隧道的版本。Cryptcat和Netcat一样，使用相同的命令行语法，但是会使用两鱼加密法(twofish encryption，参考看雪一贴和维基百科)。还可以考虑在SSH(Secure Shell)连接内使用Netcat,这也是一种加密Netcat通信流量的方法。本小节意在介绍用Netcat传输文件的很基础的只是。要了解细节性的信息，尤其是参考加密和解密文件传输，参见第6章，用Netcat传输文件。



##获取banner



抓取Banner属于一种穷举(enumeration)技术，目的是确定某个服务或应用程序的品牌(brand?)，版本，操作系统，或其他相关信息。如果你正在寻找某个版本的设备是否存在漏洞，这些信息就非常重要。

   抓取Banner的命令语法???The syntax of a banner grab is not unlike the standard Netcat command line.

   把Netcat运行在客户端模式，列出相应的(appropriate)主机名,最后列出相应服务的端口号。在某些情况，你可能没有输入信息(见图1.14)。在其他情况，你必须输入一个基于特定协议的有效命令。(见图1.15)



图1.14 SSH Banner Grabbing with Netcat
```
C:\netcat>nc -v 192.168.1.5 22

RAVENCLAW [192.168.1.5] 22 (?) open

SSH-2.0-OpenSSH_3.8.1p1

_
```








ps:
```
root@kali:~# nc -v 192.168.1.7 ssh

192.168.1.7 22 (ssh) open

SSH-2.0-OpenSSH_6.7p1 Raspbian-5
```




在图1.14,Netcat给我们两条信息：ip的主机名，运行在目标上的ssh服务的版本信息。



图1.15 HTTP Banner Grabing With Netcat
```
C:\netcat>nc -v 192.168.1.5 80

RAVENCLAW [192.168.1.5] 80 (http) open

GET / HTTP/1.1



HTTP/1.1 400 Bad Request

Date: Mon, 17 Mar 2008 00:59:36 GMT

Server: Apache/2.2.8 (Win32)

Content-Length:226

Connection:close

Content-Type: text/html; charset=iso-8859-1



....接着是网页内容....
```






   在图1.15,我们将Netcat置于客户端模式。我们的目标ip运行着一个Web服务。通过发出(issue)GET请求(先不论这个Bad Request的事实)，返回来的信息告诉我们目标的Web服务器软件和版本号。这还告诉我们Apache的这个版本可以运行在Windwos中。

更多详细的信息，请参考第4章，用Netcat抓取Banner。







##端口和流量的重定向



Netcat可以被用于重定向端口和流量，这是一个有点阴暗(??darker shade)的操作。如果你要隐藏一次攻击的来源，这就很有用。我们的思路是，通过一个中间人(middle man)来运行，使得攻击看起来是从那个中间人发起的，而非真实的来源。下面的例子就很简单，但是会用到多个重定向。这个例子也需要你"获取(???own)"到中间人的权限，并且转发。这样的流量重定向被称为中继(relay).

在源计算机:

nc <hostname of relay> 12345         windows和*nix都能测试成功

在中继:

nc -l -p 12345|nc <hostname of target> 54321



   此简易方案(scenario)中，从源计算机(客户端模式)输入的会被发送到中继(服务端)。输出通过管道，作为第二个Netcat(客户端)的输入，最终(ultimately)从这里连接到目标计算机。第二点，Netcat的最初来源端口是12345,但是(yet)看起来攻击的来源端口是54321.这是port redirection(端口重定向)的一个简单例子。这种技术还可以用于隐藏Netcat在常用端口上的端口，以免被防火墙阻止。

   对于中继，有一个明显的限制。连接管道的数据(The piped data)是一个单向(one-way)连接。因此，源计算机不能接收到目标的响应。这个的解决方案是，在目标到源计算机之间，建立第二个中继(最好是通过另外一个中间人!)。

   要了解更多有关流量重定向的信息，请参考第5章，Netcat的黑暗，以及第7章，控制Netcat的流量。



##其他用法



本节涵盖了Netcat的基本操作，唯一限制Netcat的操作是你的想象力。还有的潜力，或者说更高级的用法包含:

■漏洞扫描(见第2章，Netcat和网络的渗透测试，和第3章，Netcat和应用的渗透测试)

■通用网络的排错(troubleshooting)(见第8章，用Netcat来排错)

■审计网络和设备(见第9章，用Netcat来审计)

■备份文件，目录，甚至是驱动器

本书的其余部分就特地(dedicated to)介绍这些，以及其他的什么用途。





#总结

   Netcat是一个网络程序，被用于读取，从使用IP协议栈的TCP和UDP连接中的数据。简单的说(more simply),Netcat是UNIX系统中的cat程序的网络版本。cat读写文件，Netcat读写网络连接。在过去十年中，尽管有更先进的工具被引入，Netcat因其简单而强大的功能，受到广泛用户喜爱。

   简单却强大和本章的主题联系(ties)在一起。如你所见，Netcat的安装，无论是Windows，还是Linux(通过软件包或源码)，都很简单(straightforward).只有少数几个(a handful of)常用的选项，使得学习命令行几乎(practically)不费吹灰之力(effortless)。然而，无故障(trouble-free)的安装和简单的命令行操作掩盖(belie)了事实，即Netcat确实是一个潜在的，功能强大的程序。

   Netcat的简易(simplicity)可能会让一些人小看(overlook)它。人们说，他们"低估(underestimated)"了Netcat的用处。其他人说他们在几年后"重新发现(rediscovering)"Netcat的用处了。不管是什么原因，回答好像总是...用Netcat吧！许多用户甚至推荐用Netcat来代替Telnet。Netcat是很有用的，所以在大多数用户的工具包中都占有一席之地。无论是为网络排除故障的管理员，评估(access)客户安全的渗透测试人员，或者只是一个想要学一些新东西的用户，Netcat都能帮到你。

   几年前，Mati Aharoni，BackTrack渗透测试CD的一位核心开发者，以及www.offensive-security.com的一位创始人(悄悄ps:Metasploit的作者)曾写过一篇短篇的安全论文，来示范(demonstrated)一个完整的hack过程，从开始到结束。开始是一个端口扫描，接着抓取Banner信息，扫描应用程序的漏洞，放置后门，最后把一个文件传送到这台被占有的电脑。文件的内容只是一条简短的信息"你已经被黑了(You have been hacked!)"。如果你曾做到这步，你就知道，完成这次hack，从头到尾，只用了一个工具，Netcat。



#FAQ 常见问答

Q：我还没开始下载Netcat呢，我的杀毒软件发现Netcat是一个木马！我该怎么办？

A：如果你从没下载安装过，你可能摊上事啦！除了Netcat的普通版(the vanilla version)，还有其他编译的版本会自动设置他们的特定端口(ncx.exe运行在80端口,而ncx99.exe运行在99端口)。



Q：我的杀毒软件不让我 下载/安装/使用 Netcat。这是为啥？

A：至少有两个大型的防病毒厂商(也许更多)把Netcat标志为一个问题。在一些测试案例中，其中之一是从实质上阻止下载，因为Netcat被包含在一个更大的安装包内。第二步，隔离(quarantine)掉Netcat正在运行的"自我保护"功能。这里有几种方案，通常这会涉及到修改"默认"参数( they typically involve modifying “default” parameters)。首先，你可以禁用实时保护(live protection)，至少在你下载Netcat的这短暂时间内。其次，你可以为Netcat创建一个特殊的目录(甚至连同其他类似的可能会被杀掉的工具一起)，并设置你的实时保护/自动防御选项，忽略这个目录。最后，你可以从你的正常(narmal)扫描，或是日常(scheduled)扫描中，排除(exclude)此目录。



Q：Netcat已经安装在我的系统中了。为啥我要重新安装？

A：Netcat在Linux发行版的很多预装的包都是"安全"编译，没有GAPING_SECURITY_HOLE选项。如果没有这个功能，Netcat就不能执行程序。因为Netcat的强大就在于这个选项，所以如果你需要这个功能，你应该重新编译和安装。



Q：我怎么知道Netcat是编译了-e选项呢？

A：在Windows上，Netcat已经编译的此选项，不需要更多的操作了。在Linux上，只需要输入nc -h显示帮助信息。GNU Netcat(版本0.7.1)是已经编译了此选项，所以，也不需要更多的操作。原始UNIX版本的Netcat(通常版本是1.10)编译了此选项，帮助信息会显示(ps:我原来的nc就有-e的)。在Mac上，Netcat默认没有编译这个选项。



Q：我怎么知道Netcat是在客户端模式还是在服务端模式下运行？

A：-l意味着(denote)监听(listening)，或者称为服务端模式。没有-l就表明是客户端模式咯。



Q：我断开连接的时候，Netcat也就关闭了服务端。但是我希望连接是持久的。这能行吗？

A：当然。在Windows，用-L选项，当Netcat关闭的时候，会用相同的命令重新打开它。这种特殊的选项在Linux不可用，但是你可以写一个简单的脚本来弥补。



Q：如果能做[über-leet的功能]，Netcat还可以变的更吊(cooler)。我该怎么做呢？

A：Netcat是开源的。这意味着你可以下载源码，修改以满足你的需求(to your delight)，然后编译你的über-leet功能。



Q：我在哪能找到有关Netcat的更多信息咧？

A：首先，请参考本书的剩余章节。本丛书作者(the contributing authors)是知识渊博，在各自领域的专家。其次，Google it。在互联网上，有大量的(a wide range of)有关Netcat的文档和教程(tutorials)。第三，找到一个有关的论坛，贴出问题。如果你知道怎么样问问题(如何问好一个问题)，那里会有很多人愿意帮助你。



