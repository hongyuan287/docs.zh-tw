---
title: "/out (Visual Basic) |Microsoft 文件"
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
- /out compiler option [Visual Basic]
- -out compiler option [Visual Basic]
- out compiler option [Visual Basic]
ms.assetid: 9f148c15-0909-4cb8-a2db-777f8a8b45ae
caps.latest.revision: 17
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e3eb7af88869e4fb161a12914c02f2bc2f41864e
ms.lasthandoff: 03/13/2017

---
# <a name="out-visual-basic"></a>/out (Visual Basic)
指定輸出檔案的名稱。  
  
## <a name="syntax"></a>語法  
  
```  
/out:filename  
```  
  
## <a name="arguments"></a>引數  
  
|詞彙|定義|  
|---|---|  
|`filename`|必要項。 編譯器會建立輸出檔案的名稱。 如果檔案名稱包含空格，將名稱括在引號 ("")。|  
  
## <a name="remarks"></a>備註  
 指定完整名稱和建立檔案的副檔名。 如果不這麼做，.exe 檔案會從原始程式碼檔案包含其名稱`Sub Main`程序和.dll 檔案會從第一個原始程式檔取得其名稱。  
  
 如果您指定沒有.exe 或.dll 副檔名的檔案名稱，編譯器會自動新增延伸模組，根據指定的值`/target`編譯器選項。  
  
|設定/輸出在 Visual Studio 整合式開發環境|  
|---|  
|1.在 **方案總管**中選取專案。 在**專案**] 功能表上，按一下 [**屬性**。 如需詳細資訊，請參閱[專案設計工具簡介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.按一下 [應用程式] **** 索引標籤。<br />3.修改中的值**組件名稱**方塊。|  
  
## <a name="example"></a>範例  
 下列程式碼編譯`T2.vb`，並建立輸出檔`T2.exe`。  
  
```  
vbc t2.vb /out:t3.exe  
```  
  
## <a name="see-also"></a>另請參閱  
 [Visual Basic 命令列編譯器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [編譯命令列範例](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
