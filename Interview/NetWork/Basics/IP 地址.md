IP地址（Internet Protocol Address）是计算机网络中用于标识和定位设备的**数字标签**。它是分配给**网络中**每个参与通信的设备的**唯一地址**。IP地址分为IPv4和IPv6两个版本。

IP地址由[[IP地址转二进制|四段组成]]，每个字段是一个字节，即**4**个字节、每个字节有**8**位，最大值是**255**( $2^8$ 
=256：0~255)。

IP地址分为两个部分：网络标识和主机标识。*网络标识指示设备所在的网络*，而主机标识用于标识该网络中的特定设备。如果两个IP地址的网络部分不同，它们就属于不同的网络，通信需要通过路由器或网关进行。 ^DifferentNetworks

IP地址的分配和管理是由互联网号码分配机构（IANA）和各个地区的互联网注册管理机构（RIR）负责的。
## 五个类别
IP地址最初分为五个主要类别，即A、B、C、D和E类。这些类别基于IP地址的范围和用途。目前，主要使用的是A、B、C类地址，而D类用于多播，E类用于实验和研究。
### A类地址：
- 范围：1.0.0.0 到 126.255.255.255
- 用途：A类地址用于大型网络，支持约16百万台主机。
### B类地址：
- 范围：128.0.0.0 到 191.255.255.255
- 用途：B类地址用于中等规模的网络，支持约6万台主机。
### C类地址：
- 范围：192.0.0.0 到 223.255.255.255
- 用途：C类地址用于小型网络，支持约254台主机。
### D类地址：
- 范围：224.0.0.0 到 239.255.255.255
- 用途：D类地址用于多播（Multicast）通信，支持多个主机同时接收相同的数据。
### E类地址：
- 范围：240.0.0.0 到 255.255.255.255
- 用途：E类地址保留用于实验和研究。
### 预留地址
在IPv4地址协议中预留了3个IP地址段，作为私有地址，供组织机构内部使用。这三个地址段分别位于A、B、C三类地址内：
- A类地址内的：10.0.0.0–10.255.255.255
- B类地址内的：172.16.0.0–172.31.255.255
- C类地址内的：192.168.0.0–192.168.255.255
## 子网划分：
子网划分是将一个大的IP地址空间分割成多个小的子网，以提高网络的管理和效率。子网划分通常涉及到使用子网掩码，其中1表示网络标识，0表示主机标识，*用于标识IP地址中哪些位是网络地址，哪些位是主机地址*。子网掩码中连续的1的部分称为网络前缀。

例如，假设一个IP地址为192.0.2.15，*11000000.00000000.00000010.00001111*
子网掩码为255.255.255.0，*11111111.11111111.11111111.00000000*
那么前24位（即192.0.2）*（11000000.00000000.00000010）* 就是网络地址和子网地址，
后8位（即15）*（00001111）* 就是主机地址。

子网划分就是在主机地址中再划分出一部分作为子网地址，这样，IP地址就被划分为网络地址、子网地址和主机地址三部分。这种做法将一个大型网络划分为多个逻辑上的小型网络（即子网），每个子网内部可以进行独立的地址管理和流量控制，从而提高网络的可管理性和效率。
