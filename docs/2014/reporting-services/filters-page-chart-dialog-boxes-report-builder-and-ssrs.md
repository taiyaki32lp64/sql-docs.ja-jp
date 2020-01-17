---
title: フィルター ページで、グラフのダイアログ ボックス (レポート ビルダーおよび SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.categorygroupproperties.filters.f1
- "10409"
- sql12.rtp.rptdesigner.seriesgroupproperties.filters.f1
- "10401"
- sql12.rtp.rptdesigner.chartproperties.filters.f1
- "10165"
ms.assetid: fab97b2f-d53f-42f2-900c-c159653d89ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 268ca47f33e8e2514b297c2bb2a30eb77b7a8f08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109139"
---
# <a name="filters-page-chart-dialog-boxes-report-builder-and-ssrs"></a>[フィルター] ページ (グラフのダイアログ ボックス) (レポート ビルダーおよび SSRS)
  クリックして**フィルター**でします。  
  
-   **[カテゴリ グループのプロパティ]** ダイアログ ボックス。カテゴリ別にグループ化された系列内のデータ ポイントをフィルターできます。  
  
-   **[グラフのプロパティ]** ダイアログ ボックス。グラフのフィルター処理オプションを定義できます。  
  
-   **[系列グループのプロパティ]** ダイアログ ボックス。選択したグループの系列の数を制限できます。  
  
## <a name="options"></a>および  
 **[追加]**  
 クリックして、一覧に新しいフィルター句を追加します。  
  
 **削除**  
 選択したフィルター句を一覧から削除します。  
  
 **上矢印**  
 クリックして、選択したフィルターを一覧内で上に移動します。  
  
 **下矢印**  
 クリックして、選択したフィルターを一覧内で下に移動します。  
  
 **[式]**  
 フィルターを適用する式を入力または選択します。 式を編集するには、式 ( **[fx]** ) ボタンをクリックします。  
  
 **データ型**  
 **[値]** のデータ型を選択します。 可能であれば、 **[式]** のデータ型と一致するデータ型を選択します。  
  
 **[式]** および **[値]** の値は、同じデータ型に評価される必要があります。 たとえば、 **[式]** が System.Int32 データ型のフィールドに設定され、 **[値]** が 7 に設定されている場合、ドロップダウン リストから **Integer**を選択します。  
  
 必要なデータ型のオプションがドロップダウン リストにない場合は、値を正しいデータ型に変換する式を作成します。 詳細については、「[フィルター式の例 &#40;レポート ビルダーおよび SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)」を参照してください。  
  
 **[演算子]**  
 式と値の比較に使用する演算子を選択します。  
  
 **[値]**  
 **[式]** で指定した式の評価対象となる式または値を入力します。  
  
## <a name="see-also"></a>参照  
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 &#40;レポート ビルダーおよび SSRS&#41;](report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [式の例 (レポート ビルダーおよび SSRS)](report-design/expression-examples-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
