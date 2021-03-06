---
title: "&lt;篩選條件&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 37a87222-ec78-4728-8105-9ca1bd961f0c
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;篩選條件&gt;
`filters` 項目含有 XPath 篩選條件的集合，用於控制記錄何種訊息。  
  
 篩選條件只會於套用傳輸層，指定方式是將 `logMessagesAtTransportLevel` 設定為 `true`。  服務等級和格式錯誤訊息記錄不受篩選條件的影響。  
  
 若要將篩選條件加入至集合，請使用 `add` 關鍵字。  當定義一個或多個篩選條件時，只會記錄符合至少其中一個篩選條件的訊息。  如果沒有定義篩選條件，所有訊息都會通過。  
  
 篩選條件支援完整的 XPath 語法，並依其出現在組態檔中的順序套用。  語法不正確的篩選條件會造成組態例外狀況。  
  
 下列範例示範如何設定只記錄含有 SOAP 標頭區段之訊息的篩選條件。  
  
```  
<messageLogging logEntireMessage="true"  
     logMalformedMessages="true" logMessagesAtServiceLevel="true"  
     logMessagesAtTransportLevel="true" maxMessagesToLog="420”>  
     <filters>  
        <add xmlns:soap="http://www.w3.org/2003/05/soap-envelope">  
                        /soap:Envelope/soap:Headers  
        </add>  
     </filters>  
</messageLogging>  
```  
  
## 請參閱  
 <xref:System.ServiceModel.Configuration.DiagnosticSection>   
 <xref:System.ServiceModel.Diagnostics>   
 <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A>   
 <xref:System.ServiceModel.Configuration.MessageLoggingElement>   
 <xref:System.ServiceModel.Configuration.MessageLoggingElement.Filters%2A>   
 <xref:System.ServiceModel.Configuration.XpathMessageFilterElementCollection>   
 <xref:System.ServiceModel.Configuration.XpathMessageFilterElement>   
 <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>   
 [設定訊息記錄](../../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md)   
 [設定訊息記錄](../../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md)   
 [\<messageLogging\>](../../../../../docs/framework/configure-apps/file-schema/wcf/messagelogging.md)