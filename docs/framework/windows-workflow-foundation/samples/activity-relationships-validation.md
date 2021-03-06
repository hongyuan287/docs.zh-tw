---
title: "活動關聯性驗證 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6f11a34e-ed67-4bce-88ce-7e96bbb4d052
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 活動關聯性驗證
這個範例包含三個活動：`CreateCity`、`CreateState` 和 `CreateCountry`。`CreateCity`必須在 `CreateState`活動內部，而 `CreateState` 必須在  `CreateCountry`活動內部。基於此範例的目的，`CreateState` 活動的驗證邏輯為程式碼形式，而 `CreateCity` 活動的驗證邏輯為 XAML 形式。這兩個條件約束有相同的行為。  
  
 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 提供下列三個協助程式活動，可讓開發人員驗證活動之間的關聯性。  
  
 <xref:System.Activities.Validation.GetParentChain>  
 提供屬於目前節點父系之所有活動的集合  
  
 <xref:System.Activities.Validation.GetChildSubtree>  
 提供屬於目前節點子樹狀結構之所有活動的集合，但排除目前節點  
  
 <xref:System.Activities.Validation.GetWorkflowTree>  
 提供和目前節點位於相同樹狀結構之所有活動的集合  
  
 在此範例中，<xref:System.Activities.Statements.ForEach%601> 活動是用來逐一查核 <xref:System.Activities.Validation.GetParentChain> 所傳回的集合。針對每個集合項目，其類型與 `CreateCountry` \(如果驗證 `CreateCity` 則為 `CreateState`\) 比較，如果找到相符項目，結果旗標會設為 `true`。最後，如果結果旗標設為 `false`，<xref:System.Activities.Validation.AssertValidation> 會用來產生驗證錯誤。  
  
### 若要使用這個範例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中開啟 ContainmentValidation.sln 範例方案。  
  
2.  建置方案。  
  
3.  按 CTRL\+F5 啟動程式。  
  
> [!IMPORTANT]
>  這些範例可能已安裝在您的電腦上。請先檢查下列 \(預設\) 目錄，然後再繼續：  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目錄不存在，請移至[用於 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 與 Windows Workflow Foundation \(WF\) 範例](http://go.microsoft.com/fwlink/?LinkId=150780)，以下載所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。此範例位於下列目錄：  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Validation\ActivityRelationships`  
  
## 請參閱