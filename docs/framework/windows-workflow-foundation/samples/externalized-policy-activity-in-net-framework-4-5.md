---
title: ".NET Framework 4.5 中的外顯化原則活動 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92fd6f92-23a1-4adf-b96a-2754ea93ad3e
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# .NET Framework 4.5 中的外顯化原則活動
這個範例示範 ExternalizedPolicy4 活動如何直接使用 WF 3.5 隨附的規則引擎，以便在 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)][!INCLUDE[wf2](../../../../includes/wf2-md.md)] \(WF 4.5\) 中執行現有的 [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)][!INCLUDE[wf2](../../../../includes/wf2-md.md)] \(WF 3.5\) <xref:System.Workflow.Activities.Rules.RuleSet> 物件。您可以使用這個活動來開啟及執行任何現有的 WF 3.5 <xref:System.Workflow.Activities.Rules.RuleSet>。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]包含在 Windows Workflow Foundation 中之 WF 3.5 規則引擎的詳細資訊，請參閱[Windows Workflow Foundation Rules Engine 簡介](http://go.microsoft.com/fwlink/?LinkId=166079)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] 中的 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 移轉規則，請參閱 [移轉指引](../../../../docs/framework/windows-workflow-foundation//migration-guidance.md) 的移轉指引。  
  
## 這個範例中的專案  
  
||||  
|-|-|-|  
|專案名稱|說明|主要檔案|  
|ExternalizedPolicy4|包含 ExternalizedPolicy4 活動及其 WF 4.5 設計工具。|**ExternalizedPolicy4.cs**：活動定義。<br /><br /> **ExternalizedPolicy4Designer.xaml**：ExternalizedPolicy4 活動的自訂設計工具。它使用 WF 3.5 規則引擎中的規則編輯器 \(<xref:System.Workflow.Activities.Rules.Design.RuleSetDialog>\)。|  
|ImperativeCodeClientSample|範例用戶端應用程式，透過使用命令式 C\# 程式碼 \(未使用設計工具\) 的 ExternalizedPolicy4 應用程式，來設定及執行工作流程。|**ApplyDiscount.rules**：具有 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 規則定義的檔案。<br /><br /> **Order.cs**：代表客戶訂單的類型。規則套用至這個類型的物件。<br /><br /> **Program.cs**：設定及執行工作流程，其中有 Policy4 活動會將 ApplyDiscount.rules 中定義的規則套用至 Order 物件執行個體。<br /><br /> App.config：具有規則檔路徑的組態檔。|  
|DesignerClientSample|範例用戶端應用程式，透過使用 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 設計工具的 ExternalPolicy4 應用程式，來設定及執行工作流程。|**Sequence1.xaml**：使用 Policy4 活動執行規則評估的循序工作流程。<br /><br /> **Program.cs**：執行 Sequence1.xaml 中定義的工作流程執行個體。|  
  
## ExternalizedPolicy4 活動  
 ExternalizedPolicy4 活動是 <xref:System.Activities.NativeActivity>，允許在 WF 4.5 工作流程中執行 WF 3.5 <xref:System.Workflow.Activities.Rules.RuleSet> 物件。下列範例是活動的公用物件模型簡化定義。  
  
```  
public class ExternalizedPolicy4Activity<TResult>: CodeActivity  
{  
    public string RulesFilePath   
  
    public string RuleSetName           
  
    [RequiredArgument]  
    public InArgument<T> TargetObject   
  
    [RequiredArgument]  
    public OutArgument<T> ResultObject   
  
    public OutArgument<ValidationErrorCollection> ValidationErrors   
}  
```  
  
|||  
|-|-|  
|屬性|說明|  
|RuleSetFilePath|當活動執行時，要評估之 .NET Framework 3.5 <xref:System.Workflow.Activities.Rules.RuleSet> 檔案的路徑。|  
|RuleSetName|.rules 檔案中使用之 <xref:System.Workflow.Activities.Rules.RuleSet> 的名稱。|  
|TargetObject|評估 <xref:System.Workflow.Activities.Rules.RuleSet> 中之 <xref:System.Workflow.Activities.Rules.Rule> 物件的目標物件。|  
|ResultObject|套用規則之後的結果物件 \(例如，對 Input 引數套用規則後，結果會儲存在 Result 引數中\)。|  
|ValidationError|執行前對目標物件驗證 <xref:System.Workflow.Activities.Rules.RuleSet> 時，WF 3.5 規則引擎傳回的驗證錯誤清單。|  
  
## ExternalizedPolicy4 活動設計工具  
 ExternalizedPolicy4 設計工具讓您不需要撰寫程式碼，即可設定活動使用現有的 RuleSet。只要設定 .rules 檔案所在路徑，並指定您要使用的 <xref:System.Workflow.Activities.Rules.RuleSet> 名稱。它也可以讓您修改 <xref:System.Workflow.Activities.Rules.RuleSet>。在建置方案之後，可在工具箱的 Microsoft.Samples.Activities.Rules 區段中找到它。此設計工具可讓您選取 .rules 檔案和 <xref:System.Workflow.Activities.Rules.RuleSet>。按一下 \[**Edit RuleSet**\] 按鈕時，就會顯示 WF 3.5 <xref:System.Workflow.Activities.Rules.Design.RuleSetDialog>。這個對話方塊是重新裝載的 WF 3.5 規則編輯器，可用來檢視及編輯 ExternalizedPolicy4 活動執行的規則。  
  
## Policy4 和 ExternalPolicy4  
 [.NET Framework 4.5 中的原則活動](../../../../docs/framework/windows-workflow-foundation/samples/policy-activity-in-net-framework-4-5.md)活動可讓您在 WF 4.5 工作流程中建立及執行 .NET Framework 3.5 RuleSet。<xref:System.Workflow.Activities.Rules.RuleSet> 已序列化，內嵌於 Policy4 活動 XAML 定義中。ExternalizedPolicy4 範例示範如何使用現有的外部 <xref:System.Workflow.Activities.Rules.RuleSet> \(包含在 .rules 檔案中\)。  
  
## 使用這個範例  
 不需要特殊設定即可執行此範例。在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中開啟方案，然後按 F5 執行應用程式。  
  
 這個範例包含兩個用戶端應用程式：ImperativeCodeClientSample 和 DesignerClientSample。ImperativeCodeClientSample 用戶端示範如何透過 C\# 命令式程式碼來設定及執行 ExternalizedPolicy4 活動。DesignerClientSample 示範如何透過設計工具來設定及執行 ExternalizedPolicy4 活動。  
  
#### 若要執行 ImperativeCodeClientSample 應用程式  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 開啟 Policy4sample.sln 方案檔案。  
  
2.  在 \[**方案總管**\] 中，以滑鼠右鍵按一下 **ImperativeCodeClientSample** 專案，然後選取 \[**設定為啟始專案**\]。  
  
3.  若要執行專案，請按 CTRL\+F5。  
  
#### 若要執行 DesignerClientSample 應用程式  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 開啟 Policy4sample.sln 方案檔案。  
  
2.  在 \[**方案總管**\] 中，以滑鼠右鍵按一下 **DesignerClientSample** 專案，然後選取 \[**設定為啟始專案**\]。  
  
3.  按 CTRL\+SHIFT\+B 編譯專案。  
  
4.  按 CTRL\+F5 執行專案。  
  
> [!IMPORTANT]
>  這些範例可能已安裝在您的電腦上。請先檢查下列 \(預設\) 目錄，然後再繼續。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目錄不存在，請移至[用於 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 與 Windows Workflow Foundation \(WF\) 範例](http://go.microsoft.com/fwlink/?LinkId=150780)，以下載所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。此範例位於下列目錄。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Rules-ExternalizedPolicy4`