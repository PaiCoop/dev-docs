# PaiCoop


![language](https://img.shields.io/github/languages/top/PaiCoop/PaiCoop)
![contributors](https://img.shields.io/github/contributors/PaiCoop/PaiCoop)
![last commit](https://img.shields.io/github/last-commit/PaiCoop/PaiCoop)

[![github star](https://img.shields.io/github/stars/PaiCoop/PaiCoop?style=social)](https://github.com/PaiCoop/PaiCoop)
[![github forks](https://img.shields.io/github/forks/PaiCoop/PaiCoop?style=social)](https://github.com/PaiCoop/PaiCoop)
[![gitHub watchers](https://img.shields.io/github/watchers/PaiCoop/PaiCoop?style=social)](https://github.com/PaiCoop/PaiCoop/)

> An awesome project.

## 架构

### 理念

本着迭代开发，野蛮生长的项目演进思路，PaiCoop架构通过按需模块化和界面接口标准化，打造高聚合，低耦合的高可靠，易扩展系统。

### 组成

PaiCoop系统由运行在客户端上的UI, SDK, 以及运行在服务端的API和DB组成。

<div class="mermaid">
flowchart TB
    subgraph USER AGENT
    UI
    SDK
    end
    subgraph SERVER
    API
    DB
    end
    DB<--js-->API
    API<--stomp-->SDK
    UI<--func-->SDK
</div>

UI(User Interfalce)是用户界面，负责与用户进行直接的交互。UI运行在客户端上，其形式可以是网页，APP，甚至桌面程序等。UI通过调用SDK提供的方法（函数）与服务端交互。

SDK(Software Development Kit)是一组运行在客户端上的工具集。在PaiCoop系统中，SDK的主要作用是1）建立并维护客户端与服务端之间的可靠通信，2）对客户端进行身份识别，3）提供访客统计，通知等功能。

API(Application Interface)是运行在服务端上的一组程序。API的主要作用是1）对UI提供的数据进行处理，并存储到DB进行持久化，2）根据UI的请求提供相应的数据，3）用户身份认证及权限管理，4）通知服务。API提供一系列HTTP REST接口，SDK将且仅通过这些接口与服务端取得联系。

DB(Database)是运行在服务端上的一组具备数据存储功能的程序。各种需要持久化的数据将存储在DB中。


## Alpha版本

在PaiCoop系统的演变初期，首要目标是尽可能多地收集`2021届`毕业生的数据。考虑到项目成员暑期较繁忙，能用到项目上的时间精力宝贵且有限，Alpha版本将不开发一切非当前必须的功能，**仅保留最核心的表单提交功能**，同时在系统架构设计上使得新的功能可以灵活添加且数据能够轻易继承。为了尽可能团结一切能团结的力量，据此，Alpha版本将配合[Awesome-XJTLU](https://github.com/awesome-xjtlu/wiki)，将其作为UI的展示部分，同时保持自己的数据存储结构。


<div class="mermaid">
sequenceDiagram
    UI.Profile->>SDK: SDK.push(Object FormObject)
    SDK->>API: HTTP Request
    alt data good
        API->>DB: CURD
        API->>AwesomeXJTLU: Git Pull Request
    end
    API->>SDK: HTTP Respond [status]
    SDK->>UI.Profile: Return [status]
</div>


上图是Alpha版本的泳道图。其中描述了在提交表单后PaiCoop系统的执行细节。


<div class="mermaid">
sequenceDiagram
    PaiCoop->>AwesomeXJTLU_Github_Repo: Git Pull Request
    opt Reviewer Approved
        AwesomeXJTLU_Github_Repo->>AswsomeXJTLU_Github_Pages: Update to WebSite
    end
</div>

上图为Alpha版本与Awesome-XJTLU的详细交互细节。人工审核由Awesome-XJTLU成员完成。