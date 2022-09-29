# 如何理解 Private 和 Public 网络状态？

网络状态分为 private 和 public 两种情况。

如果是 private，意味着你可以主动发现并和 public 节点建立连接；但其它节点无法主动发现你。

如果是 public，意味着你可以主动发现并和 public 节点建立连接；其它节点也可以主动发现你并建立连接。

如果一个群组中有三个在线用户，分别是 private 的 A 和 C，public 的 B，那么 AB 能直连， BC 也能直连，而 AC 之间的消息可通过 B 来转发。

这有点像联机打游戏。链接双方有一个人端口打开，就可以建立链接和同步数据。就是说，一个网络里只要有一部分人能打开端口，整个网络就可以联通，其他人不是也没关系。

当然现在还比较简单，将来会用webrtc，穿越防火墙比现在容易。以及有一些大节点可以专门帮各种人转发（同时挖矿）。

当然，如果你连接节点越多同步就越快，运行的时间比较久就会逐渐找到更多节点。