---
title: Linux 上で SQL Server レプリケーションを構成する
description: このチュートリアルでは、Linux 上で SQL Server スナップショット レプリケーションを構成する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: acc3f556371c52d02789a03813a28606435d86cd
ms.sourcegitcommit: 56fb0b7750ad5967f5d8e43d87922dfa67b2deac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2019
ms.locfileid: "75001972"
---
# <a name="configure-replication-with-t-sql"></a>T-SQL を使用してレプリケーションを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)] 

このチュートリアルでは、Transact-SQL を使用し、SQL Server の 2 つのインスタンスを使用して、Linux 上で SQL Server スナップショット レプリケーションを構成します。 パブリッシャーとディストリビューターは同じインスタンスになり、サブスクライバーは別のインスタンスに展開されます。

> [!div class="checklist"]
> * Linux 上で SQL Server レプリケーション エージェントを有効にする
> * サンプル データベースの作成
> * SQL Server エージェントのアクセス用にスナップショット フォルダーを構成する
> * ディストリビューターの構成
> * パブリッシャーを構成する
> * パブリケーションとアーティクルを構成する
> * サブスクライバーを構成する 
> * レプリケーション ジョブを実行する

すべてのレプリケーション構成は、[レプリケーション ストアド プロシージャ](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)を使用して構成できます。

## <a name="prerequisites"></a>前提条件
このチュートリアルを完了するには、次の要件があります。

