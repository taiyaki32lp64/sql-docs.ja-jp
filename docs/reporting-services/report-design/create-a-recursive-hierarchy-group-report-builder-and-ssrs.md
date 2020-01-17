---
title: 再帰型階層グループの作成 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8a506442cca08dfa40cb3665571662a477ef5345
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581561"
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>再帰型階層グループの作成 (レポート ビルダーおよび SSRS)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートでは、再帰型階層グループは、組織階層内のマネージャーと従業員のリレーションシップを表す上司/部下構造など、複数の階層レベルから成る単一のレポート データセットのデータを編成します。  
  
 テーブル内のデータを再帰型階層グループにまとめるには、まず、すべての階層データが含まれた単一のデータセットを用意しておく必要があります。グループ化するアイテムとグループ化の基準に使用するアイテムには別々のフィールドを使用する必要があります。 たとえば、従業員をそれぞれのマネージャーの子として再帰的にまとめるデータセットには、従業員名、従業員 ID、マネージャー名、マネージャー ID などが含まれます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-recursive-hierarchy-group"></a>再帰型階層グループを作成するには  
  
1.  デザイン ビューで、テーブルを追加して、表示するデータセット フィールドをドラッグします。 通常、階層として表示する必要のあるフィールドは最初の列にあります。  
  
2.  テーブル内の任意の場所を右クリックして選択します。 選択したテーブルの詳細グループがグループ化ペインに表示されます。 行グループ ペインで、 **[詳細]** を右クリックし、 **[グループの編集]** をクリックします。 **[グループのプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[グループ式]** の **[追加]** をクリックします。 新しい行がグリッドに表示されます。  
  
4.  **[グループ化の条件]** ボックスで、グループ化するフィールドを入力または選択します。  
  
5.  **[詳細設定]** をクリックします。  
  
6.  **[再帰的な親]** ボックスで、グループ化で親として使用するフィールドを入力または選択します。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     レポートを実行します。 レポートに再帰型階層グループが表示されますが、階層を示すインデントはありません。  
  
## <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>再帰型階層グループにインデント レベルを設定するには  
  
1.  階層書式を表示するためのインデント レベルを追加する対象フィールドが含まれているテキスト ボックスをクリックします。 テキスト ボックスのプロパティがプロパティ ペインに表示されます。  
  
    > [!NOTE]  
    >  プロパティ ペインが表示されない場合は、 **[表示]** タブの **[プロパティ]** をクリックします。  
  
2.  プロパティ ペインで、 **[余白]** ノードを展開して **[左]** をクリックします。次に、ドロップダウン リストから **[\<式...>]** を選びます。  
  
3.  式ペインで次の式を入力します。  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Padding のプロパティはすべて、 *nnyy*形式の文字列が必要です。ここで、 *nn* は数字、 *yy* は単位です。 この例の式では、 **Level** 関数を使用する文字列が構築され、再帰レベルに基づいて余白のサイズが増加されます。 たとえば、レベルが 1 の行では余白は 12 ポイント (2 + (1\*10)) に、レベルが 3 の行では 32 ポイント (2 + (3\*10)) になります。 **Level** 関数の詳細については、「 [Level](../../reporting-services/report-design/report-builder-functions-level-function.md)」を参照してください。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     レポートを実行します。 グループ化されたデータの階層ビューがレポートに表示されます。  
  
## <a name="see-also"></a>参照  
 [複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
