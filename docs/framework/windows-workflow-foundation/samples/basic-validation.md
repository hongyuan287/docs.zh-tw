---
title: "基本驗證 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba1343cc-aaab-4ade-b0c0-1dd5063bf4ad
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 基本驗證
這個範例包含 `CreateProduct` 活動，會驗證其 `Cost` 引數小於或等於其 `Price` 引數。  
  
## 範例詳細資料  
 有兩個作者會使用驗證：建立活動驗證邏輯的活動作者，以及在特定工作流程上呼叫驗證服務的工作流程作者。在這個案例中，活動作者想要強制每個活動執行個體的成本必須小於或等於價格。  
  
 活動作者 \(在活動中\) 必須：  
  
-   建立條件約束 \(`PriceGreaterThanCost`\)。這是所有驗證邏輯的所在位置。  
  
-   覆寫 <xref:System.Activities.CodeActivity%601.OnGetConstraints%2A>，並將條件約束 \(`PriceGreaterThanCost`\) 加入至條件約束 <xref:System.Collections.IList>。  
  
 工作流程作者 \(主程式\) 必須：  
  
-   建立具有要驗證之活動執行個體 \(`CreateProduct`\) 的工作流程。  
  
-   呼叫 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>，傳回 <xref:System.Activities.Validation.ConstraintViolation> 的 <xref:System.Activities.Validation.ValidationResults> 集合。  
  
-   \(選擇性\) 列印 <xref:System.Activities.Validation.ConstraintViolation> 物件。  
  
#### 若要安裝、建置及執行範例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中開啟 BasicValidation.sln 範例方案。  
  
2.  建置及執行此方案。  
  
> [!IMPORTANT]
>  這些範例可能已安裝在您的電腦上。請先檢查下列 \(預設\) 目錄，然後再繼續。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目錄不存在，請移至[用於 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 與 Windows Workflow Foundation \(WF\) 範例](http://go.microsoft.com/fwlink/?LinkId=150780)，以下載所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。此範例位於下列目錄。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Validation\BasicValidation`  
  
## 請參閱