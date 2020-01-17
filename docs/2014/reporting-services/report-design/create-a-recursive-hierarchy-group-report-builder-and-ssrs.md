---
title: 再帰型階層グループの作成 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ec051870966a3a8cf9d2d028d80a2fc36708ba28
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106136"
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>再帰型階層グループの作成 (レポート ビルダーおよび SSRS)
  再帰型階層グループは、組織階層内のマネージャーと従業員のリレーションシップを表す上司/部下構造など、複数の階層レベルから成る単一のレポート データセットのデータを編成します。  
  
 テーブル内のデータを再帰型階層グループにまとめるには、まず、すべての階層データが含まれた単一のデータセットを用意しておく必要があります。グループ化するアイテムとグループ化の基準に使用するアイテムには別々のフィールドを使用する必要があります。 たとえば、従業員をそれぞれのマネージャーの子として再帰的にまとめるデータセットには、従業員名、従業員 ID、マネージャー名、マネージャー ID などが含まれます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-recursive-hierarchy-group"></a>再帰型階層グループを作成するには  
  
1.  デザイン ビューで、テーブルを追加して、表示するデータセット フィールドをドラッグします。 通常、階層として表示する必要のあるフィールドは最初の列にあります。  
  
2.  テーブル内の任意の場所を右クリックして選択します。 選択したテーブルの詳細グループがグループ化ペインに表示されます。 行グループ ペインで、 **[詳細]** を右クリックし、 **[グループの編集]** をクリックします。 **[グループのプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[グループ式]** の **[追加]** をクリックします。 新しい行がグリッドに表示されます。  
  
4.  **[グループ化の条件]** ボックスで、グループ化するフィールドを入力または選択します。  
  
5.  **[詳細設定]** をクリックします。  
  
6.  **[再帰的な親]** ボックスで、グループ化で親として使用するフィールドを入力または選択します。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     レポートを実行します。 レポートに再帰型階層グループが表示されますが、階層を示すインデントはありません。  
  
### <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>再帰型階層グループにインデント レベルを設定するには  
  
1.  階層書式を表示するためのインデント レベルを追加する対象フィールドが含まれているテキスト ボックスをクリックします。 テキスト ボックスのプロパティがプロパティ ペインに表示されます。  
  
    > [!NOTE]  
    >  プロパティ ペインが表示されない場合は、 **[表示]** タブの **[プロパティ]** をクリックします。  
  
2.  [プロパティ] ウィンドウで、展開、`Padding`ノード、をクリックして**左**、ドロップダウン リストから選択し、 **\<式… >** 。  
  
3.  式ペインで次の式を入力します。  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Padding のプロパティはすべて、 *nnyy*形式の文字列が必要です。ここで、 *nn* は数字、 *yy* は単位です。 この例の式では、`Level` 関数を使用する文字列が構築され、再帰レベルに基づいて余白のサイズが増加されます。 たとえば、レベルが 1 の行では余白は 12 ポイント (2 + (1\*10)) に、レベルが 3 の行では 32 ポイント (2 + (3\*10)) になります。 については、`Level`関数を参照してください[レベル](report-builder-functions-level-function.md)します。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     レポートを実行します。 グループ化されたデータの階層ビューがレポートに表示されます。  
  
## <a name="see-also"></a>参照  
 [複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
