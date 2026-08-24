# 阿里云企业Web上云架构实战
> ACP云计算备考实践项目

本项目基于阿里云云起实验室完成企业级Web多层架构实操，练习VPC网络、负载均衡、云数据库、NAT网关等核心云产品，理解云上高可用架构与按量付费计费规则。

## 🧩实验资源
实验一键开通按量付费资源：
- ECS云服务器 ×2（跨可用区A/B部署Web服务）
- RDS MySQL 云数据库
- ALB应用型负载均衡
- EIP弹性公网IP
- NAT公网网关

> 架构图中NAS、Redis属于参考组件，本次实验未部署，仅做原理学习。

## 🏗️架构图
```mermaid
flowchart LR
    User[用户浏览器] --> ALB[ALB负载均衡 + EIP]
    subgraph VPC专有网络
        subgraph 可用区A
            ECS1[ECS‑01 Web]
        end
        subgraph 可用区B
            ECS2[ECS‑02 Web]
        end
        ALB --> ECS1 & ECS2
        ECS1 & ECS2 --> NAT[NAT网关]
        ECS1 & ECS2 --> RDS[RDS MySQL]
    end

