---
title: "設定 HTTP 和 HTTPS | Microsoft Docs"
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
  - "設定 HTTP [WCF]"
ms.assetid: b0c29a86-bc0c-41b3-bc1e-4eb5bb5714d4
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 設定 HTTP 和 HTTPS
WCF 服務與用戶端可以透過 HTTP 和 HTTPS 進行通訊。  HTTP\/HTTPS 設定是使用 Internet Information Services \(IIS\)，或使用命令列工具設定。  在 IIS HTTP 或 HTTPS 之下裝載 WCF 服務時，設定可以在 IIS \(使用 inetmgr.exe 工具\) 內進行。  如果是自我裝載的 WCF 服務，可以使用命令列工具設定 HTTP 或 HTTPS 設定。  
  
 您至少需要設定 URL 註冊，並針對您的服務將要使用的 URL 加入防火牆例外狀況。  
  
 設定 HTTP 設定值所使用的工具取決於電腦執行的作業系統。  
  
 執行 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 或 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 時，請使用 HttpCfg.exe 工具。  [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 會自動安裝這項工具。  執行 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 時，您可以在 [Windows XP Service Pack 2 支援工具](http://go.microsoft.com/fwlink/?LinkId=88606)下載此工具。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Httpcfg 概觀](http://go.microsoft.com/fwlink/?LinkId=88605)。  
  
 執行 [!INCLUDE[wv](../../../../includes/wv-md.md)] 或 Windows 7 時，您可以透過 Netsh.exe 工具來設定這些設定。  
  
## 設定命名空間保留區  
 命名空間保留區會將一部分 HTTP URL 命名空間的權限指派給特定的使用者群組。  保留區會授予這些使用者建立服務的權限，以接聽那一部分的命名空間。  保留區是 URL 前置詞，也就是說，保留區可涵蓋保留路徑的所有子路徑。  命名空間保留區允許兩種使用萬用字元的方式。  HTTP 伺服器 API 文件說明[使用萬用字元的命名空間宣告之解析順序](http://go.microsoft.com/fwlink/?LinkId=94841)。  
  
 執行中的應用程式可以建立類似的要求來新增命名空間註冊區。  註冊區與保留區會競爭使用命名空間的各個部分。  根據[使用萬用字元的命名空間宣告之解析順序](http://go.microsoft.com/fwlink/?LinkId=94841)一文中對解析順序的說法，保留區會比註冊區優先。  在此情況中，保留區會封鎖執行中的應用程式，使其無法接收要求。  
  
### 執行 Windows XP 或 Server 2003  
 請使用 `httpcfg.exe set urlacl` 命令來變更命名空間保留區。  [Windows 支援工具文件](http://go.microsoft.com/fwlink/?LinkId=94840)會說明 Httpcfg.exe 工具的語法。  您需要系統管理員權限或是某個命名空間部分的擁有權，才能修改該部分命名空間的保留區使用權限。  一開始，整個 HTTP 命名空間都屬於本機系統管理員。  
  
 下列將說明搭配 `set urlacl` 選項的 Httpcfg 命令語法  
  
```  
httpcfg set urlacl /u {http://URL:Port/ | https://URL:Port/} /aACL  
  
```  
  
 使用 `/u` 時，需要 `set urlacl` 參數。  您需要一個包含完整 URL 的字串做為所設定之保留區的記錄識別碼。  
  
 使用 `/a` 時，同樣需要 `set urlacl` 參數。  您需要包含存取控制清單 \(ACL\) 且為 Security Descriptor Definition Language \(SDDL\) 字串格式的字串。  
  
 下列範例示範此命令的使用方式。  
  
```  
httpcfg.exe set urlacl /u http://myhost:8000/ /a "O:AOG:DAD:(A;;RPWPCCDCLCSWRCWDWOGA;;;S-1-0-0)"  
  
```  
  
### 執行 Windows Vista、Windows Server 2008 R2 或 Windows 7  
 如果您是在 [!INCLUDE[wv](../../../../includes/wv-md.md)]、Windows Server 2008 R2 或 Windows 7 上執行，請使用 Netsh.exe 工具。  下列範例示範此命令的使用方式。  
  
```  
netsh http add urlacl url=http://+:80/MyUri user=DOMAIN\user  
  
```  
  
 這個命令會針對 DOMAIN\\使用者帳戶之指定的 URL 命名空間，加入 URL 保留項目。  如需使用 netsh 命令的詳細資訊，請在命令提示字元下輸入 “netsh http add urlacl”，然後按 enter。  
  
## 設定防火牆例外狀況  
 對透過 HTTP 通訊的 WCF 服務進行自我裝載時，您必須將例外狀況加入至防火牆組態中，以允許使用特殊 URL 的傳入連線。  如需詳細資訊，請參閱[在 Windows 防火牆中開啟連接埠 \(Windows 7\)](http://go.microsoft.com/fwlink/?LinkId=239961)  
  
## 設定 SSL 憑證  
 Secure Sockets Layer \(SSL\) 通訊協定會在用戶端與伺服器上使用憑證來儲存加密金鑰。  伺服器會在連線期間提供自己的 SSL 憑證，方便用戶端驗證伺服器的身分識別。  伺服器也可以向用戶端要求憑證，以便連線的雙方進行互相驗證。  
  
 憑證會依據 IP 位址與連線的連接埠號碼，儲存在集中保管的存放區。  特殊 IP 位址 0.0.0.0 會符合本機電腦的任何 IP 位址。  請注意，憑證存放區無法依照路徑來識別 URL。  包含相同 IP 位址與連接埠號碼組合的服務必須共用憑證，就算每項服務之 URL 中的路徑都不一樣也需這麼做。  
  
 如需逐步指示，請參閱[HOW TO：使用 SSL 憑證設定連接埠](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)。  
  
## 設定 IP 接聽清單  
 一旦使用者註冊了 URL，HTTP 伺服器 API 只會繫結至 IP 位址與連接埠。  根據預設，HTTP 伺服器 API 會針對電腦中的所有 IP 位址繫結至其 URL 中的連接埠。  如果不使用 HTTP 伺服器 API 的應用程式先前已經繫結至該 IP 位址與連接埠的組合，就會產生衝突情況。  IP 接聽清單可允許所有 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務和使用某些電腦 IP 位址之連接埠的應用程式共存在一起。  如果 IP 接聽清單包含任何項目，則 HTTP 伺服器 API 只會繫結至清單所指定的特定 IP 位址。  您需要系統管理員權限才能修改 IP 接聽清單。  
  
### 執行 Windows XP 或 Server 2003  
 請使用 httpcfg 工具來修改 IP 接聽清單，如下列範例所示。  [Windows 支援工具文件](http://go.microsoft.com/fwlink/?LinkId=94840)會說明 httpcfg.exe 工具的語法。  
  
```  
httpcfg.exe set iplisten -i 0.0.0.0:8000  
```  
  
### 執行 Windows Vista 或 Windows 7  
 請使用 netsh 工具來修改 IP 接聽清單，如下列範例所示。  
  
```  
netsh http add iplisten ipaddress=0.0.0.0:8000  
```  
  
## 其他組態設定  
 使用 <xref:System.ServiceModel.WsDualHttpBinding> 時，用戶端連線會使用與命名空間保留區及 Windows 防火牆相容的預設值。  如果您選擇自訂雙向連線的用戶端基底位址，則您必須同時在用戶端上設定這些 HTTP 設定值以符合新的位址。  
  
 HTTP 伺服器 API 內含的一些進階組態設定無法透過 HttpCfg 取得。  這些設定會維護在登錄中，並套用至所有在系統中使用 HTTP 伺服器 API 的應用程式。  如需這些設定的詳細資訊，請參閱 [IIS 的 Http.sys 登錄設定](http://go.microsoft.com/fwlink/?LinkId=94843)。  大部分的使用者應該都不需要變更這些設定值。  
  
## Windows XP 的特定問題  
 IIS 不支援在 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 上共用連接埠。  如果 IIS 正在執行，而且 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務嘗試使用帶有相同連接埠的命名空間，則 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務會無法啟動。  IIS 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 都預設為使用連接埠 80。  請針對其中一項服務變更其連接埠指派，或是使用 IP 接聽清單將 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務指派給 IIS 不使用的網路介面卡。  IIS 6.0 \(含\) 以後版本已經重新設計，可以使用 HTTP 伺服器 API。  
  
## 請參閱  
 <xref:System.ServiceModel.WsDualHttpBinding>   
 [HOW TO：使用 SSL 憑證設定連接埠](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)