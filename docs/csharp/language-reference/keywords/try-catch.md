---
title: "try-catch (C# 參考) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "try"
  - "try_CSharpKeyword"
  - "catch"
  - "catch_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "catch 關鍵字 [C#]"
  - "try-catch 陳述式 [C#]"
ms.assetid: cb5503c7-bfa1-4610-8fc2-ddcd2e84c438
caps.latest.revision: 45
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 45
---
# try-catch (C# 參考)
try-catch 陳述式包含 `try` 區塊後面接著一個或多個 `catch` 子句，指定不同例外狀況的處理常式。  
  
## <a name="remarks"></a>備註  
 擲回例外狀況時，Common Language Runtime (CLR) 會尋找處理此例外狀況的 `catch` 陳述式。 如果目前執行的方法不包含這類 `catch` 區塊，CLR 會在呼叫堆疊上查看呼叫目前方法的方法，依此類推。 如果找不到 `catch` 區塊，則 CLR 會向使用者顯示未處理的例外狀況訊息，並停止執行程式。  
  
 `try` 區塊包含可能會造成例外狀況的防護程式碼。 區塊會執行直到例外狀況擲回，或已成功完成。 例如，下列嘗試轉換`null`物件引發<xref:System.NullReferenceException>例外狀況︰  
  
```c#  
object o2 = null;  
try  
{  
    int i2 = (int)o2;   // Error  
}  
```  
  
 雖然可以不含引數使用 `catch` 子句，來攔截任何類型的例外狀況，不建議使用這種用法。 一般而言，您應該只攔截那些您知道如何從中復原的例外狀況。 因此，您應該一律指定衍生自物件引數<xref:System.Exception?displayProperty=fullName> ，例如︰  
  
```c#  
catch (InvalidCastException e)   
{  
}  
```  
  
 您可以在相同 try catch 陳述式中的子句中使用多個特定的 `catch`。 在此情況下，`catch` 子句的順序很重要，因為會依順序檢查 `catch` 子句。 在較不特定的例外狀況之前攔截較特定的例外狀況。 如果您排序 catch 區塊，使得永遠不會達到較新的區塊，編譯器會產生錯誤。  
  
 使用 `catch` 引數是篩選您想要處理的例外狀況的一種方式。  您也可以使用述詞運算式，進一步檢查例外狀況來決定是否要處理。  如果述詞運算式會傳回 false，則搜尋處理常式會繼續。  
  
```c#  
catch (ArgumentException e) when (e.ParamName == “…”)  
{  
}  
```  
  
 例外狀況篩選條件優於攔截和重新擲回 (說明如下所示)，因為篩選條件不會損壞堆疊。  如果之後的處理常式傾印堆疊，您可以看到例外狀況原本來自何處，而不是只重新擲回的最後一個位置。  例外狀況篩選條件運算式的常見用法是記錄。  您可以建立一律會傳回 false 同時會輸出到記錄檔的述詞函式，您可以持續記錄例外狀況，而不必處理它們並重新擲回。  
  
 A[擲回](../../../csharp/language-reference/keywords/throw.md)陳述式可以用於`catch`區塊會攔截的例外狀況重新擲回`catch`陳述式。 下列範例會擷取來源資訊從<xref:System.IO.IOException>例外狀況，然後擲回的例外狀況的父方法。  
  
```c#  
catch (FileNotFoundException e)  
{  
    // FileNotFoundExceptions are handled here.  
}  
catch (IOException e)  
{  
    // Extract some information from this exception, and then   
    // throw it to the parent method.  
    whenDo not initialize (e.Source != null)  
        Console.WriteLine("IOException source: {0}", e.Source);  
    throw;  
}  
```  
  
 您可以攔截一個例外狀況，並擲回不同的例外狀況。 執行此動作時，請將您攔截的例外狀況指定為內部例外狀況，如下列範例所示。  
  
```c#  
catch (InvalidCastException e)   
{  
    // Perform some action here, and then throw a new exception.  
    throw new YourCustomException("Put your error message here.", e);  
}  
```  
  
 指定的條件為 true 時，您可以也重新擲回例外狀況時，如下列範例所示。  
  
```c#  
  
catch (InvalidCastException e)  
{  
    if (e.Data == null)  
    {  
        throw;  
    }  
    else  
    {  
        // Take some action.  
    }  
 }  
```  
  
 從 `try` 區塊內，僅初始化其中宣告的變數。 否則，在區塊的執行完成之前，可能會發生例外狀況。 例如，在下列程式碼範例中，變數 `n` 是在 `try` 區塊內初始化。 在 `Write(n)` 陳述式中的 `try` 區塊外嘗試使用此變數，將產生編譯器錯誤。  
  
```c#  
static void Main()   
{  
    int n;  
    try   
    {  
        // Do not initialize this variable here.  
        n = 123;  
    }  
    catch  
    {  
    }  
    // Error: Use of unassigned local variable 'n'.  
    Console.Write(n);  
}  
```  
  
 如需 catch 的詳細資訊，請參閱[試為 try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)。  
  
## <a name="exceptions-in-async-methods"></a>非同步方法中的例外狀況  
 來標記非同步方法[非同步](../../../csharp/language-reference/keywords/async.md)修飾詞，而且通常包含一個或多個 await 運算式或陳述式。 Await 運算式適用於[await](../../../csharp/language-reference/keywords/await.md)運算子<xref:System.Threading.Tasks.Task>或<xref:System.Threading.Tasks.Task%601>。  
  
 當控制項到達 `await` 方法時，方法中的進度會暫停，直到等候的工作完成。 當工作完成時，方法中的執行可以繼續。 如需詳細資訊，請參閱[使用 Async 和 Await 進行非同步程式設計](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)和[非同步程式中的控制流程](../Topic/Control%20Flow%20in%20Async%20Programs%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 套用 `await` 完成的工作可能因為傳回工作的方法中未處理的例外狀況而處於錯誤的狀態。 等候工作擲回例外狀況。 如果傳回工作的非同步程序被取消，工作也可能以取消的狀態結束。 等候已取消的工作會擲回 `OperationCanceledException`。 如需如何取消非同步處理序的詳細資訊，請參閱[微調非同步應用程式](../Topic/Fine-Tuning%20Your%20Async%20Application%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 若要攔截例外狀況，請在 `try` 區塊中等候工作，並在關聯的 `catch` 區塊中攔截例外狀況。 如需範例，請參閱＜範例＞一節。  
  
 工作可能處於錯誤狀態，因為在等候的非同步方法中發生多個例外狀況。 例如，工作可能是要呼叫的結果<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>。 當您等候這類工作時，只會攔截到其中一個例外狀況，而且您無法預測會攔截的例外狀況。 如需範例，請參閱＜範例＞一節。  
  
## <a name="example"></a>範例  
 在下列範例中，`try` 區塊包含可能會造成例外狀況的對 `ProcessString` 方法的呼叫。 `catch` 子句包含只會在螢幕上顯示訊息的例外狀況處理常式。 從 `MyMethod` 內呼叫 `throw` 陳述式時 ，系統會尋找 `catch` 陳述式，並顯示訊息 `Exception caught`。  
  
 [!code-cs[csrefKeywordsExceptions#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_1.cs)]  
  
## <a name="example"></a>範例  
 在下列範例中，使用了兩個 catch 區塊，並會攔截會先出現的最特定例外狀況。  
  
 若要攔截最不特定的例外狀況，您可以使用下列陳述式取代 `ProcessString` 中的 throw 陳述式：`throw new Exception()`。  
  
 如果您先在範例中放置最特定的 catch 區塊，會出現下列錯誤訊息：`A previous catch clause already catches all exceptions of this or a super type ('System.Exception')`。  
  
 [!code-cs[csrefKeywordsExceptions#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_2.cs)]  
  
## <a name="example"></a>範例  
 下列範例說明非同步方法的例外狀況處理。 若要擷取非同步工作擲回的例外狀況，請將 `await` 運算式放置在 `try` 區塊中，並攔截 `catch` 區塊中的例外狀況。  
  
 取消註解範例中的 `throw new Exception` 行來示範例外狀況處理。 工作的 `IsFaulted` 屬性設定為 `True`，工作的 `Exception.InnerException` 屬性設定為例外狀況，並在 `catch` 區塊攔截例外狀況。  
  
 取消註解 `throw new OperationCancelledException` 行來示範取消非同步程序時會發生的情況。 工作的 `IsCanceled` 屬性設定為 `true`，並在 `catch` 區塊攔截例外狀況。 在不適用這個範例的部分情況下，工作的 `IsFaulted` 屬性會設定為 `true` 而 `IsCanceled` 設為 `false`。  
  
 [!code-cs[csAsyncExceptions#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_3.cs)]  
  
## <a name="example"></a>範例  
 下列範例說明多項工作可能會導致多個例外狀況的例外狀況處理。 `try`區塊等候呼叫所傳回的工作<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>。 當套用所有項目的三項工作都完成時，工作即完成。  
  
 這三個工作都會造成例外狀況。 `catch`區塊逐一查看的例外狀況中找到`Exception.InnerExceptions`屬性所傳回之工作<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>。  
  
 [!code-cs[csAsyncExceptions#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_4.cs)]  
  
## <a name="c-language-specification"></a>C# 語言規格  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [C# 參考](../../../csharp/language-reference/index.md)   
 [C# 程式設計手冊](../../../csharp/programming-guide/index.md)   
 [C# 關鍵字](../../../csharp/language-reference/keywords/index.md)   
 [try、 throw 和 catch 陳述式 （c + +）](/visual-cpp/cpp/try-throw-and-catch-statements-cpp)   
 [例外狀況處理陳述式](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [擲回](../../../csharp/language-reference/keywords/throw.md)   
 [請嘗試最後](../../../csharp/language-reference/keywords/try-finally.md)   
 [如何︰ 明確擲回例外狀況](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)