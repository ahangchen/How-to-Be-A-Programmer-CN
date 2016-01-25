# 如何处理I/O代价

在很多问题上，处理器的速度比硬件交流要快得多。这种代价通常是小的I/O，可能包括网络消耗，磁盘I/O，数据库查询，文件I/O，还有其他与处理器不太接近的硬件使用。所以构建一个快速的系统通常是一个提高I/O的问题，而非在紧致的循环里优化代码或者甚至优化算法。

There are two very fundamental techniques to improving I/O: caching and representation. Caching is avoiding I/O (generally avoiding the reading of some abstract value) by storing a copy of that value locally so no I/O is performed to get the value. The first key to caching is to make it crystal clear which data is the master and which are copies. There is only one master - period. Caching brings with it the danger that the copy sometimes can't reflect changes to the master instantaneously.

Representation is the approach of making I/O cheaper by representing data more efficiently. This is often in tension with other demands, like human readability and portability.

Representations can often be improved by a factor of two or three from their first implementation. Techniques for doing this include using a binary representation instead of one that is human readable, transmitting a dictionary of symbols along with the data so that long symbols don't have to be encoded, and, at the extreme, things like Huffman encoding.

A third technique that is sometimes possible is to improve the locality of reference by pushing the computation closer to the data. For instance, if you are reading some data from a database and computing something simple from it, such as a summation, try to get the database server to do it for you. This is highly dependent on the kind of system you're working with, but you should explore it.

Next [How to Manage Memory](09-How to Manage Memory.md)
