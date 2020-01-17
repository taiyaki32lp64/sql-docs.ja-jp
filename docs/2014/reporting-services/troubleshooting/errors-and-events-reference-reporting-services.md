---
title: エラーとイベントのリファレンス (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- messages [Reporting Services]
- errors [Reporting Services]
- Reporting Services, errors and events
- troubleshooting [Reporting Services], errors
- events [Reporting Services]
ms.assetid: 818b4cc1-e65d-4f1a-bf7d-fe269e6dd739
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2708c2609d23c6094cd69bddd08d958a85262d88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099316"
---
# <a name="errors-and-events-reference-reporting-services"></a>エラーとイベントのリファレンス (Reporting Services)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]のエラーとイベントについて説明します。 エラー情報は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のログ ファイルにも記録されます。 使用可能なログ ファイルの種類とログの表示方法の詳細については、「 [Reporting Services のログ ファイルとソース](../report-server/reporting-services-log-files-and-sources.md)」を参照してください。  
  
## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Reporting Services のエラー メッセージの原因と解決方法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Web サイトでは、最も頻繁に検索されているエラーの原因と解決方法についての情報を入手できます。 詳細については、「 [Reporting Services エラーの原因と解決方法](cause-and-resolution-of-reporting-services-errors.md)」を参照してください。  
  
## <a name="report-server-events"></a>レポート サーバーのイベント  
 次のレポート サーバーのイベントは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーション ログに記録されます。  
  
|イベント ID|型|カテゴリ|ソース|説明|  
|--------------|----------|--------------|------------|-----------------|  
|106|[エラー]|スケジューリング|レポート サーバー|スケジュールされた操作 (たとえば、レポートのサブスクリプションおよび配信) を定義する場合は、SQL Server エージェントを実行する必要があります。|  
|[107](../../relational-databases/errors-events/mssqlserver-107-database-engine-error.md)|[エラー]|起動/シャットダウン|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<Source>* はレポート サーバー データベースに接続できません。 詳細については、「[レポート サーバー Windows サービス &#40;MSSQLServer&#41; 107](../../relational-databases/errors-events/mssqlserver-107-database-engine-error.md)」を参照してください。|  
|108|[エラー]|拡張子|レポート サーバー<br /><br /> レポート マネージャー|*\<Source>* は、配信、データ処理、または表示拡張機能を読み込めません。<br /><br /> 最も可能性が高い原因として、配置が完全でないか、拡張機能が削除された可能性があります。 詳細については、SQL Server オンライン ブックの「 [データ処理拡張機能の配置](../extensions/data-processing/deploying-a-data-processing-extension.md) 」および「 [配信拡張機能の配置](../extensions/delivery-extension/deploying-a-delivery-extension.md)」を参照してください。|  
|109|[情報]|管理|レポート サーバー<br /><br /> レポート マネージャー|構成ファイルが変更されています。 詳細については、「 [Reporting Services 構成ファイル](../report-server/reporting-services-configuration-files.md)」を参照してください。|  
|110|警告|管理|レポート サーバー<br /><br /> レポート マネージャー|1 つの構成ファイルの設定が変更され、設定が無効になっています。 代わりに既定値が使用されます。 詳細については、「 [Reporting Services 構成ファイル](../report-server/reporting-services-configuration-files.md)」を参照してください。|  
|111|[エラー]|ログ記録|レポート サーバー<br /><br /> レポート マネージャー|*\<Source>* はトレース ログを作成できません。 詳細については、「 [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md)」を参照してください。|  
|112|警告|セキュリティ|レポート サーバー|レポート サーバーは、サービス拒否攻撃 (DoS) の可能性を検出しました。 詳細については、「 [Reporting Services のセキュリティと保護](../security/reporting-services-security-and-protection.md)」を参照してください。|  
|113|[エラー]|ログ記録|レポート サーバー|レポート サーバーでは、パフォーマンス カウンターを作成できません。|  
|114|[エラー]|起動/シャットダウン|レポート マネージャー|レポート マネージャーは ReportServer サービスに接続できません。|  
|115|警告|スケジューリング|スケジュールおよび配信のプロセッサ|SQL Server エージェント キューの定期タスクは、変更または削除されました。|  
|116|[エラー]|Internal|レポート サーバー<br /><br /> レポート マネージャー<br /><br /> スケジュールおよび配信のプロセッサ|内部エラーが発生しました。|  
|117|[エラー]|起動/シャットダウン|レポート サーバー|レポート サーバー データベースのバージョンが無効です。|  
|118|警告|ログの記録|レポート サーバー<br /><br /> レポート マネージャー|予期されたディレクトリの場所にトレース ログがありません。既定のディレクトリに新しいトレース ログが作成されます。 詳細については、「 [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md)」を参照してください。|  
|119|[エラー]|アクティブ化|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<Source>* には、レポート サーバー データベースのコンテンツへのアクセス権がありません。|  
|120|[エラー]|アクティブ化|レポート サーバー|対称キーの暗号化を解除できません。 最も可能性が高い原因として、サービスの実行に使用されるアカウントが変更されたことが挙げられます。 詳細については、「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|121|[エラー]|起動/シャットダウン|レポート サーバー|リモート プロシージャ コール (RPC) サービスを開始できませんでした。|  
|122|警告|Delivery|スケジュールおよび配信のプロセッサ|スケジュールおよび配信のプロセッサは、電子メールの配信に使用している SMTP サーバーに接続できません。 SMTP サーバー接続の詳細については、次を参照してください。[レポート サーバー電子メール配信用に構成&#40;SSRS 構成マネージャー&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)します。|  
|123|警告|ログの記録|レポート サーバー<br /><br /> レポート マネージャー|レポート サーバーでは、トレース ログへの書き込みに失敗しました。 トレース ログの詳細については、「 [レポート サーバー サービスのトレース ログ](../report-server/report-server-service-trace-log.md)」を参照してください。|  
|124|[情報]|アクティブ化|レポート サーバー|レポート サーバー サービスが初期化されました。 詳細については、「[レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md)」を参照してください。|  
|125|[情報]|アクティブ化|レポート サーバー|データの暗号化に使用したキーは、正常に展開されました。 キーの詳細については、「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|126|[情報]|アクティブ化|レポート サーバー|データの暗号化に使用したキーは、正常に適用されました。 キーの詳細については、「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|127|[情報]|アクティブ化|レポート サーバー|暗号化されたコンテンツは、正常にレポート サーバー データベースから削除されました。 復元できない暗号化されたデータの削除に関する詳細については、「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|128|[エラー]|アクティブ化|レポート サーバー|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントのエディションが異なる場合は一緒に使用することはできません。|  
|129|[エラー]|管理|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|暗号化された構成ファイルの設定の暗号化を解除できません。|  
|130|[エラー]|管理|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<Source>* は構成ファイルを見つけられません。 レポート サーバーでは、構成ファイルが必要です。|  
|131|[エラー]|セキュリティ|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|暗号化されたユーザー データ値の暗号化を解除できませんでした。|  
|132|[エラー]|セキュリティ|レポート サーバー|ユーザー データの暗号化中にエラーが発生しました。 値は保存されません。|  
|133|[エラー]|管理|レポート サーバー<br /><br /> レポート マネージャー<br /><br /> スケジュールおよび配信のプロセッサ|構成ファイルを読み込めませんでした。 このエラーは、XML が無効な場合に発生することがあります。|  
|134|[エラー]|管理|レポート サーバー|レポート サーバーでは、構成ファイルの設定の値を暗号化できませんでした。|  
  
## <a name="see-also"></a>参照  
 [Reporting Services のサブスクリプションを監視する](../subscriptions/monitor-reporting-services-subscriptions.md)   
 [Reporting Services のログ ファイルとソース](../report-server/reporting-services-log-files-and-sources.md)  
  
  
