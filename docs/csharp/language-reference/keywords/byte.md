---
title: "byte (C# 參考)"
ms.date: 2017-03-14
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- byte
- byte_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- byte keyword [C#]
ms.assetid: 111f1db9-ca32-4f0e-b497-4783517eda47
caps.latest.revision: 19
author: BillWagner
ms.author: wiwagn
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
ms.openlocfilehash: 8ef7494e2a8a1463d37cff77d1dacebec8182b66
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# <a name="byte-c-reference"></a>byte (C# 參考)
`byte` 關鍵字表示用來儲存下表所指出值的整數型別。  
  
|類型|範圍|大小|.NET Framework 類型|  
|----------|-----------|----------|-------------------------|  
|`byte`|0 到 255|不帶正負號的 8 位元整數|<xref:System.Byte?displayProperty=fullName>|  
  
## <a name="literals"></a>常值  
 您可以宣告並初始化 `byte` 變數，如下列範例所示：  
  
```  
byte myByte = 255;  
```  
  
 在上述宣告中，整數常值 `255` 會從 [int](../../../csharp/language-reference/keywords/int.md) 隱含地轉換為 `byte`。 如果整數常值超出 `byte` 範圍，就會發生編譯錯誤。  
  
## <a name="conversions"></a>轉換  
 有一項從 `byte` 轉換為 [short](../../../csharp/language-reference/keywords/short.md)、[ushort](../../../csharp/language-reference/keywords/ushort.md)、[int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md) 或 [decimal](../../../csharp/language-reference/keywords/decimal.md) 之預先定義的隱含轉換。  
  
 您無法將較大儲存大小的非常值數字類型隱含轉換為 `byte`。 如需整數型別儲存大小的詳細資訊，請參閱[整數型別表](../../../csharp/language-reference/keywords/integral-types-table.md)。 例如，請考慮使用下列兩個 `byte` 變數 `x` 和 `y`：  
  
```  
  
byte x = 10, y = 20;  
```  
  
 因為指派運算子右側的算術運算式預設會評估為 `int`，所以下列指派陳述式將會產生編譯錯誤。  
  
```  
// Error: conversion from int to byte:  
byte z = x + y;  
```  
  
 若要修正這個問題，請使用轉型：  
  
```  
// OK: explicit conversion:  
byte z = (byte)(x + y);  
```  
  
 不過，可以使用目的地變數具有相同或較大儲存大小的下列陳述式︰  
  
```  
int x = 10, y = 20;  
int m = x + y;  
long n = x + y;  
```  
  
 同時，沒有從浮點類型轉換為 `byte` 的隱含轉換。 例如，下列陳述式會在未使用明確轉換的情況下產生編譯器錯誤：  
  
```  
// Error: no implicit conversion from double:  
byte x = 3.0;   
// OK: explicit conversion:  
byte y = (byte)3.0;  
```  
  
 呼叫多載的方法時，必須使用轉型。 例如，假設下列使用 `byte` 和 [int](../../../csharp/language-reference/keywords/int.md) 參數的多載方法：  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(byte b) {}  
```  
  
 使用 `byte` 轉型時，可以保證呼叫正確的類型，例如：  
  
```  
// Calling the method with the int parameter:  
SampleMethod(5);  
// Calling the method with the byte parameter:  
SampleMethod((byte)5);  
```  
  
 如需混合浮點類型和整數型別之算術運算式的資訊，請參閱 [float](../../../csharp/language-reference/keywords/float.md) 和 [double](../../../csharp/language-reference/keywords/double.md)。  
  
 如需隱含數值轉換規則的詳細資訊，請參閱[隱含數值轉換表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
## <a name="c-language-specification"></a>C# 語言規格  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 <xref:System.Byte>   
 [C# 參考](../../../csharp/language-reference/index.md)   
 [C# 程式設計手冊](../../../csharp/programming-guide/index.md)   
 [C# 關鍵字](../../../csharp/language-reference/keywords/index.md)   
 [整數型別表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [內建類型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隱含數值轉換表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [明確數值轉換表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
