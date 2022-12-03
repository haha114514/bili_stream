# bili_stream
A docker image based on nginx-stream for forwarding streaming to bilibili-live 

## Update 03/12/2022 目前已失效，除非手动在hosts中把live-push.bilivideo.com指向转发ip，不然叔叔的收流服务器检测不到正确的header会在1分半-2分左右强制断开推流。

前言

本次教程采用腾讯云上海免费升级的2C4G6M服务器举例，搭建基于Nginx-Stream插件进行直播流量的转发，便于海外用户直播推流B站。

参考配置


![image](https://user-images.githubusercontent.com/47912037/114272259-d0741480-9a58-11eb-837a-f5030301f8f5.png)
![image](https://user-images.githubusercontent.com/47912037/114272260-d23dd800-9a58-11eb-9809-29de68a7bd52.png)

网速注意


由于国内各大云默认出口大概率都是电信163，部分电信163访问差的线路，请窒息或者加一层中转（但是花了两个的钱了，为什么不直接去买其他现成的服务呢）

其次，也可以使用其他服务商提供的国内nat服务器等，不过请自行查看服务商的TOS，有些服务商严禁回国，请窒息。

# 中转教程


## 0.（可选）安装BBR用于增加网络稳定性和提升速度。


wget -N "https://github.000060000.xyz/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

一般来说，安装xanmod版内核(选择6)，然后使用bbr+fq_pie加速（选择12）即可。

## 1.	安装Docker


curl -fsSL https://get.docker.com | bash -s docker


## 2.	安装提供的Docker镜像

docker run --restart=always --name live -d -p 1935:1935 haha114514/bili_stream

Ps:如果使用的是nat服务器，请使用

docker run --restart=always --name live -d -p 你的端口:1935 haha114514/bili_stream

输入docker ps，检查docker镜像是否正常运行
![image](https://user-images.githubusercontent.com/47912037/114272325-14671980-9a59-11eb-8268-2d23f4b145c6.png)

如显示上图，则为正常运行

## 3.测试直播

去网站上开播（通过malus或者穿梭等免费的chrome插件即可做到）


打开obs，将 设置-推流-服务器中的连接改为rtmp://你的服务器ip/live-bvc/（例如rtmp://11.4.5.14/live-bvc/），串流密码保持b站提供的直播码不变

然后开播测试，如果正常推流则运行正常。
![image](https://user-images.githubusercontent.com/47912037/114272423-7889dd80-9a59-11eb-8107-fbaeb57131d7.png)

Ps:如果使用的是nat服务器，请将格式改为rtmp://你的服务器ip:你的端口/live-bvc/

请尽情使用吧。











