# 如何处理I/O代价

在很多问题上，处理器的速度比硬件交流要快得多。这种代价通常是小的I/O，可能包括网络消耗，磁盘I/O，数据库查询，文件I/O，还有其他与处理器不太接近的硬件使用。所以构建一个快速的系统通常是一个提高I/O的问题，而非在紧致的循环里优化代码或者甚至优化算法。

有两种基本的技术来优化I/O：缓存和代表（译者注：比如用短的字符代表长的字符）。缓存是通过本地存储数据的副本,再次获取数据时就不需要执行I/O,以此来避免I/O（通常避免读取一些抽象的值）。缓存的关键在于让（上层对于）那些数据是主干的，那些是副本完全透明。主干的数据只有一份-周期。缓存有这样一种危险：副本有时候不能立刻反映主干的修改。

代表是通过更高效地代表数据来让I/O更廉价。这通常会限制其他的要求，比如可读性和可移植性。

代表通常可以用他们第一实现中的两到三个因子来做优化。实现这点的技术包括使用二进制表示而非人类可识别的方式。Representations can often be improved by a factor of two or three from their first implementation. Techniques for doing this include using a binary representation instead of one that is human readable, transmitting a dictionary of symbols along with the data so that long symbols don't have to be encoded, and, at the extreme, things like Huffman encoding.

A third technique that is sometimes possible is to improve the locality of reference by pushing the computation closer to the data. For instance, if you are reading some data from a database and computing something simple from it, such as a summation, try to get the database server to do it for you. This is highly dependent on the kind of system you're working with, but you should explore it.

Next [How to Manage Memory](09-How to Manage Memory.md)
