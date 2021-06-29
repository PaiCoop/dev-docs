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
