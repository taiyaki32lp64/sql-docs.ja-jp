---
title: Reporting Services のサブスクリプションと配信に関するトラブルシューティング | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: ae1775f7-9919-48ca-8bd7-cc16df274e2c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 84ca5db4b8979b1b49ffc25b809638defc40fe1e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65572113"
---
# <a name="troubleshoot-reporting-services-subscriptions-and-delivery"></a>Reporting Services のサブスクリプションと配信に関するトラブルシューティング
  
    
このトピックでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] レポートのサブスクリプション、スケジュール、および配信の処理中に発生する問題のトラブルシューティングを行います。  
## <a name="log-information"></a>ログ情報
 
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] の [サブスクリプション] ページにはサブスクリプションの状態が含まれますが、サブスクリプションに問題がある場合、詳細情報は [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のログに見つかります。 
![ssrs_tutorial_datadriven_subscription_status_ReportManager](../../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png)

**トレース ログ:** トレース ログとは、次の場所に書き込まれるテキスト ファイルです。 `\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`

次にログ エントリの例を示します。

```
   subscription WindowsService_10   4c7c    05/24/2016-01:05:06  e ERROR     Failure writing file \\ServerName\SalesReports\so71949.xls : Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider+NetworkErrorException: An impersonation error occurred using the security context of the current user. ---> System.ArgumentException: Value does not fall within the expected range.  05/24/2016
```
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のトレース ログの詳細については、次を参照してください。 
+ [レポート サーバーのトレース ログ](../../reporting-services/report-server/report-server-service-trace-log.md)。
+ [Reporting Services のログ ファイル](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。

**実行ログのビュー:**

実行ログは ReportServer SQL データベースのビューです。 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] の詳細については、 [Reporting Services の ExecutionLog ビューと ExecutionLog3 ビュー](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)に関するページを参照してください。  

----------
## <a name="unable-to-send-reports-using-e-mail-with-windows-server-2003-and-pop3"></a>POP3 として構成した Windows 2003 Server で、電子メールを使用するレポートを送信できない  
Post Office Protocol version 3 (POP3) を使用する電子メール アプリケーションを Microsoft Windows Server 2003 上で実行している場合、ローカル POP3 サーバーを使用してレポートを送信できない場合があります。 ローカル POP3 サーバーで電子メールが送信されるようにレポート サーバーを構成している場合に、レポートを送信するサブスクリプションを作成すると、次のエラー メッセージが表示されることがあります。  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Failure sending mail: <error message>`  
  
\<error message> には Collaboration Data Objects (CDO) から返されたエラー メッセージの追加情報が記載されます。  
  
### <a name="to-resolve-this-problem"></a>この問題を解決するには、次のようにします。  
* `SendUsing` Rsreportserver.config **ファイルの** 要素の値を 1 に設定します。  
* `SMTPServer` プロパティの値をクリアして空になるようにします。 `SMTPServerPickupDirectory` プロパティにも値を指定する必要があります。   
  
レポートの電子メール配信のためにローカル SMTP サービスを使用する方法の詳細については、「電子メール配信用のレポート サーバーの構成」を参照してください。  
  
## <a name="failure-sending-mail-the-server-rejected-the-sender-address-the-server-response-was-454-573-client-does-not-have-permission-to-submit-mail-to-this-server"></a>電子メールを送信できません: サーバーによって送信者アドレスが拒否されました。 サーバーからの応答は次のとおりです。454 5.7.3 Client does not have permission to submit mail to this server (クライアントには、このサーバーに電子メールを送信するアクセス許可がありません)  
このエラーは、SMTP サーバーのセキュリティ ポリシーの設定により、認証されたユーザーだけがそれ以降の配信にメールを送信できる場合に発生します。 SMTP サーバーが匿名ユーザーからの電子メール送信を受け付けない場合、サーバーを使用する権限を得るにはシステム管理者に問い合わせてください。  
> このエラーは、Exchange Server の名前を SMTPServer として指定している場合にも発生します。 電子メールの配信に Exchange Server を使用するには、そのサーバー用に構成した SMTP ゲートウェイの名前を指定する必要があります。 この情報については Exchange 管理者に問い合わせてください。  
  
## <a name="subscriptions-are-not-processing"></a>サブスクリプションが処理されない  
サブスクリプションは次の条件下で失敗することがあります。   
* レポートを開始するスケジュールの有効期限が切れている場合。 レポート スナップショットの更新を開始するサブスクリプションについては、スナップショット更新用のスケジュールの有効期限が切れている可能性があります。  
  
* レポート サーバー、SQL Server エージェント、または電子メール サーバー アプリケーションのいずれかが実行されていない場合。  
* レポートが配信できない状態にある場合 (レポートが大きすぎるなど)。 レポートが大きすぎることが原因で配信が失敗するかどうかを調べるには、レポートをファイルに保存し、電子メールで送信します。 必ず、サブスクリプションで指定したものと同じ表示形式を選択してください。 配信エラーが発生した場合は、レポート サーバーの電子メールではなく、ファイル共有配信拡張機能を使用してください。  
* ファイル共有配信用のコンピューターが実行されていない場合。または、ファイル共有の構成が読み取り専用になっている場合。  
* サブスクリプションに指定されている配信拡張機能がインストールされていないか、無効になっている場合。  
* 資格情報の設定が、保存されている値から統合された値またはユーザーが入力した値に変更された場合。  
* レポート定義のパラメーター名またはデータ型が変更されてから、レポートが再度パブリッシュされた場合。 サブスクリプションに無効になったパラメーターが含まれている場合、サブスクリプションは非アクティブになります。  
  
詳細については、TechNet Wiki の [Reporting Services での問題とエラーのトラブルシューティング](https://social.technet.microsoft.com/wiki/contents/articles/1633.ssrs-troubleshoot-issues-and-errors-with-reporting-services.aspx)に関するページを参照してください。  
  
  
    
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

