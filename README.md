# 电商向量搜索

使用 Qdrant 向量数据库，并结合云端推理生成 Embedding，实现语义化商品搜索。
Embedding 模型 + Qdrant 向量搜索.

## 配置

在.env文件里填写你的凭证：


```bash
cd ~/ecommerce-search-golang
gedit .env
```

需要配置以下环境变量：

```bash
QDRANT_HOST="你的 Qdrant Cloud 主机地址"
QDRANT_API_KEY="你的 Qdrant API Key"
 
NUM_WORKERS=8

```  
 

## 导入数据

构建并运行数据导入脚本，将商品数据写入 Qdrant：

```bash
cd ~/ecommerce-search-golang
set -a
source .env
set +a 
go run ./cmd/ingest/main.go

```

可选：设置 `NUM_WORKERS` 来控制并行任务数量，默认值为 `8`。
等待几分钟后就好了。

## 运行应用

```bash 
go run ./cmd/server/main.go

```
保持这个终端运行，不关闭。
然后另开启一个终端，执行

```bash
cd frontend
npm install
npm run dev
```


- 前端：http://localhost:3000
- API：http://localhost:8080

需要注意，这只是小demo,每个商品是没有图片的，这些图片的链接早几百年就失效了。

