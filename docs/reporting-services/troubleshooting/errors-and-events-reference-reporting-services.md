---
title: エラーとイベントのリファレンス (Reporting Services) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 06/12/2019
ms.openlocfilehash: d2d1a8c853bd4ad577dd1c0ced9aed47b15a2ee7
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68258543"
---
# <a name="errors-and-events-reference-reporting-services"></a>エラーとイベントのリファレンス (Reporting Services)

この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のエラーとイベントについて説明します。 エラー情報は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のログ ファイルにも記録されます。 使用可能なログ ファイルの種類とログの表示方法の詳細については、「 [Reporting Services のログ ファイルとソース](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)」を参照してください。  

## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Reporting Services のエラー メッセージの原因と解決方法  

[!INCLUDE[msCoName](../../includes/msconame-md.md)] Web サイトでは、最も頻繁に検索されているエラーの原因と解決方法についての情報を入手できます。 詳細については、「 [Reporting Services エラーの原因と解決方法](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md)」を参照してください。  
  
## <a name="report-server-events"></a>レポート サーバーのイベント

次のレポート サーバーのイベントは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーション ログに記録されます。  
  
|イベント ID|型|カテゴリ|Source|[説明]|  
|--------------|----------|--------------|------------|-----------------|  
|106|Error|スケジューリング|レポート サーバー|スケジュールされた操作 (たとえば、レポートのサブスクリプションおよび配信) を定義する場合は、SQL Server エージェントを実行する必要があります。|  
|[107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)|Error|起動/シャットダウン|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<Source>* はレポート サーバー データベースに接続できません。 詳細については、「[レポート サーバー Windows サービス &#40;MSSQLServer&#41; 107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)」を参照してください。|  
|108|Error|拡張子|レポート サーバー<br /><br /> Web ポータル|*\<Source>* は、配信、データ処理、または表示拡張機能を読み込めません。<br /><br /> 最も可能性が高い原因として、配置が完全でないか、拡張機能が削除された可能性があります。 詳細については、SQL Server オンライン ブックの「 [データ処理拡張機能の配置](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md) 」および「 [配信拡張機能の配置](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)」を参照してください。|  
|109|[情報]|管理|レポート サーバー<br /><br /> Web ポータル|構成ファイルが変更されています。 詳細については、「 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)」を参照してください。|  
|110|警告|管理|レポート サーバー<br /><br /> Web ポータル|1 つの構成ファイルの設定が変更され、設定が無効になっています。 代わりに既定値が使用されます。 詳細については、「 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)」を参照してください。|  
|111|Error|ログ記録|レポート サーバー<br /><br /> Web ポータル|*\<Source>* はトレース ログを作成できません。 詳細については、「 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
|112|警告|Security|レポート サーバー|レポート サーバーは、サービス拒否攻撃 (DoS) の可能性を検出しました。 詳細については、「 [Reporting Services のセキュリティと保護](../../reporting-services/security/reporting-services-security-and-protection.md)」を参照してください。|  
|113|Error|ログ記録|レポート サーバー|レポート サーバーでは、パフォーマンス カウンターを作成できません。|  
|114|Error|起動/シャットダウン|Web ポータル|Web ポータルは ReportServer サービスに接続できません。|  
|115|警告|スケジューリング|スケジュールおよび配信のプロセッサ|SQL Server エージェント キューの定期タスクは、変更または削除されました。|  
|116|Error|Internal|レポート サーバー<br /><br /> Web ポータル<br /><br /> スケジュールおよび配信のプロセッサ|内部エラーが発生しました。|  
|117|Error|起動/シャットダウン|レポート サーバー|レポート サーバー データベースのバージョンが無効です。|  
|118|警告|ログ記録|レポート サーバー<br /><br /> Web ポータル|予期されたディレクトリの場所にトレース ログがありません。既定のディレクトリに新しいトレース ログが作成されます。 詳細については、「 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
|119|Error|アクティブ化|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<Source>* には、レポート サーバー データベースのコンテンツへのアクセス権がありません。|  
|120|Error|アクティブ化|レポート サーバー|対称キーの暗号化を解除できません。 最も可能性が高い原因として、サービスの実行に使用されるアカウントが変更されたことが考えられます。 詳細については、「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|121|Error|起動/シャットダウン|レポート サーバー|リモート プロシージャ コール (RPC) サービスを開始できませんでした。|  
|122|警告|Delivery|スケジュールおよび配信のプロセッサ|スケジュールおよび配信のプロセッサは、電子メールの配信に使用している SMTP サーバーに接続できません。 SMTP サーバー接続の詳細については、「[電子メールの設定-Reporting Services ネイティブモード (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)」を参照してください。|  
|123|警告|ログ記録|レポート サーバー<br /><br /> Web ポータル|レポート サーバーでは、トレース ログへの書き込みに失敗しました。 トレース ログの詳細については、「 [レポート サーバー サービスのトレース ログ](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
|124|[情報]|アクティブ化|レポート サーバー|レポート サーバー サービスが初期化されました。 詳細については、「[レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)」を参照してください。|  
|125|[情報]|アクティブ化|レポート サーバー|データの暗号化に使用したキーは、正常に展開されました。 キーの詳細については、「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|126|[情報]|アクティブ化|レポート サーバー|データの暗号化に使用したキーは、正常に適用されました。 キーの詳細については、「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|127|[情報]|アクティブ化|レポート サーバー|暗号化されたコンテンツは、正常にレポート サーバー データベースから削除されました。 復元できない暗号化されたデータの削除に関する詳細については、「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。|  
|128|Error|アクティブ化|レポート サーバー|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントのエディションが異なる場合は一緒に使用することはできません。|  
|129|Error|管理|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|暗号化された構成ファイルの設定の暗号化を解除できません。|  
|130|Error|管理|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|*\<Source>* は構成ファイルを見つけられません。 レポート サーバーでは、構成ファイルが必要です。|  
|131|Error|Security|レポート サーバー<br /><br /> スケジュールおよび配信のプロセッサ|暗号化されたユーザー データ値の暗号化を解除できませんでした。|  
|132|Error|Security|レポート サーバー|ユーザー データの暗号化中にエラーが発生しました。 値は保存されません。|  
|133|Error|管理|レポート サーバー<br /><br /> Web ポータル<br /><br /> スケジュールおよび配信のプロセッサ|構成ファイルを読み込めませんでした。 このエラーは、XML が無効な場合に発生することがあります。|  
|134|Error|管理|レポート サーバー|レポート サーバーでは、構成ファイルの設定の値を暗号化できませんでした。|  
  
## <a name="see-also"></a>参照

 [Reporting Services のサブスクリプションを監視する](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
 [Reporting Services のログ ファイルとソース](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)
