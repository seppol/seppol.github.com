---
layout: post
title: LBS中位置隐私
category: 科研
tags: 位置隐私保护
keywords: 位置隐私
description: 
---

LBS中的位置泄露可能导致很严重的隐私威胁，比如健康相关的问题，经济相关的问题，宗教信仰，家庭住址等等。最重要的是我们不知道这些隐私的泄露在未来会对用户造成怎么样的威胁。

### 构成攻击场景的因素

```
* on the definition of privacy, i.e., what information the user wants to hide
* on the communication architecture
* on the attack model, i.e.,the background knowledge of the attacker, and the inference capabilities she has 
* on the data transformation,i.e, in what way are the original data transformed in order to provide the desired privacy guaranty.
```

### LBS中主要的隐私分类

```
* location privacy (exposure of users’ locations)
* identity privacy (identifying users based on their locations)
* absence privacy (infer users’ absence at various locations) 
* colocation　privacy (location exposure in the check-ins involving　multiple users)
```

### LBS的主要框架

![1](/public/img/keyan/k02.JPG)

### 主要解决方法

```
* 空间模糊（k-匿名）
* 数据转化（密钥加密）
* 虚拟地址
```