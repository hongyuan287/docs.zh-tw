---
title: "延後執行範例 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 50f4fbac-81fe-4f26-aedf-506e21419b19
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: fdbe45ceda1c7c1d82664bcf3b84b79b4fd85511
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# <a name="deferred-execution-example-c"></a>延後執行範例 (C#)
本主題顯示延後執行與延遲評估如何影響您 LINQ to XML 查詢的執行。  
  
## <a name="example"></a>範例  
 下列範例顯示利用使用延後執行的擴充方法時的執行順序。 此範例會宣告三個字串的陣列。 接著，它會逐一查看 `ConvertCollectionToUpperCase` 所傳回的集合。  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source {0}", str);  
            yield return str.ToUpper();  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        var q = from str in stringArray.ConvertCollectionToUpperCase()  
                select str;  
  
        foreach (string str in q)  
            Console.WriteLine("Main: str {0}", str);  
    }  
}  
```  
  
 這個範例會產生下列輸出：  
  
```  
ToUpper: source abc  
Main: str ABC  
ToUpper: source def  
Main: str DEF  
ToUpper: source ghi  
Main: str GHI  
```  
  
 請注意，逐一查看 `ConvertCollectionToUpperCase` 所傳回的集合時，會從來源字串陣列擷取每個項目，並在下一個項目從來源字串陣列擷取前，轉換為大寫。  
  
 您可以看到在所傳回之集合中的每個項目在 `foreach` 的 `Main` 迴圈中處理前，字串的整個陣列都沒有轉換為大寫。  
  
 本教學課程中的下一個主題說明將查詢鏈結在一起：  
  
-   [鏈結查詢範例 (C#)](../../../../csharp/programming-guide/concepts/linq/chaining-queries-example.md)  
  
## <a name="see-also"></a>另請參閱  
 [教學課程：將查詢鏈結在一起 (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)

