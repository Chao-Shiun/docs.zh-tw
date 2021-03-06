---
title: "HOW TO：檢查或修改用戶端上的訊息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b8256335-f1c2-419f-b862-9f220ccad84c
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# HOW TO：檢查或修改用戶端上的訊息
您可以實作 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName> 並將它插入用戶端執行階段，以檢查或修改 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 用戶端內傳入或傳出的訊息。  如需詳細資訊，請參閱[擴充用戶端](../../../../docs/framework/wcf/extending/extending-clients.md)。  服務上對等的功能為 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName>。  如需完整的程式碼範例，請參閱 [訊息偵測器](../../../../docs/framework/wcf/samples/message-inspectors.md) 範例。  
  
### 檢查或修改訊息  
  
1.  實作 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName> 介面。  
  
2.  根據您要插入用戶端訊息偵測器的範圍，實作 <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName> 或 <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName>。  <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName> 允許您變更端點層級的行為。  <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName> 允許您變更合約層級的行為。  
  
3.  在 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=fullName> 上呼叫 <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=fullName> 方法前，請先插入行為。  如需詳細資訊，請參閱 [使用行為來設定與擴充執行階段](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## 範例  
 下列程式碼範例會依序顯示：  
  
-   用戶端偵測器實作。  
  
-   插入偵測器的端點行為。  
  
-   <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> 衍生類別，允許您在組態檔中加入行為。  
  
-   加入端點行為的組態檔，這個行為會將用戶端訊息偵測器插入用戶端執行階段中。  
  
```csharp  
// Client message inspector  
public class SimpleMessageInspector : IClientMessageInspector  
{  
    public void AfterReceiveReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
    {  
        // Implement this method to inspect/modify messages after a message  
        // is received but prior to passing it back to the client   
        Console.WriteLine("AfterReceiveReply called");  
    }  
  
    public object BeforeSendRequest(ref System.ServiceModel.Channels.Message request, IClientChannel channel)  
    {  
        // Implement this method to inspect/modify messages before they   
        // are sent to the service  
        Console.WriteLine("BeforeSendRequest called");  
        return null;  
    }  
}  
  
```  
  
```csharp  
// Endpoint behavior  
public class SimpleEndpointBehavior : IEndpointBehavior  
{  
    public void AddBindingParameters(ServiceEndpoint endpoint, System.ServiceModel.Channels.BindingParameterCollection bindingParameters)  
    {  
         // No implementation necessary  
    }  
  
    public void ApplyClientBehavior(ServiceEndpoint endpoint, ClientRuntime clientRuntime)  
    {  
        clientRuntime.MessageInspectors.Add(new SimpleMessageInspector());  
    }  
  
    public void ApplyDispatchBehavior(ServiceEndpoint endpoint, EndpointDispatcher endpointDispatcher)  
    {  
         // No implementation necessary  
    }  
  
    public void Validate(ServiceEndpoint endpoint)  
    {  
         // No implementation necessary  
    }  
}  
```  
  
```csharp  
// Configuration element   
public class SimpleBehaviorExtensionElement : BehaviorExtensionElement  
{  
    public override Type BehaviorType  
    {  
        get { return typeof(SimpleEndpointBehavior); }  
    }  
  
    protected override object CreateBehavior()  
    {  
         // Create the  endpoint behavior that will insert the message  
         // inspector into the client runtime  
        return new SimpleEndpointBehavior();  
    }  
}  
  
```  
  
```vb  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
    <system.serviceModel>  
        <client>  
            <endpoint address="http://localhost:8080/SimpleService/"   
                      binding="wsHttpBinding"  
                      contract="ServiceReference1.IService1"  
                      name="WSHttpBinding_IService1"/>  
        </client>  
  
      <behaviors>  
        <endpointBehaviors>  
          <behavior name="clientInspectorsAdded">  
            <simpleBehaviorExtension />  
          </behavior>  
        </endpointBehaviors>  
      </behaviors>  
      <extensions>  
        <behaviorExtensions>  
          <add  
            name="simpleBehaviorExtension"  
            type="SimpleServiceLib.SimpleBehaviorExtensionElement, Host, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null"/>  
        </behaviorExtensions>  
      </extensions>  
    </system.serviceModel>  
</configuration>  
  
```  
  
## 請參閱  
 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName>   
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName>   
 [使用行為來設定與擴充執行階段](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)