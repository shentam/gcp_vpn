使用Google Cloud搭建免费一年SSR服务器（VPN）
网上教程很多，也走了很多弯路，汇总出一个比较靠谱的搭建方法，而且也比较简单
如果帮到了你，希望可以点个赞

前期准备：一台可以翻墙的电脑（需要上Google）（例如：免费版蓝灯，或vpn软件的试用版）                

               一张双币信用卡（Google验证身份，扣款一美元，之后会退）



自己搭建的不限速 平均下载速度可以达到20M，可能是被我的国内网速限制住了，应该会更高。对应网速已经超过200M了

              

1.申请试用GCP
打开Google Cloud官方网站(网址：cloud.google.com/)，点击页面上的”免费试用”.使用你的谷歌账号登陆后，选择是否接受谷歌的邮件，并同意条款。


2.付款
下一步是填写你的付款信息以及联系信息。这里没有图，简单和大家说一下，类型选“Individual(个人)”即可，地址需要填写一个你上一步选的国家的邮编及地址（因为博主之前已经绑定过谷歌钱包的付款信息，当时写的是美国的邮编，所以这一步自动填充了），再往下是要求填写你的信用卡信息，填写后可能会有1美元的验证（过后会退回来，只是为了防止机器人注册）。全部填写成功后，就会进入到你的控制台了，如下图：



3.修改防火墙 (ps:一定要注意选中---所有实例,或者自己配置要翻的那个实例)
进入控制台后，依次点击菜单–网络–防火墙规则。然后点击右上角的“创建防火墙规则”。名字随便起一个就好，然后中间部分不用动。“目标”选“网络中的所有实例”，“来源过滤”选择“IP地址范围”，并在下方填写“0.0.0.0/0”，然后最下方选择“指定的协议和端口”，并在下方填入“tcp:0-65535;udp:0-65535”。然后点击创建。





流量方向 出站  入站  各设置一条
4.创建VM实例 (要注意选择ip和要允许https和http)
然后再回到菜单，选择“计算引擎”—“VM实例”—“创建实例”。名字随便起一个，地区建议选“asia-east1-a”（台湾地区，速度比较快），机器类型选最低配的“微型”即可，启动磁盘建议选ubuntu 16.4 因为以下教程是这个操作系统的，防火墙允许HTTP/HTTPS流量。然后点击下方的“网络”选项卡，选择“外部IP”—“新建静态IP地址”，起个名字后就会分配到一个IP地址（每个地区仅限1个），完成后点击“创建”即可。



 

如果你本机有ssh可以吧自己的rsa.pub 复制上去,这样就可以直接在shell上用ssh连接了

4.SSH连接服务器
等待几十秒配置成功后，就可以在列表中看到你刚创建的实例了，点击右侧的“SSH”，现在让我们来搭建Shadowsocks服务器。





5.安装ssr






使用方法：
使用root用户登录，运行以下命令：

sudo su

wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh

chmod +x shadowsocks.sh

./shadowsocks.sh 2>&1 | tee shadowsocks.log

复制代码
四条命令依次输入ssh执行



这一步是选择加密方式，随便选择一个就可以，选择默认也行

端口号也是一样，选择默认或者随便输入一个未被占用的

6.显示配置
安装完成后，脚本提示如下：

Congratulations, Shadowsocks-python server install completed!
Your Server IP        :your_server_ip
Your Server Port      :your_server_port
Your Password         :your_password
Your Encryption Method:your_encryption_method

Welcome to visit:https://teddysun.com/342.html
Enjoy it!复制代码

http://dfei.vip/post/198.html
