---
title: "210 - MessageThrottleExceeded | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24ca08ea-c11c-4753-946e-98aa820f8711
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 210 - MessageThrottleExceeded
## 屬性  
  
|||  
|-|-|  
|ID|210|  
|關鍵字|EndToEndMonitoring，HealthMonitoring，Troubleshooting，ServiceModel|  
|層級|Warning|  
|通道|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## 描述  
 有三個主要的服務節流閥，只要其中一個超出，則會發出此事件。請注意，此事件只有在節流閥限制初次超過時才會發出。例如，假設同時呼叫的節流閥限制是 10，則第 11 個同時呼叫會引起 `MessageThrottleExceeded` 事件。第 12 個呼叫不會引起另一個事件。此外，為了避免太多事件資料流，在限制範圍附近的活動並不會造成另一個事件。在此範例中，如果有數個呼叫完成，就會有 9 個同時呼叫。如果後續又有兩個呼叫，目前的值會再變成 11。這並不會引起另一個事件。當目前的值降至節流閥限制的 70%，就會發出不同的事件，指出活動已經減慢。未來超出限制的活動，將會引起另一個 `MessageThrottleExceeded` 事件發出。在此範例中，如果同時呼叫的數量降到 7 個，然後再次達到 11 個，就會發出另一個 `MessageThrottleExceeded` 事件。  
  
## 訊息  
 已達到 '%1' 的節流閥限制 '%2'。  
  
## 詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|------------|------------|--------|  
|節流閥名稱|`xs:string`|已超出的節流閥名稱。`MaxConcurrentCalls`、`MaxConcurrentInstances` 或 `MaxConcurrentSessions`。|  
|限制|`xs:long`|目前設定的節流閥限制。|  
|HostReference|`xs:string`|若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。其格式定義為 'Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'。範例：'Default Web Site\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|