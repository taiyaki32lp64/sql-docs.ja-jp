## <a name="prerequisites"></a>前提条件

可用性グループを作成する前に、以下のことを行う必要があります。

- 可用性レプリカをホストするすべてのサーバーが通信できるように環境を設定します。
- SQL Server をインストールします。

>[!NOTE]
>Linux でクラスターで管理するには、クラスター リソースとして追加する前に可用性グループを作成する必要があります。 このドキュメントでは、可用性グループを作成する例を示します。 クラスターを作成し、可用性グループをクラスターのリソースとして追加するディストリビューション固有の説明については、「次のステップ」の後のリンクをご覧ください。

1. 各ホストのコンピューター名を更新します。

   各 SQL Server 名には次の条件があります。
   
   - 15 文字以下。
   - ネットワーク内で一意。
   
   コンピューター名を設定するには、`/etc/hostname` を編集します。 次のスクリプトを使うと、`vi` で `/etc/hostname` を編集できます。

   ```bash
   sudo vi /etc/hostname
   ```

2. hosts ファイルを構成する。

    >[!NOTE]
    >ホスト名が IP アドレスで DNS サーバーに登録されている場合、次の手順を実行する必要はありません。 可用性グループの一部として構成されているすべてのノードが、相互通信できることを確認します。 (そのホスト名を ping した場合、その対応する IP アドレスが返される必要があります)。また、/etc/hosts ファイルに、localhost IP アドレス 127.0.0.1 をノードのホスト名とマップするレコードが含まれないことを確認します。
    >

   すべてのサーバー上の hosts ファイルには、可用性グループに参加するすべてのサーバーの IP アドレスと名前が含まれています。 

   次のコマンドは、現在のサーバーの IP アドレスを返します。

   ```bash
   sudo ip addr show
   ```

   `/etc/hosts` を更新します。 次のスクリプトを使うと、`vi` で `/etc/hosts` を編集できます。

   ```bash
   sudo vi /etc/hosts
   ```

   次の例は、**node1** の `/etc/hosts` を示しています。**node1**、**node2**、**node3** に対して追加があります。 このドキュメントで **node1** は、プライマリ レプリカをホストするサーバーを指します。 また、**node2** と **node3** は、セカンダリ レプリカをホストするサーバーを指します。

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>SQL Server をインストールする

SQL Server をインストールします。 次のリンクは、SQL Server のさまざまなディストリビューションでのインストール手順です。 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>AlwaysOn 可用性グループを有効にして mssql-server を再起動する

SQL Server インスタンスをホストする各ノードで AlwaysOn 可用性グループを有効にします。 次に、`mssql-server` を再起動します。 次のスクリプトを実行します。

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwayson_health-event-session"></a>AlwaysOn_health イベント セッションを有効にする 

オプションで、AlwaysOn 可用性グループの拡張イベントを有効にすると、可用性グループのトラブルシューティング時の根本原因の診断に役立ちます。 SQL Server の各インスタンスで次のコマンドを実行します。 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

この XE セッションの詳細については、「[AlwaysOn の拡張イベント](https://msdn.microsoft.com/library/dn135324.aspx)」を参照してください。

## <a name="create-a-certificate"></a>証明書を作成する

Linux 上の SQL Server サービスは、ミラーリングのエンドポイント間の通信を認証するのに証明書を使用します。 

次の Transact-SQL スクリプトでは、マスター キーと証明書を作成します。 その後、証明書をバックアップし、秘密キーでファイルをセキュリティ保護します。 強力なパスワードでスクリプトを更新してください。 プライマリ SQL Server インスタンスに接続します。 次の Transact-SQL スクリプトを実行して、証明書を作成します。

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

この時点で、プライマリ SQL Server レプリカの `/var/opt/mssql/data/dbm_certificate.cer` には証明書が、`var/opt/mssql/data/dbm_certificate.pvk` には秘密キーが作成されています。 これら 2 つのファイルを、可用性レプリカをホストするすべてのサーバー上の同じ場所にコピーします。 mssql ユーザーを使うか、またはこれらのファイルへのアクセス許可を mssql ユーザーに付与します。 

たとえば、ソース サーバーでは、次のコマンドでファイルがターゲット コンピューターにコピーされます。 `**<node2>**` の値を、レプリカをホストする SQL Server インスタンスの名前に置き換えます。 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

各ターゲット サーバーで証明書にアクセスするアクセス許可を mssql ユーザーに付与します。

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>セカンダリ サーバーで証明書を作成する

次の Transact-SQL スクリプトでは、プライマリ SQL Server レプリカで作成したバックアップからマスター キーと証明書を作成します。 強力なパスワードでスクリプトを更新してください。 暗号化解除パスワードは、前の手順で .pvk ファイルの作成に使ったものと同じパスワードです。 すべてのセカンダリ サーバーで次のスクリプトを実行し、証明書を作成します。

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>すべてのレプリカにデータベース ミラーリング エンドポイントを作成する

データベース ミラーリング エンドポイントでは、伝送制御プロトコル (TCP) を使用して、データベース ミラーリング セッションに参加するサーバー インスタンス間、または可用性レプリカをホストするサーバー インスタンス間でメッセージを送受信します。 データベース ミラーリング エンドポイントでは、一意な TCP ポート番号でリッスンします。 

次の Transact-SQL スクリプトでは、可用性グループに対して `Hadr_endpoint` という名前のリスニング エンドポイントを作成します。 エンドポイントが起動され、作成した証明書に接続許可が付与されます。 スクリプトを実行する前に、`**< ... >**` の間の値を置き換えます。 必要に応じて、IP アドレス `LISTENER_IP = (0.0.0.0)` を含めることができます。 リスナー IP アドレスは、IPv4 アドレスである必要があります。 `0.0.0.0` を使用することもできます。 

すべての SQL Server インスタンスで、ご利用の環境に合わせて次の Transact-SQL スクリプトを更新します。 

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

>[!NOTE]
>構成専用のレプリカのホストに 1 つのノードで SQL Server Express Edition を使用する場合、`ROLE` に有効な値は `WITNESS` のみです。 SQL Server Express Edition で次のスクリプトを実行します。

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

ファイアウォールの TCP ポートをリスナー ポート用に開く必要があります。



>[!IMPORTANT]
>SQL Server 2017 リリースのデータベース ミラーリング エンドポイントでサポートされる唯一の認証方法は `CERTIFICATE` です。 `WINDOWS` オプションは今後のリリースで有効になる予定です。

詳細については、「[データベース ミラーリング エンドポイント (SQL Server)](https://msdn.microsoft.com/library/ms179511.aspx)」を参照してください。


