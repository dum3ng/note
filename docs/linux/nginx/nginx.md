# nginx

## nginx 的事件模型

nginx 的高性能的原因。

Apache 使用多线程来对请求进行处理。
当请求数很多时，每个请求都需要一个进程来处理，增加了内存的消耗，
而且 cpu 对多线程的处理，需要频繁地切换上下文，导致 cpu 的利用率也不高。

nginx 启动时，先启动一个 master 进行，然后启动`worker_process`个 worker 进程,
每一个 worker 进程

TODO:

首先不需要 cpu 进行上下文的切换，
其次只有固定数目的 work 进程。
各个进程相互独立，不需要对内存等进行管理。

!!!note 进程和线程

    进程是程序的一次执行。
    线程是cpu操作的最小单元。一个进程可以包含多个线程。
    各个线程可以访问进程申请的内存单元。
    访问共享内存需要利用锁来进行访问限制。

    多任务的处理可以通过高频cpu利用快速切换来实现（时分复用）。
    然而真正的多进程和多线程的实现必须依赖多核cpu。

### [select / epoll ][1]

阻塞

当一个进程**A**由于对 socket 的等待，而进入阻塞，操作系统将其从执行队列中移出，
放入该 socket 的等待队列中；
一旦该 socket 接收了数据，操作系统再将此进程**A** 移回执行队列中。

select/epoll 是监听多个 socket 的方法。

select 函数能够选择所有接收事件的进程。
当调用 select 函数时，会将进程放入其所监听的所有 socket 的等待队列中，
并进入阻塞状态；
只要其中有一个 socket 接受到数据，进程就会被唤醒，进入执行状态；
这时，只需要对 socket 列表进行一次遍历，就可以对有数据的 socket 进行处理。

```c
int s = socket(AF_INET, SOCK_STREAM, 0);
bind(s, ...)
listen(s, ...)

int fds[] =  存放需要监听的socket

while(1){
    int n = select(..., fds, ...)
    for(int i=0; i < fds.count; i++){
        if(FD_ISSET(fds[i], ...)){
            //fds[i]的数据处理
        }
    }
}

```

`select`的缺点

- 每次调用都需要将 socket 列表重新传入
- 进程唤醒后，并不知道哪个 socket 获取了数据，必须遍历 socket 列表

epoll（event polling) 选中所有活动的进程，同时包含相应的内存缓冲区事件。

```c
int s = socket(AF_INET, SOCK_STREAM, 0);
bind(s, ...)
listen(s, ...)

int epfd = epoll_create(...);
epoll_ctl(epfd, ...); //将所有需要监听的socket添加到epfd中

while(1){
    int n = epoll_wait(...)
    for(接收到数据的socket){
        //处理
    }
}
```

`epoll` 将添加监听列表和阻塞进行了功能分离，不同于`select`只有一个单独的函数来实现，
`epoll`包括`epoll_create`(创建 epoll 对象), `epoll_ctl`(添加 socket 列表),
`epoll_wait`(等待事件).

而且，内核维护了一个`rdlist`列表，其中保存了就绪状态的 socket 的引用，这样
当进程被唤醒时，不必去遍历所有监听的 socket，而只需要去遍历`rdlist`中的 socket 即可。

#### eventpoll 原理

    Everything is a file.
                          -- unix philosophy

`epoll_create` 创建一个 epoll 对象，该对象也属于文件系统的一员，同 socket 一样，
也有等待队列。
当调用`epoll_wait`时，进程被放入 epoll 对象的等待队列中。
当进程被唤醒时，系统将 epoll 对象所维护的就绪列表`rdlist` 进行更新，
包含所监听的 socket 列表中处于就绪状态的 socket.

## [HTTP 协议][2]

一个 webserver 对 HTTP 请求的处理都要包括

- 读取请求行
- 读取请求头
- 读取请求体
- 响应行，响应头,响应体

```http
POST http://example.com HTTP/1.1
Accept: application/json
Content-Type: application/json

{
  "q": "google"
}
```

---

## references

[1]: https://www.zhihu.com/question/20122137
[2]: https://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html

[select/epoll](https://zhuanlan.zhihu.com/p/64138532)
