---
title: '[アイテムの移動] ページ (レポート マネージャー) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fc83b8d2-bc79-4b56-8970-34a1cbbcc176
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f64a9e9efe180c2db776c38553403e5f7cdfac9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108222"
---
# <a name="move-items-page-report-manager"></a>[<ItemName> を移動] ページ (レポート マネージャー)
  [アイテムの移動] ページは、レポート、フォルダー、またはその他のアイテムを、レポート サーバー上の新しい場所に移動するときに使用します。 レポート サーバーの名前空間内の移動先を参照する際は、移動先のパスを入力することも、ツリー ビューを使用することもできます。 移動できるアイテムは、移動する権限を持っていて、現在のレポート サーバーに保存されているアイテムに限ります。  
  
 別のアイテムによって参照されるアイテム (たとえば、多数のレポートによって参照される共有データ ソースまたはモデル) を移動すると、そのアイテムのパス情報は自動的に更新されます。 共有データ ソースを移動しても、それを使用するレポートおよびモデルへのデータ ソース接続は切断されません。 共有データ ソースやモデルの移動先がユーザーに権限のないフォルダーであっても、ユーザーは引き続きそのデータ ソースやモデルを参照するレポートを実行できます。ただし、権限のないユーザーに対してはフォルダー階層にアイテムが表示されなくなります。  
  
 **[場所]** にはフォルダーへの完全なパスを、ルート フォルダー名から指定します。 フォルダーを参照する際は、パス名を入力することも、ツリー ビューを使用することもできます。  
  
> [!NOTE]  
>  すべてのアイテムを移動できるとは限りません。 [ホーム]、[個人用レポート]、[Users フォルダー] などの予約済みフォルダーは移動できません。 レポート履歴またはスナップショットは他の場所に移動できません。 履歴およびスナップショットは、基になるレポートと同じ場所に常に配置し、そのレポートからアクセスします。  
  
## <a name="navigation"></a>ナビゲーション  
 ユーザー インターフェイス (UI) のこの場所に移動するには、次の手順に従います。  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-details-view"></a>詳細ビューの [コンテンツ] ページから [<ItemName> を移動] ページを開くには  
  
1.  レポート マネージャーを開き、移動するアイテムが含まれるフォルダーに移動します。 レポート マネージャーのホーム ページからアイテムを移動することもできます。  
  
2.  ツール バーの **[詳細ビュー]** をクリックします。  
  
    > [!NOTE]  
    >  **[タイル ビュー]** しか表示されない場合は、既に **[詳細ビュー]** になっています。  
  
3.  アイテムの横にあるチェック ボックスをオンにし、ツール バーの **[移動]** をクリックします。 複数のアイテムを同じ新規の場所に移動する場合は、複数のチェック ボックスをオンにできます。  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-tiles-view"></a>タイル ビューの [コンテンツ] ページから [<ItemName> を移動] ページを開くには  
  
1.  レポート マネージャーを開き、移動するアイテムが含まれるフォルダーに移動します。 レポート マネージャーのホーム ページからアイテムを移動することもできます。  
  
2.  ツール バーの **[タイル ビュー]** をクリックします。  
  
    > [!NOTE]  
    >  **[詳細ビュー]** しか表示されない場合は、既に **[タイル ビュー]** になっています。  
  
3.  アイテムの上にマウス ポインターを移動し、下矢印をクリックします。  
  
4.  ドロップダウン メニューの **[移動]** をクリックします。  
  
###### <a name="to-open-the-move-items-page-from-the-general-properties-page-of-an-item"></a>アイテムの [全般] プロパティ ページから [<ItemName> を移動] ページを開くには  
  
1.  レポート マネージャーを開き、移動するアイテムが含まれるフォルダーに移動します。 レポート マネージャーのホーム ページからアイテムを移動することもできます。  
  
2.  アイテムの上にマウス ポインターを移動し、下矢印をクリックします。  
  
3.  ドロップダウン メニューの **[管理]** をクリックします。 この操作により、アイテムの [全般] プロパティ ページが開きます。  
  
4.  アイテムのツール バーの **[移動]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [[全般] プロパティ ページ、フォルダー&#40;レポート マネージャー&#41;](../../2014/reporting-services/general-properties-page-folders-report-manager.md)   
 [全般プロパティ ページ、レポート &#40;レポート マネージャー&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [[全般] プロパティ ページ、リソース&#40;レポート マネージャー&#41;](../../2014/reporting-services/general-properties-page-resources-report-manager.md)   
 [[全般] プロパティ ページ、共有データ ソース&#40;レポート マネージャー&#41;](../../2014/reporting-services/general-properties-page-shared-data-sources-report-manager.md)   
 [レポート マネージャー F1 ヘルプ](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
