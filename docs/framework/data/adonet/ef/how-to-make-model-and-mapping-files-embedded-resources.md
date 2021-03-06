---
title: "HOW TO：讓模型和對應檔變成內嵌資源 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
  - "jsharp"
ms.assetid: 20dfae4d-e95a-4264-9540-f5ad23b462d3
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# HOW TO：讓模型和對應檔變成內嵌資源
[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 可以讓您部署模型和對應檔，作為應用程式的內嵌資源。  具有內嵌模型和對應檔的組件必須載入與實體連接相同的應用程式定義域中。  如需詳細資訊，請參閱[連接字串](../../../../../docs/framework/data/adonet/ef/connection-strings.md)。  根據預設，[!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)] 工具會內嵌模型和對應檔。當您手動定義模型和對應檔時，請使用這個程序，確保檔案與 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 應用程式已一起部署為內嵌資源。  
  
> [!NOTE]
>  若要維護內嵌資源，您必須在每次修改模型和對應檔時重複這個程序。  
  
### 內嵌模型和對應檔  
  
1.  在 \[**方案總管**\] 中，選取概念 \(.csdl\) 檔案。  
  
2.  在 \[**屬性**\] 窗格中，將 \[**建置動作**\] 設定為 \[**內嵌資源**\]。  
  
3.  針對儲存 \(.ssdl\) 檔和對應檔 \(.msl\) 重複步驟 1 和 2。  
  
4.  在 \[**方案總管**\] 中，按兩下 App.config 檔，然後根據下列其中一個格式來修改 `connectionString` 屬性中的 `Metadata` 參數：  
  
    -   `Metadata=` `res://<assemblyFullName>/<resourceName>;`  
  
    -   `Metadata=` `res://*/<resourceName>;`  
  
    -   `Metadata=res://*;`  
  
     如需詳細資訊，請參閱[連接字串](../../../../../docs/framework/data/adonet/ef/connection-strings.md)。  
  
## 範例  
 下列連接字串會參考 [AdventureWorks Sales Model](http://msdn.microsoft.com/zh-tw/f16cd988-673f-4376-b034-129ca93c7832) 的內嵌模型和對應檔。  此連接字串儲存在專案的 App.config 檔案中。  
  
  
  
## 請參閱  
 [模型化及對應檔案](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)   
 [HOW TO：定義連接字串](../../../../../docs/framework/data/adonet/ef/how-to-define-the-connection-string.md)   
 [HOW TO：建立 EntityConnection 連接字串](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/zh-tw/91076853-0881-421b-837a-f582f36be527)