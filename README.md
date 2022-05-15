定义一个LenthyLogger.mo，是一个actor class，由它引用ic-logger/Logger。

主合约是由MyLogger定义，它里面定义了一个loggers，保存LenthyLogger的数组，空间不够则继续创建新的LenthyLogger。

这三者的关系如下：

MyLogger(1) -> LenthyLogger(n)
LenthyLogger(1) -> ic-logger/Logger(1)

LenthyLogger: actor class
MyLogger: actor

MyLogger对外暴露四个四个函数。

print_info为调试使用，在后台打印所有的log。

append为往合约中添加新的log数组。

stats返回合约的主要信息：page_size，count，offset 和 page。他们满足的计算关系为：count = PAGE_SIZE * (page - 1) + offset

roll_over是内部函数，由它实际来创建LenthyLogger的actor class。[参见这里](https://github.com/alexxuyang/icp_course_H_1/blob/b17e7c5e33a87655c7bbe9389b502c4c645fba79/MyLogger.mo#L48)

您如果需要本地调试，建议将[PAGE_SIZE](https://github.com/alexxuyang/icp_course_H_1/blob/b17e7c5e33a87655c7bbe9389b502c4c645fba79/MyLogger.mo#L21)改成4，以达到创建多个actor class的效果。

下面是我在本地的一些测试配图

[本地candid UI](https://github.com/alexxuyang/icp_course_H_1/blob/main/images/1.png)
