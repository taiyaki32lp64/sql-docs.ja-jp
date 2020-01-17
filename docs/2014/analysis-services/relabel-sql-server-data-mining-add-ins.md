---
title: ラベルの変更 (SQL Server データ マイニング アドイン) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- relabel
- data cleaning
ms.assetid: af041b39-fdd1-4cb5-a5ef-2f3ddab84614
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5471720cbd3084c661dec93d9c7f4f680e066b86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070402"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>ラベルの変更 (SQL Server データ マイニング アドイン)
  ![ラベルの変更ツールの office 13 アイコン](media/dm13-relabel.gif "ラベルの変更ツールの Office 13 アイコン")  
  
 Excel 用のデータ マイニング クライアントでは、データの新しいラベルを作成して、分析結果を理解しやすくできます。  
  
 ラベルを変更する理由は次のとおりです。  
  
-   データがコード化された結果を含んでいる場合 (たとえば 1 は男性、2 は女性など)。  
  
-   バケット化した数値の範囲に、わかりやすい名前を付ける場合。  
  
-   長い名前を簡単にする場合。  
  
## <a name="using-the-relabel-wizard"></a>ラベルの変更ウィザードの使用  
  
1.  **データ マイニング**リボンで、をクリックして**クリーン**選び**ラベルの変更**します。  
  
2.  Select the table or data range that has the data you want to fix.修正するデータが含まれているテーブルまたはデータ範囲を選択します。  
  
3.  **ラベルの変更**ページ、ウィザードの 1 つの列が選択に、ドロップダウン リストから列を選択するかで列をクリックして、**データ サンプル**ウィンドウ。  
  
     **データ サンプル**ウィンドウでは、約 50 行のデータにのみ表示されますが、これらをサンプリングする値の適切な分散が表示されることを確認します。  
  
     列のヘッダーをクリックします。**カウント**各値の数で並べ替える。  
  
     並べ替えることもできます**元のラベル**、まずラベル最大股は最小値を変更する場合に便利です。  
  
4.  **ラベルの変更**の値を確認すると、ウィザードのデータ ページ、**元のラベル**列で、グループまたはそれらを編集する方法を決定します。  
  
5.  下の行に新しい値を入力**新しいラベル**します。 値は、既存の値の一覧から選択できます。 新しい値は、入力した直後から再利用に使用できるようになります。  
  
6.  十分な行を入力すると、クリックして **[次へ]** 、し、**先の選択**ページで、選択、ラベルが変更されたデータを保存します。  
  
    -   **現在のワークシートに新しい列として追加します。**  
  
         新しい値が格納されている列をテーブルに追加する場合に選択します。  
  
    -   **新しいワークシートに変更されたシートのデータをコピーします。**  
  
         更新されたデータが格納された新しいワークシートを作成する場合に選択します。  
  
    -   **データの場所を変更します。**  
  
         元データを新しい値に置き換える場合に選択します。  
  
## <a name="see-also"></a>関連項目  
 [データの探索とクリーニング](exploring-and-cleaning-data.md)  
  
  
