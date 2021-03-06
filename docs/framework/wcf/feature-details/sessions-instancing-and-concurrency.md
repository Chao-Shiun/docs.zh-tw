---
title: "工作階段、執行個體與並行 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 50797a3b-7678-44ed-8138-49ac1602f35b
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 工作階段、執行個體與並行
「*工作階段*」\(Session\) 是兩個端點之間所傳送之所有訊息的相互關聯。 「*執行個體*」\(Instancing\) 是指控制使用者定義之服務物件的存留時間，以及其相關的 <xref:System.ServiceModel.InstanceContext> 物件。 「*並行*」\(Concurrency\) 是指控制在 <xref:System.ServiceModel.InstanceContext> 中同時執行的執行緒數目。  
  
 本主題將說明這些設定、這些設定的使用方式，以及這些設定間的各種互動。  
  
## 工作階段  
 當服務合約將 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName> 屬性設定為 <xref:System.ServiceModel.SessionMode?displayProperty=fullName> 時，該合約會指出所有的呼叫 \(即支援呼叫的基礎訊息交換模式\) 必須是同一個對話的一部分。 如果合約指定其允許工作階段，但不需要工作階段，則用戶端可以連線，並選擇是否要建立工作階段。 如果工作階段終止並透過相同之工作階段型的通道傳送訊息，就會擲回例外狀況。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 工作階段在概念上有下列主要特色：  
  
-   工作階段是由呼叫的應用程式明確地初始化及終止。  
  
-   工作階段期間傳遞的訊息是依其接收的順序進行處理。  
  
-   工作階段會將一群訊息互相關聯為對話。 此相互關聯的意義是一種抽象概念。 例如，某個工作階段架構通道可能會根據共用的網路連線將訊息相互關聯，而另一個工作階段架構通道可能會根據訊息本文內的共用標記將訊息相互關聯。 這些可以衍生自工作階段的功能視相互關聯的本質而定。  
  
-   沒有與 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 工作階段關聯的一般資料存放區。  
  
 如果您很熟悉 <xref:System.Web.SessionState.HttpSessionState?displayProperty=fullName> 應用程式內的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 類別及其所提供的功能，則您可能會注意到這類工作階段和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 工作階段之間有下列不同之處：  
  
