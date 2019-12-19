# docker

## 基础技术
### Linux Namespace
    Namespace的API主要使用3个系统调用
    <ul>
        <li>clone()创建新进程。根据系统调用参数来判断哪些类型的Namespace被创建，而且它们的子进程也会被包含到这些Namespace中。</li>
        <li>unshare()将进程移出某个Namespace</li>
        <li>setns()将进程加入到Namespace</li>
    </ul>
