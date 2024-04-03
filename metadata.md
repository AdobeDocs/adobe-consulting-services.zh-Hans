---
product: adobe experience manager
solution: Experience Manager
description: 咨询Experience Manager文档
type: Documentation
git-repo: https://github.com/AdobeDocs/adobe-consulting-services.zh-Hans
index: y
source-git-commit: e2dac4b36fb94d72b72ef6f73a77e3f566539444
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 54%

---


# 内部使用的元数据

GitHub创作系统中的元数据是分层的，并定义了以下相对于前一项的递增级别。

1. metadata.md
1. ToC
1. 文章

在 metadata.md 文件中的定义的元数据应用到整个存储库，但可以在 ToC 和文章级别覆盖。任何覆盖元数据的操作应在尽可能最低的级别进行。

metadata.md

* `product`
* `git-repo`
* `index: y`

ToC

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`

有关元数据的其他信息，请参见 [内部创作指南](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/authoring/metadata.html).
