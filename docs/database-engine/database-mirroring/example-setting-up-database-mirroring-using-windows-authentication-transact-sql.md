---
title: Windows 認証でのデータベース ミラーリングの構成 (T-SQL)
description: Transact-SQL (T-SQL) で Windows 認証を使用して、ミラーリング監視サーバーを利用するデータベース ミラーリング セッションを作成する場合に必要なすべての段階を示す例
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- Windows authentication [SQL Server]
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: 35800769-aede-4aac-b077-0e0e487e302f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2a263cd161370a4d3f87c673209e82296ec2a28c
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822262"
---
# <a name="example-configure-database-mirroring-using-windows-authentication-transact-sql"></a>例:Windows 認証を使用したデータベース ミラーリングの構成 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  この例では、Windows 認証を使用してミラーリング監視サーバーを利用するデータベース ミラーリング セッションを作成する場合に必要なすべての段階を示しています。 このトピックの例では、 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用する代わりに、データベース ミラーリング セキュリティ構成ウィザードを使用してデータベース ミラーリングを設定することもできます。 詳細については、このトピックの後半の「 [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)」を参照してください。  
  
## <a name="prerequisite"></a>前提条件  
 この例では、既定により単純復旧モデルを使用する **AdventureWorks** サンプル データベースを使用します。 このデータベースでデータベース ミラーリングを使用するには、完全復旧モデルを使用するように変更する必要があります。 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用してこの変更を行うには、次のように ALTER DATABASE ステートメントを使用します。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks   
SET RECOVERY FULL;  
GO  
```  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の復旧モデルを変更する方法については、「[データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)」をご覧ください。  
  
### <a name="permissions"></a>アクセス許可  
 データベースにおける ALTER 権限、および CREATE ENDPOINT 権限、または **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="example"></a>例  
 この例では、2 つのパートナーとミラーリング監視サーバーが、3 つのコンピューター システムの既定のサーバー インスタンスです。 3 つのサーバー インスタンスは同じ Windows ドメインで実行されますが、ミラーリング監視サーバー インスタンスはユーザー アカウント (スタートアップ サービス アカウントとして使用されます) が異なります。  
  
 次の表は、この例で使用する値をまとめたものです。  
  
|初期ミラー化ロール|ホスト システム|ドメイン ユーザー アカウント|  
|----------------------------|-----------------|-------------------------|  
|プリンシパル|PARTNERHOST1|*\<Mydomain>\\<dbousername\>*|  
|ミラー|PARTNERHOST5|*\<Mydomain>\\<dbousername\>*|  
|ミラーリング監視サーバー|WITNESSHOST4|*\<Somedomain>\\<witnessuser\>*|  
  
1.  プリンシパル サーバー インスタンス (PARTNERHOST1 の既定のインスタンス) でエンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=PARTNER)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    -- Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
2.  ミラー サーバー インスタンス (PARTNERHOST5 の既定のインスタンス) でエンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
3.  ミラーリング監視サーバー インスタンス (WITNESSHOST4 の既定のインスタンス) でエンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=WITNESS)  
    GO  
    --Create a login for the partner server instances,  
    --which are both running as Mydomain\dbousername:  
    USE master ;  
    GO  
    CREATE LOGIN [Mydomain\dbousername] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
4.  ミラー データベースを作成します。 詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)を使用します。  
  
5.  PARTNERHOST5 のミラー サーバー インスタンスで、PARTNERHOST1 のサーバー インスタンスをパートナーとして設定します (初期プリンシパル サーバー インスタンスにします)。  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER =   
        'TCP://PARTNERHOST1.COM:7022'  
    GO  
    ```  
  
6.  PARTNERHOST1 のプリンシパル サーバー インスタンスで、PARTNERHOST5 のサーバー インスタンスをパートナーとして設定します (初期ミラー サーバー インスタンスにします)。  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://PARTNERHOST5.COM:7022'  
    GO  
    ```  
  
7.  プリンシパル サーバーで、ミラーリング監視サーバー (WITNESSHOST4) を設定します。  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET WITNESS =   
        'TCP://WITNESSHOST4.COM:7022'  
    GO  
    ```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
-   [TRUSTWORTHY プロパティを使用するようにミラー データベースを設定する方法 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
-   [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [例:証明書を使用したデータベース ミラーリングの設定 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [データベース ミラーリングと Always On 可用性グループのトランスポート セキュリティ &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
