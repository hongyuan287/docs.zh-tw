---
title: "HOW TO：實作非同步服務作業 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e5d2ea5-d8f8-4712-bd18-ea3c5461702c
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# HOW TO：實作非同步服務作業
在 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 應用程式中，服務作業可以透過非同步或同步方式實作，不需規定用戶端呼叫服務作業的方式。例如，非同步服務作業可以利用同步方式呼叫，而同步服務作業可以透過非同步方式呼叫。如需顯示如何在用戶端應用程式內以非同步方式呼叫作業的範例，請參閱 [HOW TO：以非同步方式呼叫 WCF 服務作業](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)。[!INCLUDE[crabout](../../../includes/crabout-md.md)]非同步和同步作業的詳細資訊，請參閱[設計服務合約](../../../docs/framework/wcf/designing-service-contracts.md)和[同步和非同步作業](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)。本主題描述非同步服務作業的基本結構，程式碼尚未完成。如需服務與用戶端兩者的完整範例，請參閱[Asynchronous](http://msdn.microsoft.com/zh-tw/833db946-f511-4f64-a26f-2759a11217c7)。  
  
### 以非同步方式實作服務作業  
  
1.  在您的服務合約中，根據 .NET 非同步設計方針宣告一個非同步方法組。`Begin` 方法可接受一個參數、回呼物件和狀態物件，並傳回 <xref:System.IAsyncResult?displayProperty=fullName> 和對應的 `End` 方法，該方法會接受 <xref:System.IAsyncResult?displayProperty=fullName> 並傳回其傳回值。如需非同步呼叫的詳細資訊，請參閱[非同步程式設計模式](http://go.microsoft.com/fwlink/?LinkId=248221)。  
  
2.  使用 <xref:System.ServiceModel.OperationContractAttribute?displayProperty=fullName> 屬性 \(Attribute\) 來標記非同步方法組中的 `Begin` 方法，並將 <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A?displayProperty=fullName> 屬性 \(Property\) 設定為 `true`。例如，下列程式碼會執行步驟 1 和 2。  
  
     [!code-csharp[C_SyncAsyncClient#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#6)]
     [!code-vb[C_SyncAsyncClient#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#6)]  
  
3.  根據非同步設計方針，在您的服務類別內實作 `Begin/End` 方法組。例如，下列程式碼範例會顯示利用非同步服務作業的 `Begin` 和 `End` 兩個部分，將字串寫入主控台的實作，以及傳回用戶端之 `End` 作業的傳回值。如需完整的程式碼範例，請參閱＜範例＞一節。  
  
     [!code-csharp[C_SyncAsyncClient#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#3)]
     [!code-vb[C_SyncAsyncClient#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#3)]  
  
## 範例  
 下列程式碼範例會顯示：  
  
1.  服務合約介面，其中具有：  
  
    1.  一個同步 `SampleMethod` 作業。  
  
    2.  一個非同步 `BeginSampleMethod` 作業。  
  
    3.  一個非同步 `BeginServiceAsyncMethod`\/`EndServiceAsyncMethod` 作業組。  
  
2.  一個使用 <xref:System.IAsyncResult?displayProperty=fullName> 物件的服務實作。  
  
 [!code-csharp[C_SyncAsyncClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#1)]
 [!code-vb[C_SyncAsyncClient#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#1)]  
  
## 請參閱  
 [設計服務合約](../../../docs/framework/wcf/designing-service-contracts.md)   
 [同步和非同步作業](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)