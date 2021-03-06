---
title: "實作 UI 自動化 Table 控制項模式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI 自動化 Table 控制項模式"
  - "控制項模式資料表"
  - "TableControl 模式"
ms.assetid: 880cd85c-aa8c-4fb5-9369-45491d34bb78
caps.latest.revision: 19
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 18
---
# 實作 UI 自動化 Table 控制項模式
> [!NOTE]
>  這份文件適用於.NET Framework 開發人員想要使用 managed[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中定義的類別<xref:System.Windows.Automation>命名空間。 如需最新資訊[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，請參閱[Windows Automation API: UI 自動化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主題介紹的指導方針和慣例實作<xref:System.Windows.Automation.Provider.ITableProvider>，包括屬性、 方法和事件的相關資訊。 其他參考的連結會在概觀的結尾列出。  
  
 <xref:System.Windows.Automation.TablePattern>控制項模式用來支援控制項，做為容器的子元素的集合。 此元素的子系必須實作<xref:System.Windows.Automation.Provider.ITableItemProvider>和組織可以周遊資料列和資料行的二維邏輯座標系統中。 此控制項模式相當於<xref:System.Windows.Automation.Provider.IgridProvider>，但任何控制項的實作差異<xref:System.Windows.Automation.Provider.ITableProvider>也必須公開的資料行和/或資料列標題關聯性每個子項目。 如需實作此控制項模式的控制項的範例，請參閱[控制項模式對應 UI 自動化用戶端的](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>實作方針和慣例  
 實作表格控制項模式時，請注意下列方針和慣例：  
  
-   個別儲存格的內容的存取權是透過二維的邏輯座標系統或需要同時實作所提供的陣列<xref:System.Windows.Automation.Provider.IGridProvider>。  
  
-   資料行或資料列標頭可以包含在資料表物件中，也可以是與資料表物件建立關係的個別標頭物件。  
  
-   資料行和資料列標頭可同時包含主要標頭和任何支援的標頭。  
  
> [!NOTE]
>  這個概念可以明顯看出中[!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)]試算表，其中使用者已定義的 「 名字 」 資料行。 此資料行現在有兩個標頭—使用者定義的「名字」標頭和應用程式指派給該資料行的英數字元指定。  
  
-   請參閱[實作 UI 自動化 Grid 控制項模式](../../../docs/framework/ui-automation/implementing-the-ui-automation-grid-control-pattern.md)方格相關功能。  
  
 ![包含複雜標頭項目的資料表。](../../../docs/framework/ui-automation/media/uia-tablepattern-complex-column-headers.PNG "UIA_TablePattern_Complex_Column_Headers")  
具有複雜資料行標頭的資料表範例  
  
 ![具有模稜兩可之 RowOrColumnMajor 屬性的資料表。](../../../docs/framework/ui-automation/media/uia-tablepattern-roworcolumnmajorproperty.PNG "UIA_TablePattern_RowOrColumnMajorProperty")  
具有模稜兩可之 RowOrColumnMajor 屬性的資料表範例  
  
<a name="Required_Members_for_ITableProvider"></a>   
## <a name="required-members-for-itableprovider"></a>ITableProvider 的必要成員  
 ITableProvider 介面需要下列屬性和方法。  
  
|必要成員|成員類型|備註|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.ITableProvider.RowOrColumnMajor%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.ITableProvider.GetColumnHeaders%2A>|方法|無|  
|<xref:System.Windows.Automation.Provider.ITableProvider.GetRowHeaders%2A>|方法|無|  
  
 此控制項模式沒有任何相關聯的事件。  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>例外狀況  
 此控制項模式沒有任何相關聯的例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [UI 自動化控制項模式概觀](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [支援 UI 自動化提供者的控制項模式](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [用戶端的 UI 自動化控制項模式](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [實作 UI 自動化 TableItem 控制項模式](../../../docs/framework/ui-automation/implementing-the-ui-automation-tableitem-control-pattern.md)   
 [實作 UI 自動化 Grid 控制項模式](../../../docs/framework/ui-automation/implementing-the-ui-automation-grid-control-pattern.md)   
 [UI 自動化樹狀目錄概觀](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [使用 UI 自動化中的快取](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)