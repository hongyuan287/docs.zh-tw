---
title: "System.TimeSpan 方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9333fee8-1454-4374-855b-8c14c002f48f
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# System.TimeSpan 方法
<xref:System.TimeSpan?displayProperty=fullName> 的成員支援主要取決於您所使用的 .NET Framework 和 Microsoft SQL Server 版本。  
  
 不支援某種方法、運算子或屬性時，就表示 LINQ to SQL 無法轉譯該成員，以便在 SQL Server 上執行。  雖然您仍然可以在程式碼中使用這些成員，  但是必須在查詢轉譯成 Transact\-SQL 之前或從資料庫中擷取結果之後，評估這些成員。  
  
## 先前的限制  
 使用 LINQ to SQL 搭配 .NET Framework 3.5 SP1 之前的 .NET Framework 版本時，您無法將 SQL Server 資料庫欄位對應至 <xref:System.TimeSpan?displayProperty=fullName>。  但是，支援 <xref:System.TimeSpan> 的作業，因為 <xref:System.TimeSpan> 值可以從 <xref:System.DateTime> 減法傳回，或引進運算式中做為常值或繫結變數。  
  
## 支援的 System.TimeSpan 方法支援  
 下列 LINQ to SQL 支援的方法、運算子和屬性都可讓您用於 LINQ to SQL 查詢中。  一旦在物件模型 \(Object Model\) 或外部對應檔案中對應之後，LINQ to SQL 就可讓您在 LINQ to SQL 查詢內部呼叫許多 <xref:System.TimeSpan?displayProperty=fullName> 成員。  
  
|支援的 <xref:System.TimeSpan> 方法|支援的 <xref:System.TimeSpan> 運算子|支援的 <xref:System.TimeSpan> 屬性|  
|-------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.TimeSpan.Compare%2A>|<xref:System.TimeSpan.op_Equality%2A>|<xref:System.TimeSpan.Days%2A>|  
|<xref:System.TimeSpan.CompareTo%28System.TimeSpan%29>|<xref:System.TimeSpan.op_GreaterThan%2A>|<xref:System.TimeSpan.Hours%2A>|  
|<xref:System.TimeSpan.Duration%2A>|<xref:System.TimeSpan.op_GreaterThanOrEqual%2A>|<xref:System.TimeSpan.MaxValue>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%2CSystem.TimeSpan%29>|<xref:System.TimeSpan.op_Inequality%2A>|<xref:System.TimeSpan.Milliseconds%2A>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%29>|<xref:System.TimeSpan.op_LessThan%2A>|<xref:System.TimeSpan.Minutes%2A>|  
||<xref:System.TimeSpan.op_LessThanOrEqual%2A>|<xref:System.TimeSpan.MinValue%2A>|  
  
> [!NOTE]
>  透過 LINQ to SQL 將 <xref:System.TimeSpan?displayProperty=fullName> 對應至 SQL `TIME` 資料行的功能需要 .NET Framework 3.5 SP1 和更新版本。  SQL `TIME` 資料型別只能在 Microsoft SQL Server 2008 和更新版本中使用。  
  
### 加法和減法  
 雖然 CLR <xref:System.TimeSpan?displayProperty=fullName> 型別支援加法和減法，但是 SQL `TIME` 型別卻不支援。  因此，如果您的 LINQ to SQL 查詢嘗試在對應至 SQL `TIME` 型別時進行加法和減法，它們將會產生錯誤。  您可以在 [SQL\-CLR 型別對應](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md) 中找到使用 SQL 日期與時間型別的其他考量。  
  
## 請參閱  
 [查詢概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)   
 [建立物件模型](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)   
 [SQL\-CLR 型別對應](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)   
 [資料型別和函式](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)