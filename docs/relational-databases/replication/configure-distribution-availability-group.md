---
title: 可用性グループのディストリビューション データベースを構成する
description: Always On 可用性グループを使用して、SQL Server レプリケーションのディストリビューション データベースを構成します。
ms.custom: seo-lt-2019
ms.date: 01/16/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d5f721d589354d5e7f4ec970bf0ea086895df129
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75320005"
---
# <a name="set-up-replication-distribution-database-in-always-on-availability-group"></a>Always On 可用性グループのレプリケーション ディストリビューション データベースを設定する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、Always On 可用性グループ (AG) の SQL Server レプリケーション ディストリビューション データベースを設定する方法について説明します。

SQL Server 2017 CU 6 と SQL Server 2016 SP2-CU3 では、次のメカニズムを使用して AG のレプリケーション ディストリビューション データベースをサポートするようになりました。

- ディストリビューション データベース AG にはリスナーが必要です。 パブリッシャーでは、ディストリビューターを追加する場合、リスナー名をディストリビューター名として使用します。
- レプリケーション ジョブの作成では、リスナー名をディストリビューター名として使用します。 ディストリビューション サーバー上で作成されたレプリケーション スナップショット ジョブ、ログ リーダー ジョブ、ディストリビューション エージェント (プッシュ サブスクリプション) ジョブは、ディストリビューション DB 用 AG のすべてのセカンダリ レプリカ上で作成されます。
 >[!NOTE]
 >プル サブスクリプション用のディストリビューション エージェント ジョブは、サブスクライバー サーバー上には作成されますが、ディストリビューション サーバー上には作成されません。 
- 新しいジョブでは、ディストリビューション データベースの状態 (AG 内でプライマリかセカンダリか) を監視し、ディストリビューション データベースの状態に基づいてレプリケーション ジョブを有効または無効にします。

AG のディストリビューション データベースを下記の手順に基づいて構成したら、ディストリビューション データベース AG のフェールオーバーの前後にレプリケーション構成ジョブおよびランタイム ジョブが正常に実行されるようになります。

## <a name="supported-scenarios"></a>サポートされるシナリオ

- AG に含めるディストリビューション データベースを構成します。
- AG フェールオーバーの前後にパブリケーションやサブスクリプションなどのレプリケーションを構成します。
- フェールオーバーの前後に機能するレプリケーション ジョブ。
- ディストリビューション データベースが AG に含まれている場合にディストリビューター側およびパブリッシャー側でレプリケーションを削除します。
- 既存のディストリビューション データベース AG にノードを追加、またはその AG からノードを削除します。
- ディストリビューターには複数のディストリビューション データベースが存在する場合があります。 各ディストリビューション データベースは独自の AG に属することはできますが、任意の AG に属することはできません。 複数のディストリビューション データベースで AG を共有することができます。
- パブリッシャーとディストリビューターは別々の SQL Server インスタンス上に置く必要があります。
- ディストリビューション データベースをホストしている可用性グループのリスナーが、既定以外のポートを使用するように構成されている場合は、リスナーと既定以外のポートに別名を設定する必要があります。

## <a name="limitations-or-exclusions"></a>制限事項または適用除外事項

- ローカル ディストリビューターはサポートされていません。 たとえば、パブリッシャーとディストリビューターは、別々の SQL Server インスタンスでなければなりません。 これらのインスタンスは、同じノード セットでホストできます。  自身をディストリビューターとして使用するパブリッシャー ( ローカル ディストリビューターとも呼ばれる) では、AG のディストリビューション データベースをサポートすることはできません。
- Oracle パブリッシャーはサポートされていません。
- マージ レプリケーションはサポートされていません。
- 即時更新サブスクライバーまたはキュー更新サブスクライバーでのトランザクション レプリケーションはサポートされていません。
- ピア ツー ピア レプリケーションはサポートされていません。
- ディストリビューション データベースのレプリカをホストする SQL Server 2017 インスタンスはすべて、SQL Server 2017 CU 6 以降とする必要があります。 
- ディストリビューション データベースのレプリカをホストする SQL Server 2016 インスタンスはすべて、SQL Server 2016 SP2-CU3 以降とする必要があります。
- ディストリビューション データベースのレプリカをホストする SQL Server インスタンスはすべて、同じバージョンである必要があります。ただし、アップグレードが実行される狭いタイムフレームの期間中は例外です。
- ディストリビューション データベースは、完全復旧モードである必要があります。
- 復旧し、トランザクション ログの切り捨てを許可するには、完全バックアップとトランザクション ログ バックアップを構成します。
- ディストリビューション データベース AG では、リスナーが構成されている必要があります。
- ディストリビューション データベース AG 内のセカンダリ レプリカは、同期または非同期のいずれにも指定できます。 同期モードが推奨され、優先されます。
- 双方向のトランザクション レプリケーションはサポートされていません。
- ディストリビューション データベースが可用性グループに追加されたときに、SSMS でディストリビューション データベースが同期中/同期済みとして表示されることはありません。


   >[!NOTE]
   >任意のレプリケーション ストアド プロシージャ (たとえば、`sp_dropdistpublisher`、`sp_dropdistributiondb`、`sp_dropdistributor`、 `sp_adddistributiondb`、`sp_adddistpublisher`) をセカンダリ レプリカ上で実行するには、レプリカが完全に同期されていることを事前に確認しておきます。

