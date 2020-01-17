---
title: Integration Services 式の詳細の例 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- operators [Integration Services]
- expressions [Integration Services], examples
- examples [Integration Services]
ms.assetid: c7794ba3-0de5-466b-ae8a-9ddd27360049
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9272a6c11ce226f385c0b1f79f965a2a0f55835e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901123"
---
# <a name="examples-of-advanced-integration-services-expressions"></a>Integration Services 式の詳細の例
  このセクションでは、複数の演算子と関数を組み合わせた詳細な式の例について説明します。 式が優先順位制約または条件分割変換で使用される場合、式はブール型に評価される必要があります。 ただしこの制限は、プロパティ式、変数、派生列変換、または For ループ コンテナーで使用される式には適用されません。  
  
 次の例では、 **AdventureWorks** および [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを使用します。 それぞれの例では、式で使用するテーブルを判別します。  
  
## <a name="boolean-expressions"></a>ブール式  
  
-   この例では、 **Product** テーブルを使用します。 式は、 **SellStartDate** 列の月エントリを評価し、その月が 6 月以降の場合に TRUE を返します。  
  
    ```  
    DATEPART("mm",SellStartDate) > 6  
    ```  
  
-   この例では、 **Product** テーブルを使用します。 式は、 **ListPrice** 列を **StandardCost** 列で割った結果を丸め、その結果が 1.5 よりも大きい場合に TRUE を返します。  
  
    ```  
    ROUND(ListPrice / StandardCost,2) > 1.50  
    ```  
  
-   この例では、 **Product** テーブルを使用します。 式は、3 つの演算すべてが TRUE に評価された場合に TRUE を返します。 **Size** 列のデータ型と **BikeSize** 変数のデータ型に互換性がない場合、式には、2 番目の例で示すように明示的なキャストが必要です。 DT_WSTR へのキャストには、文字列の長さも含まれます。  
  
    ```  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE && Size != @BikeSize  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE  && Size != (DT_WSTR,10)@BikeSize  
    ```  
  
-   この例では、 **CurrencyRate** テーブルを使用します。 式は、テーブル内の値と変数を比較します。 **FromCurrencyCode** 列または **ToCurrencyCode** 列のエントリが変数の値と等しく、かつ **AverageRate** の値が **EndOfDayRate**の値よりも大きい場合、式は TRUE を返します。  
  
    ```  
    (FromCurrencyCode == @FromCur || ToCurrencyCode == @ToCur) && AverageRate > EndOfDayRate  
    ```  
  
-   この例では、 **Currency** テーブルを使用します。 **Name** 列の最初の文字が a または A でない場合、式は TRUE を返します。  
  
    ```  
    SUBSTRING(UPPER(Name),1,1) != "A"  
    ```  
  
     次の式は同じ結果を返しますが、1 文字だけ大文字に変換されるため、より効率的です。  
  
    ```  
    UPPER(SUBSTRING(Name,1,1)) != "A"  
    ```  
  
## <a name="non-boolean-expressions"></a>ブール式以外の式  
 ブール式以外の式は、派生列変換、プロパティ式、および For ループ コンテナーで使用されます。  
  
-   この例では、 **Contact** テーブルを使用します。 式は、 **FirstName**、 **MiddleName**、および **LastName** 列から先頭および末尾のスペースを削除します。 **MiddleName** 列が NULL でない場合は最初の文字を抽出し、そのミドル ネーム イニシャルと **FirstName** および **LastName**の値を連結して、値の間に適切なスペースを挿入します。  
  
    ```  
    TRIM(FirstName) + " " + (!ISNULL(MiddleName) ? SUBSTRING(MiddleName,1,1) + " " : "") + TRIM(LastName)  
    ```  
  
-   この例では、 **Contact** テーブルを使用します。 式は、 **Salutation** 列のエントリを検証します。 **Salutation** のエントリまたは空の文字列を返します。  
  
    ```  
    (Salutation == "Sr." || Salutation == "Ms." || Salutation == "Sra." || Salutation == "Mr.") ? Salutation : ""  
    ```  
  
-   この例では、 **Product** テーブルを使用します。 式は、 **Color** 列の最初の文字を大文字に変換し、残りの文字を小文字に変換します。  
  
    ```  
    UPPER(SUBSTRING(Color,1,1)) + LOWER(SUBSTRING(Color,2,15))  
    ```  
  
-   この例では、 **Product** テーブルを使用します。 式は、製品が販売された月数を計算し、 **SellStartDate** または **SellEndDate** 列のどちらかが NULL の場合、文字列 "Unknown" を返します。  
  
    ```  
    !(ISNULL(SellStartDate)) && !(ISNULL(SellEndDate)) ? (DT_WSTR,2)DATEDIFF("mm",SellStartDate,SellEndDate) : "Unknown"  
    ```  
  
-   この例では、 **Product** テーブルを使用します。 式は、 **StandardCost** 列の利益率を計算し、その結果を有効桁数 2 桁に丸めます。 結果はパーセンテージで表されます。  
  
    ```  
    ROUND(ListPrice / StandardCost,2) * 100  
    ```  
  
## <a name="related-tasks"></a>Related Tasks  
 [データ フロー コンポーネントで式を使用する](../use-an-expression-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 pragmaticworks.com の技術記事「 [SSIS 式チート シート](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet)」  
  
  
