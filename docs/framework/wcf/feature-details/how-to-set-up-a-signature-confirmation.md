---
title: "HOW TO：設定簽章確認 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "簽章確認"
  - "WCF, 安全性"
ms.assetid: 2424c137-c7c2-4aa9-8d5d-a066e12fefda
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# HOW TO：設定簽章確認
「*簽章確認*」\(Signature confirmation\) 是訊息啟動器的機制，可確認收到的回覆已產生用來回應寄件者的原始訊息。簽章確認是定義在 WS\-Security 1.1 規格中。如果端點支援 WS\-Security 1.0，您就無法使用簽章確認。  
  
 下列程序會指定如何使用 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 啟用簽章確認。您可以搭配 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 使用相同的程序。這個程序是以 [HOW TO：使用 SecurityBindingElement 建立自訂繫結](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)中的基本步驟為基礎。  
  
### 若要在程式碼中啟用簽章確認  
  
1.  建立 <xref:System.ServiceModel.Channels.BindingElementCollection> 類別的執行個體。  
  
2.  建立 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 類別的執行個體。  
  
3.  將 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> 設定為 `true`。  
  
4.  將安全性項目新增至繫結集合中。  
  
5.  依 [HOW TO：使用 SecurityBindingElement 建立自訂繫結](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)中所指定的方式建立自訂繫結。  
  
### 若要在組態中啟用簽章確認  
  
1.  將 `<customBinding>` 項目新增至組態檔的 `<bindings>` 區段中。  
  
2.  新增 `<binding>` 項目，並將名稱屬性設為適當值。  
  
3.  新增適當的編碼項目。下列範例會新增 `<TextMessageEncoding>` 項目。  
  
4.  新增 `<security>` 子項目並將 `requireSignatureConfirmation` 屬性設定為 `true`。  
  
5.  選擇項，若要在啟動安裝期間啟用簽章確認，請新增 [\<secureConversationBootstrap\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) 子項目並將 `equireSignatureConfirmation` 屬性設定為 `true`。  
  
6.  新增適當的傳輸項目。下列範例會新增 [\<httpTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md)：  
  
    ```  
    <bindings>  
      <customBinding>  
        <binding name="SignatureConfirmationBinding">  
          <security requireSignatureConfirmation="true">  
            <secureConversationBootstrap requireSignatureConfirmation="true" />  
              </security>  
           <textMessageEncoding />  
             <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
## 範例  
 下列程式碼會建立 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 的執行個體，並將 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> 屬性設定為 `true`。請注意，這個範例並未使用之前範例中出現的 `<secureConversationBootstrap>` 項目，但會在使用 Windows \(Kerberos 通訊協定\) 權杖時示範簽章確認。在這種情況下，來自服務的所有回應中都會傳回用戶端的簽章，並且經由用戶端確認。  
  
 [!code-csharp[c_SignatureConfirmation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_signatureconfirmation/cs/source.cs#1)]
 [!code-vb[c_SignatureConfirmation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_signatureconfirmation/vb/source.vb#1)]  
  
## 請參閱  
 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A>   
 [HOW TO：使用 SecurityBindingElement 建立自訂繫結](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [HOW TO：為指定的驗證模式建立 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)