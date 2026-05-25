---
product: adobe experience manager
solution: Experience Manager
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
usetq: true
description: 咨询Experience Manager文档
type: Documentation
git-repo: https://github.com/AdobeDocs/adobe-consulting-services.en
index: true
source-git-commit: e0159a3db7c79d12ee150be018ee5d005975b95a
workflow-type: tm+mt
source-wordcount: 94
ht-degree: 2%

---


# 元数据供内部使用

GitHub创作系统中的元数据是分层的，并定义了以下相对于前一项的递增级别。

1. metadata.md
1. ToC
1. 文章

在metadata.md文件中定义的元数据应用到整个存储库，但可以在ToC和文章级别覆盖。 任何覆盖元数据的操作应在尽可能最低的级别进行。

metadata.md

* `product`
* `git-repo`
* `index: y`

ToCs

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`

有关元数据的其他信息可在[内部创作指南](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/authoring/metadata.html)中找到。
