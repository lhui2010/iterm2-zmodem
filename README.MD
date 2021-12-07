# 项目介绍

在 mac 下，实现与服务器进行便捷的文件上传和下载操作。


# 步骤

1.安装支持rz和sz命令的lrzsz（Mojave测试通过）：
```bash
curl -o lrzsz-0.12.20.tar.gz https://www.ohse.de/uwe/releases/lrzsz-0.12.20.tar.gz
tar -xvzf lrzsz-0.12.20.tar.gz
cd lrzsz-0.12.20
./configure
make -j 6
sudo make install
cd /usr/local/bin
sudo ln -s lrz rz
sudo ln -s lsz sz
```
2.在本地/usr/local/bin/目录下保存iterm2-send-zmodem.sh 和iterm2-recv-zmodem.sh两个脚本

3.设置一下两个脚本的权限

```bash
chmod +x /usr/local/bin/iterm2-*
```

4.设置Iterm2的Tirgger特性，profiles->default->editProfiles->Advanced中的Tirgger

添加两条trigger，分别设置 Regular expression，Action，Parameters，Instant如下：

```
1.第一条
        Regular expression: rz waiting to receive.\*\*B0100
        Action: Run Silent Coprocess
        Parameters: /usr/local/bin/iterm2-send-zmodem.sh
        Instant: checked
2.第二条
        Regular expression: \*\*B00000000000000
        Action: Run Silent Coprocess
        Parameters: /usr/local/bin/iterm2-recv-zmodem.sh
        Instant: checked
```

![如图](https://github.com/aikuyun/iterm2-zmodem/blob/master/imgs/01.png)


如果不工作，手工在iterm2运行下rz和sz，把输出的代码改成trigger的代码。比如我的send是`\*\*B0100000023be50`，recv是`\*\*B00000000000000`。


