---
title: SQL Server on Linux の可用性グループを作成および構成する
description: このチュートリアルでは、SQL Server on Linux の可用性グループを作成および構成する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 06/28/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5d341d7bbda403b405268fe253cff7d60cea4d0d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077439"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>SQL Server on Linux の可用性グループを作成および構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このチュートリアルでは、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] on Linux の可用性グループ (AG) を作成および構成する方法について説明します。 [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] on Windows 以前とは異なり、基になる Pacemaker クラスターを最初に作成してもしなくても AG を有効にできます。 必要な場合でも、クラスターとの統合は後まで行われません。

チュートリアルには次のタスクが含まれます。
 
> [!div class="checklist"]
> * 可用性グループを有効にします。
> * 可用性グループのエンドポイントと証明書を作成します。
> * [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) または Transact-SQL を使用して可用性グループを作成します。
> * Pacemaker の [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] ログインとアクセス許可を作成します。
> * Pacemaker クラスターに可用性グループのリソースを作成します (外部タイプのみ)。

## <a name="prerequisite"></a>前提条件
- Pacemaker 高可用性クラスターを「[SQL Server on Linux の Pacemaker クラスターをデプロイする](sql-server-linux-deploy-pacemaker-cluster.md)」の説明に従ってデプロイします。


## <a name="enable-the-availability-groups-feature"></a>可用性グループ機能を有効にする

Windows とは異なり、PowerShell または [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Configuration Manager を使用して可用性グループ (AG) 機能を有効にすることはできません。 Linux では、`mssql-conf` を使用して機能を有効にする必要があります。 可用性グループの機能を有効にするには、`mssql-conf` ユーティリティを使用する方法と、手動で `mssql.conf` ファイルを編集する方法の 2 つがあります。

> [!IMPORTANT]
> [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)] の場合でも、AG 機能を構成専用レプリカに対して有効にする必要があります。

### <a name="use-the-mssql-conf-utility"></a>mssql-conf ユーティリティを使用する

プロンプトで次を発行します。

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>mssql ファイルを編集する

`/var/opt/mssql` フォルダーにある `mssql.conf` ファイルを変更して、次の行を追加することもできます。

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] を再起動する
Windows の場合と同様に、可用性グループを有効にした後で、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] を再起動する必要があります。 これは、次のようにして行うことができます。

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>可用性グループのエンドポイントと証明書を作成する

可用性グループは通信に TCP エンドポイントを使用します。 Linux では、AG のエンドポイントがサポートされるのは、認証に証明書が使用される場合のみです。 つまり、1 つのインスタンスの証明書を、他のすべてのインスタンス (同じ AG に参加するレプリカになる) で復元する必要があります。 証明書のプロセスは構成専用レプリカでも必要です。 

エンドポイントの作成と証明書の復元は、Transact-SQL を使用してのみ実行できます。 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] によって生成されていない証明書も使用できます。 また、証明書を管理したり有効期限が切れた証明書を置き換えるプロセスも必要です。

> [!IMPORTANT]
> [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] ウィザードを使用して AG を作成する予定の場合でも、Linux で Transact-SQL を使用して証明書を作成および復元する必要があります。

さまざまなコマンドで使用できるオプション (追加のセキュリティなど) の完全な構文については、次を参照してください。

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> 可用性グループを作成する場合でも、エンドポイントの種類として *FOR DATABASE_MIRRORING* を使用します。特徴の一部が、現在非推奨となっているこの機能と共通しているためです。

この例では、3 ノード構成の証明書を作成します。 インスタンス名は、LinAGN1、LinAGN2、および LinAGN3 です。

1.  LinAGN1 で次のように実行して、マスター キー、証明書、およびエンドポイントを作成し、証明書をバックアップします。 この例では、標準の TCP ポート 5022 がエンドポイントに使用されています。
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN1_Cert
    WITH SUBJECT = 'LinAGN1 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN1_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN1_Cert,
        ROLE = ALL);
    
    GO
    ```
    
2.  LinAGN2 で同じ操作を実行します。
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    WITH SUBJECT = 'LinAGN2 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN2_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN2_Cert,
        ROLE = ALL);
    
    GO
    ```
    
