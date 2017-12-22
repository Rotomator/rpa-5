# UiPath高可用部署

UiPath Server用来在客户端监控、记录、控制机器人的运行。

## 逻辑视图

UiPath Server主要包含三层：

**用户交互层\(User Interface Layer\)**

* Web应用程序

**Web服务层\(Web Services Layer\)**

* 监控服务\( Monitoring Service \)
* 日志服务\(Logging Service\)
* 部署服务\(Deployment Service\)
* 设置服务\(Configuration Service\)
* 队列服务\(Queues Service\)

**持久化层\(Persistence Layer\)**

* SQL Server
* ElasticSearch

![](/assets/import2.png)

### Web应用层

Web Application中用户可以监控机器人，创建机器人组，为组分配任务等,分析每个机器人的任务和进行。它连接了5类服务。该web服务被部署在 Internet Information Services \(IIS\) version 7.0 及以上。它需要安装Microsoft .NET Framework 4.5。

### web服务层

这5类服务:

**监控服务\(Monitoring Service\)**的职责是注册agent\(客户端电脑上的机器人的代理\)以及维护session ID, 交付配置。它可以执行和接收来自代理的通知的进程列表。它从数据库读取识别机器人数据。  
**配置服务\(Configuration Service\)**用来维护和交付配置信息。例如机器人所属组，每组能够执行的进程。它从数据库中读取配置信息  
**日志服务\(Logging Service\)**用来从代理中收集日志，并存储和索引日志 \(ElasticSearch\)  
**部署服务\(Deployment Service\)** 确保机器人能够正确的执行  
**队列服务\(Queues Service\)**被用来管理队列以及队列内容-添加数据到队列，从队列中获取数据，设置队列内容的状态等等

### 持久化层\(Persistence Layer\)

持久化层是由以下两个组件组成的：  
1. SQL Server,一方面用来存储机器人的配置。机器人的分组以及关联的进程。这些信息是通过Web Application来管理的。另一方面用来管理队列。  
2. 索引服务Indexer Server \(ElasticSearch\)用来存储和索引机器人的日志信息。SQL Server使用版本SQL Server 2008, SQL Server 2012 或者 SQL Server  
2014, 也支持SQL Server Express edition。索引服务使用ElasticSearch \(开源项目\)，全文搜索引擎。机器人的所有日志和消息通过日志服务器存储到索引。

在客户端机器上运行着机器人被作为一个执行者\(Executor\)。可以同时运行多个业务项目，每个项目都有相应的执行者。UiPath 代理Agent是Windows服务，它是唯一和执行者通信的组件。UiPath Agent也需要发送每一个机器人的状态给监控服务以及从部署服务中下载需要执行的包。

## 物理视图

方式一：Web Application和 Web Services 部署在同一台服务器。中等规模的机器人部署（10-50个机器人）

![](/assets/import3.png)  
方式二：部分服务分离。大型规模的机器人部署（100-200个机器人）

![](/assets/import4.png)

方式三：高可用和高扩展部署。高可用模式，7X24服务。

![](/assets/import1.png)

方式四：云端部署。有几种组合可用，下图采用3种云混合部署。分别是Azure，Amazon和MyGet

![](/assets/import5.png)

Orchestrator是使用Web服务构建的。机器人和Web服务之间的通信，

Web应用程序和Web服务之间以及Web服务之间的通信都是采用Web

服务URL，这使可以在混合云中部署。  
Azure – 部署web application和web services。SQL Azure Database – 使用SQL Server as a service作为数据库。  
Elasticsearch服务 – 使用WAS的Elasticsearch服务。  
NuGet Feed – 提供了 NuGet feed注册库, NuGet 是免费、开源的包管理开发工具，专注于在 .NET 应用开发过程中，简单地合并第三方的组件库。当需要分享开发的工具或是库，需要建立一个Nuget package，然后把这个package放到Nuget的站点。如果想要使用别人已经开发好的工具或是库，只需要从站点获得这个package，并且安装到自己的Visual Studio项目或是解决方案里。

## 安全性

web服务（REST API）能够使用以下方式保护其安全性 :

认证应该在以下级别实现：

* Web Application
* 配置
* 监控

授权应在以下级别实现:

* Web Application
* 配置

所有的web services都启用了SSL。所有的通信都支持HTTP和HTTPS。

## 基础设施需求

操作系统的最低需求:

* Windows Server 2008 R2 SP1
* Windows Server 2012 R2
* Windows Server 2014

数据库的版本：

* SQL Server 2008 Standard Edition with at least SP1  
* SQL Server 2012 Standard Edition
* SQL Server 2014 Standard Edition

注意： Windows操作系统和SQL Server的licenses需要客户自己准备。

## 硬件需求

### Demo、开发、UAT环境\(10-50机器人\)

方式一： 3台服务器

**Web App和Web Services服务器**

|  | 10-50个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 2 X 1.8Ghz cores | 4 X 2.4Ghz cores |
| RAM | 8G | 16G |
| HDD | 100G | 250G |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |

**SQL Server**

