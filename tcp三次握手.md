# TCP三次握手

### 目的
+ 为了防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误（官方解释）。主要目的：防止server端一直等待，浪费资源。假设不采用“三次握手”，那么只要server发出确认，新的连接就建立了。由于现在client并没有发出建立连接的请求，因此不会理睬server的确认，也不会向server发送数据。但server却以为新的运输连接已经建立，并一直等待client发来数据。这样，server的很多资源就白白浪费掉了。
### 过程（A主动打开连接，B被动打开连接）
+ 1.客户端A将同步位SYN置为1，选择一个初始序号seq=x，客户端A进入SYN-SENT（同步已发送）状态，等待服务端B确认；

  2.服务端B收到数据包后，如同意建立连接，则将SYN和ACK都置为1，确认号ack=x+1，自己也选择一个初始序号seq=y，而后向A发送该确认报文，服务端B进入SYN-RCVD（同步收到）状态；

  3.客户端A收到确认后，要向B给出确认。确认报文段的ACK置1，确认号ack=y+1，自己序号seq =x+1，而后A进入ESTABLISHED（已建立连接）状态。B收到A的确认后，也进入ESTABLISHED状态。此时则完成三次握手，随后客户端A与服务端B之间可以开始传输数据。

+ 三次握手图：

+ [三次握手](https://github.com/geyixin/Trivial-But-Important/blob/master/Image/%E4%B8%89%E6%AC%A1%E6%8F%A1%E6%89%8B.jpg)
