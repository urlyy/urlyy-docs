# docsify


有个docusaurus和docsify，我选择了后者。感觉会比较简洁纯净一些。

本来想白嫖serverless，但是看了一圈，vercel、cf、github都国内不太好访问，腾讯的edgeone必须要绑定备案域名，gitee的pages服务关掉了。所以只好自己找服务器了。

最后选择了京东云。新人有个一年2c2g，49元的轻量云主机，还是很便宜的。人生就80年，需要自己买服务器的估计也就10多年，几个厂商薅一遍就差不多了🤣。

通过宝塔面板装nginx和webhook，然后也要登录服务器装git以及配置git。

然后按照[宝塔 WebHook 使用教程](https://xxb.im/2018/11/02/pagoda-webhook-use-tutorial/)配置服务器上的webhook，将生成的链接复制到github仓库的配置里，就可以实现push仓库后，仓库触发我的服务器上的一个hook，hook里写的就是拉取更新代码。

ps: 好像还有一种持续部署方案是让github workflow在push后，登录我们的服务器，将最新的代码通过ftp等方式上传到服务器上。但这样的话我的文档仓库就不能公开了，而且让github登录私人服务器感觉不太安全，就弃用了。