3.  最後に、LinAGN3 で同じ手順を実行します。
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    WITH SUBJECT = 'LinAGN3 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN3_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN3_Cert,
        ROLE = ALL);
    
    GO
    ```
    
4.  `scp` または別のユーティリティを使用して、証明書のバックアップを AG の一部となる各ノードにコピーします。
    
    この例の場合は次のとおりです。
    
    - LinAGN1_Cert.cer を LinAGN2 と LinAGN3 にコピーします。
    - LinAGN2_Cert.cer を LinAGN1 と LinAGN3 にコピーします。
    - LinAGN3_Cert.cer を LinAGN1 と LinAGN2 にコピーします。
    
5.  所有権と、コピーした証明書ファイルに関連付けられているグループを `mssql` に変更します。
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  LinAGN2 と LinAGN3 に関連付けられたインスタンスレベルのログインとユーザーを LinAGN1 上に作成します。
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  LinAGN2_Cert と LinAGN3_Cert を LinAGN1 に復元します。 他のレプリカの証明書があることが、AG の通信とセキュリティの重要な側面です。
    
    ```SQL
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
8.  Grant the logins associated with LinAG2 and LinAGN3 permission to connect to the endpoint on LinAGN1.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
9.  LinAGN1 と LinAGN3 に関連付けられたインスタンスレベルのログインとユーザーを LinAGN2 上に作成します。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10. LinAGN1_Cert と LinAGN3_Cert を LinAGN2 に復元します。
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    ```
    
11. LinAG1 と LinAGN3 に関連付けられたログインに、LinAGN2 のエンドポイントに接続するアクセス許可を付与します。
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12. LinAGN1 と LinAGN2 に関連付けられたインスタンスレベルのログインとユーザーを LinAGN3 上に作成します。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13. LinAGN1_Cert と LinAGN2_Cert を LinAGN3 に復元します。 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    ```
    
14. LinAG1 と LinAGN2 に関連付けられたログインに、LinAGN3 のエンドポイントに接続するアクセス許可を付与します。
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>可用性グループを作成する

このセクションでは、[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) または Transact-SQL を使用して [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] の可用性グループを作成する方法を説明します。

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] を使用してください。

このセクションでは、新しい可用性グループ ウィザードを使用して、SSMS を使用する外部タイプのクラスターの AG を作成する方法を説明します。

1.  SSMS で、 **[Always On 高可用性]** を展開し、 **[可用性グループ]** を右クリックし、 **[新しい可用性グループ ウィザード]** を選択します。

2.  [概要] ダイアログで、 **[次へ]** をクリックします。

3.  [可用性グループ オプションの指定] ダイアログに、可用性グループの名前を入力し、ドロップダウンでクラスターのタイプとして [外部] または [なし] を選択します。 Pacemaker をデプロイする予定がある場合は [外部] を使用する必要があります。 [なし] は、読み取りスケールアウトなどの特殊なシナリオを対象としています。[データベース レベルの正常性検出] のオプションの選択は省略可能です。 このオプションについて詳しくは、「[可用性グループのデータベース レベルの正常性検出フェールオーバー オプション](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)」をご覧ください。 **[次へ]** をクリックします。

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  [データベースの選択] ダイアログで、AG に参加するデータベースを選択します。 データベースを AG に追加するには、その前にデータベースごとに完全バックアップが必要です。 **[次へ]** をクリックします。

5.  [レプリカの指定] ダイアログで **[レプリカの追加]** をクリックします。

6.  [サーバーに接続] ダイアログで、セカンダリ レプリカにする [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] の Linux インスタンスの名前と、接続するための資格情報を入力します。 **[接続]** をクリックします。

7.  前の 2 つの手順を、構成専用レプリカまたは別のセカンダリ レプリカを格納するインスタンスに対して繰り返します。

8.  これで、3 つのインスタンスすべてが [レプリカの指定] ダイアログに表示されます。 実際にセカンダリにするセカンダリ レプリカでクラスター タイプ [外部] を使用している場合は、可用性モードがプライマリ レプリカのものと一致し、フェールオーバー モードが [外部] に設定されていることを確認します。 構成専用レプリカについては、可用性モードとして [構成のみ] を選択します。

    次の例に示す AG には、クラスター タイプ が [外部] のものと構成専用レプリカの 2 つのレプリカが含まれます。

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    次の例に示す AG には、クラスター タイプ が [なし] のものと構成専用レプリカの 2 つのレプリカが含まれます。

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  バックアップの設定を変更する場合は、[バックアップの設定] タブをクリックします。AG のバックアップ設定について詳しくは、[可用性レプリカでのバックアップ構成](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)に関するページをご覧ください。

