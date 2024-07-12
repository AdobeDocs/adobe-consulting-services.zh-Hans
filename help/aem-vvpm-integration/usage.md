---
title: Veeva Vault集成使用
description: Veeva Vault集成使用
exl-id: efff7af1-eb25-4a1d-b7ef-52e3336970ff
source-git-commit: 19949a48cfee0c17481e52f286a460e9d81d7ff0
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---

# 集成使用

## 演练

以下视频演练介绍了如何使用连接器：

>[!VIDEO](https://video.tv.adobe.com/v/332137/?quality=12&learn=on)

## 设置

本指南将指导您完成连接器的启动和运行。

>[!IMPORTANT]
>
>对于每个系统，这些步骤需要由每个系统的&#x200B;**管理员**&#x200B;执行。
>
>本文档中的步骤将指导您创建涉及分配权限和/或管理员访问权限的集成/注册。  在执行之前，您有责任确保这些步骤符合贵公司的政策，并仔细执行这些政策。
>

### 安装集成包

您将获得对集成AEM包的访问权限。 可使用以下两个选项安装集成：

1. **软件包安装** — 直截了当，较少涉及。
2. **POM安装** — 更高级，但在使用AEM Cloud Manager和升级集成时可能很有用。

#### 包安装

要安装包，请通过载入电子邮件中提供的链接下载包。 [单击此处可找到有关安装AEM包的详细说明。](https://experienceleague.adobe.com/docs/experience-manager-64/administering/contentmanagement/package-manager.html?#installing-packages)

#### POM安装

要将连接器包括在POM中，请执行以下步骤。 将您的用户名和密码替换为载入电子邮件中收到的用户名和密码。

1. 将以下内容添加到项目中的`.cloudmanager/maven/settings.xml`文件或计算机上的`~/.m2/settings.xml`中。 将`YOUR_USERNAME`替换为用户名，将`YOUR_PASSWORD`替换为登录电子邮件中提供的密码。

   >[!IMPORTANT]
   >
   >如果使用Cloud Manager，则安全方法是按照此处为[受密码保护的Maven存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/create-application-project/setting-up-project.html?lang=en#password-protected-maven-repositories)找到的步骤进行操作。
   >

   ```
   <settings>
       ...
       <servers>
           ...
           <server>
               <id>repo.ea.adobe.net</id>
               <username>YOUR_USERNAME</username>
               <password>YOUR_PASSWORD</password>
               <filePermissions>BucketOwnerFullControl</filePermissions>
               <configuration>
                 <wagonProvider>s3</wagonProvider>
               </configuration>
           </server>
           ...
       </servers>
       ...
   </settings>
   ```

2. 将以下内容添加到项目的`pom.xml`文件：

   ```
   <project>
       ...
       <build>
           ...
           <extensions>
               ...
               <extension>
                   <groupId>com.allogy.maven.wagon</groupId>
                   <artifactId>maven-s3-wagon</artifactId>
                   <version>1.2.0</version>
               </extension>
               ...
           </extensions>
           ...
       </build>
       ...
       <repositories>
           ...
           <repository>
               <id>repo.ea.adobe.net</id>
               <url>s3://repo.ea.adobe.net/release</url>
               <releases>
                   <enabled>true</enabled>
               </releases>
           </repository>
           ...
       </repositories>
       ...
   </project>
   ```

3. 将以下内容添加到项目的`all/pom.xml`文件。 将`project.dependencies.dependency.version`替换为相应的版本，将`project.build.plugins.plugin.configuration.embeddeds.embedded.target`替换为正确的路径。

   ```
   <project>
       ...
       <build>
           ...
           <plugins>
               ...
               <plugin>
                   <groupId>org.apache.jackrabbit</groupId>
                   <artifactId>filevault-package-maven-plugin</artifactId>
                   ...
                   <configuration>
                       ...
                       <embeddeds>
                           ...
                           <embedded>
                               <groupId>com.adobe.acs.aemveeva</groupId>
                               <artifactId>aem-veeva-connector.all</artifactId>
                               <type>zip</type>
                               <target>/apps/APP_NAME-packages/application/install</target>
                           </embedded>
                           ...
                       </embeddeds>
                   </configuration>
               </plugin>
               ...
           </plugins>
           ...
       </build>
       ...
       <dependencies>
           ...
           <dependency>
               <groupId>com.adobe.acs.aemveeva</groupId>
               <artifactId>aem-veeva-connector.all</artifactId>
               <version>1.0.5</version>
               <type>zip</type>
           </dependency>            
           ...
       </dependencies>
       ...
   </project>
   ```

### 云配置

通过在连接器将操作的文件夹上创建云配置来配置此集成。 请按照以下步骤创建云配置：

1. 导航到Veeva云配置。

   ![导航到云配置](assets/cloud-config-navigate.png)

2. 在相应的文件夹中创建新的Veeva云配置，并按照以下部分中所述填充。

   ![创建云配置](assets/cloud-config-create.png)

#### “配置”选项卡

在配置选项卡中填写以下内容：

![配置选项卡](assets/configuration-tab.png)

1. 必需。 Veeva保险库连接器配置的标题。 此值可以是任意值。 （例如`Veeva Vault Configuration`）
2. 必需。 Veeva实例的域URL（例如`https://my-instance.veevavault.com/`）
3. 必需。 调用Veeva Vault API所需的ClientID。 该值可以是任意值，主要用于调试。 （例如`adobe-aem-vvtechpartner`）
4. 必需。 Veeva保险库用户名。 请参阅[Veeva用户创建](#veeva-user-creation)。
5. 必需。 Veeva保险库密码。 请参阅[Veeva用户创建](#veeva-user-creation)。

#### “AdobeIO”选项卡

如果项目需要为页面生成PDF或图像，则需要此选项卡。 在adobe io选项卡中填写以下内容：

![AdobeIO选项卡](assets/adobe-io-tab.png)

1. 必需。 用于创建载入电子邮件中提供的PDF图像的AdobeIO端点。 （例如`https://my-namespace.adobeioruntime.net/api/v1/web/aem-veeva-serverless-0.0.2/trigger-action.json`）
2. 必需。 用于生成页面图像的操作名称。 此值必须为`aem-veeva-integration/get-image-async`。
3. 必需。 用于生成html图像的操作名称。 此值必须为`aem-veeva-integration/get-pdf-async-new`。
4. 必需。 AdobeIO端点，用于获取载入电子邮件中提供的生成状态。（例如`https://my-namespace.adobeioruntime.net/api/v1/web/aem-veeva-serverless-0.0.2/get-state-value`）
5. 必需。 AdobeIO使用的AEM用户名。 请参阅[AEM用户创建](#aem-user-creation)。
6. 必需。 AdobeIO使用的AEM密码。 请参阅[AEM用户创建](#aem-user-creation)。
7. 可选。 默认超时是允许页面在指定的时间之前响应，在此时间之后，AIO服务将停止尝试获取响应。 默认值为`30000`。
8. 可选。 延迟是指页面以200响应延迟，以便所有图像在拍摄屏幕快照之前呈现。 默认值为`2000`。
9. 可选。 屏幕快照/PDF生成的URL将在配置值（以秒为单位）后过期。
10. 可选。 AdobeIO屏幕快照/PDF生成服务是异步的。 AEM服务调用AIO状态端点以获取屏幕快照/PDF。 此属性将决定每个状态调用之间的暂停时间（以毫秒为单位）。 默认值为`10000`。
11. 可选。 对AdobeIO进行状态调用以获取屏幕快照/PDF的最大重试计数。 默认值为`10`。

#### “高级”选项卡

在高级选项卡中填写以下内容：

![高级选项卡](assets/advanced-tab.png)

1. 生成PDF/图像时需要使用。 创建PDF/图像时使用的文件名模式。 可以对`{name}`进行模板。 （例如`{name}-screenshot`）
2. 可选。 除桌面设备外，需要页面屏幕截图的设备类型。 有效类型包括`Tab (iPad)`和`Mobile (iPhone X)`。
3. 可选。 Veeva中表示上述演绎版的演绎版类型值。 （例如`web_ready__c`）
4. 生成PDF/图像时需要使用。 要创建的屏幕快照类型。 `PDF`或`Image`。
5. 生成PDF/图像时需要使用。 要生成的PDF类型。 `Print CSS Based PDF`或`Pixel Perfect Screenshot PDF`。
6. 生成PDF/图像时需要使用。 要生成的图像类型。 `PNG`或`JPEG`。
7. 必需。 一旦Veeva Vault批准触发器触发运行，即会运行工作流。
8. 必需。 表示“已批准”的状态属性值。 （例如`Approved for Distribution`）
9. 必需。 Veeva保险库拒绝触发器触发后要运行的工作流。
10. 必需。 表示已拒绝/未批准的状态属性值。 （例如`Rejected`）
11. 可选。 Veeva Vault中文档ID的属性名称。 默认值为`id`。
12. 可选。 Veeva Vault中Status的属性名称。 默认值为`status__v`。
13. 可选。 文档修改日期的属性名称。 默认值为`version_modified_date__v`。
14. 可选。 文档资源URL的属性名称。 默认值为`external_id__v`。 如果此字段已被使用，请在Veeva中创建其他字段并在此处填充该字段名称。 此字段将在Veeva中用于保存AEM资源路径。 自动化元数据同步需要此项。
15. 可选。 Veeva Vault中主版本号的属性名称。 默认值为`major_version_number__v`。
16. 可选。 Veeva Vault中次版本号的属性名称。 默认值为`minor_version_number__v`。
17. 可选。 Veeva保险库关系类型值。 添加到页面的所有资产都将根据该值表示为相关。 默认值为`supporting_document__c`。

#### “页面”选项卡

如果正在同步页面，请在页面选项卡中填写以下内容：

![页选项卡](assets/page-tab.png)

1. 必需。 将资产从AEM映射到Veeva。
a. AEM属性名称。 可以从AEM属性中进行选择。 （例如`jcr:title`） `{name}`可以模板。
b.完全在输入的Veeva属性名称在Veeva中存在。 （例如`name__v`）\
   c.属性类型。 `Text`或`Multiline Text`。

2. 必需。 将资产从Veeva映射到AEM。
a.完全在输入的Veeva属性名称在Veeva中存在。 （例如`name__v`）
b. AEM属性名称。 可以从AEM属性中进行选择。 （例如`jcr:title`）
c.属性类型。 `Text`或`Multiline Text`。


#### “资源”选项卡

如果正在同步资源，请在资源选项卡中填写以下内容：

![资产选项卡](assets/asset-tab.png)

1. 必需。 将资产从AEM映射到Veeva。
a. AEM属性名称。 可以从AEM属性中进行选择。 （例如`/jcr:content/metadata/jcr:title`） `{name}`可以模板。
b.完全在输入的Veeva属性名称在Veeva中存在。 （例如`name__v`）
c.属性类型。 `Text`或`Multiline Text`。

2. 必需。 将资产从Veeva映射到AEM。
a.完全在输入的Veeva属性名称在Veeva中存在。 （例如`name__v`）
b. AEM属性名称。 可以从AEM属性中进行选择。 （例如`/jcr:content/metadata/jcr:title`）
c.属性类型。 `Text`或`Multiline Text`。

### 其他设置

#### AEM用户创建

在PDF/图像生成期间，需要创建AEM用户才能从AEM获取页面。 通过以下链接创建并授予用户只读权限：

如果使用AEM 6.5.5+：

* [在AEM中创建用户](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/setup-organize-users/adding-configuring-users.html?#create-a-user)
* [在AEM中为用户添加权限](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?#permissions-in-aem)

如果使用AEMCloud Service：

* [使用AEMCloud Service管理用户](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?#accessing)

AEM服务用户需要对将转换为PDF/图像并推送到Veeva的内容拥有以下权限：

* 读取

>[!IMPORTANT]
>
> 必须以管理员身份对每个系统执行这些操作。
> 在创建用户和设置权限时，您必须遵守组织的安全标准。
>

#### Veeva用户创建

要使用此集成，需要在Veeva Vault中创建用户。 要创建用户，请执行以下步骤：

1. 导航到管理员 — >用户和组 — >保险库用户 — >创建

   ![导航到Veeva用户](assets/veeva-user-navigate.png)

2. 填写所需的输入。 最简单的设置是将`License Type`设置为`Full User`，将`Security Profile`设置为`Vault Owner`。 完成后保存。

   ![创建Veeva用户](assets/veeva-user-create.png)

使用的特定Veeva文档类型需要以下权限：

* 创建/读取文档
* 创建/读取版本
* 创建/更新元数据
* 创建/更新演绎版

>[!IMPORTANT]
>
> 必须以管理员身份对每个系统执行这些操作。
> 在创建用户和设置权限时，您必须遵守组织的安全标准。
>
