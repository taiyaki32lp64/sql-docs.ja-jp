---
title: レポート履歴ページ (レポート マネージャー) |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 0b0841e031ee1a98f4f678406f790996a709e90f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104480"
---
# <a name="report-history-page-report-manager"></a>[レポート履歴] ページ (レポート マネージャー)

[レポート履歴] ページには、一定期間に生成および保存したレポート スナップショットが表示されます。 レポート サーバーで設定されているオプションによっては、新しいスナップショットのみがレポート ヒストリに保存されます。  
  

レポート ヒストリは、常に元のレポートのコンテキスト内で表示されます。 すべてのレポートのヒストリをレポート サーバーの 1 か所に表示することはできません。  
  
レポート ヒストリを生成するには、レポートが自動的に実行されるようにする必要があります (つまり、保存されている資格情報を使用する必要があります。また、パラメーター化されたレポートには、すべてのパラメーターのパラメーター値を含める必要があります)。 レポート ヒストリの生成は、手動またはスケジュールに設定した操作によって行うことができます。 レポート ヒストリの作成方法は、レポートのヒストリ プロパティによって決まります。  
  
レポート ヒストリ スナップショットをクリックすると、そのスナップショットが表示されます。 レポート ヒストリに表示されるスナップショットは、作成日時だけで識別されます。 スナップショットがスケジュールの設定を受けて生成されたのか、手動で生成されたのかを識別する表示はありません。  
  
> [!NOTE]  
>  この機能は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
## <a name="navigation"></a>ナビゲーション  
 ユーザー インターフェイス (UI) のこの場所に移動するには、次の手順に従います。  
  
### <a name="to-open-the-report-history-page"></a>[レポート履歴] ページを開くには  
  
1.  レポート マネージャーを開き、レポート スナップショットを表示するレポートを探します。  
  
2.  レポートの上にマウス ポインターを移動し、下矢印をクリックします。  
  
3.  ドロップダウン メニューの **[レポート履歴の表示]** をクリックします。  
  
## <a name="options"></a>および  
 **削除**  
 1 つ以上のスナップショットを削除する場合にクリックします。 削除するスナップショットの横のチェック ボックスをオンにしてから、 **[削除]** をクリックします。  
  
 **新しいスナップショット**  
 レポート履歴にスナップショットを追加する場合にクリックします。 レポートの [レポート履歴] プロパティ ページの **[レポート履歴の手動作成を許可する]** をオンにしたときに、このボタンが有効になります。  
  
 **[最終実行]**  
 スナップショットが作成された日時が表示されます。 説明をクリックすると、特定のスナップショットが表示されます。  
  
 **Size**  
 レポートのレポート定義とデータを合わせたサイズが表示されます。 この値は、レポート定義とデータがレポート サーバー データベースの領域をどのくらい使用しているのかを示します。 書式を含めた表示レポートの実際のサイズは、この値より大きくなります。 現在のレポートのレポート履歴に保存されているすべてのスナップショットの合計サイズは、かっこ内に表示されます。  
  
## <a name="see-also"></a>参照  
 [表示、またはレポート履歴の削除&#40;レポート マネージャー&#41;](../../2014/reporting-services/view-or-delete-report-history-report-manager.md)   
 [レポート履歴へのスナップショットの追加 &#40;レポート マネージャー&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [全般プロパティ ページ、レポート &#40;レポート マネージャー&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [レポート マネージャー F1 ヘルプ](../../2014/reporting-services/report-manager-f1-help.md)   
 [スナップショット オプション プロパティ ページ&#40;レポート マネージャー&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)