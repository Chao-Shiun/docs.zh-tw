---
title: "在 Visual Basic 中的基本概念的字串 |Microsoft 文件"
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
- strings [Visual Basic], Like operator
- strings [Visual Basic], Visual Basic
- strings [Visual Basic], regular expressions
ms.assetid: 5674418d-f00d-4f72-9f98-d15897793350
caps.latest.revision: 14
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
ms.openlocfilehash: a9475c57f01c78fd5c4e2d2674f22f18ad4772e5
ms.lasthandoff: 03/13/2017

---
# <a name="string-basics-in-visual-basic"></a>Visual Basic 中的字串基礎
`String` 資料類型代表一系列字元 (每個依序代表 `Char` 資料類型的一個執行個體)。 本主題介紹 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中字串的基本概念。  
  
## <a name="string-variables"></a>字串變數  
 可將代表字元數列的常值指派給字串的執行個體。 例如:   
  
 [!code-vb[VbVbalrStrings #&63;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_1.vb)]  
  
 `String` 變數也可以接受評估為字串的任何運算式。 範例如下所示：  
  
 [!code-vb[VbVbalrStrings #&64;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_2.vb)]  
  
 指派給 `String` 變數的任何常值必須括在引號 ("") 內。 這表示無法以引號表示字串內的引號。 例如，下列程式碼會導致編譯器錯誤：  
  
 [!code-vb[VbVbalrStrings #&65;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_3.vb)]  
  
 此程式碼會造成錯誤，因為編譯器會終止第二個引號後的字串，並將字串的其餘部分解譯為程式碼。 為解決此問題，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 會將字串常值中的兩個引號解譯為字串中的一個引號。 下列範例示範在字串中包含引號的正確方式：  
  
 [!code-vb[VbVbalrStrings #&66;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_4.vb)]  
  
 在上述範例中，`Look` 文字前面的兩個引號會成為字串中的一個引號。 一行結尾處的三個引號表示字串和字串結束字元的一個引號。  
  
 字串常值可以包含多行：  
  
```vb  
Dim x = "hello  
world"  
  
```  
  
 產生的字串包含用於字串常值 (vbcr、vbcrlf 等) 的新行字元序列。  您不再需要使用舊的因應措施：  
  
```vb  
Dim x = <xml><![CDATA[Hello  
World]]></xml>.Value  
  
```  
  
## <a name="characters-in-strings"></a>字串中的字元  
 字串可以視為 `Char` 值序列，且 `String` 類型具有內建函式，可讓您在字串上執行許多操作 (類似於陣列所允許的操作)。 如 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 中的所有陣列，這些都是以零起始的陣列。 您可以透過 `Chars` 屬性參考字串中的特殊字元 ，讓您能夠依字元在字串中的出現位置存取該字元。 例如:   
  
 [!code-vb[VbVbalrStrings #&67;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_5.vb)]  
  
 在上述範例中，字串的 `Chars` 屬性會傳回字串中的第四個字元，也就是 `D`，並將其指派給 `myChar`。 您也可以透過 `Length` 屬性取得特定字串的長度。 如果您需要在字串上執行多個陣列類型操作，您可以使用字串的 `ToCharArray` 函式將它轉換為 `Char` 執行個體陣列。 例如:   
  
 [!code-vb[VbVbalrStrings #&68;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_6.vb)]  
  
 變數 `myArray` 現在包含 `Char` 值的陣列，每個都代表 `myString` 的一個字元。  
  
## <a name="the-immutability-of-strings"></a>字串的不變性  
 字串是*變*，的也就是說，其值無法變更一次建立。 不過，這不會讓您將多個值指派給一個字串變數。 參考下列範例：  
  
 [!code-vb[VbVbalrStrings #&69;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_7.vb)]  
  
 在這裡會建立字串變數、指定值，然後變更其值。  
  
 更具體來說，在第一行中，會建立類型 `String` 的執行個體並提供值 `This string is immutable`。 在此範例的第二行，建立新執行個體並指定值 `Or is it?`，且字串變數會捨棄其對第一個執行個體的參考，並儲存新執行個體的參考。  
  
 不同於其他內建資料類型，`String` 是參考類型。 將參考類型的變數做為引數傳遞給函式或副程式時，會傳遞儲存資料的記憶體位址的參考，而不是字串的實際值。 因此在前一個範例中，變數的名稱維持不變，但是它指向 `String` 類別的全新和不同的執行個體，其中包含新值。  
  
## <a name="see-also"></a>另請參閱  
 [在 Visual Basic 中的字串簡介](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [字串資料類型](../../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [Char 資料類型](../../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [基本字串作業](http://msdn.microsoft.com/library/8133d357-90b5-4b62-9927-43323d99b6b6)
