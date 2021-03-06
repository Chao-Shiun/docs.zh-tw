---
title: "文化特性如何影響在 Visual Basic 中的字串 |Microsoft 文件"
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
- locale, effect on strings
- strings [Visual Basic], locale dependence
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
caps.latest.revision: 20
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
ms.openlocfilehash: 63228a40897b29d0324be73ca1a17bcb19af2a16
ms.lasthandoff: 03/13/2017

---
# <a name="how-culture-affects-strings-in-visual-basic"></a>在 Visual Basic 中文化特性如何影響字串
這個說明網頁會討論如何[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使用文化特性資訊來執行字串轉換和比較。  
  
## <a name="when-to-use-culture-specific-strings"></a>何時使用特定文化特性的字串  
 一般而言，您應該使用特定文化特性的字串的所有資料呈現給讀取使用者，和用於應用程式的內部資料的文化特性而異的字串。  
  
 例如，如果您的應用程式會要求使用者輸入日期做為字串，它應預期使用者會根據其文化特性，將字串格式化，而應用程式應該適當地轉換字串。 如果您的應用程式然後顯示該日期在其使用者介面，它應該呈現使用者的文化特性。  
  
 不過，如果應用程式會將日期上載到中央伺服器，它應該格式根據某一特定文化特性，以避免混淆之間可能有不同的日期格式字串。  
  
## <a name="culture-sensitive-functions"></a>區分文化特性的函式  
 所有的[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]字串轉換函式 (除了`Str`和`Val`函式) 以確定轉換和比較都適合使用的文化特性的應用程式的使用者使用應用程式的文化特性資訊。  
  
 要成功地在不同的文化特性設定的電腦執行的應用程式中使用字串轉換函式的索引鍵是了解哪些函式會使用特定文化特性設定，並使用目前文化特性設定。 請注意，應用程式的文化特性設定，根據預設，繼承自作業系統的文化特性設定。 如需詳細資訊，請參閱<xref:Microsoft.VisualBasic.Strings.Asc%2A>， <xref:Microsoft.VisualBasic.Strings.AscW%2A>， <xref:Microsoft.VisualBasic.Strings.Chr%2A>， <xref:Microsoft.VisualBasic.Strings.ChrW%2A>， <xref:Microsoft.VisualBasic.Strings.Format%2A>， <xref:Microsoft.VisualBasic.Conversion.Hex%2A>， <xref:Microsoft.VisualBasic.Conversion.Oct%2A>，和[類型轉換函式](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)。</xref:Microsoft.VisualBasic.Conversion.Oct%2A> </xref:Microsoft.VisualBasic.Conversion.Hex%2A> </xref:Microsoft.VisualBasic.Strings.Format%2A> </xref:Microsoft.VisualBasic.Strings.ChrW%2A> </xref:Microsoft.VisualBasic.Strings.Chr%2A> </xref:Microsoft.VisualBasic.Strings.AscW%2A> </xref:Microsoft.VisualBasic.Strings.Asc%2A>  
  
 `Str` （將數字轉換為字串） 和`Val`（將數字字串） 函式不會使用應用程式的文化特性資訊字串和數字之間轉換時。 相反地，它們只將句點 （.） 辨識為有效的十進位分隔符號。 這些函式的文化特性感知類似情況如下︰  
  
-   **使用目前文化特性的轉換。** `CStr`和`Format`函式會將數字轉換為字串，而`CDbl`和`CInt`函式會將字串轉換為數字。  
  
-   **使用特定文化特性的轉換。** 每一個數字的物件有`ToString(IFormatProvider)`方法，將數字轉換為字串，和`Parse(String, IFormatProvider)`方法，將字串轉換為數字。 例如，`Double`類型提供<xref:System.Double.ToString%28System.IFormatProvider%29>和<xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29>方法。</xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29> </xref:System.Double.ToString%28System.IFormatProvider%29>  
  
 如需詳細資訊，請參閱<xref:Microsoft.VisualBasic.Conversion.Str%2A>和<xref:Microsoft.VisualBasic.Conversion.Val%2A>.</xref:Microsoft.VisualBasic.Conversion.Val%2A> </xref:Microsoft.VisualBasic.Conversion.Str%2A>  
  
## <a name="using-a-specific-culture"></a>使用特定文化特性  
 假設您正在開發的應用程式傳送至 Web 服務的日期 （格式為字串）。 在此情況下，您的應用程式必須使用特定文化特性的字串轉換。 為了說明原因，請考慮使用的日期，導致<xref:System.DateTime.ToString>方法︰ 如果您的應用程式會使用該方法，若要格式化日期為 2005 年 7 月 4 日，則會傳回 「 2005 年 7 月 4 日 12:00:00 AM 」 使用美式英文 (EN-US) 文化特性執行時，但它會傳回"04.07.2005 00:00:00 」 使用德國 (DE-DE) 文化特性執行時。</xref:System.DateTime.ToString>  
  
 當您需要執行的特定文化特性格式的字串轉換時，您應該使用`CultureInfo`類別是內建於[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]。 您可以建立新`CultureInfo`物件的特定文化特性的文化特性將名稱傳遞給<xref:System.Globalization.CultureInfo.%23ctor%2A>建構函式。</xref:System.Globalization.CultureInfo.%23ctor%2A> 支援的文化特性名稱會列在<xref:System.Globalization.CultureInfo>類別說明頁面。</xref:System.Globalization.CultureInfo>  
  
 或者，您可以取得的執行個體*文化特性而異*從<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>屬性。</xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 而異的文化特性為基礎的英文文化特性，但有一些差異。 例如，文化特性而異指定 24 小時制時鐘，而不是採用 12 小時制。  
  
 若要將日期轉換成文化特性的字串，傳遞<xref:System.Globalization.CultureInfo>date 物件的物件<xref:System.DateTime.ToString%28System.IFormatProvider%29>方法。</xref:System.DateTime.ToString%28System.IFormatProvider%29> </xref:System.Globalization.CultureInfo> 例如，下列程式碼會顯示 「 07/04/2005年 00:00:00"，不論應用程式的文化特性設定。  
  
 [!code-vb[VbVbalrConcepts #&1;](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/codesnippet/VisualBasic/how-culture-affects-strings_1.vb)]  
  
> [!NOTE]
>  日期常值一律會解譯為根據英文的文化特性。  
  
## <a name="comparing-strings"></a>比較字串  
 有兩個重要的情況需要字串比較的。  
  
-   **排序資料以供顯示給使用者。** 使用根據目前文化特性，因此能適當地排序字串的作業。  
  
-   **決定是否兩個應用程式內部的字串完全符合 （通常是針對安全性目的）。** 使用忽略目前的文化特性的作業。  
  
 您可以執行這兩種類型的比較與[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]<xref:Microsoft.VisualBasic.Strings.StrComp%2A>函式。</xref:Microsoft.VisualBasic.Strings.StrComp%2A> 指定選擇性`Compare`控制的比較類型的引數︰`Text`大部分的輸入和輸出`Binary`判斷完全相符項目。  
  
 `StrComp`函式會傳回一個整數，表示排序順序為基礎的比較兩個字串之間的關聯性。 結果為正值表示第一個字串大於第二個字串。 負數的結果會指出第一個字串較小，且零表示字串相等。  
  
 [!code-vb[VbVbalrStrings #&22;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-culture-affects-strings_2.vb)]  
  
 您也可以使用[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]夥伴`StrComp`函式，<xref:System.String.Compare%2A?displayProperty=fullName>方法。</xref:System.String.Compare%2A?displayProperty=fullName> 這是字串基底類別的靜態多載方法。 下列範例將說明如何使用這個方法︰  
  
 [!code-vb[VbVbalrStrings #&48;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-culture-affects-strings_3.vb)]  
  
 更精細地控制如何執行比較的詳細資訊，您可以使用的其他多載<xref:System.String.Compare%2A>方法。</xref:System.String.Compare%2A> 使用<xref:System.String.Compare%2A?displayProperty=fullName>方法中，您可以使用`comparisonType`引數指定要使用的比較類型。</xref:System.String.Compare%2A?displayProperty=fullName>  
  
|值`comparisonType`引數|比較的類型|使用時機|  
|---|---|---|  
|`Ordinal`|依據字串元件位元組的比較。|比較時使用此值︰ 區分大小寫的識別項、 安全性相關的設定或位元組必須完全符合其他非語言識別項。|  
|`OrdinalIgnoreCase`|依據字串元件位元組的比較。<br /><br /> `OrdinalIgnoreCase`使用不變文化特性資訊來判斷兩個字元不同大小寫。|比較時使用此值︰ 不區分大小寫的識別項、 安全性相關設定，以及儲存在 Windows 中的資料。|  
|`CurrentCulture` 或 `CurrentCultureIgnoreCase`|在目前的文化特性的字串解譯為基礎的比較。|比較時使用這些值︰ 資料顯示給使用者，大部分使用者輸入，以及其他需要語言解譯的資料。|  
|`InvariantCulture` 或 `InvariantCultureIgnoreCase`|而異的文化特性的字串解譯為基礎的比較。<br /><br /> 這是不同於`Ordinal`和`OrdinalIgnoreCase`，因為文化特性而異視為相等的非變異字元可接受的範圍之外的字元。|只比較持續資料或顯示的語言相關資料時，需要固定的排序次序，請使用這些值。|  
  
### <a name="security-considerations"></a>安全性考量  
 如果您的應用程式進行比較或大小寫變更作業的結果為基礎的安全性決策，則作業應該使用<xref:System.String.Compare%2A?displayProperty=fullName>方法，然後傳遞`Ordinal`或`OrdinalIgnoreCase`的`comparisonType`引數。</xref:System.String.Compare%2A?displayProperty=fullName>  
  
## <a name="see-also"></a>另請參閱  
 <xref:System.Globalization.CultureInfo></xref:System.Globalization.CultureInfo>   
 [在 Visual Basic 中的字串簡介](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [類型轉換函式](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
