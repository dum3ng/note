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

!!!note 进程和线程

    进程是程序的一次执行。
    线程是cpu操作的最小单元。一个进程可以包含多个线程。

    多任务的处理可以通过高频cpu利用快速切换来实现（时分复用）。
    然而真正的多进程和多线程的实现必须依赖多核cpu。

### [select / epoll ][1]

select 函数能够选择所有接收事件的进程。

epoll（event polling) 选中所有活动的进程，同时包含相应的内存缓冲区事件。

[1]: https://www.zhihu.com/question/20122137