- ディストリビューション データベース AG 内のセカンダリ レプリカはすべて読み取り可能である必要があります。
- ディストリビューション データベース AG 内のノードはすべて同じドメイン アカウントを使用して SQL Server エージェントを実行する必要があります。このドメイン アカウントの権限は各ノードで同じである必要があります。
- 任意のレプリケーション エージェントをプロキシ アカウントで実行する場合、このプロキシ アカウントがディストリビューション データベース AG 内のすべてのノードに割り当てられており、その権限は各ノードで同じである必要があります。
- ディストリビューション データベース AG に参加しているすべてのレプリカで、ディストリビューターまたはディストリビューション データベースのプロパティを変更します。
- ディストリビューション データベース AG に参加しているすべてのレプリカで、msdb ストアド プロシージャまたは SQL Server Management Studio を介してレプリケーション ジョブに変更を加えます。
- パブリッシャー上でディストリビューターを構成する場合は、スクリプトを使用する必要があります。 レプリケーション ウィザードを使用することはできません。 レプリケーション ウィザードおよびプロパティ シートは他の目的ではサポートされています。
- ディストリビューション データベースに対して AG を構成するには、スクリプトしか使用できません。
- AG のディストリビューション データベースの設定は、新しいレプリケーション構成として行う必要があります。 既存のディストリビューション データベースを AG に切り替えることはサポートされていません。 また、ディストリビューション データベースは AG から外されると、有効なディストリビューション データベースとして機能しなくなります。そのようなディストリビューション データベースは削除する必要があります。

## <a name="configuration-architecture"></a>構成アーキテクチャ

この記事の例では、次のサーバー名と設定を使用します。

- DIST1、DIST2、DIST3 はディストリビューター サーバーです。
- PUB はパブリッシャー サーバーです。
- ディストリビューション データベースの AG が形成された後、リスナー名は DISTLISTENER となります。
- DIST1 はディストリビューション データベース AG の初期のプライマリ レプリカとなることを目的としています。

## <a name="configure-distributor-distribution-database-and-publisher"></a>ディストリビューター、ディストリビューション データベース、パブリッシャーを構成する

この例では、ディストリビューターとパブリッシャーを新規に構成し、ディストリビューション データベースを AG に含めます。

### <a name="distributors-workflow"></a>ディストリビューターのワークフロー

1. `sp_adddistributor @@servername` を使用して DIST1、DIST2、DIST3 をディストリビューターとして構成します。 `@password` によって `distributor_admin` のパスワードを指定します。 `@password` は、DIST1、DIST2、DIST3 の間で同じにする必要があります。
2. `sp_adddistributiondb` を使用して DIST1 上にディストリビューション データベースを作成します。 ディストリビューション データベースの名前は `distribution` です。 `distribution` データベースの回復モードを簡易から完全に変更します。
3. DIST1、DIST2、および DIST3 上でレプリカを使用して `distribution` データベース用の AG を作成します。 すべてのレプリカを同期させることをお勧めします。 セカンダリ レプリカを読み取り可能に構成するか、読み取りを許可するように構成します。 この時点では、ディストリビューション データベースは AG であり、DIST1 がプライマリ レプリカ、DIST2 と DIST3 がセカンダリ レプリカです。
4. AG 用に `DISTLISTENER` という名前のリスナーを構成します。
5. 復旧し、トランザクション ログの切り捨てを許可するには、完全バックアップとトランザクション ログ バックアップを構成します。
6. DIST2 および DIST3 上で次を実行します。

   ```sql
   sp_adddistributiondb 'distribution'
   ```

1. `PUB` をパブリッシャーとして DIST1 に追加するには、次を実行します。
   
   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   `@working_directory` の値は、DIST1、DIST2、および DIST3 とは無関係のネットワーク パスとする必要があります。

