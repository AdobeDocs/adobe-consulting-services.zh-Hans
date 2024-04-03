---
title: Veeva Vault集成概述
description: Veeva Vault集成概述
exl-id: 52cc7290-b7e1-4476-877f-48934e6daf68
source-git-commit: 4d27e7ecca662b2082a18621becb0b8ec7735824
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Veeva Vault促销活动与Adobe Experience Manager集成快速入门

此集成将管理您的内容，强制执行权限和合规性，同时利用同类领先的体验交付。

此集成需要以下最低软件版本：

* Adobe Experience Manager，6.5.5+
* Veeva Vault PromoMats，20R3.2+

>[!NOTE]
>
>两个系统中都需要服务用户和适当的权限才能进行集成。
>

>[!IMPORTANT]
>
>此功能并非作为产品的一部分现成可用。 实施需要Adobe咨询维护合同。 请联系您的Adobe代表以了解更多信息。
>

## 原理和功能

此集成旨在支持两个主要用例：

1. 内容审批 — 当在AEM中创建了新内容或编辑了现有内容时，必须批准该内容可在VVPM中使用，以支持生命科学的医疗、法律和法规(MLR)审批流程。

2. 内容管理 — 通过在PromoMats中为源自AEM的文档建立数字策略（如电子邮件、演示文稿、网站）与其在AEM中创建的元素（如徽标、照片、图形）之间的关系，提供资产利用情况的可见性。

其优势包括：

* 跨数字存储库维护资产和内容的单一真实来源，避免重复。
* 将Veeva Vault用于权限和合规管理，并将AEM用于同类最佳的内容和资产创建/交付。
* 帮助在AEM和Veeva Vault之间自动移动内容和元数据。
* 减少将内容发送到Veeva以进行批准工作流程时的手动工作。
* 每个系统都有其优势，并且连接器有助于在系统之间自动移动内容，从而加快上市时间。

该集成有什么作用？

* 支持将AEM站点页面、资产、内容片段和体验片段发送到VPM。 AEM页面、内容片段和体验片段可以作为屏幕快照PDF或图像发送。 AEM Assets二进制文件按原样发送。
* 支持手动和自动同步可从AEM配置到VVPM的选定元数据元素。
* 支持手动和自动同步从VVPM配置到AEM的选定元数据元素。
* 支持VVPM中AEM Site Pages、Assets、内容片段和体验片段之间的关系，以自动化内容关系。
* 支持为多种设备类型生成节目。

>[!NOTE]
>
>有关配置选项的更多详细信息，请参阅集成使用文档。
>

连接器不执行什么操作？

* 不会在Veeva中复制AEM流程和功能，反之亦然。
* MLR本身并不存在。 它有助于自动将内容发送到Veeva并发送到MLR发生的地方。
* 不用于在AEM和Veeva之间创建相同的设置。 并非所有内容都需要在两个平台之间移动。


>[!IMPORTANT]
>
>此集成当前将AEM视为内容同步的真实来源。
>

## 获取集成

要配置此集成，您需要执行以下步骤。

请按照下面的流程图和流程图详细信息请求和配置集成。

![请求访问](assets/integration-request.png)

流程图详细信息（映射到上述步骤）：

* **步骤1**  — 假定您已拥有Veeva Vault PromoMats和Adobe Experience Manager的许可证，或正在获取该许可证。
* **步骤2**  — 需要与Adobe咨询签署一份新的销售订单(SO)，其中列出了维护协议，以便利用集成。
* **步骤3**  — 安装、激活和配置集成包。

## 支持

以下介绍了如何联系支持团队并记录问题。

### 请求集成或Adobe Experience Manager支持

支持工单可由Adobe客户关怀团队记录。 您的Adobe Experience Cloud管理员需要登录到 [Adobe Admin Console](https://adminconsole.adobe.com/)，单击支持选项卡，然后创建案例。 对于集成期间出现的任何问题，请确保包括以下信息：

* **进程标题**： `AEM - Veeva Vault Integration`
* **进程所有者**： `Data Engineering`
* **描述**： `Description of the issue`
* **联系点**： `The email address(es) for relavant AEM point of contacts for your organization.`
* **AEM实例URL**： `Place the Adobe Experience Manager instance url here.`
* **Veeva实例URL**： `Place the Veeva Vault PromoMats instance url here.`

### 请求Veeva保险库促销支持

有时，遇到的问题与Veeva保险库PromoMats实例的运行有关。 如果是这种情况，可能会指导您的Veeva Vault PromoMats管理员创建支持工单，其中 [Veeva支持](http://support.veeva.com/). 通过导航到，可查看Veeva实例的状态 [Veeva Trust](http://trust.veeva.com/).
