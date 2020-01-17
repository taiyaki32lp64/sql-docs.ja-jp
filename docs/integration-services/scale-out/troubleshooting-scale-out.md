---
title: SQL Server Integration Services (SSIS) Scale Out のトラブルシューティング | Microsoft Docs
description: この記事では、SSIS Scale Out での一般的な問題をトラブルシューティングする方法について説明します
ms.custom: performance
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 87f5ab815fc7d3a5df23aa3675e92ffa206bfcdf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896153"
---
# <a name="troubleshoot-scale-out"></a>Scale Out のトラブルシューティング

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SSIS Scale Out には、SSIS カタログ データベース `SSISDB`、Scale Out Master サービス、Scale Out Worker サービス間の通信が含まれます。 この通信は、構成の誤り、アクセス許可がない、およびその他の理由により中断する場合があります。 この記事は、Scale Out 構成に関する問題のトラブルシューティングに役立ちます。

発生した現象を調査するため、問題が解決されるまで、以下の手順を 1 つずつ実行してください。

## <a name="scale-out-master-fails"></a>Scale Out Master が失敗する

### <a name="symptoms"></a>現象 
-   Scale Out Master が SSISDB に接続できない。 

-   Scale Out Manager にマスター プロパティが表示できない。

-   マスター プロパティがビュー `[catalog].[master_properties]` に入力されない。

### <a name="solution"></a>解決方法
1.  Scale Out が有効になっているかどうかを確認します。

    SSMS のオブジェクト エクスプローラーで **[SSISDB]** を右クリックして、 **[Scale Out 機能が有効です]** を確認します。

    ![Scale Out が有効になっているか](media/isenabled.PNG)

    プロパティ値が False の場合は、ストアド プロシージャ `[catalog].[enable_scaleout]` を呼び出して、Scale Out を有効にします。

2.  Scale Out Master 構成ファイルで指定された SQL Server 名が正しいかどうかを確認し、Scale Out Master サービスを再起動します。

## <a name="scale-out-worker-fails"></a>Scale Out Worker が失敗する

### <a name="symptoms"></a>現象 
-   Scale Out Worker が Scale Out Master に接続できない。

-   Scale Out Worker が、Scale Out Manager に追加した後に表示されなくなる。

-   Scale Out Worker がビュー `[catalog].[worker_agents]` に表示されない。

-   Scale Out Worker サービスは実行されているが、Scale Out Worker がオフラインである。

### <a name="solution"></a>解決方法
`\<drive\>:\Users\\*[account running worker service]*\AppData\Local\SSIS\Cluster\Agent` にある Scale Out Worker サービス ログのエラー メッセージを確認します。

## <a name="no-endpoint-listening"></a>リッスンしているエンドポイントがない

### <a name="symptoms"></a>現象

*"System.ServiceModel.EndpointNotFoundException: メッセージを受信できる https://* [MachineName]:[Port] */ClusterManagement/ でリッスンしているエンドポイントがありませんでした。"*

### <a name="solution"></a>解決方法

1.  Scale Out Master のサービス構成ファイルで指定されたポート番号が正しいかどうかを確認し、Scale Out Master サービスを再起動します。 

2.  Scale Out Worker サービスの構成で指定されたマスター エンドポイントが正しいかどうかを確認し、Scale Out Worker サービスを再起動します。

3.  Scale Out Master ノードでファイアウォール ポートが開いているかどうかを確認します。

4.  Scale Out Master ノードと Scale Out Worker ノード間のその他の接続の問題を解決します。

## <a name="could-not-establish-trust-relationship"></a>信頼関係を確立できませんでした

### <a name="symptoms"></a>現象
*""System.ServiceModel.Security.SecurityNegotiationException: 機関 '[Machine Name]:[Port]' との SSL/TLS のセキュリティで保護されているチャネルに対する信頼関係を確立できませんでした。"*

*"System.Net.WebException: 基になる接続が閉じられました: SSL/TLS のセキュリティで保護されているチャネルに対する信頼関係を確立できませんでした。"*

