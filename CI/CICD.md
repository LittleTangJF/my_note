## 关键词
Gitlab + Gitlab Runner 、集成、 交付、部署、.gitlab-ci.yml、Pipeline

## 定义

通过在自动化来频繁向客户交付应用的方法；

核心：持续集成、持续交付和持续部署

持续自动化和持续监贯穿于应用的整个生命周期（从集成和测试阶段，到交付和部署）

意义：重复劳动被去除了大部分，多出来的这部分时间我可以用来干更多有意义的事情


## 实现流程

### 核心
- gitlab 自带的 CI/CD 能力
- .gitlab-ci.yml

### 1、代码合并
- jest单元测试
- eslint+preterer 代码格式规范
- git-hooks：pre-commit阶段lint-staged进行检查
	- 如何跳过：git commit -no-vertify
- pr阶段
	- 根据api再跑一遍检查
	- 检查时机：feature-** + pr
- code-review
### 2、打包
- webhooks平台提供： push、merge事件
#### [[gitlab ci]]
- 基于runner：Runner 独立部署到新机器上
- 检测到代码更新
- 符合`.gitlab-ci.yml`触发规则 -  产生pipeline
- stage - 定义 join： build stage  deploy stage  
#### github actions实现

#### docker compose实现
### 3、部署
- push到该静态服务器资源目录


