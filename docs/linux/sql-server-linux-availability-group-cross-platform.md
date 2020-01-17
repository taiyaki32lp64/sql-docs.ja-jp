---
title: Windows 上と Linux 上で SQL Server の Always On 可用性グループを構成する
description: Windows 上と Linux 上でレプリカを使用して SQL Server 可用性グループを構成します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/31/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: f6758760d8ea73d9ec0ac95a0e824a0fd46a6dbb
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68045190"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>Windows 上と Linux 上で SQL Server の Always On 可用性グループを構成する (クロスプラットフォーム)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

この記事では、Windows サーバー上の 1 つのレプリカと Linux サーバー上のもう 1 つのレプリカを使用して、Always On 可用性グループ (AG) を作成する手順について説明します。 レプリカが異なるオペレーティング システム上にあるため、この構成はクロスプラットフォームです。 この構成は、プラットフォーム間の移行またはディザスター リカバリー (DR) を目的として使用してください。 クロスプラットフォーム構成を管理するクラスター ソリューションがないため、この構成では高可用性はサポートされません。 

![ハイブリッド None](./media/sql-server-linux-availability-group-overview/image1.png)

先に進む前に、Windows と Linux での SQL Server インスタンスのインストールと構成について理解しておく必要があります。 

## <a name="scenario"></a>シナリオ

このシナリオでは、2 台のサーバーが異なるオペレーティング システム上に配置されています。 `WinSQLInstance` という名前の Windows Server 2016 で、プライマリ レプリカがホストされます。 `LinuxSQLInstance` という名前の Linux サーバーで、セカンダリ レプリカがホストされます。

## <a name="configure-the-ag"></a>AG を構成する 

AG を作成する手順は、読み取りスケール ワークロード用に AG を作成する手順と同じです。 クラスター マネージャーがないため、AG クラスターの種類は NONE になります。 

   >[!NOTE]
   >この記事のスクリプトでは、山かっこ `<` と `>` を使用して、お使いの環境に合う値に置き換える必要がある値を識別しています。 スクリプトには、山かっこそのものは必要ありません。 

