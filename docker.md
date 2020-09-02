### docker常用命令

创建一个tag为1.2.0，仓库名为blog的镜像

```
docker build -t blog:1.2.0
```

查看镜像列表

```
docker images
```

删除镜像

```
docker rmi +image ID
```

创建名为plumemo为指定镜像容器

```
docker create -name plumemo +image ID
```

启动容器

```
docker run -itd -p 8086：8086 blog：1.2.0

-a, --attach=[]             Attach to STDIN, STDOUT or STDERR 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项
--add-host=[]               Add a custom host-to-IP mapping (host:ip)
--blkio-weight=0            Block IO (relative weight), between 10 and 1000
-c, --cpu-shares=0          CPU shares (relative weight)
--cap-add=[]                Add Linux capabilities
--cap-drop=[]               Drop Linux capabilities
--cgroup-parent=            Optional parent cgroup for the container
--cidfile=                  Write the container ID to the file
--cpu-period=0              Limit CPU CFS (Completely Fair Scheduler) period
--cpu-quota=0               Limit the CPU CFS quota
--cpuset-cpus=              CPUs in which to allow execution (0-3, 0,1) 绑定容器到指定CPU运行
--cpuset-mems=              MEMs in which to allow execution (0-3, 0,1) 绑定容器到指定MEM运行
-d, --detach=false          Run container in background and print container ID 后台运行容器，并返回容器ID
--device=[]                 Add a host device to the container
--dns=[]                    Set custom DNS servers 指定容器使用的DNS服务器，默认和宿主一致
--dns-search=[]             Set custom DNS search domains 指定容器DNS搜索域名，默认和宿主一致
-e, --env=[]                Set environment variables 设置环境变量
--entrypoint=               Overwrite the default ENTRYPOINT of the image
--env-file=[]               Read in a file of environment variables 从指定文件读入环境变量
--expose=[]                 Expose a port or a range of ports
-h, --hostname=             Container host name 指定容器的hostname
--help=false                Print usage
-i, --interactive=false     Keep STDIN open even if not attached 以交互模式运行容器，通常与 -t 同时使用
--ipc=                      IPC namespace to use
-l, --label=[]              Set meta data on a container
--label-file=[]             Read in a line delimited file of labels
--link=[]                   Add link to another container
--log-driver=               Logging driver for container
--log-opt=[]                Log driver options
--lxc-conf=[]               Add custom lxc options
-m, --memory=               Memory limit
--mac-address=              Container MAC address (e.g. 92:d0:c6:0a:29:33)
--memory-swap=              Total memory (memory + swap), ‘-1‘ to disable swap
--name=                     Assign a name to the container 为容器指定一个名称
--net=bridge                Set the Network mode for the container  指定容器的网络连接类型，支持 bridge/host/none/container:<name|id> 四种类型
--oom-kill-disable=false    Disable OOM Killer
-P, --publish-all=false     Publish all exposed ports to random ports
-p, --publish=[]            Publish a container‘s port(s) to the host
--pid=                      PID namespace to use
--privileged=false          Give extended privileges to this container
--read-only=false           Mount the container‘s root filesystem as read only
--restart=no                Restart policy to apply when a container exits
--rm=false                  Automatically remove the container when it exits
--security-opt=[]           Security Options
--sig-proxy=true            Proxy received signals to the process
-t, --tty=false             Allocate a pseudo-TTY 为容器重新分配一个伪输入终端，通常与 -i 同时使用
-u, --user=                 Username or UID (format: <name|uid>[:<group|gid>])
--ulimit=[]                 Ulimit options
--uts=                      UTS namespace to use
-v, --volume=[]             Bind mount a volume
--volumes-from=[]           Mount volumes from the specified container(s)
-w, --workdir=              Working directory inside the container
```

查询已启动的容器列表

```
docker ps
```

查询所有容器列表，包括没启动的容器

```
docker ps -a
```

删除指定容器	-f是强制删除正在运行的容器

```
docker rm -f +container ID
```

启动、停止和重启指定容器

```
docker start+container ID
docker stop +container ID
docker restart +container ID

-a, --attach=false         Attach STDOUT/STDERR and forward signals 启动一个容器并打印输出结果和错误
-i, --interactive=false    Attach container‘s STDIN 启动一个容器并进入交互模式
-t, --time=10      Seconds to wait for stop before killing the container 停止或者重启容器的超时时间（秒），超时后系统将杀死进程。
```

镜像的历史

```
docker history -H blog:1.2.0

-H, --human=true     Print sizes and dates in human readable format 以可读的格式打印镜像大小和日期
--no-trunc=false     Don‘t truncate output 显示完整的提交记录
-q, --quiet=false    Only show numeric IDs 仅列出提交记录ID
```

