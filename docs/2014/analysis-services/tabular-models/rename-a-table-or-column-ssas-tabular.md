---
title: テーブルまたは列 (SSAS テーブル) の名前を変更する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.renametableorcolumn.f1
ms.assetid: 88061a39-c5aa-403d-a52b-7fdb365fc235
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d9d9f11b8713ea26cd79e95b9edc3f36c0bf3564
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066686"
---
# <a name="rename-a-table-or-column-ssas-tabular"></a>テーブルまたは列名の変更 (SSAS テーブル)
  **テーブルのインポート ウィザード**の **[テーブルとビューの選択]** ページで**表示名**を入力することにより、インポート処理中にテーブルの名前を変更できます。 **テーブルのインポート ウィザード** の **[SQL クエリの指定]** ページでクエリを指定してデータをインポートした場合は、テーブルおよび列の名前を変更することもできます。  
  
 データをモデルに追加すると、テーブルの名前 (つまりタイトル) がモデル デザイナーの下部にあるテーブル タブに表示されます。 テーブルの名前は、より適切な名前に変更できます。 列の名前は、データをモデルに追加した後で変更することもできます。 このオプションは、複数のソースからデータをインポートして、別のテーブルの列にわかりやすい名前を付けたい場合に特に重要となります。  
  
### <a name="to-rename-a-table"></a>テーブル名を変更するには  
  
1.  モデル デザイナーで、名前を変更するテーブルが入っているタブを右クリックして、 **[名前の変更]** をクリックします。  
  
2.  新しい名前を入力します。  
  
    > [!NOTE]  
    >  **[テーブルのプロパティの編集]** ダイアログ ボックスを使用すると、接続情報や列マッピングなど、名前以外のテーブルのプロパティを編集できます。 ただし、このダイアログ ボックスでは、名前を変更できません。  
  
### <a name="to-rename-a-column"></a>列名を変更するには  
  
1.  モデル デザイナーで名前を変更する列の見出しをダブルクリックするか、見出しを右クリックし、コンテキスト メニューの **[列名の変更]** をクリックします。  
  
2.  新しい名前を入力します。  
  
## <a name="naming-requirements-for-columns-and-tables"></a>列とテーブルの名前付けに関する要件  
 次の単語と文字をテーブルまたは列の名前で使用することはできません。  
  
-   先頭または末尾の空白。  
  
-   制御文字。  
  
-   (これは、Analysis Services オブジェクトの名前に無効な) 次の文字:.、;'/。\\*|?& % $! + = (){}<>  
  
-   Analysis Services の予約済みキーワード。多次元式 (MDX) とデータ マイニング拡張機能 (DMX) の関数名と演算子を含みます。  
  
## <a name="effect-of-renaming-on-existing-tables-columns-and-calculations"></a>既存のテーブル、列、および計算名を変更することによる影響  
 テーブルの名前を変更するたびに、基になるテーブル オブジェクトの名前も変更されます。このテーブル オブジェクトには複数の列またはメジャーが含まれていることがあります。 そのため、テーブル内のすべての列、およびテーブルを使用するすべてのリレーションシップを更新して、定義内で新しい名前を使用するようにする必要があります。 この更新は自動的に行われる場合があります。 メジャーは自動的に更新されません。  
  
 さらに名前を変更したテーブルを使用する計算、および名前を変更したテーブルの列を使用する計算を更新し、これらの計算から派生したデータも更新して再計算する必要があります。 影響を受けるテーブルと計算の数によっては、完了までに時間がかかることがあります。 このため、テーブル名を変更するタイミングとしては、インポート処理時か、複雑なリレーションシップや計算を構築する前が最適です。  
  
## <a name="see-also"></a>参照  
 [テーブルと列 &#40;SSAS テーブル&#41;](tables-and-columns-ssas-tabular.md)   
 [PowerPivot からインポート&#40;SSAS 表形式&#41;](import-from-power-pivot-ssas-tabular.md)   
 [Analysis Services からのインポート (SSAS テーブル)](import-from-analysis-services-ssas-tabular.md)  
  
  
