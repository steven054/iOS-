###### 三十二、从IPv4到IPv6的迁移

基于IPv4的公共因特网如何迁移到IPv6呢？这是个非常现实的问题
虽然IPv6使能系统可做成向后兼容，即能接收、发送和路由IPv4数据报，但已部署的IPv4使能系统却不能处理IPv6数据报

**1、双协议栈**

引入IPv6使能结点的最直接方式是**双栈**方法，即使用该方法的`IPv6结点`还有完整的IPv4实现，即**IPv6/IPv4结点**，具有接收和发送IPv4和IPv6两种数据报的能力。
当与`IPv4结点`互操作时，`IPv6/IPv4结点`可使用IPv4数据报；当与`IPv6结点`互操作时，`IPv6/IPv4结点`又可使用IPv6数据报。

`IPv6/IPv4结点`必须有IPv6与IPv4两种地址。此外，它们还必须能确定另一个结点是否是IPv6使能的或仅IPv4使能的。

可以使用**DNS**来解决，若要解析的结点名字是IPv6使能的，则DNS会返回一个IPv6地址，否则返回一个IPv4地址。如果发出DNS请求的结点是仅IPv4使能的，则只返回一个IPv4地址。
两个IPv6使能的结点不应相互发送IPv4数据报，而如果发送方或接收方任意一个仅为IPv4使能的,则必须使用IPv4数据报。

**2、隧道**

**建隧道**是另一种双栈方法，该方法能解决上述问题。
假定两个IPv6结点要使用IPv6数据报进行交互，但是它们是经由中间IPv4路由器互联的。将两台IPv6路由器中间的IPv4路由器的集合成为一个隧道，如`B->C->D->E`。

**3、NAT-PT**

除了双栈和隧道方案外，还有一种**NAT-PT(Network Address Translator - Protocol Translator)附带协议转换器的网络地址转换器**