1. DIST2 および DIST3 上で次を実行します。  

   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   `@working_directory` の値は、前の手順と同じにする必要があります。

### <a name="publisher-workflow"></a>パブリッシャーのワークフロー

`distribution` データベース AG のリスナーをディストリビューターとして PUB に追加するには、次を実行します。 

   ```sql
   sp_adddistributor @distributor = 'DISTLISTENER', @password = <distributor_admin password> 
   ```

   @password の値は、ディストリビューターのワークフローでディストリビューターを構成したときに指定した値とする必要があります。

## <a name="remove-distributor-and-publisher"></a>ディストリビューターとパブリッシャーを削除する

この例では、ディストリビューション データベースが AG 内にある場合に、パブリッシャーとディストリビューターを削除します。

### <a name="publisher-workflow"></a>パブリッシャーのワークフロー

PUB 上で、このパブリッシャー用のサブスクリプションとパブリケーションをすべて削除してから、`sp_dropdistributor` を呼び出します。

### <a name="distributors-workflow"></a>ディストリビューターのワークフロー

この例では、DIST1 が `distribution` データベース AG の現在のプライマリ レプリカです。 DIST2 と DIST3 は、セカンダリ レプリカです。

1. DIST2 および DIST3 上で次を実行します。

   ```sql
   sp_dropdistpublisher 'PUB',  @no_checks = 1
   ```

1. DIST1 上で次を実行します。

   ```sql
   sp_dropdistpublisher 'PUB'
   ```

1. AG を削除します。
2. DIST2 および DIST3 上で、回復によってデータベースを復元することで、`distribution` データベースを read_write モードに変更します。
   
   ```sql
   RESTORE DATABASE distribution WITH RECOVERY, KEEP_REPLICATION
   ```

1. `distribution` データベースを削除し、スナップショット ディレクトリを保持するには、次を実行します。 

   ```sql
   sp_dropdistributiondb 'distribution' , @former_ag_secondary=1
   ```

  この手順では、このレプリカに対するすべての未解決ジョブを削除します。

1. DIST1 上で `distribution` データベースを削除するには、次を実行します。

   ```sql
   sp_dropdistributiondb 'distribution'
   ``` 

1. AG 内にディストリビューション データベースが他に存在しない場合は、DIST1、DIST2、および DIST3 上で `sp_dropdistributor` を実行します。

## <a name="add-a-replica-to-distribution-database-ag"></a>ディストリビューション データベース AG にレプリカを追加する

この例では、AG のディストリビューション データベースを対象にした既存のレプリケーション構成に新しいディストリビューターを追加します。 この例では、既存のディストリビューション データベースは AG に含まれています。 DIST1 および DIST2 はディストリビューターです。`distribution` は AG に含まれているディストリビューション データベースです。PUB はパブリッシャーです。 AG にレプリカとして DIST3 を追加する

### <a name="distributors-workflow"></a>ディストリビューターのワークフロー

1. `sp_adddistributor @@servername` を使用して DIST3 をディストリビューターとしてする必要があります。 @password パラメーターを使用して、`distributor_admin` のパスワードを指定する必要があります。 パスワードは、DIST1 および DIST2 に対して指定したものと同じにする必要があります。
2. 現在のディストリビューション データベース用の AG に DIST3 を追加します。
3. DIST3 上で次を実行します。

   ```sql
   sp_adddistributiondb 'distribution'
   ```

4. DIST3 上で次を実行します。 

   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   `@working_directory` の値は、DIST1 および DIST2 に対して指定したものと同じにする必要があります。

4. DIST3 では、サブスクライバ―に対してリンク サーバーを再作成する必要があります。

## <a name="remove-a-replica-from-distribution-database-ag"></a>ディストリビューション データベース AG からレプリカを削除する

この例では、現在のディストリビューション データベース AG からディストリビューターを削除しますが、ディストリビューション データベース AG 内の残りのレプリカには影響ありません。 この例では、ディストリビューション データベースは AG に含まれています。 DIST1、DIST2、および DIST3 はディストリビューターです。`distribution` は AG に含まれているディストリビューション データベースです。PUB はパブリッシャーです。 AG から DIST3 を削除します。

### <a name="distributors-workflow"></a>ディストリビューターのワークフロー

1. DIST3 が `distribution` データベース AG のセカンダリ レプリカであることを確認します。
2. `distribution` データベース AG から DIST3 を削除します。
3. DIST3 上で、回復によってデータベースを復元することで、`distribution` データベースを read_write モードに変更します。 たとえば、次のコマンドを実行します。  
   
   ```sql
   RESTORE DATABASE distribution WITH RECOVERY, KEEP_REPLICATION.
   ```
   
