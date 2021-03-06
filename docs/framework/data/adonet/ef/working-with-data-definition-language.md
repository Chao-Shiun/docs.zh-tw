---
title: "使用資料定義語言 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ec50083d-44f4-4093-9b23-5eacd601f96e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 使用資料定義語言
從 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 4 版開始，[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 就支援資料定義語言 \(DDL\)。  這可讓您根據連接字串和儲存體 \(SSDL\) 模型的中繼資料，建立或刪除資料庫執行個體。  
  
 <xref:System.Data.Objects.ObjectContext> 的下列方法會使用連接字串和 SSDL 內容來達成下列目的：建立或刪除資料庫、檢查資料庫是否存在，以及檢視產生的 DDL 指令碼：  
  
-   <xref:System.Data.Objects.ObjectContext.CreateDatabase%2A>  
  
-   <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A>  
  
-   <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A>  
  
-   <xref:System.Data.Objects.ObjectContext.CreateDatabaseScript%2A>  
  
> [!NOTE]
>  執行 DDL 命令需要足夠的權限。  
  
 先前所列的方法會將大部分工作委派給基礎 ADO.NET 資料提供者。  提供者要負責確保用來產生資料庫物件的命名慣例與用於查詢和更新的慣例一致。  
  
 下列範例將為您示範如何根據現有的模型產生資料庫。  此外，這個範例也會將新的實體物件加入至物件內容，然後將它儲存至資料庫。  
  
## 程序  
  
#### 若要根據現有的模型定義資料庫  
  
1.  建立主控台應用程式。  
  
2.  將現有的模型加入至應用程式。  
  
    1.  加入名為 `SchoolModel` 的空模型。  若要建立空的模型，請參閱 [How to: Create a New .edmx File](http://msdn.microsoft.com/zh-tw/beb8189e-e51c-4051-839c-9902c224abf2)主題。  
  
     SchoolModel.edmx 檔案就會加入至您的專案。  
  
    1.  從 [School Model](http://msdn.microsoft.com/zh-tw/859a9587-81ea-4a45-9bc0-f8d330e1adac)主題中複製 School 模型的概念、儲存體和對應內容。  
  
    2.  開啟 SchoolModel.edmx 檔案並在 `edmx:Runtime` 標記中貼上內容。  
  
3.  將下列程式碼加入至 main 函式。  此程式碼會將連接字串初始化為資料庫伺服器、檢視 DDL 指令碼、建立資料庫、將新的實體加入至內容，並且將變更儲存至資料庫。  
  
     [!code-csharp[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/csharp/VS_Snippets_Data/DP ObjectServices Concepts/CS/Source.cs#ddl)]
     [!code-vb[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP ObjectServices Concepts/VB/Source.vb#ddl)]