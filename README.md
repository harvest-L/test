# 小程序中首页应用的检测

1. 图片大小检测

  标准：小于70kb

  原因：图片过大会导致网络请求耗时增加，使用户等待交互的时间过长，应尽量控制图片大小，建议进行压缩或合理剪裁

  级别： p1

  实现手段？


2. 页面请求域名收敛检测检测

  标准：前6个请求的域名总数占比超过90%
  
  原因：页面多个请求的域名建议尽量收敛在一起，如果域名太过分散，DNS和链接复用率低，影响资源的加载速度，同时也需要考虑同域资源是否有并行加载的能力
  
  级别： p2

  实现手段？

3. 短时间发起太多图片请求检测

  检测标准：小于20个/秒
  
  原因： 短时间内发起太多图片请求会触发浏览器并行加载的限制，可能导致图片加载慢，用户一直处理等待。应该合理控制数量，可考虑使用雪碧图技术或在屏幕外的图片使用懒加载
  
  级别： p1

  实现手段？

4. 白屏时间检测

  标准：不大于 1000 ms
  
  原因： 页面打开期间，如果白屏时间过长，用户可能没有耐心等待而选择离开，建议实现错误处理函数，记录函数执行情况，定位原因，尽可能减少白屏耗时。
  
  级别： p1

  实现手段？

5. 废弃api检测

  标准： 不使用废弃api。

  实现手段？

6. JSAPI调用次数检测

  标准：调用同一个JSAPI小于20次
  
  级别： p2

  实现手段 

7. 首页流量消耗

  检测标准：小于4096kb
  
  级别： p0

8. 小程序包大小检测（可以换成js）

  检测标准：小于2048.0kb
 
  级别：p1


9. 短时间内发起太多请求

  检测标准：小于20个/秒
  
  级别： p1

10. JS函数耗时 

  检测标准：耗时小于100ms
  
  原因：页面打开期间调用的js函数较多，如果多个函数执行耗时都较长，那串行起来会更长，会严重影响用户体验，因此建议对耗时较长的函数进行优化
  
  级别：p1

11. JSAPI调用耗时过长

  检测标准：单次调用耗时小于1000ms
  
  原因:
  
  级别：p1

12. 图片尺寸检测

  标准：小于3倍
  
  原因: 图片太大而有效显示区域较小时会增加内存的消耗，应根据显示区域大小合理控制图片大小
  
  级别：p2

13. 渲染界面耗时过长检

  测检测标准：小于1000ms
  
  原因： 渲染界面的耗时过长会让用户觉得卡顿，体验较差，出现这一情况时，需要校验下是否同时渲染的区域太大
  
  级别： p1

14. setData数据量检测
  检测标准：小于256K
  
  原因： setData 数据量不宜过大，避免一次性传递过长的列表。 首屏请勿一次性构造太多节点，服务端可能一次请求传递大量数据，请勿一次性 setData，可先 setData 一部分数据，然后等待一段时间（比如   400ms，具体需要业务调节）再调用 $spliceData 将其他数据传输过去
  
  级别： p0

15. https请求资源检测

  检测标准：非HTTPS请求数个数为0

16. JSAPI调用异常检测

  检测标准：JSAPI调用异常数为0

17. 数据请求时机检测、

  检测标准：页面onReady中无请求发送

18. 文本资源压缩

  检测检测标准：文本资源未使用gzip/deflate压缩的个数为0

19. 首页启动耗时

  检测标准：小于3000ms
  
  原因：首屏内容全部显示出来的时间，它代表了用户可以感受到页面是否加载完成，可以进行交互，耗时过长会严重影响用户体验。

20. 请求耗时

  检测标准：耗时小于1000ms
  
  请求的耗时太长会让用户一直等待甚至离开，应当优化好服务器处理时间、减小回包大小，让请求快速响应应避免首页消耗过多的设备内存。内存占用过高，会影响新页面的内存提供，从而造成OOM。

21. 首页平均内存

  检测标准： 小于300M
  
  原因：应避免首页消耗过多的设备内存。内存占用过高，会影响新页面的内存提供，从而造成OOM。

22. js报错检测

  检测标准：报错个数为0
  
  原因： 应尽量避免JavaScript异常，出现异常可能会导致程序的不稳定，我们应追求零异常
  
  级别： p0

23. 图片分屏检测

  标准： 屏幕外图片加载个数为0
  
  原因： 加载当前屏幕中暂时不需要展示的图片，会影响页面加载耗时，增大内存消耗，建议分屏懒加载

24. JSAPI同步调用检测

  标准：单个页面JSAPI同步调用总耗时低于1000ms
  
  原因：单个页面JSAPI同步调用总耗时低于1000ms

25. AXML复杂度检测

  标准： 总节点数少于1500，最大深度为32个节点，没有超过60个子节点的父节点
  
  原因： 建议一个页面使用少于 1500 个节点，节点树深度少于 32 层，子节点数不大于 60 个，一个过大的DOM树会引起内存消耗增长，样式计算时间过长，与复杂的样式规则相结合可能会严重减慢渲染速度
  
  级别： p2

26. setData调用频率检测

  检测标准：小于20次/秒
  
  原因：避免频繁触发 setData 或者 $spliceData。需要频繁触发重新渲染时，避免使用页面级别的 setData 和 $spliceData， 将这一块封装成自定义组件，然后使用组件级别的 setData 或          $spliceData 触发组件重新渲染。长列表数据触发渲染时，使用 $spliceData 多次追加数据，而不用传递整个列表。复杂页面建议封装成自定义组件，减少页面级别的 setData
  
  级别： p0

27. 图片等比缩放检测

  标准：非等比缩放的图片个数为0
  
  级别： p2

28. 页面重复请求检测

  标准：单个页面中重复请求数0
  
  原因： 请求失败可能导致小程序的交互无法进行下去，应当保证所有请求都能成功

29. JS文件大小检测

  检测标准：小于300KB
  
  级别： p2

30. 请求失败检测

  检测标准： 失败数为0
  
  级别： p0



# 页面功能评测

加载耗时，
内存，
cpu

检查点：

  1. 空屏检测
  2，页面加载异常检测
  3. js错误
  4. 控件点击无响应








