- 一键安装成功，但是浏览器无法访问？

1. 检查docker容器状态是否正常
2. 检查web服务器容器日志
    `docker logs -f $(docker ps | grep decept-defense:latest | awk '{print $1}')`

- 为什么模拟攻击没有攻击日志？

1. 通过透明代理列表，网络探测检查攻击IP、端口可以访问。
2. 确保密网服务器上/home/ehoney_proxy目录下对应的代理文件存在。

- 为什么我部署了多台探针Agent，但是探针列表只显示一个？

1. 删除agent/conf目录下agent文件，重新启动agent进程，确保每台服务器上agentID不一致。

- 为什么蜜罐列表中新建蜜罐失败？

1. 检查密网服务器资源状态，有可能是磁盘、cpu利用率满了。一般一台2核4G服务器上最多支持部署20个蜜罐。
2. 如果访问harbor不是https协议，需要在docker启动的时候指定insecure-registry。可以通过`kubectl describe pod`查看具体报错信息。

- 为什么蜜罐拓扑图不显示蜜罐和相关连线？

1. 蜜罐拓扑图中是以协议代理、透明代理为维度，如果没有代理则不会显示相关蜜罐。

- 为什么我部署了探针但是探针列表却不显示？

1. 检查agent中配置是否正确。主要检查conf/agent.json中strategyAddr(redis地址)、strategyPass(redis密码)、sshKeyUploadUrl(服务端更新sshkey地址)。
2. 确认探针服务器和web/蜜网服务器网络可以通信。

- 为什么协议代理创建失败？

1. 查看协议代理日志/home/relay/agent/proxy/log/proxy.log
2. 检查转发端口是否被占用/ssh_proxy文件是否正确

