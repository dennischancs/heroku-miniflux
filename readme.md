## deploy

1. switch to [main branch](../../tree/main)
2. deploy with [heroku button](https://heroku.com/deploy)

## auto update

1. deploy app as above
2. **fork** this repo
3. enable [github action](../../actions)
4. go to [heroku dashboard](https://dashboard.heroku.com/apps), then choose your app
5. set **deployment method** to **github**
6. select your repo, **main** branch
7. click **enable automatic deploy**



## Notice
miniflux默认 [`"POLLING_FREQUENCY": "60"`](https://miniflux.app/docs/configuration.html#polling-frequency)，但heroku的Free版本 web应用 30分钟未使用就停机了，导致miniflux的订阅无法及时更新。

解决方案如下：既节省free版时长，又要能及时看到RSS更新。

1. 在app.json的env中，添加 `"POLLING_FREQUENCY": "10"`，改为10分钟更新一次。确保停机后下一次开机的30分钟内能自动更新2次以上，为更新失败留有余量。
2. 使用[UptimeRobot](https://uptimerobot.com) ，每6小时监测heroku的web app一次，即让其开机运行30分钟。

注意：heroku每次再开机虽然会重置网页容器的配置，但这个RSS miniflux容器的数据和配置均储存在postgres数据库容器中，停机也没事，故不需要把UptimeRobot调成25分钟监测一次。