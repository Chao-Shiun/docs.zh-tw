---
title: ".NET Framework 使用者入門 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework，使用者入門"
  - "使用者入門 [.NET Framework]"
ms.assetid: c693fd34-88fe-4d90-b332-19eeadf3b7e7
caps.latest.revision: 35
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 29
---
# .NET Framework 使用者入門
.NET Framework 是執行階段執行環境，負責管理以 .NET Framework 為目標的應用程式。 它是由 Common Language Runtime 以及大量類別庫所組成，前者提供記憶體管理和其他系統服務，後者則可讓程式設計人員利用適用於應用程式開發所有主要範疇的強固、可靠程式碼。  
  
<a name="Introducing"></a>   
## 什麼是 .NET Framework？  
 .NET Framework 是 Managed 執行環境，可為執行的應用程式提供多樣的服務。 它是由兩個主要元件所組成：Common Language Runtime \(CLR\) 和 .NET Framework 類別庫，前者負責處理執行應用程式的執行引擎，後者為開發人員提供可在自己的應用程式中呼叫、通過測試且可重複使用的程式庫。 .NET Framework 提供用於執行應用程式的服務包括：  
  
-   記憶體管理。 在許多程式語言中，程式設計人員負責配置和釋放記憶體，以及處理物件存留期。 在 .NET Framework 應用程式中，CLR 會代表應用程式提供這些服務。  
  
-   一般類型系統。 在傳統的程式語言中，基本類型是由編譯器所定義，這會讓跨語言互通性變得很複雜。 在 .NET Framework 中，基底類型是由 .NET Framework 類型系統所定義，可在所有以 .NET Framework 為目標的語言之間通用。  
  
-   大量類別庫。 程式設計人員不再需要撰寫大量的程式碼來處理常見的低階程式設計作業，而能夠使用 .NET Framework 類別庫中可立即存取的類型程式庫及其成員。  
  
-   開發架構和技術。 .NET Framework 包含特定應用程式開發領域所需的程式庫，例如 Web 應用程式所需的 ASP.NET、資料存取所需的 ADO.NET，以及服務導向應用程式所需的 Windows Communication Foundation。  
  
-   語言互通性。 以 .NET Framework 為目標的語言編譯器會發出稱為通用中間語言 \(CIL\) 的中繼程式碼，這個程式碼接著會在執行階段由 Common Language Runtime 進行編譯。 有了這項功能，使用某一種語言撰寫的常式就能供其他語言存取，而且程式設計人員可以使用慣用的一種或多種語言專注地建立應用程式。  
  
-   版本相容性。 在極少數例外狀況下，使用某一特定 .NET Framework 版本開發的應用程式可不經修改直接在新版上執行。  
  
-   並存執行。 .NET Framework 允許在同一部電腦上存在多個版本的 Common Language Runtime，藉此協助解決版本衝突。 這表示，多個應用程式版本可以共存，而且應用程式可以在其建置所在的 .NET Framework 版本上執行。  
  
-   多目標。 藉由鎖定 .NET Framework 可攜式類別庫做為目標，開發人員就可以建立可在多個 .NET Framework 平台 \(例如 Windows 7、Windows 8、Windows 8.1、Windows 10、Windows Phone 和 Xbox 360\) 上運作的組件。  
  
<a name="ForUsers"></a>   
## 適用於使用者的 .NET Framework  
 如果您並未開發而是使用 .NET Framework 應用程式，就不需要具備任何有關 .NET Framework 或其作業的特定知識。 對使用者而言，.NET Framework 大致上是完全淺顯易懂的。  
  
 如果您使用的是 Windows 作業系統，您的電腦上可能已經安裝了 .NET Framework。 此外，如果您安裝的應用程式需要 .NET Framework，應用程式的安裝程式可能會在您的電腦上安裝特定的 .NET Framework 版本。 在某些情況下，您可能會看到對話方塊，要求您安裝 .NET Framework。 如果出現這個對話方塊時，您才剛嘗試執行應用程式，而且電腦可以存取網際網路，則可以前往網頁安裝遺漏的 .NET Framework 版本。  
  
 一般而言，您不應該解除安裝電腦上已安裝的任何 .NET Framework 版本。 不這麼做的原因有兩個：  
  
