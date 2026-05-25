1. 文件夹app_yaml中存放针对大华应用的查询数据库(excel)的工具, 如果大华应用的域名改变了, 本工具(Dahua_Excel_DB_Select.yaml)中的url也要改成一样的

2. 剩余文件则是dify的相关代码改动

----- 

启动dify, 参考dify官方文档, 下面只是部分代码(会根据版本不同而不同)

启动后端
uv run flask run --host 0.0.0.0 --port=5001 --debug
启动Celery
uv run celery -A app.celery worker -P gevent -c 1 --loglevel INFO -Q dataset,dataset_summary,priority_dataset,priority_pipeline,pipeline,mail,ops_trace,app_deletion,plugin,workflow_storage,conversation,workflow,schedule_poller,schedule_executor,triggered_workflow_dispatcher,trigger_refresh_executor,retention,workflow_based_app_execution
启动前端
cd web && docker build . -t dify-web
docker run -dit -p 3000:3000 -e CONSOLE_API_URL=https://dify.dahuaconsulting.cn -e APP_API_URL=https://dify.dahuaconsulting.cn -e ALLOW_EMBED=true --name dify-web dify-web