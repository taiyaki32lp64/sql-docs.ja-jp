---
title: レポート サーバー システムのプロパティ | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- system-specific properties [Reporting Services]
ms.assetid: cd874117-00e5-4ae6-8629-eb9ba9f40478
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 30455d77efff3c9a9e4f48b9cbeccfa983001220
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128815"
---
# <a name="reporting-services-properties---report-server-system-properties"></a>Reporting Services のプロパティ - レポート サーバーのシステム プロパティ
  次のシステム プロパティ名は予約されています。 同じ名前のユーザー定義プロパティは作成できません。 Web サービス メソッドを使用すると、これらのプロパティの多くの読み取りや修正ができます。  
  
## <a name="properties"></a>Properties  
  
|プロパティ|[説明]|  
|--------------|-----------------|  
|SiteName|ユーザー インターフェイスに表示されるレポート サーバー サイトの名前。 既定値は **Microsoft Report Server** です。 このプロパティには空の文字列を指定できます。 最大長は 8,000 文字です。|  
|SystemSnapshotLimit|レポートに格納されるスナップショットの最大数。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値が **-1**の場合、スナップショットに制限はありません。|  
|SystemReportTimeout|レポート サーバー名前空間で管理されているすべてのレポートの既定のレポート処理タイムアウト値 (秒単位)。 この値はレポート レベルでオーバーライドできます。 このプロパティを設定すると、レポート サーバーは指定された時間が経過した後、レポートの処理を停止しようとします。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値に **-1**を設定すると、名前空間内のレポートが処理中にタイムアウトしません。 既定値は **1800**です。|  
|UseSessionCookies|レポート サーバーがクライアント ブラウザーとの通信時にセッションクッキーを使用する必要があるかどうかを指定します。 既定値は **true**です。|  
|SessionTimeout|セッションがアクティブな状態になっている期間 (秒単位)。 既定値は **600**です。|  
|EnableMyReports|個人用レポート機能が有効になっているかどうかを指定します。 値 **true** は、機能が有効になっていることを示します。|  
|MyReportsRole|ユーザーの個人用レポート フォルダーに、セキュリティ ポリシーを作成する際に使用するロールの名前。 既定値は **My Reports Role**です。|  
|EnableExecutionLogging|レポート実行のログ記録が有効になっているかどうかを示します。 既定値は **true**です。|  
|ExecutionLogDaysKept|レポート実行情報を実行ログに保持する日数。 このプロパティの有効値は **0** ～ **2**、**147**、**483**、**647** です。 値が **0** の場合、エントリは実行ログ テーブルから削除されません。 既定値は **60**です。|  
|SnapshotCompression|スナップショットの圧縮方法を定義します。 既定値は **SQL**です。 有効な値は次のとおりです。<br /><br /> **SQL** = スナップショットは、レポート サーバー データベースへの格納時に圧縮されます。 これは現在の動作です。<br /><br /> **なし** = スナップショットは圧縮されません。<br /><br /> **すべて** = すべてのストレージ オプションのスナップショットが圧縮されます。このオプションには、レポート サーバー データベースやファイル システムが含まれます。|  
|EnableClientPrinting|レポート サーバーからのダウンロードに RSClientPrint ActiveX コントロールが使用可能かどうかを示します。 有効値は **true** および **false**です。 既定値は **true**です。 このコントロールに必要な追加設定に関する詳細については、「 [Reporting Services のクライアント側印刷機能の有効化と無効化](../../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)」を参照してください。|  
|EnableIntegratedSecurity|統合セキュリティをレポート データ ソース接続でサポートするかどうかを決定します。 既定値は **True**です。 有効な値は次のとおりです。<br /><br /> **True** = 統合セキュリティが有効になります。<br /><br /> **False** = 統合セキュリティが有効になりません。 統合セキュリティを使用するように構成されているレポート データ ソースは実行されません。|  
|EnableRemoteErrors|リモート コンピューターからレポートを要求したユーザーに返されるエラー メッセージに、外部エラー情報 (レポート データ ソースに関するエラー情報など) を含めます。 有効値は **true** および **false**です。 既定値は **false**です。 詳細については、「[リモート エラーの有効化 (Reporting Services)](../../../reporting-services/report-server/enable-remote-errors-reporting-services.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 <xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>   
 <xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>   
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [レポート サーバー Web サービス](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [テクニカル リファレンス (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
