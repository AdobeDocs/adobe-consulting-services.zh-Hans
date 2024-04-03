---
title: Veeva保险库集成常见问题解答
description: Veeva保险库集成常见问题解答
exl-id: c308ebb3-7881-4094-9f35-c67a96fb5ab1
source-git-commit: e4a5e55ac9b79a8de7dfa8ddd3d0ad99560917b8
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 常见问题解答

**哪些元数据应同步到Veeva？**

基于Veeva门户中的内容类型（如促销活动）了解元数据很重要。 查看Veeva门户后，在AEM中构建内容元数据架构以保存每个资产/页面的所有相关元数据，并配置集成以在这两个系统之间映射元数据。

**集成是否支持Veeva链接文档？ 如果不是，则支持哪些关系类型？**

不适用。 请参阅 [Veeva文档](https://vaulthelp2.vod309.com/wordpress/admin-user-help/documents-admin-user-help/about-document-relationships/). 链接的文档（引用关系类型）是标准关系类型之一，无法通过API创建或删除，因为它们具有特殊的Vault行为。 组件、支持文档以及任何未在此列表中的其他组件应能够通过AEM Veeva云配置进行配置。

**该集成是否支持AEM模块化内容？**

是，该集成支持AEM内容片段和体验片段。

**该集成是否支持Veeva模块化内容？**

不，现在不行。

**集成是否将Veeva可视注释同步到AEM？**

不，现在不行。 可视批注只能通过API作为PDF访问。

**我们如何对通过集成同步的VPM文档设置权限？**

集成使用服务用户通过API上传文档。  仅在VVPM用户界面中支持文档默认和覆盖规则（文档上的默认角色），在使用API时不会应用这些规则。 建议使用DAC（动态访问控制）进行角色分配。 DAC通过所有接触点（包括API）执行。 [请参阅此文档。](http://vaulthelp2.vod309.com/wordpress/admin-user-help/ah-user-permissions-access-control/about-dynamic-access-control-for-documents/)

**集成是否支持多个VVPM实例？**

该集成使用云配置方法，该方法允许从一个AEM实例配置多个Veeva端点。

**集成是否支持AEM发布？**

否，此集成仅适用于AEM作者。 它旨在促进内容发布前的MLR审查周期。
