---
title: 指定されたデータ型およびコンテンツ タイプ (基本的なデータ マイニング チュートリアル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 583a6fda2dbb4698405a3d69f33955531b3c1c10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62720048"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>データ型およびコンテンツの種類の指定 (基本的なデータ マイニング チュートリアル)
  前の作業では、構造の作成およびモデルのトレーニングに使用する列を選択しました。次の作業では、ウィザードによって設定されたデータ型およびコンテンツの種類を変更します。  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>各列のコンテンツの種類とデータ型の確認および変更  
  
1.  **指定列のコンテンツおよびデータ型**] ページで [**検出**既定データと各列のコンテンツの種類を決定するアルゴリズムを実行します。  
  
2.  エントリを確認、**コンテンツの種類**と**データ型**列設定が次の表に示したものと同じであることを確認して、必要な場合に変更します。  
  
     通常は、ウィザードによって数値が検出され適切な数値データ型が割り当てられますが、数値をテキストとして処理することが必要なシナリオも数多くあります。 たとえば、 **GeographyKey**ことがあります。 この識別子の算術演算を実行するために、テキストとして処理する必要があります。  
  
    |[列]|コンテンツの種類|データ型|  
    |------------|------------------|---------------|  
    |**アドレス Line1**|**不連続**|**Text**|  
    |**アドレス Line2**|**不連続**|**Text**|  
    |**経過時間**|**継続的です**|**Long**|  
    |**Bike Buyer**|**不連続**|**Long**|  
    |**Commute Distance**|**不連続**|**Text**|  
    |**CustomerKey**|**[キー]**|**Long**|  
    |**DateLastPurchase**|**継続的です**|**Date**|  
    |**Email Address**|**不連続**|**Text**|  
    |**English Education**|**不連続**|**Text**|  
    |**English Occupation**|**不連続**|**Text**|  
    |**FirstName**|**不連続**|**Text**|  
    |**Gender**|**不連続**|**Text**|  
    |**Geography Key**|**不連続**|**Text**|  
    |**House Owner Flag**|**不連続**|**Text**|  
    |**[Last Name]**|**不連続**|**Text**|  
    |**Marital Status**|**不連続**|**Text**|  
    |**Number Cars Owned**|**不連続**|**Long**|  
    |**Number Children At Home**|**不連続**|**Long**|  
    |**Region**|**不連続**|**Text**|  
    |**Total Children**|**不連続**|**Long**|  
    |**Yearly Income**|**継続的です**|**Double**|  
  
3.  **[次へ]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [構造のテスト データ セットの指定&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>このレッスンの前の作業  
 [ターゲット メーリングのマイニング モデル構造の作成&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>関連項目  
 [コンテンツの種類 &#40;です。 データ マイニング&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [データ型 (データ マイニング)](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
