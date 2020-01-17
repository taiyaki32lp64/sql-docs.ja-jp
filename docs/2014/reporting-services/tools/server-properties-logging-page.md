---
title: '[サーバーのプロパティ] ([ログ記録] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a04c27fd790a1ad5c4ba453b43af5983a6440e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099529"
---
# <a name="server-properties-logging-page"></a>[サーバーのプロパティ]\([ログ記録] ページ)
  このページを使用すると、レポート サーバーで収集されるレポート実行データに制限を設定できます。 実行データはレポート サーバー データベースに内部的に格納されます。 ネイティブ モードまたは SharePoint 統合モードで実行されているレポート サーバーのレポート処理を追跡できます。 レポート サーバーがスケールアウト配置の一部である場合、レポート実行ログでは、配置全体に対するすべてのレポート処理のレコードが 1 つのログ ファイルで保持されます。  
  
 このページを開くには、開始[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]レポート サーバーへの接続で、レポート サーバーの名前を右クリックし、選択**プロパティ**します。 **[ログ記録]** をクリックするとこのページが開きます。  
  
## <a name="options"></a>および  
 **[レポート実行のログ記録を有効にする]**  
 サーバーのレポート処理に関する情報を作成して保存する場合にクリックします。 このオプションを有効にした場合、レポート サーバーにより、使用されたレポートの種類、レポート処理の頻度、実行されたレポート操作の種類、出力形式、およびレポートの実行者が追跡されます。 ログにキャプチャされるその他のデータ ポイントの詳細については、次を参照してください。[レポート サーバー実行ログと ExecutionLog3 ビュー](../report-server/report-server-executionlog-and-the-executionlog3-view.md)します。  
  
 **[次の日数が経過したログ エントリを削除する]**  
 レポート実行ログからログ エントリが削除されるまでの経過日数を指定します。 既定値は 60 日です。  
  
## <a name="see-also"></a>参照  
 [レポート サーバーのプロパティを設定する (Management Studio)](set-report-server-properties-management-studio.md)   
 [Management Studio でレポート サーバーに接続する](connect-to-a-report-server-in-management-studio.md)   
 [Reporting Services のログ ファイルとソース](../report-server/reporting-services-log-files-and-sources.md)   
 [Management Studio のレポート サーバーの F1 ヘルプ](report-server-in-management-studio-f1-help.md)   
 [レポート サーバー実行ログと ExecutionLog3 ビュー](../report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