10. 読み取り可能なセカンダリを使用している場合、または読み取りスケール用にタイプが [なし] のクラスターの AG を作成している場合は、[リスナー] タブを選択してリスナーを作成できます。リスナーは後で追加することもできます。 リスナーを作成するには、 **[可用性グループ リスナーの作成]** オプションを選択し、名前と TCP/IP ポート、および静的 DHCP IP アドレスと自動割り当て DHCP IP アドレスのどちらを使用するかを入力します。 クラスター タイプが [なし] の AG では、IP は静的にする必要があり、プライマリの IP アドレスを設定する必要があることに注意してください。

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. 読み取り可能なシナリオ用にリスナーが作成されている場合、SSMS 17.3 以降では、ウィザードで読み取り専用ルーティングを作成できます。 これは後から SSMS または Transact-SQL を使用して追加することもできます。 すぐに読み取り専用ルーティングを追加にするには:

    A.  [読み取り専用ルーティング] タブを選択します。

    B.  読み取り専用レプリカの URL を入力します。 これらの URL はエンドポイントに似ていますが、エンドポイントではなくインスタンスのポートを使用する点が異なります。

    c.  各 URL を選択し、下部で読み取り可能なレプリカを選択します。 複数選択するには、SHIFT キーを押すか、クリックしてドラッグします。

12. **[次へ]** をクリックします。

13. セカンダリ レプリカの初期化方法を選択します。 既定では、[自動シード処理](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md)が使用されます。この場合、AG に参加しているすべてのサーバーで同じパスが必要になります。 また、ウィザードでバックアップ、コピー、復元を実行したり (2 番目の方法)、データベースを手動でバックアップし、コピーして、レプリカに復元した場合に、ウィザードを使用して参加させたり (3 番目の方法)、後からデータベースを追加したりすることもできます (最後の方法)。 証明書と同様に、手動でバックアップを作成してコピーする場合は、バックアップファイルに対するアクセス許可を他のレプリカに設定する必要があります。 **[次へ]** をクリックします。

14. [検証] ダイアログで、すべてが成功として返されない場合は調査します。 リスナーを作成しない場合など、一部の警告は許容され致命的ではありません。 **[次へ]** をクリックします。

15. [概要] ページで **[完了]** をクリックします。 これで、AG を作成するプロセスが開始されます。

16. AG の作成が完了したら、[結果] で **[閉じる]** をクリックします。 これで、動的管理ビューでレプリカに対する AG を表示することも、SSMS の [Always On 高可用性] フォルダーに AG を表示することもできるようになりました。

### <a name="use-transact-sql"></a>Transact-SQL の使用

