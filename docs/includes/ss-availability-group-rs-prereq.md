---
ms.openlocfilehash: 336162ea06533901107c83dd47f062fc94fdd869
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213324"
---
## <a name="prerequisites"></a>Prerequisites

可用性グループを作成する前に、以下のことを行う必要があります。

- 可用性レプリカをホストするすべてのサーバーが通信できるように環境を設定します。
- SQL Server をインストールします。 詳細については、「[SQL Server をインストールする](../database-engine/install-windows/install-sql-server.md)」を参照してください。

## <a name="enable-always-on-availability-groups-and-restart-mssql-server"></a>Always On 可用性グループを有効にして mssql-server を再起動する

>[!NOTE]
>次のコマンドでは、PowerShell ギャラリーで公開されている sqlserver モジュールのコマンドレットを利用しています。 Install-Module コマンドを使用して、このモジュールをインストールすることができます。

SQL Server インスタンスをホストする各レプリカで Always On 可用性グループを有効にします。 次に、SQL Server サービスを再起動します。 次のコマンドを実行し、SQL Server サービスを有効にして再起動します。

```powershell
Enable-SqlAlwaysOn -ServerInstance <server\instance> -Force
```

## <a name="enable-an-alwaysonhealth-event-session"></a>AlwaysOn_health イベント セッションを有効にする

 可用性グループのトラブルシューティング時に根本原因を診断できるように、オプションで Always On 可用性グループの拡張イベント (XEvents) セッションを有効にすることができます。 この操作を行うには、SQL Server の各インスタンスで次のコマンドを実行します。

```sql
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

この XEvents セッションの詳細については、「[Always On 可用性グループの拡張イベント](../database-engine/availability-groups/windows/always-on-extended-events.md)」を参照してください。

## <a name="database-mirroring-endpoint-authentication"></a>データベース ミラーリング エンドポイントの認証

同期が正常に機能するように、読み取りスケール可用性グループに関連するレプリカでは、エンドポイントを介して認証する必要があります。 このような認証に使用できる 2 つの主なシナリオを、次のセクションで説明します。

### <a name="service-account"></a>サービス アカウント

すべてのセカンダリ レプリカが同じドメインに参加している Active Directory 環境では、SQL Server はサービス アカウントを利用して認証することができます。 SQL Server インスタンスでそれぞれ明示的に、サービス アカウントのログインを作成する必要があります。

```sql
CREATE LOGIN [<domain>\service account] FROM WINDOWS;
```

### <a name="sql-login-authentication"></a>SQL ログイン認証

セカンダリ レプリカが Active Directory ドメインに参加していない可能性がある環境では、SQL 認証を利用する必要があります。 次の Transact-SQL スクリプトでは、`dbm_login` という名前のログインと `dbm_user` という名前のユーザーを作成します。 強力なパスワードでスクリプトを更新します。 データベース ミラーリング エンドポイントのユーザーを作成するには、すべての SQL Server インスタンスで次のコマンドを実行します。

```sql
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

#### <a name="certificate-authentication"></a>証明書の認証

SQL 認証での認証が必要なセカンダリ レプリカを利用する場合は、証明書を使用してミラーリング エンドポイント間の認証を行います。

次の Transact-SQL スクリプトでは、マスター キーと証明書を作成します。 その後、証明書をバックアップし、秘密キーでファイルをセキュリティ保護します。 強力なパスワードでスクリプトを更新してください。 プライマリ SQL Server インスタンスで次のスクリプトを実行し、証明書を作成します。

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

この時点で、プライマリ SQL Server レプリカの `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer` には証明書が、`c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk` には秘密キーが作成されています。 これら 2 つのファイルを、可用性レプリカをホストするすべてのサーバー上の同じ場所にコピーします。

各セカンダリ レプリカで、SQL Server インスタンスのサービス アカウントに証明書へのアクセス権限があることを確認します。

#### <a name="create-the-certificate-on-secondary-servers"></a>セカンダリ サーバーで証明書を作成する

次の Transact-SQL スクリプトでは、プライマリ SQL Server レプリカで作成したバックアップからマスター キーと証明書を作成します。 コマンドではユーザーが証明書にアクセスすることも承認します。 強力なパスワードでスクリプトを更新してください。 暗号化解除パスワードは、前の手順で *.pvk* ファイルの作成に使ったものと同じパスワードです。 証明書を作成するには、すべてのセカンダリ サーバーで次のスクリプトを実行します。

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    AUTHORIZATION dbm_user
    FROM FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-database-mirroring-endpoints-on-all-replicas"></a>すべてのレプリカにデータベース ミラーリング エンドポイントを作成する

データベース ミラーリング エンドポイントでは、伝送制御プロトコル (TCP) を使用して、データベース ミラーリング セッションに参加するサーバー インスタンス間、または可用性レプリカをホストするサーバー インスタンス間でメッセージを送受信します。 データベース ミラーリング エンドポイントでは、一意の TCP ポート番号でリッスンします。

次の Transact-SQL スクリプトでは、可用性グループに対して `Hadr_endpoint` という名前のリスニング エンドポイントを作成します。 これで、エンドポイントが開始され、前の手順で作成した SQL ログインまたはサービス アカウントへの接続権限が与えられます。 スクリプトを実行する前に、`**< ... >**` の間の値を置き換えます。 必要に応じて、IP アドレス `LISTENER_IP = (0.0.0.0)` を含めることができます。 リスナー IP アドレスは、IPv4 アドレスである必要があります。 `0.0.0.0` を使用することもできます。

すべての SQL Server インスタンスで、ご利用の環境に合わせて次の Transact-SQL スクリプトを更新します。

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [<service account or user>];
```

ファイアウォールの TCP ポートをリスナー ポート用に開く必要があります。

詳細については、「[データベース ミラーリング エンドポイント (SQL Server)](https://docs.microsoft.com/sql/database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server?view=sql-server-2017)」を参照してください。
