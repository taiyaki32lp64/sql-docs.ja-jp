---
title: 追加、変更、または (レポート ビルダーおよび SSRS) レポート パラメーターの既定値の削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10460"
- sql12.rtp.rptdesigner.reportparameters.defaultvalues.f1
- "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c973f249a60b8a6180d5233604a9c372928d0a48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106670"
---
# <a name="add-change-or-delete-default-values-for-a-report-parameter-report-builder-and-ssrs"></a>レポート パラメーターの既定値の追加、変更、または削除 (レポート ビルダーおよび SSRS)
  レポート パラメーターを作成した後、既定値のリストを指定できます。 すべてのパラメーターに有効な既定値がある場合、レポートは、最初に表示またはプレビューしたときに自動的に実行します。  
  
 レポート パラメーターは単一値または複数値を表すことができます。 単一値については、リテラルまたは式を指定できます。 複数値については、静的リストまたはレポート データセットからのリストを指定できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 レポートをパブリッシュした後、パラメーター プロパティの値をレポート サーバーに設定して、レポート作成ツールのレポートで定義される既定値をオーバーライドできます。 リンク レポートを作成して、既定のパラメーター値の複数のセットを指定することもできます。 詳細については、「  [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](report-parameters-report-builder-and-report-designer.md)  
  
### <a name="to-add-or-change-the-default-values-for-a-report-parameter"></a>レポート パラメーターの既定値を追加または変更するには  
  
1.  レポート データ ペインで **[パラメーター]** ノードを展開します。 パラメーターを右クリックし、 **[編集]** をクリックします。 **[レポート パラメーターのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  レポート データ ペインが表示されていない場合は、 **[表示]** をクリックしてから **[レポート データ]** をクリックします。  
  
2.  **[既定値]** をクリックします。  
  
3.  既定のオプションを選択します。  
  
    -   1 つの値または値のリストを手動で指定するには、 **[値の指定]** をクリックします。 **[追加]** をクリックして、 **[値]** ボックスに値を入力します。 値を求める式を記述することもできます。 データ型はパラメーターのデータ型と一致する必要があります。 フィールド名は、パラメーターの式では使用できません。  
  
         複数値パラメーターの場合は、指定する値の数だけこの手順を繰り返します。 この一覧に表示されるアイテムの順序によって、ユーザーに表示されるドロップダウン リストのアイテムの順序が決まります。 一覧のアイテムの順序を変更するには、 **[値]** ボックスをクリックしてアイテムを選択し、上矢印および下矢印ボタンを使用して一覧内のアイテムを上下に移動します。  
  
    -   値を取得する既存のデータセットの名前を指定するには、 **[クエリから値を取得]** をクリックします。 **[データセット]** で、データセットの名前を選択します。  
  
         **[値フィールド]** で、パラメーター値を指定するフィールドの名前を選択します。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-the-default-values-for-a-report-parameter"></a>レポート パラメーターの既定値を削除するには  
  
1.  レポート データ ペインで **[パラメーター]** ノードを展開します。 パラメーターを右クリックし、 **[編集]** をクリックします。 **[レポート パラメーターのプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[既定値]** をクリックします。  
  
3.  **[次のオプションから 1 つを選択]** で、 **[既定値なし]** をクリックします。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](report-parameters-report-builder-and-report-designer.md)   
 [カスケード型パラメーターのレポートへの追加 (レポート ビルダーおよび SSRS)](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [チュートリアル: レポートへのパラメーターの追加 &#40;レポート ビルダー&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Parameters コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)   
 [レポート パラメーターの順序の変更 (レポート ビルダーおよび SSRS)](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [レポート パラメーターの追加、変更、または削除 (レポート ビルダーおよび SSRS)](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