-   如果您使用的應用程式與特定版本的 .NET Framework 相關，移除該版本可能會損毀應用程式。  
  
-   有些 .NET Framework 版本是舊版的就地更新。 例如，[!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] 是 2.0 版的就地更新，而 .NET Framework 4.6 是 4、4.5、4.5.1 和 4.5.2 版的就地更新。 如需詳細資訊，請參閱 [.NET Framework 版本和相依性](../../../docs/framework/migration-guide/versions-and-dependencies.md)。  
  
 如果選擇移除 .NET Framework，請一律使用 \[控制台\] 中的 \[程式和功能\] 解除安裝。 請勿手動移除任何 .NET Framework 版本。  
  
 請注意，您可以在單一電腦上同時載入多個 .NET Framework 版本。 這表示，您不需要解除安裝舊版，就可以直接安裝新版。  
  
<a name="ForDevelopers"></a>   
## 適用於開發人員的 .NET Framework  
 如果您是開發人員，可以選擇任何支援 .NET Framework 的程式語言來建立應用程式。 由於 .NET Framework 提供語言獨立性和互通性，因此不論開發時使用的語言為何，您都可以與其他 .NET Framework 應用程式和元件互動。  
  
 若要開發 .NET Framework 應用程式或元件，請執行下列步驟：  
  
1.  安裝將做為應用程式目標的 .NET Framework 版本。 最新的產品版本是 [.NET Framework 4.6.1](http://go.microsoft.com/fwlink/?LinkId=671729)。 另外還有非常態 \(Out of Band\) 發行的其他 .NET Framework 套件。 如需這些套件的詳細資訊，請參閱 [.NET Framework 和 Out\-of\-Band 發行版本](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)。  
  
2.  選取您要用來開發應用程式的 .NET Framework 語言。 有多種語言可供選擇，包括 Microsoft 的 Visual Basic、C\#、Visual F\# 和 C\+\+  \(可讓您開發 .NET Framework 應用程式的程式語言會遵循[通用語言基礎結構 \(CLI\) 規格](http://go.microsoft.com/fwlink/?LinkId=199862)\)。 如需可用程式語言的清單，請參閱 [Visual Studio 語言](http://go.microsoft.com/fwlink/?LinkId=199863)。  
  
3.  選取並安裝您將用來建立應用程式，且支援您所選取程式語言的開發環境。 適用於 .NET Framework 應用程式的 Microsoft 整合式開發環境 \(IDE\) 為 [Visual Studio](http://go.microsoft.com/fwlink/?LinkId=325532)。 它提供了一些零售和免費版本。  
  
 如需有關開發以 .NET Framework 為目標之應用程式的詳細資訊，請參閱 [開發指南](../../../docs/framework/development-guide.md)。  
  
## 相關主題  
  
|標題|描述|  
|--------|--------|  
|[概觀](../../../docs/framework/get-started/overview.md)|為建置目標為 .NET Framework 之應用程式的開發人員提供詳細資訊。|  
|[.NET Framework 和 Out\-of\-Band 發行版本](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)|描述 .NET Framework 非常態 \(Out\-of\-Band\) 版本以及如何在您的應用程式中使用它們。|  
|[系統需求](../../../docs/framework/get-started/system-requirements.md)|列出執行 .NET Framework 的硬體及軟體需求。|  
|[.NET 的核心和開放原始碼](../../../docs/framework/get-started/net-core-and-open-source.md)|描述 .NET Core 的相關 .NET Framework 功能，以及如何存取開放原始碼 .NET Core 專案。|  
|[安裝指南](../../../docs/framework/install/guide-for-developers.md)|提供安裝 .NET Framework 的相關資訊。|  
  
## 請參閱  
 [.NET Framework 4.6 和 4.5](../Topic/.NET%20Framework%204.6%20and%204.5.md)   
 [新功能](../../../docs/framework/whats-new/index.md)   
 [.NET Framework 類別庫](http://go.microsoft.com/fwlink/?LinkId=227195)   
 [開發指南](../../../docs/framework/development-guide.md)