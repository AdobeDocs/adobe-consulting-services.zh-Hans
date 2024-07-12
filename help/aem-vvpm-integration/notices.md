---
title: Veeva Vault集成注意事项
description: Veeva Vault集成注意事项
exl-id: 1a188671-d123-4475-a607-65743ba0dadd
source-git-commit: 07eab1e439626bd3bb3416c9e7d0c1666927a7aa
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# 最佳实践、护栏和声明

## 版本

此集成需要以下最低软件版本：

* Adobe Experience Manager，6.5.5+
* Veeva Vault PromoMats，20R3.2+

## 数据隐私

此集成旨在在Adobe Experience Manager和Veeva Vault PromoMats之间传输内容。 作为数据控制者，贵公司有责任遵守适用于您收集和使用数据的任何隐私法规。

## 内容同步频率

触发集成工作流后，AEM内容和元数据会从AEM同步到VVPN。 这可以自动或手动完成。 VPM元数据已从VPM同步到AEM。 您可以通过调度程序自动完成这项操作，或通过单击按钮手动完成这项操作。

## 集成限制和最佳实践及保障

使用此集成时，请考虑以下限制：

* 同步元数据时仅支持以下数据类型：“文本”和“多行文本”。
* 虽然集成支持AEM模块化内容（内容片段和体验片段），但它不支持VVPM模块化内容。
* 不支持VVPM链接文档。
* 不支持将VVPM可视注释从VVPM同步到AEM。
* 该集成不会将内容从VVPM导入AEM。
* 不支持元数据验证。
* 根据Veeva许可证，文档数量有限。 请参阅[许可证限制](#veeva-license-limitations)。
* 根据Veeva许可证，API调用的数量有限。 有关详细信息，请参阅[API限制](https://developer.veevavault.com/docs/#what-are-rate-limits)。 请参阅[许可证限制](#veeva-license-limitations)。

## Veeva许可证限制

您可以通过导航到VVPM常规设置来监视实例限制。

![Veeva限制](assets/veeva-limits.png)
