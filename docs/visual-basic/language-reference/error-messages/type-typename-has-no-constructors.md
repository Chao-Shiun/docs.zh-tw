---
title: "類型 &quot;&lt;typename&gt;&quot; 沒有建構函式 |Microsoft 文件"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30251
- vbc30251
dev_langs:
- VB
helpviewer_keywords:
- BC30251
ms.assetid: aff3e1df-abe6-4bc0-9abc-a1e70514c561
caps.latest.revision: 9
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
ms.openlocfilehash: 505e3bbdfa830394efcea7226897ec0d3e6d2b02
ms.lasthandoff: 03/13/2017

---
# <a name="type-39lttypenamegt39-has-no-constructors"></a>類型 '&lt;typename&gt;' 沒有建構函式
類型不支援呼叫 `Sub New()`。 一個可能原因是編譯器或二進位檔案損毀。  
  
 **錯誤識別碼︰** BC30251  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
1.  如果類型是在不同專案中，或是在參考的檔案中，請重新安裝專案或檔案。  
  
2.  如果類型是在相同專案中，請重新編譯包含類型的組件。  
  
3.  如果問題重複發生，請重新安裝 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 編譯器。  
  
4.  如果錯誤持續發生，請收集情況的相關資訊，並通知 Microsoft 產品支援服務。  
  
## <a name="see-also"></a>另請參閱  
 [物件和類別](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [告訴我們](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
