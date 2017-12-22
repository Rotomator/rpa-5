#UiPath Orchestrator概述

UiPath Orchestrator是一个Web应用。在这个应用中，你可以编排机器人。同时可以创建、监控、部署资源。

##UiPath Orchestrator用例
UiPath Orchestrator主要的能力就是管理机器人。机器人的三种类型： Attended, Unattended和NonProduction,它们都可以连接到Orchestrator。
**助理式（Attended）** - 这种类型的机器人由用户触发，Orchestrator可以部署程序和记录助理式机器人的日志。
**无人看管式\(Unattended\)** 机器人无人看管式的运行在虚拟环境中，Orchestrator的负责远程执行，监控，计划等功能。
**非生产式\(NonProduction\)**,这种机器人类似无人看管式的，但是仅仅被用在开发和测试环境，不能被用于生产环境。所以Orchestrator不管理这些机器人。
Orchestrator的主要功能：


