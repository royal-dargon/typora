### CRAWLER

爬虫的概念 ： 访问web服务器，获取指定数据信息的程序。

工作流程 ：

1. 明确目标 Url
2. 发送请求，获取应答数据包。
3. 保存，过滤数据，提取有用信息。
4. 使用分析得到数据信息。

写爬虫的时候要分析页数的变化，记住 strconv.Itoa的函数使用。