このセクションでは、Transact-SQL を使用して AG を作成する例を示します。 リスナーと読み取り専用ルーティングは、AG の作成後に構成できます。 AG そのものは `ALTER AVAILABILITY GROUP` を使用して変更できますが、クラスター タイプの変更は [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] ではできません。 タイプが [外部] のクラスターを含む AG を作成する予定ではなかった場合は、削除して、クラスター タイプ [なし] を含む AG を再作成する必要があります。 詳細およびその他のオプションについては、次のリンクを参照してください。

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [可用性グループの読み取り専用ルーティングの構成 (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [可用性グループ リスナーの作成または構成 (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one---two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>例 1 - 構成専用レプリカの 2 つのレプリカ ([外部] クラスター タイプ)

この例では、構成専用レプリカを使用する、2 つのレプリカの AG を作成する方法を示します。

1.  データベースの完全な読み取り/書き込みコピーが含まれている、プライマリ レプリカとなるノードで実行します。 この例では自動シード処理を使用します。

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1' WITH (
       ENDPOINT_URL = N' TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       SEEDING_MODE = AUTOMATIC),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       AVAILABILITY_MODE = CONFIGURATION_ONLY);
       
    GO
    ```
    
2.  他のレプリカに接続しているクエリ ウィンドウで次を実行して、レプリカを AG に参加させ、プライマリからセカンダリ レプリカへのシード処理を開始します。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3. 構成専用レプリカに接続しているクエリ ウィンドウで、それを AG に参加させます。
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two---three-replicas-with-read-only-routing-external-cluster-type"></a>例 2 - 読み取り専用ルーティングの 3 つのレプリカ ([外部] クラスター タイプ)

この例では、3 つの完全なレプリカを示し、最初の AG 作成の一部として読み取り専用ルーティングを構成する方法を説明します。

1.  データベースの完全な読み取り/書き込みコピーが含まれている、プライマリ レプリカとなるノードで実行します。 この例では自動シード処理を使用します。

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN2.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:1433')),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN2.FullyQualified.Name:1433')),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN3.FullyQualified.Name:1433'))
    LISTENER '<ListenerName>' (WITH IP = ('<IPAddress>', '<SubnetMask>'), Port = 1433);
    
    GO
    ```
    
    この構成に関する注意事項:
    
    - *AGName* は、可用性グループの名前です。
    - *DBName* は、可用性グループで使用されるデータベースの名前です。 名前をコンマで区切って指定することもできます。
    - *ListenerName* は、基になるサーバー/ノードとは異なる名前です。 これは、*IPAddress* と共に DNS に登録されます。
    - *IPAddress* は、*ListenerName* 関連付けられた IP アドレスです。 また、これは一意であり、どのサーバー/ノードとも同じではありません。 アプリケーションおよびエンド ユーザーは、*ListenerName* または *IPAddress* を使用して AG に接続します。
    - *SubnetMask* は、*IPAddress* のサブネット マスク (255.255.255.0 など) です。

2.  他のレプリカに接続しているクエリ ウィンドウで次を実行して、レプリカを AG に参加させ、プライマリからセカンダリ レプリカへのシード処理を開始します。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  3 番目のレプリカに対して手順 2 を繰り返します。

#### <a name="example-three---two-replicas-with-read-only-routing-none-cluster-type"></a>例 3 - 読み取り専用ルーティングの 2 つのレプリカ ([なし] クラスター タイプ)

この例では、クラスター タイプ [なし] を使用する 2 レプリカ構成を作成しています。 これはフェールオーバーが不要な読み取りスケールのシナリオで使用されます。 これによって、実際にプライマリ レプリカになるリスナーと、ラウンドロビン機能を使用する読み取り専用ルーティングが作成されます。

1.  データベースの完全な読み取り/書き込みコピーが含まれている、プライマリ レプリカとなるノードで実行します。 この例では自動シード処理を使用します。

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = NONE)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name: <PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name'.'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:<PortOfInstance>'));
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:<PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL =N'TCP://LinAGN2.FullyQualified.Name:<PortOfInstance>'));
    LISTENER '<ListenerName>' (WITH IP = ('<PrimaryReplicaIPAddress>', '<SubnetMask>'), Port = <PortOfListener>);
    
    GO
    ```
    
    場所
    - *AGName* は、可用性グループの名前です。
    - *DBName* は、可用性グループで使用されるデータベースの名前です。 名前をコンマで区切って指定することもできます。
    - *PortOfEndpoint* は、作成されるエンドポイントで使用されるポート番号です。
    - *PortOfInstance* は、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] のインスタンスによって使用されるポート番号です。
    - *ListenerName* は、基になるレプリカのいずれとも異なる名前です。実際には使用されません。
    - *PrimaryReplicaIPAddress* は、プライマリ レプリカの IP アドレスです。
    - *SubnetMask* は、*IPAddress* のサブネット マスクです。 たとえば、255.255.255.0 です。
    
2.  セカンダリ レプリカを AG に参加させ、自動シード処理を開始します。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>Pacemaker の [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] ログインおよびアクセス許可を作成する

[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] on Linux に基づいている Pacemaker 高可用性クラスターは、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] インスタンスにアクセスする必要があり、可用性グループそのものへのアクセス許可も必要です。 これらの手順では、ログインおよび関連するアクセス許可、さらに [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] へのログイン方法を Pacemaker に指示するファイルが作成されます。

1.  最初のレプリカに接続しているクエリ ウィンドウで、次のように実行します。

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD ='<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  ノード 1 で、コマンドを入力します。 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    Emacs エディターが開きます。
    
3.  エディターに次の 2 行を入力します。

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  Ctrl キーを押したまま、X キー、C キーの順に押し、ファイルを終了して保存します。

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    ファイルをロック ダウンします。

6.  レプリカとして機能する他のサーバーで手順 1 - 5 を繰り返します。

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Pacemaker クラスターに可用性グループのリソースを作成する (外部タイプのみ)

クラスター タイプ [外部] を指定したときは、可用性グループが [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] に作成された後で、対応するリソースを Pacemaker に作成する必要があります。 AG に関連付けられているリソースには、AG 自体と IP アドレスの 2 つがあります。 リスナー機能を使用しない場合、IP アドレス リソースの構成は省略可能ですが推奨されます。

作成される AG リソースは、クローンと呼ばれる特別な種類のリソースです。 AG リソースは基本的に各ノードのコピーを含み、マスターと呼ばれる制御リソースが 1 つあります。 マスターは、プライマリ レプリカをホストするサーバーに関連付けられています。 セカンダリ レプリカ (標準または構成専用) はスレーブと見なされ、フェールオーバー時にマスターに昇格できます。

1.  次の構文を使用して AG リソースを作成します。

    **Red Hat Enterprise Linux (RHEL) と Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failure-timeout=30s --master meta notify=true
    ```

    >[!NOTE]
    >RHEL 7.4 では、--master を使用すると警告が発生する場合があります。 これを回避するには、`sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failover-timeout=30s master notify=true` を使用します。
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
    meta failure-timeout=60s \
    op start timeout=60s \
    op stop timeout=60s \
    op promote timeout=60s \
    op demote timeout=10s \
    op monitor timeout=60s interval=10s \
    op monitor timeout=60s interval=11s role="Master" \
    op monitor timeout=60s interval=12s role="Slave" \
    op notify timeout=60s
    ms ms-ag_cluster <NameForAGResource> \
    meta master-max="1" master-node-max="1" clone-max="3" \
    clone-node-max="1" notify="true" \
    commit
    ```
    
    ここで、*NameForAGResource* は AG のこのクラスター リソースに付ける一意の名前、*AGName* は作成された AG の名前です。
 
2.  リスナー機能に関連付ける AG の IP アドレス リソースを作成します。

    **RHEL と Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForIPResource> ocf:heartbeat:IPaddr2 ip=<IPAddress> cidr_netmask=<Netmask>
    ```

    **SLES**
    
    ```bash
    crm configure \
    primitive <NameForIPResource> \
       ocf:heartbeat:IPaddr2 \
       params ip=<IPAddress> \
          cidr_netmask=<Netmask>
    ```
    
    ここで、*NameForIPResource* は IP リソースの一意の名前、*IPAddress* はリソースに関連付けられる静的 IP アドレスです。 SLES では、ネットマスクも指定する必要があります。 たとえば、255.255.255.0 では *Netmask* の値は 24 です。
    
3.  IP アドレスと AG リソースが同じノードで実行するように、コロケーション制約を構成する必要があります。

    **RHEL と Ubuntu**
    
    ```bash
    sudo pcs constraint colocation add <NameForIPResource> <NameForAGResource>-master INFINITY with-rsc-role=Master
    ```

    **SLES**
    
    ```bash
    crm configure <NameForConstraint> inf: \
    <NameForIPResource> <NameForAGResource>:Master 
    commit
    ```
    
    ここで、*NameForIPResource* は IP リソースの名前、*NameForAGResource* は AG リソースの名前です。また、SLES では *NameForConstraint* は制約の名前です。

4.  順序制約を作成して、IP アドレスよりも前に AG リソースが稼働するようにします。 コロケーション制約により順序制約が暗黙に示されますが、これによって適用されます。

    **RHEL と Ubuntu**
    
    ```bash
    sudo pcs constraint order promote <NameForAGResource>-master then start <NameForIPResource>
    ```
    
    **SLES**
    
    ```bash
    crm configure \
    order <NameForConstraint> inf: <NameForAGResource>:promote <NameForIPResource>:start
    commit
    ```
    
    ここで、*NameForIPResource* は IP リソースの名前、*NameForAGResource* は AG リソースの名前です。また、SLES では *NameForConstraint* は制約の名前です。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] on Linux の可用性グループ (AG) を作成および構成する方法について説明しました。 以下の方法を学習しました。
> [!div class="checklist"]
> * 可用性グループを有効にします。
> * AG エンドポイントと証明書を作成します。
> * [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) または Transact-SQL を使用して AG を作成します。
> * Pacemaker の [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] ログインとアクセス許可を作成します。
> * Pacemaker クラスターに AG リソースを作成します。

アップグレードやフェールオーバーなど、ほとんどの AG 管理タスクについては、以下を参照してください。

> [!div class="nextstepaction"]
> [SQL Server on Linux での HA 可用性グループの操作](sql-server-linux-availability-group-failover-ha.md)

