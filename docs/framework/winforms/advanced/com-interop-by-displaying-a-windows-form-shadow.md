---
title: "如何：顯示 Windows Form 和 ShowDialog 方法以支援 COM Interop | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "COM [Windows Form]"
  - "Windows Form, Unmanaged"
  - "COM Interop, 呼叫方法"
  - "ActiveX 控制項 [Windows Forms], COM Interop"
  - "ShowDialog 方法"
  - "Windows Form, Interop"
ms.assetid: 87aac8ad-3c04-43b3-9b0c-d0b00df9ee74
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：顯示 Windows Form 和 ShowDialog 方法以支援 COM Interop
您可以藉由在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 訊息迴圈上顯示 Windows Forms 來解決元件物件模型 \(COM\) 互通性問題，而此訊息迴圈是使用 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=fullName> 方法建立而成。  
  
 為了讓表單能夠在 COM 用戶端應用程式中正確運作，您必須在 Windows Forms 訊息迴圈上執行它。 若要執行此工作，請使用下列的其中一個方法：  
  
-   使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法，以顯示 Windows Forms。  
  
-   在個別執行緒上顯示每個 Windows Form。 如需詳細資訊，請參閱[如何：在自己的執行緒上顯示每個 Windows Form 以支援 COM Interop](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)。  
  
## 程序  
 若要在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 訊息迴圈上顯示表單，最簡單的方式是使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法，因為在所有方法中，它所需實作的程式碼最少。  
  
 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法會暫止 Unmanaged 應用程式的訊息迴圈，並將表單顯示成對話方塊。 因為主應用程式的訊息迴圈已經暫止，所以 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法會建立新的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 訊息迴圈來處理表單的訊息。  
  
 使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法的缺點是表單會被開啟為強制回應對話方塊。 當 Windows Forms 開啟時，這個行為會封鎖呼叫應用程式中的任何使用者介面 \(UI\)。 當使用者結束表單時，[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 訊息迴圈便會關閉，而先前應用程式的訊息迴圈會再次開始執行。  
  
 您可以在 Windows Forms 中建立類別庫，此類別庫具有顯示表單的方法，然後再建置用於 COM Interop 的類別庫。 您可以在 Visual Basic 6.0 或 Microsoft Foundation Class \(MFC\) 中使用這個 DLL 檔，並在這些環境中呼叫 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法以顯示表單。  
  
#### 若要使用 ShowDialog 方法來顯示 Windows 表單以支援 COM Interop  
  
-   在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 元件中，將所有對 <xref:System.Windows.Forms.Form.Show%2A?displayProperty=fullName> 方法的呼叫取代為對 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法的呼叫。  
  
## 請參閱  
 [將 .NET Framework 元件公開給 COM](../../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [如何：在自己的執行緒上顯示每個 Windows Form 以支援 COM Interop](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)   
 [Windows Form 和 Unmanaged 應用程式](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md)