|  | 10-50个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 2 X 1.8Ghz cores | 4 X 2.4Ghz cores |
| RAM | 8G | 16G |
| HDD | 200G | 500G |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |
| Relational DB | SQL Server 2008 R2 Standard Edition w/ Service Pack 3 OR SQL Server 2012 R2 Standard Edition OR SQL Server 2014 Standard Edition | SQL Server 2008 R2 Standard Edition w/ Service Pack 3 OR SQL Server 2012 R2 Standard Edition OR SQL Server 2014 Standard Edition |

**ElasticSearch Server**

|  | 10-50个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 2 X 1.8Ghz cores | 4 X 2.4Ghz cores |
| RAM | 8G | 16G |
| HDD | 250G | 500G |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |

方式二： 2台服务器

**Web App和Web Services服务器**

|  | 10-50个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 2 X 1.8Ghz cores | 4 X 2.4Ghz cores |
| RAM | 8G | 16G |
| HDD | 100G | 250G |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |

**SQL Server和ElasticSearch**

|  | 10-50个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 2 X 1.8Ghz cores | 4 X 2.4Ghz cores |
| RAM | 8G | 16G |
| HDD | 500G | 1T |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |
| Relational DB | SQL Server 2008 R2 Standard Edition w/ Service Pack 3 OR SQL Server 2012 R2 Standard Edition OR SQL Server 2014 Standard Edition | SQL Server 2008 R2 Standard Edition w/ Service Pack 3 OR SQL Server 2012 R2 Standard Edition OR SQL Server 2014 Standard Edition |

### 生产环境\(无高可用和故障转移\)

**Web Application, Configuration Web Service, Deployment Web Service**

|  | 10-100个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 4 X 2.4Ghz cores | 8 X 2.4Ghz cores |
| RAM | 16G | 32G |
| HDD | 250G | 500G |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |

**SQL Server**

|  | 10-100个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 8 X 2.4Ghz cores | 16 X 2.4Ghz cores |
| RAM | 32G | 64G |
| HDD | 1T | 1T |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |
| Relational DB | SQL Server 2008 R2 Standard Edition w/ Service Pack 3 OR SQL Server 2012 R2 Standard Edition OR SQL Server 2014 Standard Edition | SQL Server 2008 R2 Standard Edition w/ Service Pack 3 OR SQL Server 2012 R2 Standard Edition OR SQL Server 2014 Standard Edition |

**ElasticSearch Server**

|  | 10-100个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 8 X 2.4Ghz cores | 16 X 2.4Ghz cores |
| RAM | 32G | 64G |
| HDD | 1T | 2T |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |

**Logging Web Service**

|  | 10-100个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 8 X 2.4Ghz cores | 16 X 2.4Ghz cores |
| RAM | 32G | 64G |
| HDD | 250G | 250G |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |

**Queues Web Service**

|  | 10-100个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 8 X 2.4Ghz cores | 16 X 2.4Ghz cores |
| RAM | 32G | 64G |
| HDD | 250G | 250G |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |

**Monitoring Web Service**

|  | 10-100个机器人 |  |
| :--- | :--- | :--- |
|  | 最小 | 推荐 |
| CPU | 8 X 2.4Ghz cores | 16 X 2.4Ghz cores |
| RAM | 32G | 64G |
| HDD | 250G | 250G |
| OS | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 | Windows Server 2008 R2 OR Windows Server 2012 R2 OR Windows Server 2014 |

### 生产环境，高可用、高扩展\(10 – 200个机器人\)

Web Application,  Configuration Web Service 以及Deployment Web Service,Monitoring Web Service需要安装在 Windows Failover Cluster \(主备\).  
Queues Web Service cluster \(双活\)和Logging Web Service cluster \(双活\)。需要网络的负载均衡F5或者Nginx

SQL Server的高可用需要使用“AlwaysOn”功能，只有在SQL Server 2012 Enterprise Edition \(标准版中并无此功能\)或者SQL Server 2014 Standard Edition.  AlwaysOn功能并不需要额外的存储，但是需要至少3 SQLServer节点。另外有存储可能需要使用基于windows主备模式的集群。整体上需要的硬件请参考上节。

## TCP端口

默认需要使用80，443两个端口，分别对应http和https。当然这些端口可以在安装的时候或者安装后变更。  
Logging web service连接到Elasticsearch需要9200端口。  
Orchestrator通过5601端口来访问 Kibana web plugin。  
SQL Server port \(默认1433\)需要开放。

## 客户端需求

|  | 最小 | 推荐 |
| :--- | :--- | :--- |
| 硬件 | PC | PC |
| CPU | 1GHz 32-bit \(x86\) | Dual Core 64-bit \(x64\) |
| RAM | 1G | 4G |
| 软件 |  |  |
| UiPath Studio |  |  |
| OS | Windows 7 | Windows 7+ |
| .NET | 4.5 | 4.6 |
| UiPath Robot |  |  |
| OS | Windows 7 | Windows 7+ |
| .NET | 4.5 | 4.6 |
|  |  |  |
| 启动磁空间 | 70M | 180M |
|  |  |  |