*"System.Security.Authentication.AuthenticationException: 検証プロシージャによると、リモート証明書は無効です。"*

### <a name="solution"></a>解決方法
1.  Scale Out Master 証明書を Scale Out Worker ノードのローカル コンピューターのルート証明書ストアにインストールして (証明書がまだインストールされていない場合)、Scale Out Worker サービスを再起動します。

2.  マスター エンドポイント内のホスト名が Scale Out Master 証明書の CN に含まれているかどうかを確認します。 含まれていない場合は、Scale Out Worker の構成ファイル内のマスター エンドポイントをリセットし、Scale Out Worker サービスを再起動します。 

    > [!NOTE]
    > DNS の設定が原因でマスター エンドポイントのホスト名を変更できない場合は、Scale Out Master 証明書を変更する必要があります。 「[Scale Out の証明書の管理](deal-with-certificates-in-ssis-scale-out.md)」を参照してください。

3.  Scale Out Worker の構成で指定されたマスター サムプリントが Scale Out Worker 証明書のサムプリントと一致するかどうかを確認します。 

## <a name="could-not-establish-secure-channel"></a>セキュリティで保護されたチャネルを確立できませんでした

### <a name="symptoms"></a>現象

*"System.ServiceModel.Security.SecurityNegotiationException: オーソリティ '[Machine Name]:[Port]' と、セキュリティで保護された SSL/TLS のチャネルを確立できませんでした。"*

*"System.Net.WebException: 要求は中止されました: SSL/TLS のセキュリティで保護されているチャネルを作成できませんでした。"*

### <a name="solution"></a>解決方法
次のコマンドを実行して、Scale Out Worker サービスを実行するアカウントに、Scale Out Worker 証明書へのアクセス権があるかどうかを確認します。

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

アカウントにアクセス権がない場合は、次のコマンドを実行してアクセス権を付与し、Scale Out Worker サービスを再起動します。

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

## <a name="http-request-forbidden"></a>HTTP 要求が禁止されている

### <a name="symptoms"></a>現象

*"System.ServiceModel.Security.MessageSecurityException: この HTTP 要求は、クライアントの認証方式 'Anonymous' で許可されませんでした。"*

*"System.Net.WebException: リモート サーバーがエラーを返しました: 403 許可されていません。"*

### <a name="solution"></a>解決方法
1.  Scale Out Worker 証明書を、Scale Out Master ノードのローカル コンピューターのルート証明書ストアにインストールし (証明書がまだインストールされていない場合)、Scale Out Worker サービスを再起動します。

2.  Scale Out Master ノード上のローカル コンピューターのルート証明書ストア内の不要な証明書をクリーンアップします。

