# Zurl

Zurl 是一款简单且实用的短链接系统，可以快速生成短链接，方便分享和管理。Zurl 旨在提供一个轻量级的解决方案，帮助用户更好地管理和跟踪链接。

![970c82f82f62fe5c.png](https://img.rss.ink/imgs/2025/08/04/970c82f82f62fe5c.png)

![c57c3cce4618acd3.png](https://img.rss.ink/imgs/2025/08/04/c57c3cce4618acd3.png)

## 功能特点

* [x] **短链接生成**：用户可以将长链接转换为短链接，便于分享和传播。
* [x] **链接管理**：提供直观的界面，管理员可以查看、编辑和删除。
* [x] **延迟计数**：系统会延迟记录每个短链接的点击次数，避免高并发时压力过大。
* [x] **自动获取标题**：添加链接时，系统会尝试自动获取长链接的标题，方便后续识别。
* [x] **支持UA屏蔽**：管理员可以自定义需要屏蔽的User-Agent，防止恶意访问。
* [x] **数据迁移**：支持将YOURLS数据迁移到Zurl，帮助用户过渡。
* [x] **API**：提供API接口，方便二次开发和集成到任意系统。
* [x] API Token管理
* [ ] 高级分析
* [ ] 自定义站点信息
* [ ] 中英文双语支持
* [ ] 登录会话管理

## 安装Zurl

> 目前仅支持Docker安装，请确保您已经安装Docker和Docker Compose

新建`docker-compose.yaml`文件，内容如下：

```yaml
version: '3.8'

services:
  zurl:
    container_name: zurl
    image: beeseek/zurl
    ports:
      - "3080:3080"
    restart: always
    volumes:
      - ./data:/opt/zurl/app/data
```

输入`docker-compose up -d`启动，然后访问`http://IP:3080` 根据提示完成初始化！

## 升级

1.使用 Docker Compose 停止服务：

```
docker-compose down

```

2.拉取最新镜像

Zurl 的镜像beeseek/zurl更新后，需拉取最新版本：

```
docker-compose pull

```
3.重新启动服务

使用新镜像启动容器，挂载的./data目录会自动复用（保留原有数据和配置）：

```
docker-compose up -d

```

4.验证升级结果

访问http://IP:3080，确认服务正常启动。

登录管理员后台，检查数据（短链接、配置等）是否完整。

## 设置

**UA屏蔽**

可以在挂载目录下找到`config.toml`中的`app.DENY_UA`添加需要屏蔽的User-Agent，默认屏蔽：

* *信
* *Q

> 注意：修改配置后需要重启容器！

**重置密码**

如果您忘记了管理员账号或密码，可以删除挂载目录下的`config.toml`文件，然后重启容器并重新访问Zurl完成初始化即可。（此操作不影响数据）

> 切勿删除挂载目录下的`db`目录，否则会导致链接数据丢失。

## 演示

* 演示站点：[https://zurl.demo.mba](https://zurl.demo.mba)
* 用户名：`xiaoz`
* 密码：`blog.xiaoz.org`

## 问题反馈

* 如果有任何问题可以在[Issues](https://github.com/helloxz/zurl/issues) 中提交。
* 或者添加我的微信：`xiaozme`，请务必备注Zurl

## 技术栈

* 后端：Python3 + FastAPI
* 前端：Vue3 + Element Plus
* 数据库：SQLite3
* 缓存：Redis

## 其他产品

如果您有兴趣，还可以了解我们的其他产品。

* [Zdir](https://www.zdir.pro/zh/) - 一款轻量级、多功能的文件分享程序。
* [OneNav](https://www.onenav.top/) - 高效的浏览器书签管理工具，将您的书签集中式管理。
* [ImgURL](https://www.imgurl.org/) - 2017年上线的免费图床。
