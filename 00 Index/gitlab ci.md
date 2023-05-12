## [关键词](https://www.bilibili.com/video/BV18y4y1S7VC?p=9&vd_source=0fa5bd2a88ebd5d46bbac0029ffe9f2e)

job、script 、 stages、 tags、 when、 retry、 timeout 、only、 except 、rules、variable

## 1 过程

1. 安装gitlab-Runner
2. 注册Runner server
	1. gitlab-runner register
		2. gitlab url
		3. token
		4. description
		5. tags
		6. shell executor
3. 编写pipeline脚本
	1. gitlab-ci.yml

```js
stages:
  - docker-build
variables:
  GIT_SUBMODULE_STRATEGY: recursive
docker-build:
  stage: docker-build
  script:
    - pwd
    - git branch
    - git status
    - make localpush tag=$CI_COMMIT_REF_NAME
  tags: // 对应runner的tags
    - lm-local
  after_script:
    - pipline_notify.sh
```

make命令用来执行项目目录下的Makefile文件内定义的脚本方法

```js
TAG = $(tag)

localpush:
	docker build -f Dockerfile . -t harbor.apulis.cn:8443/apulis-iqi/app/frontend-admin:$(TAG)
	docker push harbor.apulis.cn:8443/apulis-iqi/app/frontend-admin:$(TAG)

get-deps:
	git submodule sync // 命令会将子模块的远程仓库 URL 更新为其 .gitmodules 文件中指定的 URL。
	git submodule sync --recursive // 命令会递归更新所有子模块的远程仓库 URL。
	git submodule update --init --recursive // 命令会将本地仓库的子模块更新到指定的版本，即更新子模块对应的 Git 仓库的代码。

```