1. Windows Server 2016 に SQL Server 2017 をインストールし、SQL Server 構成マネージャーから Always On 可用性グループを有効にし、混合モード認証を設定します。 

   >[!TIP]
   >このソリューションを Azure で検証する場合は、両方のサーバーを同じ可用性セットに配置して、それらがデータ センター内で確実に分離されるようにします。 

   **可用性グループを有効にする**

   手順については、「[Always On 可用性グループ機能を有効または無効にする (SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)」を参照してください。

   ![可用性グループを有効にする](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   SQL Server 構成マネージャーでは、このコンピューターがフェールオーバー クラスター内のノードではないことが認識されます。 

   可用性グループを有効にした後、SQL Server を再起動します。

   **混合モード認証を設定する**

   手順については、「[サーバーの認証モードの変更](../database-engine/configure-windows/change-server-authentication-mode.md#SSMSProcedure)」を参照してください。

1. Linux 上に SQL Server 2017 をインストールします。 手順については、[SQL Server のインストール](sql-server-linux-setup.md)に関する記事をご覧ください。 mssql-conf 経由で `hadr` を有効にします。

   シェル プロンプトから mssql conf 経由で `hadr` を有効にするには、次のコマンドを発行します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   `hadr` を有効にした後、SQL Server インスタンスを再起動します。  

   次の図に、この手順全体を示します。

   ![Linux 上で可用性グループを有効にする](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. 両方のサーバーで hosts ファイルを構成するか、DNS にサーバー名を登録します。

1. Windows と Linux の両方で、TPC 1433 と 5022 に対してファイアウォール ポートを開放します。

1. プライマリ レプリカで、データベース ログインとパスワードを作成します。

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. プライマリ レプリカで、マスター キーと証明書を作成し、秘密キーを使用して証明書をバックアップします。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
   BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
       );
   GO
   ```

1. 証明書と秘密キーを Linux サーバー (セカンダリ レプリカ) の `/var/opt/mssql/data` にコピーします。 これらのファイルを Linux サーバーにコピーするには、`pscp` を使用できます。 

1. 秘密キーと証明書のグループと所有権を `mssql:mssql` に設定します。

   次のスクリプトで、ファイルのグループと所有権を設定します。 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   次の図では、証明書とキーに対して所有権とグループが正しく設定されています。

   ![Linux 上で可用性グループを有効にする](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. セカンダリ レプリカで、データベース ログインとパスワードを作成し、マスター キーを作成します。

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. セカンダリ レプリカで、`/var/opt/mssql/data` にコピーした証明書を復元します。 

   ```sql
   CREATE CERTIFICATE dbm_certificate   
       AUTHORIZATION dbm_user
       FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
       WITH PRIVATE KEY (
       FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
       DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
   )
   GO
   ```

1. プライマリ レプリカで、エンドポイントを作成します。

   ```sql
   CREATE ENDPOINT [Hadr_endpoint]
       AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
       FOR DATA_MIRRORING (
           ROLE = ALL,
           AUTHENTICATION = CERTIFICATE dbm_certificate,
           ENCRYPTION = REQUIRED ALGORITHM AES
           );
   ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
   GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]
   GO
   ```

   >[!IMPORTANT]
   >リスナー TCP ポートに対してファイアウォールを開放する必要があります。 前述のスクリプトでは、このポートは 5022 です。 使用可能な任意の TCP ポートを使用してください。 

1. セカンダリ レプリカで、エンドポイントを作成します。 セカンダリ レプリカで上記のスクリプトを繰り返して、エンドポイントを作成します。 

1. プライマリ レプリカで、`CLUSTER_TYPE = NONE` で AG を作成します。 このサンプル スクリプトでは、`SEEDING_MODE = AUTOMATIC` を使用して AG を作成します。 

   >[!NOTE]
   >SQL Server の Windows インスタンスでデータ ファイルとログ ファイルに対して異なるパスを使用する場合、これらのパスはセカンダリ レプリカには存在しないため、SQL Server の Linux インスタンスに対する自動シード処理は失敗します。 クロスプラットフォーム AG に対して次のスクリプトを使用するには、データベースのデータ ファイルとログ ファイルのパスを Windows Server と同じにする必要があります。 または、スクリプトを更新して `SEEDING_MODE = MANUAL` を設定した後、`NORECOVERY` でデータベースをバックアップして復元して、データベースをシード処理できます。 
   >
   >この動作は、Azure Marketplace のイメージに適用されます。 
   >
   >自動シード処理の詳細については、[自動シード処理のディスク レイアウト](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout)に関する記事をご覧ください。 

   スクリプトを実行する前に、お使いの AG の値を更新します。

      * `<WinSQLInstance>` を、プライマリ レプリカの SQL Server インスタンスのサーバー名に置き換えます。

      * `<LinuxSQLInstance>` を、セカンダリ レプリカの SQL Server インスタンスのサーバー名に置き換えます。 

   AG を作成するには、値を更新し、プライマリ レプリカでスクリプトを実行します。  

   ```sql
   CREATE AVAILABILITY GROUP [ag1]
       WITH (CLUSTER_TYPE = NONE)
       FOR REPLICA ON
           N'<WinSQLInstance>' 
        WITH (
           ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            SEEDING_MODE = AUTOMATIC,
            FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
           N'<LinuxSQLInstance>' 
       WITH (
            ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
           SEEDING_MODE = AUTOMATIC,
           FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
           )
   GO
   ```
   
   詳細については、「[CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)」を参照してください。

1. セカンダリ レプリカで、AG に参加します。

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. AG 用のデータベースを作成します。 この例の手順では、`<TestDB>` という名前のデータベースを使用します。 自動シード処理を使用する場合は、データ ファイルとログ ファイルの両方に同じパスを設定してください。 

   スクリプトを実行する前に、データベース用の値を更新します。

      * `<TestDB>` を、お使いのデータベースの名前に置き換えます。

      * `<F:\Path>` を、お使いのデータベースとログ ファイルのパスに置き換えます。 データベースとログ ファイルで同じパスを使用します。 

      既定のパスを使用することもできます。 

    データベースを作成するには、次のスクリプトを実行します。 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. データベースの完全バックアップを実行します。 

1. 自動シード処理を使用しない場合は、セカンダリ レプリカ (Linux) サーバーにデータベースを復元します。 [バックアップと復元を使用して SQL Server データベースを Windows から Linux に移行します](sql-server-linux-migrate-restore-database.md)。 データベースを `WITH NORECOVERY` を指定してセカンダリ レプリカに復元します。 

1. AG にデータベースを追加します。 サンプル スクリプトを更新します。 `<TestDB>` を、お使いのデータベースの名前に置き換えます。 プライマリ レプリカで、次の SQL クエリを実行して、データベースを AG に追加します。

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. セカンダリ レプリカのデータベースにデータが設定されることを確認します。 

## <a name="fail-over-the-primary-replica"></a>プライマリ レプリカをフェールオーバーする

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

この記事では、移行または読み取りスケール ワークロードをサポートするクロスプラットフォーム AG を作成する手順を確認しました。 それは、ディザスター リカバリー目的でも使用できます。 AG をフェールオーバーする方法についても説明しました。 クロスプラットフォーム AG では クラスターの種類として `NONE` が使用され、クロスプラットフォームのクラスター ツールが存在しないため、高可用性はサポートされません。 

## <a name="next-steps"></a>次の手順

[Always On 可用性グループの概要](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[Linux デプロイでの SQL Server の可用性の基本](sql-server-linux-ha-basics.md)
