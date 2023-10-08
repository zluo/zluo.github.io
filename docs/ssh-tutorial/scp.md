---
layout: default
title: scp
parent: SSH Tutorial
nav_order: 3
---
# scp 命令

`scp`是 secure copy 的缩写，相当于`cp`命令 + SSH，用来在两台主机之间加密传送文件（即复制文件）。

## 基本语法

```bash
$ scp user@host:foo.txt bar.txt
# copy multiple files
$ scp source1 source2 destination
```

上面命令将远程主机（`user@host`）用户主目录下的`foo.txt`，复制到本机当前目录的`bar.txt`。主机与文件之间要使用冒号（`:`）分隔。

{:.note }
`scp`可以使用 `.ssh/config` 配置文件

### Examles

**（1）本地文件复制到远程**
```bash
$ scp file.txt remote_username@10.10.0.2:/remote/directory
#Copy Directory
$ scp -r documents username@server_ip:/path_to_remote_directory
```

**（2）远程文件复制到本地**
```bash
$ scp remote_username@10.10.0.2:/remote/file.txt /local/directory
# Copy Directory
$ scp -r username@server_ip:/path_to_remote_directory local-machine/path_to_the_directory/
```

**（3）两个远程hosts之间的复制**
```bash
$ scp user1@host1.com:/files/file.txt user2@host2.com:/files
```

### Options

**（1）`-c`**

`-c`参数用来指定文件拷贝数据传输的加密算法。

```bash
$ scp -c blowfish some_file your_username@remotehost.edu:~
```

上面代码指定加密算法为`blowfish`。

**（2）`-C`**

`-C`参数表示是否在传输时压缩文件。

```bash
$ scp -c blowfish -C local_file your_username@remotehost.edu:~
```

**（3）`-F`**

`-F`参数用来指定 ssh_config 文

```bash
$ scp -F /home/pungki/proxy_ssh_config Label.pdf root@172.20.10.8:/root
```

**（4）`-i`**

`-i`参数用来指定 private key

```bash
$ scp -vCq -i private_key.pem ~/test.txt root@192.168.1.3:/some/path/test.txt
```

**（5）`-l`**

`-l`参数用来限制传输数据的带宽速率，单位是 Kbit/sec

```bash
$ scp -l 80 yourusername@yourserver:/home/yourusername/* .
```

上面代码中，`scp`命令占用的带宽限制为每秒 80K 比特位，即每秒 10K 字节。

**（6）`-p`**

`-p`参数用来保留修改时间（modification time）、访问时间（access time）、文件状态（mode）等原始文件的信息。

```bash
$ scp -p ~/test.txt root@192.168.1.3:/some/path/test.txt
```

**（7）`-P`**

`-P`参数用来指定远程主机的 SSH 端口。如果远程主机使用默认端口22，可以不用指定，否则需要用`-P`参数在命令中指定。

```bash
$ scp -P 2222 user@host:directory/SourceFile TargetFile
```

**（8）`-q`**

`-q`参数用来关闭显示拷贝的进度条。

```bash
$ scp -q Label.pdf mrarianto@202.x.x.x:.
```

**（9）`-r`**

`-r`参数表示是否以递归方式复制目录。

**（10）`-v`**

`-v`参数用来显示详细的输出。

```bash
$ scp -v ~/test.txt root@192.168.1.3:/root/help2356.txt
```

