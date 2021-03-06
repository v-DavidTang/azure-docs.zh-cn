---
title: 适用于 Windows 应用商店 JavaScript 应用的移动服务入门 | Microsoft Docs
description: 按照本教程开始使用 Azure 移动服务通过 JavaScript 进行 Windows 应用商店开发。
services: mobile-services
documentationcenter: windows
author: ggailey777
manager: erikre
editor: ''

ms.service: mobile-services
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: javascript
ms.topic: get-started-article
ms.date: 07/21/2016
ms.author: glenga

---
# 移动服务入门
[!INCLUDE [mobile-services-selector-get-started](../../includes/mobile-services-selector-get-started.md)]

&nbsp;

[!INCLUDE [mobile-service-note-mobile-apps](../../includes/mobile-services-note-mobile-apps.md)]

> 有关本主题的对等移动应用版本，请参阅[使用移动应用创建 Windows 应用](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started.md)。
> 
> 

本教程说明如何使用 Azure 移动服务向 Windows 应用商店 JavaScript 应用添加基于云的后端服务。在本教程中，你将要创建一个新的移动服务，以及一个在新移动服务中存储应用程序数据的简单*待办事项列表*应用程序。要创建的移动服务将为服务器端业务逻辑使用 JavaScript。

若要完成本教程，您需要以下各项：

* 有效的 Azure 帐户。如果你没有帐户，只需花费几分钟就能创建一个免费试用帐户。有关详细信息，请参阅 [Azure 免费试用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdocumentation%2Farticles%2Fmobile-services-javascript-backend-windows-store-javascript-get-started%2F)。
* [Visual Studio 2013 Express for Windows]

## 创建新的移动服务
[!INCLUDE [mobile-services-create-new-service](../../includes/mobile-services-create-new-service.md)]

## 创建新的 Windows 应用商店应用程序
创建移动服务后，你可以在 Azure 经典门户中按照简单的快速入门来创建一个新的可连接到移动服务的 Windows 应用商店 8.1 JavaScript 应用。

1. 在 [Azure 经典门户]中，单击“移动服务”，然后单击刚刚创建的移动服务。
2. 在快速入门选项卡中，单击“选择平台”下的“Windows”，然后展开“创建新的 Windows 应用商店应用程序”。
3. 在本地计算机或虚拟机上下载并安装 [Visual Studio 2013][Visual Studio 2013 Express for Windows]（如果尚未这么做）。
4. 单击“创建 TodoItem 表”以创建用于存储应用程序数据的表。
5. 在“下载并运行应用”下，选择应用的语言，然后单击“下载”。
   
      随即将会下载已连接到移动服务的示例*待办事项列表*应用程序的项目。将压缩的项目文件保存到本地计算机，并记下保存位置。

## 运行 Windows 应用程序
本教程的最后一个阶段是生成和运行你的新应用程序。

1. 浏览到您保存压缩项目文件的位置，在计算机上展开文件，并在 Visual Studio 中打开解决方案文件。
2. 按 **F5** 键以重新构建项目并启动此应用。
3. 在应用程序中的“插入 TodoItem”中键入有意义的文本（例如 *Complete the tutorial*），然后单击“保存”。
   
       这样可向在 Azure 中托管的新移动服务发送 POST 请求。来自请求的数据被插入到 TodoItem 表。移动服务返回存储在表中的项，数据显示在应用的第二列中。
4. （可选）再次运行应用，并注意在应用启动后将从移动服务加载在上一步中保存的数据。
5. 返回 [Azure 经典门户]中，单击“数据”选项卡，然后单击“TodoItems”表。
   
       这使您可以浏览此应用插入表中的数据。

> [!NOTE]
> 你可以查看访问你的移动服务以查询和插入数据的代码，这些代码在 default.js 文件中。
> 
> 

## 后续步骤
完成快速入门后，请了解如何使用[适用于 HTML/JavaScript 的移动服务客户端](mobile-services-html-how-to-use-client-library.md)。

[!INCLUDE [app-service-disqus-feedback-slug](../../includes/app-service-disqus-feedback-slug.md)]

<!-- Anchors. -->
[Getting started with Mobile Services]: #getting-started
[Create a new mobile service]: #create-new-service
[Define the mobile service instance]: #define-mobile-service-instance
[Next Steps]: #next-steps

<!-- Images. -->

<!-- URLs. -->
[Visual Studio 2013 Express for Windows]: http://go.microsoft.com/fwlink/?LinkId=257546
[Mobile Services SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure 经典门户]: https://manage.windowsazure.com/

<!---HONumber=AcomDC_0921_2016-->