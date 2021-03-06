---
title: "Azure 搜索中的数据上传 | Microsoft Docs"
description: "了解如何将数据上载到 Azure 搜索中的索引。"
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: ashmaka
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 2ebe71b3456420f29ffe06bc15471d3fd2121f8c


---
# <a name="upload-data-to-azure-search"></a>将数据上载到 Azure 搜索
> [!div class="op_single_selector"]
> * [概述](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

## <a name="data-upload-models-in-azure-search"></a>Azure 搜索中的数据上载模型
有两种方法使用你的数据填充 Azure 搜索索引。 第一种方法是使用 Azure 搜索 [REST API](search-import-data-rest-api.md) 或 [.NET SDK](search-import-data-dotnet.md) 将数据手动推送至索引。 第二种方法是 [将支持的数据源指向](search-indexer-overview.md) Azure 搜索索引，并让 Azure 搜索自动将数据拉入搜索服务。

尽管本指南仅涵盖使用数据上载推送模型的说明（仅在 [REST API](search-import-data-rest-api.md) 和 [.NET SDK](search-import-data-dotnet.md) 中受支持），但仍可了解有关以下拉模型的详细信息。

### <a name="push-data-to-an-index"></a>将数据推送至索引
这种方法是指以编程方式将数据发送到 Azure 搜索以使其可供搜索。 对于具有极低延迟要求的应用程序（例如，如果需要搜索操作与动态库存数据库同步），只能选择推送模型。

可以使用 [REST API](https://msdn.microsoft.com/library/azure/dn798930.aspx) 或 [.NET SDK](search-import-data-dotnet.md) 将数据推送至索引。 目前尚没有支持通过门户推送数据的工具。

此方法相比拉模型更加灵活，因为你可以单个或批量上载文档（每批最多 1000 个或 16MB，以先达到为准）。 推送模型还允许你将文档上载到 Azure Search，而不考虑数据的位置。

### <a name="pull-data-into-an-index"></a>将数据拉入索引
拉模型对支持的数据源进行爬网并将数据自动上载到 Azure Search 索引。 除了识别新文档外，通过跟踪对现有文档的更改和删除外，索引器免除了主动管理索引中数据的必要。

在 Azure 搜索中，此功能通过*索引器*实现，当前可用于 [Blob 存储（预览版）](search-howto-indexing-azure-blob-storage.md)、[DocumentDB](http://aka.ms/documentdb-search-indexer)、[Azure SQL 数据库和 Azure VM 上的 SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)。

在 [Azure 门户](search-import-data-portal.md)和 [REST API](https://msdn.microsoft.com/library/azure/dn946891.aspx) 中可找到索引器功能。




<!--HONumber=Nov16_HO2-->


