我们前面介绍了文件的创建、打开和关闭。下面我们就要对文件的内容进行操作了。最基础的就是读写文件了。

##系统调用——read

read系统调用，是从指定的文件描述符中读取数据。
```
#include<unistd.h>

ssize_t read(int fd, void *buf, size_t count);

调用成功返回读到的字节数，读到文件尾则返回0。错误返回-1；
```

参数count代表最多能读取的字节数，buf是，指将文件中的内容读取到buf所指向的缓冲区中（buf是地址）。我们在上一小节的代码中可以看到这个代码：
        
    read(fd, &recvdata, 100）;
    这个代码就是从已经打开的文件描述符（fd），读取最多100个字节（可以小于100）到recvdata所指向的内存中。




##系统调用——write

write系统调用，是给指定的文件描述符中写入数据。

```
#include<unistd.h>

ssize_t write(int fd, void *buf, size_t count);

调用成功返回写入数据的字节数，错误返回-1。
```

参数count类似read系统调用，代表写入文件的字节数。buf是指，将buf所指向的存储区的数据写入文件。我们可能会遇到该系统调用返回值小于count。原因是磁盘已经满了或者进程资源对文件大小的限制。


当然，有很多童鞋就会想，这些系统调用跟我们刚接触的C语言中的文件读写有什么区别呢？

其实很简单，c语言的函数是在stdio库中，他们属于用户态的函数，这些函数在底层调用的还是现在所展示的这些系统调用。

![](images/two_kinds_of_io.png)


从这个图就能看出来它们之间的关系了吧？