-   [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 工作階段一律由伺服器啟動。  
  
-   [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 工作階段具有隱含未排序特性。  
  
-   [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 工作階段提供了跨要求的一般資料儲存機制。  
  
 用戶端應用程式和服務應用程式會以不同的方式與工作階段互動。 用戶端應用程式會初始化工作階段，接著並接收及處理在工作階段內傳送的訊息。 服務應用程式可以將工作階段當做擴充點使用，以便加入其他行為。 其做法是直接使用 <xref:System.ServiceModel.InstanceContext> 或實作自訂的執行個體內容提供者。  
  
## 執行個體  
 執行個體行為 \(使用 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> 屬性設定\) 會控制 <xref:System.ServiceModel.InstanceContext> 對傳入訊息建立回應的方法。 根據預設，每一個 <xref:System.ServiceModel.InstanceContext> 都會與一個使用者定義的服務物件產生關聯，因此 \(在預設的情形下\) 設定 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 屬性也會控制使用者定義之服務物件執行個體。<xref:System.ServiceModel.InstanceContextMode> 列舉型別 \(Enumeration\) 會定義執行個體模式。  
  
 以下為可用的執行個體模式：  
  
-   <xref:System.ServiceModel.InstanceContextMode>：為每個用戶端要求所建立的新 <xref:System.ServiceModel.InstanceContext> \(因此為服務物件\)。  
  
-   <xref:System.ServiceModel.InstanceContextMode>：為每個新用戶端工作階段所建立的新 <xref:System.ServiceModel.InstanceContext> \(因此為服務物件\)，並維持該工作階段的存留期 \(這麼做需要支援工作階段的繫結\)。  
  
-   <xref:System.ServiceModel.InstanceContextMode>：單一的 <xref:System.ServiceModel.InstanceContext> \(因此為服務物件\)，負責處理所有應用程式之存留期的用戶端要求。  
  
 下列程式碼範例示範預設的 <xref:System.ServiceModel.InstanceContextMode> 值，在服務類別上會明確地設定 <xref:System.ServiceModel.InstanceContextMode>。  
  
```  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]   
public class CalculatorService : ICalculatorInstance   
{   
    ...  
}  
```  
  
 當 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> 屬性控制釋放 <xref:System.ServiceModel.InstanceContext> 的頻率時，<xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=fullName> 和 <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A?displayProperty=fullName> 屬性會控制釋放服務物件的時機。  
  
### 已知的單一服務  
 單一執行個體服務物件的其中一個變化有時可能會很有用處：您可以自行建立服務物件，並建立使用該物件的服務主機。 若要這麼做，您必須同時將 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> 屬性設定為 <xref:System.ServiceModel.InstanceContextMode>，否則在開啟服務主機時會擲回例外狀況。  
  
 請使用 [ServiceHost.ServiceHost\(Object, Uri\<xref:System.ServiceModel.ServiceHost.%23ctor%28System.Object%2CSystem.Uri%5B%5D%29?displayProperty=fullName> 建構函式建立此類服務。 當您想要將特定物件執行個體提供給單一服務使用時，它提供了另一種實作自訂 <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer?displayProperty=fullName> 的方式。 當服務實作類型很難建構時 \(例如，無法實作沒有參數的預設公用建構函式時\)，您可以使用這個多載。  
  
 請注意，提供物件給這個建構函式時，某些與 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 執行個體行為相關的功能會以不同的方式運作。 例如，提供單一物件執行個體時，呼叫 <xref:System.ServiceModel.InstanceContext.ReleaseServiceInstance%2A?displayProperty=fullName> 將沒有任何作用。 同樣的，也會忽略任何其他執行個體的釋放機制。<xref:System.ServiceModel.ServiceHost> 的行為就像是所有作業都已將 <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=fullName> 屬性設定為 <xref:System.ServiceModel.ReleaseInstanceMode?displayProperty=fullName>。  
  
### 共用 InstanceContext 物件  
 您也可以自行執行該關聯，以控制哪個工作階段通道或呼叫應與哪個 <xref:System.ServiceModel.InstanceContext> 物件產生關聯。  
  
## 並行  
 並行是指控制在 <xref:System.ServiceModel.InstanceContext> 內同時為作用中的執行緒數目。 這是透過使用 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=fullName> 與 <xref:System.ServiceModel.ConcurrencyMode> 列舉型別的方式予以控制。  
  
 以下為可用的三種並行模式：  
  
-   <xref:System.ServiceModel.ConcurrencyMode>：每一個執行個體內容同時最多可以在執行個體內容中，擁有一個處理訊息的執行緒。 其他希望使用相同執行個體內容的執行緒必須封鎖，直到原始的執行緒結束執行個體內容為止。  
  
-   <xref:System.ServiceModel.ConcurrencyMode>：每一個服務執行個體都可以同時擁有多個處理訊息的執行緒。 此服務實作必須是安全執行緒，才能使用這種並行模式。  
  
-   <xref:System.ServiceModel.ConcurrencyMode>：每一個服務執行個體在同一時間內會處理一個訊息，但接受可重新進入 \(Re\-entrant\) 的作業呼叫。 此服務只在其透過 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 用戶端物件向外呼叫時，才會接受這些呼叫。  
  
> [!NOTE]
>  您應該了解，開發能夠安全地使用一個以上之執行緒的程式碼，可能會很難順利地撰寫。 在使用 <xref:System.ServiceModel.ConcurrencyMode> 或 <xref:System.ServiceModel.ConcurrencyMode> 值之前，請確定已適當地設計您的服務以使用這些模式[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>.  
  
 並存的使用與執行個體模式有關。 在 <xref:System.ServiceModel.InstanceContextMode>``執行個體中，與並存沒有任何相關，因為每個訊息都是由新的 <xref:System.ServiceModel.InstanceContext> 所處理，因此 <xref:System.ServiceModel.InstanceContext> 內不會有一個以上的使用中執行緒。  
  
 下列程式碼會示範將 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> 屬性設定為 <xref:System.ServiceModel.ConcurrencyMode>。  
  
```  
[ServiceBehavior(ConcurrencyMode=ConcurrencyMode.Multiple, InstanceContextMode = InstanceContextMode.Single)]   
public class CalculatorService : ICalculatorConcurrency   
{   
    ...  
}  
  
```  
  
## 與 InstanceContext 設定互動的工作階段  
 工作階段和 <xref:System.ServiceModel.InstanceContext> 會根據合約內 <xref:System.ServiceModel.SessionMode> 列舉型別值的組合以及服務實作上的 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> 屬性而進行互動，以控制通道與特定服務物件的關聯。  
  
 下表根據服務的 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName> 屬性與 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> 屬性等值的組合，說明支援工作階段或不支援工作階段之傳入通道的結果。  
  
|InstanceContextMode 值|<xref:System.ServiceModel.SessionMode>|<xref:System.ServiceModel.SessionMode>|<xref:System.ServiceModel.SessionMode>|  
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|  
|PerCall|-   工作階段通道的行為：工作階段與每個呼叫的 <xref:System.ServiceModel.InstanceContext>。<br />-   無工作階段通道的行為：擲回例外狀況。|-   工作階段通道的行為：工作階段與每個呼叫的 <xref:System.ServiceModel.InstanceContext>。<br />-   無工作階段通道的行為：每個呼叫的 <xref:System.ServiceModel.InstanceContext>。|-   工作階段通道的行為：擲回例外狀況。<br />-   無工作階段通道的行為：每個呼叫的 <xref:System.ServiceModel.InstanceContext>。|  
|PerSession|-   工作階段通道的行為：工作階段與每個通道的 <xref:System.ServiceModel.InstanceContext>。<br />-   無工作階段通道的行為：擲回例外狀況。|-   工作階段通道的行為：工作階段與每個通道的 <xref:System.ServiceModel.InstanceContext>。<br />-   無工作階段通道的行為：每個呼叫的 <xref:System.ServiceModel.InstanceContext>。|-   工作階段通道的行為：擲回例外狀況。<br />-   無工作階段通道的行為：每個呼叫的 <xref:System.ServiceModel.InstanceContext>。|  
|Single|-   工作階段通道的行為：單一工作階段與所有呼叫的單一 <xref:System.ServiceModel.InstanceContext>。<br />-   無工作階段通道的行為：擲回例外狀況。|-   工作階段通道的行為：工作階段與每個所建立或使用者指定之單一個體的 <xref:System.ServiceModel.InstanceContext>。<br />-   無工作階段通道的行為：每個所建立或使用者指定之單一個體的 <xref:System.ServiceModel.InstanceContext>。|-   工作階段通道的行為：擲回例外狀況。<br />-   無工作階段通道的行為：每個所建立之單一個體或使用者指定之單一個體的 <xref:System.ServiceModel.InstanceContext>。|  
  
## 請參閱  
 [使用工作階段](../../../../docs/framework/wcf/using-sessions.md)   
 [HOW TO：建立需要工作階段的服務](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)   
 [HOW TO：控制服務執行個體](../../../../docs/framework/wcf/feature-details/how-to-control-service-instancing.md)   
 [並行](../../../../docs/framework/wcf/samples/concurrency.md)   
 [執行個體](../../../../docs/framework/wcf/samples/instancing.md)   
 [工作階段](../../../../docs/framework/wcf/samples/session.md)