- 最新バージョンの SQL Server on Linux を使用した SQL Server の 2 つのインスタンス
- SQLCMD や SSMS などのレプリケーションを設定する T-SQL クエリを発行するツール

   「[SSMS を使用して SQL Server on Linux を管理する](./sql-server-linux-manage-ssms.md)」を参照してください。

   >[!NOTE]
   >[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)] ([CU18](https://support.microsoft.com/help/4527377)) 以降では、SQL Server on Linux のインスタンス用の SQL Server レプリケーションがサポートされています。

## <a name="detailed-steps"></a>詳細な手順

1. Linux 上で SQL Server レプリケーション エージェントを有効にします。 両方のホスト マシン上のターミナルで次のコマンドを実行します。 

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   sudo systemctl restart mssql-server
   ```

1. サンプル データベースとテーブルを作成します。 パブリッシャーで、パブリケーションのアーティクルとして機能するサンプル データベースとテーブルを作成します。

   ```sql
   CREATE DATABASE Sales
   GO
   USE [SALES]
   GO 
   CREATE TABLE CUSTOMER([CustomerID] [int] NOT NULL, [SalesAmount] [decimal] NOT NULL)
   GO 
   INSERT INTO CUSTOMER (CustomerID, SalesAmount) VALUES (1,100),(2,200),(3,300)
   ```

   他の SQL Server インスタンスであるサブスクライバーで、アーティクルを受け取るデータベースを作成します。

   ```sql
   CREATE DATABASE Sales
   GO
   ```

1. SQL Server エージェントの読み取り用および書き込み用のスナップショット フォルダーを作成します。ディストリビューターで、スナップショット フォルダーを作成し、'mssql' ユーザーにアクセス権を付与します。 

   ```bash
   sudo mkdir /var/opt/mssql/data/ReplData/
   sudo chown mssql /var/opt/mssql/data/ReplData/
   sudo chgrp mssql /var/opt/mssql/data/ReplData/
   ```

1. ディストリビューターを構成します。 この例では、パブリッシャーはディストリビューターでもあります。 パブリッシャーで次のコマンドを実行して、ディストリビューション用にもインスタンスを構成します。

   ```sql
   DECLARE @distributor AS sysname
   DECLARE @distributorlogin AS sysname
   DECLARE @distributorpassword AS sysname
   -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
   SET @distributor = N'<distributor instance name>'--in this example, it will be the name of the publisher
   SET @distributorlogin = N'<distributor login>'
   SET @distributorpassword = N'<distributor password>'
   -- Specify the distribution database. 
   
   use master
   exec sp_adddistributor @distributor = @distributor -- this should be the hostname

   -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
   exec sp_adddistributiondb @database = N'distribution', @log_file_size = 2, @deletebatchsize_xact = 5000, @deletebatchsize_cmd = 2000, @security_mode = 0, @login = @distributorlogin, @password = @distributorpassword
   GO

   DECLARE @snapshotdirectory AS nvarchar(500)
   SET @snapshotdirectory = N'/var/opt/mssql/data/ReplData/'

   -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
   use [distribution] 
   if (not exists (select * from sysobjects where name = 'UIProperties' and type = 'U ')) 
          create table UIProperties(id int) 
   if (exists (select * from ::fn_listextendedproperty('SnapshotFolder', 'user', 'dbo', 'table', 'UIProperties', null, null))) 
          EXEC sp_updateextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties' 
   else 
         EXEC sp_addextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties'
   GO
   ```

1. パブリッシャーを構成します。 パブリッシャーで次の TSQL コマンドを実行します。

   ```sql
   DECLARE @publisher AS sysname
   DECLARE @distributorlogin AS sysname
   DECLARE @distributorpassword AS sysname
   -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
   SET @publisher = N'<instance name>' 
   SET @distributorlogin = N'<distributor login>'
   SET @distributorpassword = N'<distributor password>'
   -- Specify the distribution database. 

   -- Adding the distribution publishers
   exec sp_adddistpublisher @publisher = @publisher, 
   @distribution_db = N'distribution', 
   @security_mode = 0, 
   @login = @distributorlogin, 
   @password = @distributorpassword, 
   @working_directory = N'/var/opt/mssql/data/ReplData', 
   @trusted = N'false', 
   @thirdparty_flag = 0, 
   @publisher_type = N'MSSQLSERVER'
   GO
   ```

1. パブリケーション ジョブを構成します。 パブリッシャーで次の TSQL コマンドを実行します。

   ```sql
   DECLARE @replicationdb AS sysname
   DECLARE @publisherlogin AS sysname
   DECLARE @publisherpassword AS sysname
   SET @replicationdb = N'Sales'
   SET @publisherlogin = N'<Publisher login>'
   SET @publisherpassword = N'<Publisher Password>'

   use [Sales]
   exec sp_replicationdboption @dbname = N'Sales', @optname = N'publish', @value = N'true'
   
   -- Add the snapshot publication
   exec sp_addpublication 
   @publication = N'SnapshotRepl', 
   @description = N'Snapshot publication of database ''Sales'' from Publisher ''<PUBLISHER HOSTNAME>''.',
   @retention = 0, 
   @allow_push = N'true', 
   @repl_freq = N'snapshot', 
   @status = N'active', 
   @independent_agent = N'true'

   exec sp_addpublication_snapshot @publication = N'SnapshotRepl', 
   @frequency_type = 1, 
   @frequency_interval = 1, 
   @frequency_relative_interval = 1, 
   @frequency_recurrence_factor = 0, 
   @frequency_subday = 8, 
   @frequency_subday_interval = 1, 
   @active_start_time_of_day = 0,
   @active_end_time_of_day = 235959, 
   @active_start_date = 0, 
   @active_end_date = 0, 
   @publisher_security_mode = 0, 
   @publisher_login = @publisherlogin, 
   @publisher_password = @publisherpassword
   ```

1. sales テーブルからアーティクルを作成します。パブリッシャーで次の TSQL コマンドを実行します。

   ```sql
   use [Sales]
   exec sp_addarticle 
   @publication = N'SnapshotRepl', 
   @article = N'customer', 
   @source_owner = N'dbo', 
   @source_object = N'customer', 
   @type = N'logbased', 
   @description = null, 
   @creation_script = null, 
   @pre_creation_cmd = N'drop', 
   @schema_option = 0x000000000803509D,
   @identityrangemanagementoption = N'manual', 
   @destination_table = N'customer', 
   @destination_owner = N'dbo', 
   @vertical_partition = N'false'
   ```

1. サブスクリプションを構成します。 パブリッシャーで次の TSQL コマンドを実行します。

   ```sql
   DECLARE @subscriber AS sysname
   DECLARE @subscriber_db AS sysname
   DECLARE @subscriberLogin AS sysname
   DECLARE @subscriberPassword AS sysname
   SET @subscriber = N'<Instance Name>' -- for example, MSSQLSERVER
   SET @subscriber_db = N'Sales'
   SET @subscriberLogin = N'<Subscriber Login>'
   SET @subscriberPassword = N'<Subscriber Password>'

   use [Sales]
   exec sp_addsubscription 
   @publication = N'SnapshotRepl', 
   @subscriber = @subscriber,
   @destination_db = @subscriber_db, 
   @subscription_type = N'Push', 
   @sync_type = N'automatic', 
   @article = N'all', 
   @update_mode = N'read only', 
   @subscriber_type = 0

   exec sp_addpushsubscription_agent 
   @publication = N'SnapshotRepl', 
   @subscriber = @subscriber,
   @subscriber_db = @subscriber_db, 
   @subscriber_security_mode = 0, 
   @subscriber_login = @subscriberLogin,
   @subscriber_password = @subscriberPassword,
   @frequency_type = 1,
   @frequency_interval = 0, 
   @frequency_relative_interval = 0, 
   @frequency_recurrence_factor = 0, 
   @frequency_subday = 0, 
   @frequency_subday_interval = 0, 
   @active_start_time_of_day = 0, 
   @active_end_time_of_day = 0, 
   @active_start_date = 0, 
   @active_end_date = 19950101
   GO
   ```

1. レプリケーション エージェント ジョブを実行します。 次のクエリを実行してジョブの一覧を取得します。

   ```sql
   SELECT name, date_modified FROM msdb.dbo.sysjobs order by date_modified desc
   ```

   スナップショット レプリケーション ジョブを実行してスナップショットを生成します。

   ```sql
   USE msdb;   
   --generate snapshot of publications, for example
   EXEC dbo.sp_start_job N'PUBLISHER-PUBLICATION-SnapshotRepl-1'
   GO
   ```

   スナップショット レプリケーション ジョブを実行してスナップショットを生成します。

   ```sql
   USE msdb;
   --distribute the publication to subscriber, for example
   EXEC dbo.sp_start_job N'DISTRIBUTOR-PUBLICATION-SnapshotRepl-SUBSCRIBER'
   GO
   ```

1. サブスクライバーに接続し、レプリケートされたデータを照会します。    

   サブスクライバーで、次のクエリを実行してレプリケーションが機能していることを確認します。

   ```sql
   SELECT * from [Sales].[dbo].[CUSTOMER]
   ```

このチュートリアルでは、Transact-SQL を使用し、SQL Server の 2 つのインスタンスを使用して、Linux 上で SQL Server スナップショット レプリケーションを構成します。

> [!div class="checklist"]
> * Linux 上で SQL Server レプリケーション エージェントを有効にする
> * サンプル データベースの作成
> * SQL Server エージェントのアクセス用にスナップショット フォルダーを構成する
> * ディストリビューターの構成
> * パブリッシャーを構成する
> * パブリケーションとアーティクルを構成する
> * サブスクライバーを構成する 
> * レプリケーション ジョブを実行する

## <a name="see-also"></a>参照

レプリケーションの詳細については、[SQL Server レプリケーションのドキュメント](../relational-databases/replication/sql-server-replication.md)を参照してください。

## <a name="next-steps"></a>次のステップ

[概念:Linux での SQL Server のレプリケーション](sql-server-linux-replication.md)

[レプリケーション ストアド プロシージャ](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。
