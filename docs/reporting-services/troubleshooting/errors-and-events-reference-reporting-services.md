---
title: "エラーおよびイベント リファレンス (Reporting Services) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- messages [Reporting Services]
- errors [Reporting Services]
- Reporting Services, errors and events
- troubleshooting [Reporting Services], errors
- events [Reporting Services]
ms.assetid: 818b4cc1-e65d-4f1a-bf7d-fe269e6dd739
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a0738c8ac950a86ef877c26fd8b6a0f6a6b075f2
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="errors-and-events-reference-reporting-services"></a>エラーとイベントのリファレンス (Reporting Services)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]のエラーとイベントについて説明します。 エラー情報は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のログ ファイルにも記録されます。 使用可能なログ ファイルの種類とログの表示方法の詳細については、「 [Reporting Services のログ ファイルとソース](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)」を参照してください。  
  
## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Reporting Services のエラー メッセージの原因と解決方法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Web サイトでは、最も頻繁に検索されているエラーの原因と解決方法についての情報を入手できます。 詳細については、「 [Reporting Services エラーの原因と解決方法](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md)」を参照してください。  
  
## <a name="report-server-events"></a>レポート サーバーのイベント  
 次のレポート サーバーのイベントは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーション ログに記録されます。  
  
|イベント ID|型|カテゴリ|ソース|Description|  
|--------------|----------|--------------|------------|-----------------|  
|106|[エラー]|スケジューリング|レポート サーバー|スケジュールされた操作 (たとえば、レポートのサブスクリプションおよび配信) を定義する場合は、SQL Server エージェントを実行する必要があります。|  
|[107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)|[エラー]|起動/シャットダウン|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<ソース >*レポート サーバー データベースに接続できません。 詳細については、「[レポート サーバー Windows サービス &#40;MSSQLServer&#41; 107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)」を参照してください。|  
|108|[エラー]|拡張子|レポート サーバー<br /><br /> レポート マネージャー|*\<ソース >*配信、データ処理または表示拡張機能を読み込むことはできません。<br /><br /> 最も可能性が高い原因として、配置が完全でないか、拡張機能が削除された可能性があります。 詳細については、SQL Server オンライン ブックの「 [データ処理拡張機能の配置](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md) 」および「 [配信拡張機能の配置](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)」を参照してください。|  
|109|情報|管理|レポート サーバー<br /><br /> レポート マネージャー|構成ファイルが変更されています。 詳細については、「 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)」を参照してください。|  
|110|警告|管理|レポート サーバー<br /><br /> レポート マネージャー|1 つの構成ファイルの設定が変更され、設定が無効になっています。 代わりに既定値が使用されます。 詳細については、「 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)」を参照してください。|  
|111|[エラー]|ログ記録|レポート サーバー<br /><br /> レポート マネージャー|*\<ソース >*トレース ログを作成することはできません。 詳細については、「 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
|112|警告|Security|レポート サーバー|レポート サーバーは、サービス拒否攻撃 (DoS) の可能性を検出しました。 詳細については、「 [Reporting Services のセキュリティと保護](../../reporting-services/security/reporting-services-security-and-protection.md)」を参照してください。|  
|113|[エラー]|ログ記録|レポート サーバー|レポート サーバーでは、パフォーマンス カウンターを作成できません。|  
|114|[エラー]|起動/シャットダウン|レポート マネージャー|レポート マネージャーは ReportServer サービスに接続できません。|  
|115|警告|スケジューリング|スケジュールおよび配信のプロセッサ|SQL Server エージェント キューの定期タスクは、変更または削除されました。|  
|116|[エラー]|Internal|レポート サーバー<br /><br /> レポート マネージャー<br /><br /> スケジュールおよび配信のプロセッサ|内部エラーが発生しました。|  
|117|[エラー]|起動/シャットダウン|レポート サーバー|レポート サーバー データベースのバージョンが無効です。|  
|118|警告|ログ記録|レポート サーバー<br /><br /> レポート マネージャー|予期されたディレクトリの場所にトレース ログがありません。既定のディレクトリに新しいトレース ログが作成されます。 詳細については、「 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
|119|[エラー]|アクティブ化|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<ソース >*レポート サーバー データベースの内容へのアクセスが与えられていません。|  
|120|[エラー]|アクティブ化|レポート サーバー|対称キーの暗号化を解除できません。 最も可能性が高い原因として、サービスの実行に使用されるアカウントが変更されたことが挙げられます。 詳細については、次を参照してください[構成と暗号化キーの管理 &#40;。SSRS 構成マネージャー &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|121|[エラー]|起動/シャットダウン|レポート サーバー|リモート プロシージャ コール (RPC) サービスを開始できませんでした。|  
|122|警告|Delivery|スケジュールおよび配信のプロセッサ|スケジュールおよび配信のプロセッサは、電子メールの配信に使用している SMTP サーバーに接続できません。 SMTP サーバー接続の詳細については、「 [電子メール配信用にレポート サーバーを構成する (SSRS 構成マネージャー)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)」を参照してください。|  
|123|警告|ログ記録|レポート サーバー<br /><br /> レポート マネージャー|レポート サーバーでは、トレース ログへの書き込みに失敗しました。 トレース ログの詳細については、「 [レポート サーバー サービスのトレース ログ](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
|124|情報|アクティブ化|レポート サーバー|レポート サーバー サービスが初期化されました。 詳細については、次を参照してください。[レポート サーバー &#40; を初期化します。SSRS 構成マネージャー &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).|  
|125|情報|アクティブ化|レポート サーバー|データの暗号化に使用したキーは、正常に展開されました。 キーの詳細については、次を参照してください[構成と暗号化キーの管理 &#40;。SSRS 構成マネージャー &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|126|情報|アクティブ化|レポート サーバー|データの暗号化に使用したキーは、正常に適用されました。 キーの詳細については、次を参照してください[構成と暗号化キーの管理 &#40;。SSRS 構成マネージャー &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|127|情報|アクティブ化|レポート サーバー|暗号化されたコンテンツは、正常にレポート サーバー データベースから削除されました。 詳細については、回復できない暗号化されたデータを削除すると、次を参照してください[構成と暗号化キーの管理 &#40;。SSRS 構成マネージャー &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|128|[エラー]|アクティブ化|レポート サーバー|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントのエディションが異なる場合は一緒に使用することはできません。|  
|129|[エラー]|管理|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|暗号化された構成ファイルの設定の暗号化を解除できません。|  
|130|[エラー]|管理|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<ソース >*構成ファイルを見つけることができません。 レポート サーバーでは、構成ファイルが必要です。|  
|131|[エラー]|Security|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|暗号化されたユーザー データ値の暗号化を解除できませんでした。|  
|132|[エラー]|Security|レポート サーバー|ユーザー データの暗号化中にエラーが発生しました。 値は保存されません。|  
|133|[エラー]|管理|レポート サーバー<br /><br /> レポート マネージャー<br /><br /> スケジュールおよび配信のプロセッサ|構成ファイルを読み込めませんでした。 このエラーは、XML が無効な場合に発生することがあります。|  
|134|[エラー]|管理|レポート サーバー|レポート サーバーでは、構成ファイルの設定の値を暗号化できませんでした。|  
  
## <a name="see-also"></a>参照  
 [Reporting Services のサブスクリプションを監視する](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)   
 [Reporting Services のログ ファイルとソース](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]
