---
title: "x:Member Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4d8394ef-644c-4331-b6c5-be855d392980
caps.latest.revision: 5
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 5
---
# x:Member Directive
在標記中宣告 XAML 成員。  
  
## XAML 物件項目用法  
  
```  
  
<object x:Class="className">  
  <x:Members>  
    <x:Member Name="propertyName"/>  
    additionalMembers  
  </x:Members>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`className`|XAML 生產的支援類別或部分類別名稱。|  
|`memberName`|正在定義之屬性的成員名稱。|  
  
## 備註  
 在 .NET Framework XAML 服務實作中，  `x:Member` 沒有直接的類型支援，但受到 <xref:System.Windows.Markup.MemberDefinition> 類別的支援。  在 XAML 節點資料流中，`x:Member` 項目會以 XAML 語言 XAML 命名空間中名為 `Member` 的成員表示。  成員 `Member` 包含以標記宣告的屬性。  
  
 `Name` 和 `Type` 的意義不是在 .NET Framework XAML 服務層級上指派。  它們會在初始 XAML 節點資料流中儲存為字串值，以便稍後依據特定架構可能加諸的規則解譯。  這個意義可能與 XAML 名稱和 XAML 類型的意義一致，或可能只是在支援類型系統中有效，視實作而定。  
  
 若要支援實際使用 `x:Members` 做為在標記中指定成員定義的方法，這些成員必須與可修改的類別相關聯。  預期的模型是 `x:Members` 做為可指定 `x:Class` 之類型成員的形式存在。  不過，.NET Framework XAML 服務層級不支援關聯類型與成員或產生動態成員定義的機制。  這會保留給具有支援 XAML 成員定義之應用程式模型的個別架構。  通常需要 MSBUILD 建置動作以標記編譯 XAML，然後與程式碼後置整合，或是從 XAML 產生純組件，才能支援該功能。  
  
## Windows Workflow Foundation 的 x:Property  
 針對 Windows Workflow Foundation，`x:Property` 會定義完全以 XAML 撰寫之自訂活動的成員，或程式碼後置活動設計工具的 XAML 定義動態成員。  `x:Class` 也必須在 XAML 生產的根項目上指定。  這不是 .NET Framework XAML 服務層級的需求，但是當 XAML 生產是由支援自訂活動和 Windows Workflow Foundation XAML 的 MSBUILD 建置動作載入時，通常會變成需求。  Windows Workflow Foundation 不會使用純 XAML 類型做為 `x:Property` `Type` 屬性所需的值，而是改用這裡未記載的慣例。  如需詳細資訊，請參閱[建立動態活動](http://msdn.microsoft.com/library/dd807392.aspx)。