# jekyll docker 镜像运行注意事项

## docker 运行命令
```docker run --rm -v /home/mao/jekyll/srv:/srv/jekyll -v /home/mao/jekyll/bundles:/usr/local/bundle -p 32400:4000 --env JEKYLL_ENV=production -it jekyll/jekyll:$JEKYLL_VERSION jekyll server --config _config.yml,_config_siteurl.yml```

## 挂载卷
### 主题以及内容卷
容器内挂载点为 /srv/jekyll, 目录属主为 1000:1000

## 环境变量
### JEKYLL_ENV 
需要设置为 ```production``` ，否则静态链接会被替换为默认的 ```0.0.0.0:4000``` ，参考此 [issue](https://github.com/mmistakes/hpstr-jekyll-themes/isssues/167)

## site.url
```site.url``` 的值在 ```_config.yml``` 中配置，但是这个值是一个部署变量，随着部署环境变化而变化，因此需要通过部署参数方式传递给 Jekyll 。
Jekyll 可以支持多个 ```_config.yml``` 文件，因此采用覆盖的方式。
这里例子的 ```_config_siteurl.url``` :

```
url: http://43.254.1.134:32400
```