1. DIST3 に対する孤立したジョブをすべて削除するには、次を実行します。 

   ```sql
   sp_dropdistpublisher 'PUB', @no_checks = 1
   ```

1. DIST3 上で次を実行します。

   ```sql
   sp_dropdistributiondb 'distribution', @former_ag_secondary=1
   ```

1. DIST3 上で次を実行します。 

   ```sql
   sp_dropdistributor
   ```

## <a name="remove-a-publisher-from-distribution-database-ag"></a>ディストリビューション データベース AG からパブリッシャーを削除する

この例では、ディストリビューターの現在のディストリビューション データベース AG からパブリッシャーを削除しますが、このディストリビューション データベース AG によって提供されている残りのパブリッシャーには影響ありません。 この例では、既存の構成のディストリビューション データベースは AG に含まれています。 DIST1、DIST2、および DIST3 はディストリビューターです。`distribution` は AG に含まれているディストリビューション データベースです。PUB1 と PUB2 は `distribution` データベースによって提供されているパブリッシャーです。 例では、これらのディストリビューターから PUB1 を削除します。

### <a name="publisher-workflow"></a>パブリッシャーのワークフロー

PUB1 上で、このパブリッシャー用のサブスクリプションとパブリケーションをすべて削除してから、`sp_dropdistributor` を呼び出します。

### <a name="distributor-workflow"></a>ディストリビューターのワークフロー

DIST1 は `distribution` データベース AG の現在のプライマリ レプリカです。

1. DIST2 および DIST3 上で次を実行します。

   ```sql
   sp_dropdistpublisher 'PUB1',  @no_checks = 1
   ```

1. DIST1 上で次を実行します。

   ```sql
   sp_dropdistpublisher 'PUB1'
   ```

1. この時点で、DIST2 または DIST3 には PUB1 に関連する孤立したジョブが存在する可能性があります。 DIST2 および DIST3 へのフェールオーバーが発生するたびに、PUB1 のすべてのパブリケーションに関連する孤立したジョブは `Monitor and sync replication agent jobs` ジョブによって削除されます。

## <a name="add-subscription"></a>サブスクリプションを追加する

この例は、ディストリビューター間でサブスクライバー情報を正しく構成する方法について示します。 この例ではサブスクライバーを追加します。 DIST1 は AG 内のディストリビューション データベースの現在のプライマリ レプリカであり、DIST2 と DIST3 は AG 内のディストリビューション データベースの現在のセカンダリ レプリカです。 サブスクライバーの名前は SUB です。

### <a name="publisher-workflow"></a>パブリッシャーのワークフロー

PUB 上で、サブスクライバー `SUB` に対して通常行うのと同様にサブスクリプションを追加します。

### <a name="distributor-workflow"></a>ディストリビューターのワークフロー

DIST2 および DIST3 上で、'SUB' のリンク サーバーが DIST2 または DIST3 にまだ登録されていない場合は追加します。 次のサンプルは、リンク サーバーの作成用の TSQL です。

   ```sql 
   EXEC master.dbo.sp_addlinkedserver@server =N'SUB', @srvproduct=N'SQL Server'
   /* For security reasons the linked server remote logins password is changed with ######## */
   EXEC master.dbo.sp_addlinkedsrvlogin@rmtsrvname=N'SUB', @useself=N'True',@locallogin=NULL,@rmtuser=NULL,@rmtpassword=NULL
   ```

## <a name="add-a-pull-subscription"></a>プル サブスクリプションを追加する

### <a name="subscriber-workflow"></a>サブスクライバーのワークフロー

AG 内のディストリビューション データベースでのパブリケーションのためにプル サブスクリプションを追加するには、`@distributor` の `sp_addpullsubscription_agent` パラメーターに AG リスナー名を使用します。

## <a name="sample-t-sql-create-distribution-db-in-ag"></a>サンプル T-SQL: AG でのディストリビューション DB の作成

次のスクリプトは、可用性グループ内でディストリビューション データベースを有効にします。 

