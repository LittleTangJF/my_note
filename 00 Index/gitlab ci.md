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