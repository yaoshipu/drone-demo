# drone-demo

## User Guide

### Clone

#### 1. Clone 自身项目

- agent 默认会注入github commit 的信息到 git-plugin 容器，clone自身项目不需要提供额外的参数。
- drone 默认的 clone 路径为 /drone/src/github.com/yaoshipu/drone-demo

```
clone:
  # 自定义tag，一般用repo的名称	
  clone-demo.git:
	# 选择 git-plugin 镜像
    image: index.qiniu.com/spock/git-plugin:cs-proxy
```

#### 2. clone 多个项目

- 如果一个repo有其他依赖的库，则可以在 clone 里面配置多个项目。
- 用户需要自定义 clone 的 workspace，所有的 repos 会被 checkout 到指定目录

```
workspace:
  # 指定所有 repos 都被 checkout 到 /workspae 目录
  base: /workspace

clone:
  drone-demo.git:
    image: index.qiniu.com/spock/git-plugin:cs-proxy
	# 设置 clone 路径
    path: /workspace/drone-demo

  base.git:
    image: index.qiniu.com/spock/git-plugin:cs-proxy
	# 配置依赖库地址，注意: remote url 只能配置 https
    remote_url: https://github.com/qbox/base.git
    branch: master
    path: /workspace/base
```