3.  Scale Out Master ノードに次のレジストリ エントリを追加することで、TLS/SSL のハンドシェイク プロセス中に信頼されたルート証明機関の一覧を送信しないように、Schannel を構成します。

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL`

    値の名前:**SendTrustedIssuerList** 

    値の型:**REG_DWORD** 

    値のデータ:**0 (False)**

4.  手順 2 の説明のように自己署名以外の証明書をすべて消去できない場合、次のレジストリ キーの値を 2 に設定します。

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL`

    値の名前:**ClientAuthTrustMode** 

    値の型:**REG_DWORD** 

    値のデータ:**2**

    > [!NOTE]
    > 自己署名以外の証明書がルート証明書ストアにある場合は、クライアント証明書の認証が失敗します。 詳細については、「[Internet Information Services (IIS) 8 may reject client certificate requests with HTTP 403.7 or 403.16 errors](https://support.microsoft.com/help/2802568/internet-information-services-iis-8-may-reject-client-certificate-requ)」(インターネット インフォメーション サービス (IIS) 8 で HTTP 403.7 エラーまたは 403.16 エラーが発生してクライアント証明書の要求が拒否される可能性がある) を参照してください。

## <a name="http-request-error"></a>HTTP 要求エラー

### <a name="symptoms"></a>現象

*"System.ServiceModel.CommunicationException: https://[Machine Name]:[Port]/ClusterManagement/ に対する HTTP 要求の発行中にエラーが発生しました。これは、HTTPS ケースの HTTP.SYS でサーバー証明書が正しく構成されていないという事実が原因と考えられます。またはクライアントとサーバーの間でセキュリティ バインドが整合していないことも原因になり得ます。"*

### <a name="solution"></a>解決方法
1.  次のコマンドを実行して、Scale Out Master 証明書がマスター ノード上のマスター エンドポイントのポートに正しくバインドされているかどうかを確認します。

    ```dos
    netsh http show sslcert ipport=0.0.0.0:{Master port}
    ```

    表示される証明書ハッシュが Scale Out Master 証明書のサムプリントと一致しているかどうかを確認します。 バインドが正しくない場合は、次のコマンドを実行してバインドをリセットし、Scale Out Worker サービスを再起動します。

    ```dos
    netsh http delete sslcert ipport=0.0.0.0:{Master port}
    netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root  appid={random guid}
    ```

## <a name="cannot-open-certificate-store"></a>証明書ストアを開けない

### <a name="symptoms"></a>現象
Scale Out Manager で Scale Out Worker を Scale Out Master に接続したときに、 *"マシン上で証明書ストアを開けません"* というエラー メッセージが表示され、検証が失敗する。

### <a name="solution"></a>解決方法

1.  管理者として Scale Out Manager を実行します。 SSMS で Scale Out Manager を開く場合は、SSMS を管理者として実行する必要があります。

2.  コンピューターでリモート レジストリ サービスを起動します (実行されていない場合)。

## <a name="execution-doesnt-start"></a>実行が開始されない

### <a name="symptoms"></a>現象
Scale Out で実行が開始されない。

### <a name="solution"></a>解決方法

ビュー `[catalog].[worker_agents]` でパッケージを実行するために選択したコンピューターの状態を確認します。 少なくとも 1 つのワーカーがオンラインで有効になっている必要があります。

## <a name="no-log"></a>ログがない

### <a name="symptoms"></a>現象 
パッケージは正常に実行されているが、メッセージがログに記録されない。

### <a name="solution"></a>解決方法

SSISDB をホストする SQL Server インスタンスにより SQL Server 認証が許可されているかどうかを確認します。

> [!NOTE]  
> Scale Out ログのアカウントを変更した場合は、「[Scale Out ログのアカウントの変更](change-logdb-account.md)」を参照し、ログ記録に使用する接続文字列を確認します。

## <a name="error-messages-arent-helpful"></a>エラー メッセージが役に立たない

### <a name="symptoms"></a>現象
パッケージ実行レポート内のエラー メッセージが、トラブルシューティングには不十分である。

### <a name="solution"></a>解決方法
`WorkerSettings.config` で構成されている `TasksRootFolder` には、さらに多くの実行ログがあります。 既定では、このフォルダーは `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks` です。 *[account]* は、既定値が `SSISScaleOutWorker140` の Scale Out Worker サービスを実行しているアカウントです。

*[execution ID]* を持つパッケージ実行のログを見つけるには、次の Transact-SQL コマンドを実行して *[task ID]* を取得します。 次に、`TasksRootFolder` で *[task ID]* を含むサブフォルダー名を見つけます。

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```

> [!WARNING]
> このクエリはトラブルシューティング専用です。 クエリで参照されている内部ビューは、今後、変更される可能性があります。 

## <a name="next-steps"></a>次の手順
詳細については、SSIS Scale Out のセットアップと構成に関する以下の記事を参照してください。
-   [1 台のコンピューターでの Integration Services (SSIS) Scale Out の概要](get-started-with-ssis-scale-out-onebox.md)
-   [チュートリアル:Integration Services Scale Out をセットアップする](walkthrough-set-up-integration-services-scale-out.md)
