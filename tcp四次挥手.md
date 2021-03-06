# TCP四次挥手

### 目的

> 数据传输结束，释放TCP连接。
### 过程

>由于A和B都处于EATABLISHED状态，那A的应用进程会主动先向其TCP发出连接释放报文段，并停止再发送数据，主动关闭TCP连接。
>
>1. A把连接释放报文段段的终止控制为FIN置1，序号seq=u，A进入FIN-WAIT-1（终止等待1）状态；
>2. B收到连接释放报文段后立即发出确认，确认号ack=u+1，随机产生序号seq=v，B进入CLOSE-WAIT（等待关闭）状态，此时已经处于半关闭状态了：A——>B连接已释放，B——>A 还没释放；
>3. A收到B的报文之后进入FIN-WAIT-2（终止等待2）状态，等待B发出连接释放的报文段；
>4. 若B没有数据需要发送给A，那应用进程就会通知TCP释放连接。这时B也发出连接释放报文段，FIN=1，序号seq=w，重复上次的确认号ack=u+1，而后，B进入LAST-ACK（最后确认）状态；
>5. A收到之后，仍需发出确认报文。确认号ack=w+1，同时提供自己的序号seq=u+1，而后进入TIME-WAIT（时间等待）状态。当B收到此回复后，B进入CLOSED状态。但A还没进入CLOSED状态，也就是连接还未释放完毕。A需要经过2MSL（MSL：maximum segment lifetime，最长报文段寿命，建议的MSL=2min）时间后才进入CLOSED状态。
>
>补充：
>
>A在TIME-WAIT之后必须等待2MSL?
>
>1.保证A发送的最后一个ACK报文段可以达到B；
>
>2.防止已失效的连接请求报文段出现在在本连接中。（2MSL时间足以使本次连接内产生的报文段都消失）

![四次挥手](https://github.com/geyixin/Trivial-But-Important/blob/master/Image/%E5%9B%9B%E6%AC%A1%E6%8C%A5%E6%89%8B.jpg)
