---
{"dg-publish":true,"created":"2025-04-17T18:43","updated":"2025-04-17T18:43","permalink":"/105-极客/自托管的类youtube产品——peertube，视频网站/","dgPassFrontmatter":true,"noteIcon":""}
---


[[peertube\|peertube]]

## 部署记录
- 使用官方镜像需要修改 `docker-compose.yml` 和 `.env` 里面的网段，否则就会报错 `It does not belong to any of this network's subnets`
- 自带 docker-compose. yml 文件不能自动初始化数据库，要注意用户名与密码
- 走ip访问是不能登录的，必须解析成域名。