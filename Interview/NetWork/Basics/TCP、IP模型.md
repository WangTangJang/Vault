TCP/IP 模型是一种计算机网络体系结构，是**实际互联网通信**所采用的模型。它是一个四层次的**协议栈**，包含链路层、网络层、传输层和应用层。下面详细介绍 TCP/IP 模型的各层：
### 1. 链路层（Link Layer）：
- **功能：** 链路层主要负责通过物理介质（如以太网、Wi-Fi等）传输数据帧。它定义了数据的格式、物理寻址（MAC 地址）以及如何访问物理介质。
- **协议和设备：** 典型的协议包括以太网、Wi-Fi、PPP（Point-to-Point Protocol）等。设备包括网卡、交换机等。
### 2. 网络层（Internet Layer）：
- **功能：** 网络层主要处理数据包的寻址和路由。它使用 IP 协议定义了数据包的格式，以及如何在网络中找到目标主机。
- **协议：** 典型的协议包括 IP（Internet Protocol）和 ICMP（Internet Control Message Protocol）。
### 3. 传输层（Transport Layer）：
- **功能：** 传输层提供端到端的通信服务。它负责数据的分段、传输控制和差错恢复。
- **协议：** TCP（Transmission Control Protocol）提供可靠的、面向连接的通信，而 UDP（User Datagram Protocol）提供无连接、不可靠的通信。
### 4. 应用层（Application Layer）：
- **功能：** 应用层提供网络服务给用户和应用程序。它包括了各种高层次的协议，如 HTTP、FTP、SMTP 等。
- **协议：** 典型的应用层协议有 HTTP（HyperText Transfer Protocol）、FTP（File Transfer Protocol）、SMTP（Simple Mail Transfer Protocol）、DNS（Domain Name System）等。
## TCP/IP 模型的特点：
- **简化结构：** 相较于 OSI 模型，TCP/IP 模型将物理层和数据链路层合并成链路层，更贴合互联网实际结构。
- **实际应用：** TCP/IP 模型是互联网的基础，**几乎所有**的互联网通信都基于 TCP/IP 协议栈。
- **开放标准：** TCP/IP 协议是**开放**标准，便于扩展和适应不同的网络需求。
- **灵活性：** TCP/IP 模型的每一层都是独立的，可以根据需要使用不同的协议。
