---
title: "如何：在 Visual Basic 中尋找具有特定模式的檔案"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- files, finding
- pattern matching
- patterns, matching
ms.assetid: 25e3b71d-b844-4293-9e4e-f06c5836b5cc
caps.latest.revision: 23
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 5e5d7dc692bf68ebccc459e9cf3f92c3683b8145
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# How to: Find Files with a Specific Pattern in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

<xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A> 方法會傳回代表檔案的路徑名稱之字串的唯讀集合。  您可以使用 `wildCards` 參數，指定特定的模式。  如果要在搜尋中包含子目錄，請將 `searchType` 參數設定為 `SearchOption.SearchAllSubDirectories`。  
  
 如果找不到符合指定之模式的檔案，則會傳回空集合。  
  
> [!NOTE]
>  如需傳回使用 `System.IO` 命名空間的 `DirectoryInfo` 類別的檔案清單的詳細資訊，請參閱 <xref:System.IO.DirectoryInfo.GetFiles%2A>。  
  
### 若要搜尋具有指定模式的檔案  
  
-   使用 `GetFiles` 方法，提供要搜尋之目錄的名稱與路徑，並指定模式。  下列範例會傳回目錄中副檔名為 `.dll` 的所有檔案，並將它們加入至 `ListBox1`。  
  
     [!code-vb[VbFileIOMisc#4](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-find-files-with-a-specific-pattern_1.vb)]  
  
## .NET Framework 安全性  
 下列情形可能會造成例外狀況 \(Exception\)：  
  
-   因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 \(開頭為 \\\\.  \\\) \(<xref:System.ArgumentException>\).  
  
-   路徑無效，因為它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   `directory` 不存在 \(<xref:System.IO.DirectoryNotFoundException>\)。  
  
-   `directory` 會指向現有的檔案 \(<xref:System.IO.IOException>\)。  
  
-   路徑超過系統定義的最大長度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   路徑中的檔案或資料夾名稱含有冒號 \(:\)，或者是無效的格式 \(<xref:System.NotSupportedException>\)。  
  
-   使用者缺乏必要的使用權限來檢視路徑 \(<xref:System.Security.SecurityException>\)。  
  
-   使用者缺乏必要的使用權限 \(<xref:System.UnauthorizedAccessException>\)。  
  
## 請參閱  
 <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A>   
 [如何：尋找具有特定模式的子目錄](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)   
 [疑難排解：讀取和寫入文字檔](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [如何：取得目錄的檔案集合](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)