```sql
--- WorkFlow to Enable Distribution Database In AG.

-- SECTION 1 ---- CONFIGURE THE DISTRIBUTOR SERVERS

-- Step1 - Configure the Distribution DB nodes (AG Replicas) to act as a distributor
:Connect SQLNode1
sp_adddistributor @distributor = @@ServerName, @password = 'Pass@word1'
Go 
:Connect SQLNode2
sp_adddistributor @distributor = @@ServerName, @password = 'Pass@word1'
Go

-- Step2 - Configure the Distribution Database
:Connect SQLNode1
USE master
EXEC sp_adddistributiondb @database = 'DistributionDB', @security_mode = 1;
GO
Alter Database [DistributionDB] Set Recovery Full
Go
Backup Database [DistributionDB] to Disk = 'Nul'
Go
-- Step 3 - Create AG for the Distribution DB.
:Connect SQLNode1
USE [master]
GO
CREATE ENDPOINT [Hadr_endpoint] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)   
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE
, ENCRYPTION = REQUIRED ALGORITHM AES)
GO

:Connect SQLNode2
USE [master]
GO
CREATE ENDPOINT [Hadr_endpoint] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)   
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE
, ENCRYPTION = REQUIRED ALGORITHM AES)
GO

:Connect SQLNode1
-- Create the Availability Group
CREATE AVAILABILITY GROUP [DistributionDB_AG]
FOR DATABASE [DistributionDB]
REPLICA ON 'SQLNode1'
WITH (ENDPOINT_URL = N'TCP://SQLNode1.contoso.com:5022', 
         FAILOVER_MODE = AUTOMATIC, 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
         BACKUP_PRIORITY = 50, 
         SECONDARY_ROLE(ALLOW_CONNECTIONS = ALL), 
         SEEDING_MODE = AUTOMATIC),
N'SQLNode2' WITH (ENDPOINT_URL = N'TCP://SQLNode2.contoso.com:5022', 
     FAILOVER_MODE = AUTOMATIC, 
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
     BACKUP_PRIORITY = 50, 
     SECONDARY_ROLE(ALLOW_CONNECTIONS = ALL), 
     SEEDING_MODE = AUTOMATIC);
 GO


:Connect SQLNode2
ALTER AVAILABILITY GROUP [DistributionDB_AG] JOIN
GO  
ALTER AVAILABILITY GROUP [DistributionDB_AG] GRANT CREATE ANY DATABASE
Go

--STEP4 - Create the Listener for the Availability Group. This is very important.
:Connect SQLNode1

USE [master]
GO
ALTER AVAILABILITY GROUP [DistributionDB_AG]
ADD LISTENER N'DistributionDBList' (
WITH IP
((N'10.0.0.8', N'255.255.255.0')) , PORT=1500);
GO

-- STEP 5 - Enable SQLNode1 also as a Distributor
:CONNECT SQLNODE2
EXEC sp_adddistributiondb @database = 'DistributionDB', @security_mode = 1;
GO

--STEP 6 - On all Distributor Nodes Configure the Publisher Details 
:CONNECT SQLNODE1
EXEC sp_addDistPublisher @publisher = 'SQLNode4', @distribution_db = 'DistributionDB', 
    @working_directory = '\\sqlfileshare\Dist_Work_Directory\'
GO
:CONNECT SQLNODE2
EXEC sp_addDistPublisher @publisher = 'SQLNode4', @distribution_db = 'DistributionDB', 
    @working_directory = '\\sqlfileshare\Dist_Work_Directory\'
GO

-- SECTION 2 ---- CONFIGURE THE PUBLISHER SERVER
:CONNECT SQLNODE4
EXEC sp_addDistributor @distributor = 'DistributionDBList', -- Listener for the Distribution DB.    
    @password = 'Pass@word1'
Go

-- SECTION 3 ---- CONFIGURE THE SUBSCRIBERS 
-- On Publisher, create the publication as one would normally do.
-- On the Secondary replicas of the Distribution DB, add the Subscriber as a linked server.
:CONNECT SQLNODE2
EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE5', @srvproduct=N'SQL Server'
 /* For security reasons the linked server remote logins password is changed with ######## */
EXEC master.dbo.sp_addlinkedsrvlogin @rmtsrvname=N'SQLNODE5',@useself=N'True',@locallogin=NULL,@rmtuser=NULL,@rmtpassword=NULL 
```

## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [ディストリビューターのセキュリティ保護](../../relational-databases/replication/security/secure-the-distributor.md)  
  
## <a name="next-steps"></a>次のステップ
 [ディストリビューターとパブリッシャーのプロパティの表示および変更](view-and-modify-distributor-and-publisher-properties.md)  
 [パブリッシングおよびディストリビューションの無効化](disable-publishing-and-distribution.md)  
 [レプリケーションのデータベースの有効化 (SQL Server Management Studio)](enable-a-database-for-replication-sql-server-management-studio.md) 
