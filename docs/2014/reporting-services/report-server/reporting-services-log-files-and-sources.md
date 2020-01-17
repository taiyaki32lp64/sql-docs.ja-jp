---
title: Reporting Services のログ ファイルとソース | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c0e935cc3d5264a1d2f5569b62db416d85b0427
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103379"
---
# <a name="reporting-services-log-files-and-sources"></a>Reporting Services のログ ファイルとソース
  A[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]レポート サーバーとレポート サーバー環境は、さまざまなサーバー操作および状態に関する情報を記録するログの保存先をサポートします。 ログ記録には、実行のログ記録とトレースのログ記録という 2 つの基本的なカテゴリがあります。 実行のログ記録には、レポート実行統計、監査、パフォーマンスの診断、および最適化に関する情報が含まれます。 トレースのログ記録は、エラー メッセージおよび一般的な診断に関する情報です。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint モード | [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ネイティブ モード  
  
 次の表に、ログの場所やログの内容を表示する方法を含む、各ログに関する追加情報へのリンクを示します。  
  
|Log|説明|  
|---------|-----------------|  
|[レポート サーバー実行ログと ExecutionLog3 ビュー](report-server-executionlog-and-the-executionlog3-view.md)|実行ログは、レポート サーバー データベースに格納されている SQL Server のビューです。<br /><br /> レポート サーバー実行ログには、レポートが実行された日時、実行したユーザー、レポートの配信先、使用された表示形式など、特定のレポートに関するデータが含まれます。|  
|SharePoint トレース ログ|SharePoint で実行されているレポート サーバーの SharePoint トレース ログには、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の情報が含まれています。 SharePoint 統合ログ サービスに対して [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 固有の情報を構成することもできます。 詳細については、「 [SharePoint トレース ログの Reporting Services イベントをオンにする (ULS)](turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)|  
|[レポート サーバー サービスのトレース ログ](report-server-service-trace-log.md)|サービスのトレース ログには、アプリケーションのデバッグまたは問題やイベントの調査を行う場合に役立つ詳細情報が含まれます。<br /><br /> `C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles`|  
|[レポート サーバーの HTTP ログ](report-server-http-log.md)|HTTP ログ ファイルには、レポート サーバー Web サービスおよびレポート マネージャーによって処理された HTTP 要求および HTTP 応答がすべて記録されます。|  
|[Windows アプリケーション ログ](windows-application-log.md)|Microsoft Windows アプリケーション ログには、レポート サーバーのイベントに関する情報が含まれます。|  
|Windows パフォーマンス ログ|Windows パフォーマンス ログには、レポート サーバーのパフォーマンス データが含まれます。 パフォーマンス ログを作成してから、収集するデータを決定するカウンターを選択できます。 詳細については、「 [レポート サーバーのパフォーマンスの監視](monitoring-report-server-performance.md)」を参照してください。|  
|セットアップ ログ ファイル|ログ ファイルはセットアップ中にも作成されます。 セットアップに失敗または成功した際に警告メッセージや他のメッセージが表示された場合、ログ ファイルを検証して問題のトラブルシューティングを行うことができます。 詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。|  
|IIS ログ|Microsoft インターネット インフォメーション サービス (IIS) によって作成されたログ ファイル。 詳細については、次を参照してください。[インターネット インフォメーション サービス (IIS) のログ記録を有効にする方法](https://support.microsoft.com/kb/313437)します。|  
|ビデオ|Microsoft Power Query を使用して [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ログ ファイルを表示する方法を示す短いビデオを表示します。<br /><br /> ![Power Query および SSRS ログに関するビデオを表示](../media/generic-video-thumbnail.png "Power Query および SSRS ログに関するビデオを表示")|  
  
## <a name="see-also"></a>参照  
 [Reporting Services レポート サーバー &#40;ネイティブ モード&#41;](reporting-services-report-server-native-mode.md)   
 [エラーとイベントのリファレンス &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
