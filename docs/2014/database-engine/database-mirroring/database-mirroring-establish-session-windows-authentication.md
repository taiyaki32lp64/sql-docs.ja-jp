---
title: データベース ミラーリング (TRANSACT-SQL) の Windows 認証を使用してセッションを確立 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 143c68a5-589f-4e7f-be59-02707e1a430a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c1ea3cd62c97cecd9af0b8b696156b9f2622f5b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62755508"
---
# <a name="establish-a-database-mirroring-session-using-windows-authentication-transact-sql"></a>Windows 認証を使用してデータベース ミラーリング セッションを確立する方法 (Transact-SQL)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] を使用します。  
  
 ミラー データベースを準備した後 (「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)」を参照)、データベース ミラーリング セッションを確立できます。 プリンシパル サーバー、ミラー サーバー、およびミラーリング監視サーバーのインスタンスは、別々のホスト システムにある別々のサーバー インスタンスでなければなりません。  
  
> [!IMPORTANT]  
>  ミラーリングの構成はパフォーマンスに影響する場合があるので、データベース ミラーリングの構成はピーク タイム以外の時間に行うことをお勧めします。  
  
> [!NOTE]  
>  特定のサーバー インスタンスを、同じパートナーまたは別のパートナーを含む複数の同時実行データベース ミラーリング セッションに参加させることができます。 また、サーバー インスタンスを、あるセッションではパートナーとし、別のセッションではミラーリング監視にすることができます。 ミラー サーバー インスタンスでは、プリンシパル サーバー インスタンスと同じエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されている必要があります。 データベース ミラーリングは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。 また、ワークロードの処理能力が同程度のシステム上で運用することを強くお勧めします。  
  
### <a name="to-establish-a-database-mirroring-session"></a>データベース ミラーリング セッションを確立するには  
  
1.  ミラー データベースを作成します。 詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)のすべてのエディションで使用できるわけではありません。  
  
2.  各サーバー インスタンスにセキュリティを設定します。  
  
     データベース ミラーリング セッションの各サーバー インスタンスには、データベース ミラーリング エンドポイントが必要です。 エンドポイントが存在しない場合は、作成する必要があります。  
  
    > [!NOTE]  
    >  サーバー インスタンスによりデータベースのミラーリングに使用される認証の形式は、データベース ミラーリング エンドポイントのプロパティで指定します。 データベース ミラーリングのトランスポートには、Windows 認証と証明書ベースの認証の 2 種類のセキュリティを使用できます。 詳細については、次を参照してください。[データベース ミラーリングと AlwaysOn 可用性グループのトランスポート セキュリティ&#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)します。  
  
     各パートナー サーバーで、データベース ミラーリング用のエンドポイントが存在していることを確認します。 サポートするミラーリング セッションの数にかかわらず、サーバー インスタンスではデータベース ミラーリング エンドポイントを 1 つしか持つことができません。 このサーバー インスタンスをデータベース ミラーリング セッションでパートナー専用に使用する場合は、パートナーのロールをエンドポイントに割り当てることができます (ROLE **=** PARTNER)。 また、このサーバーを他のデータベース ミラーリング セッションのミラーリング監視サーバーとしても使用する場合は、エンドポイントのロールを ALL として割り当てます。  
  
     SET PARTNER ステートメントを実行するには、両方のパートナーのエンドポイントの STATE が、STARTED に設定されている必要があります。  
  
     サーバー インスタンスにデータベース ミラーリング エンドポイントがあるかどうかを調べて、そのロールと状態を確認するには、そのインスタンスで、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
    > [!IMPORTANT]  
    >  使用中のデータベース ミラーリング エンドポイントは再構成しないでください。 データベース ミラーリング エンドポイントが存在し、既に使用されている場合、サーバー インスタンスのすべてのセッションでそのエンドポイントを使用することをお勧めします。 使用中のエンドポイントを削除すると、そのエンドポイントが再起動され、既存のセッションの接続が切断される場合があります。この場合、他のサーバー インスタンスからはエラーが発生したように見える可能性があります。 これは、自動フェールオーバーを伴う高い安全性モードでは特に重要です。この場合、パートナーでエンドポイントを再構成すると、フェールオーバーの原因になることがあります。 また、セッションにミラーリング監視サーバーが設定されている場合、データベース ミラーリング エンドポイントを削除すると、そのセッションのプリンシパル サーバーがクォーラムを失う可能性があります。プリンシパル サーバーがクォーラムを失うと、データベースがオフラインになりユーザー接続が切断されます。 詳細については、「[クォーラム: データベースの可用性にミラーリング監視サーバーが与える影響 &#40;データベース ミラーリング&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md)」を参照してください。  
  
     いずれかのパートナーにエンドポイントがない場合は、「[Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)」を参照してください。  
  
3.  サーバー インスタンスが別のドメイン ユーザー アカウントで実行されている場合、それぞれに他方のインスタンスの **master** データベースのログインが必要になります。 ログインが存在しない場合は、作成する必要があります。 詳細については、「 [Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md)のすべてのエディションで使用できるわけではありません。  
  
4.  プリンシパル サーバーをミラー データベースのパートナーとして設定するには、ミラー サーバーに接続し、次のステートメントを実行します。  
  
     ALTER DATABASE *<database_name>* SET PARTNER **=** _<server_network_address>_  
  
     *<database_name>* はミラー化するデータベースの名前 (両方のパートナーで同一の名前にします)、 *<server_network_address>* はプリンシパル サーバーのサーバー ネットワーク アドレスです。  
  
     サーバー ネットワーク アドレスの構文は次のとおりです。  
  
     TCP<strong>://</strong>\<*system-address>* <strong>:</strong>\<*port>*  
  
     \<*system-address*> は目的のコンピューター システムを明確に指定する文字列です。また、\<*port>* はパートナー サーバー インスタンスのミラーリング エンドポイントが使用するポート番号です。 詳細については、「 [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](specify-a-server-network-address-database-mirroring.md)を使用します。  
  
     たとえば、ミラーリング サーバー インスタンスで、次の ALTER DATABASE ステートメントは元のプリンシパル サーバー インスタンスとしてパートナーを設定します。 データベース名は **AdventureWorks**、システムのアドレスは DBSERVER1 (パートナーのシステム名)、パートナーのデータベース ミラーリング エンドポイントが使用するポートは 7022 です。  
  
    ```  
    ALTER DATABASE AdventureWorks   
       SET PARTNER = 'TCP://DBSERVER1:7022'  
    ```  
  
     このステートメントを実行すると、プリンシパル サーバーからの接続時にミラー サーバーにセッションを確立する準備が整います。  
  
5.  ミラー サーバーをプリンシパル データベースのパートナーとして設定するには、プリンシパル サーバーに接続し、次のステートメントを実行します。  
  
     ALTER DATABASE *<database_name>* SET PARTNER **=** _<server_network_address>_  
  
     詳細については、手順 4. を参照してください。  
  
     たとえば、プリンシパル サーバー インスタンスで、次の ALTER DATABASE ステートメントは元のミラー サーバー インスタンスとしてパートナーを設定します。 データベース名は **AdventureWorks**、システムのアドレスは DBSERVER2 (パートナーのシステム名)、パートナーのデータベースのミラーリング エンドポイントが使用するポートは 7025 です。  
  
    ```  
    ALTER DATABASE AdventureWorks SET PARTNER = 'TCP://DBSERVER2:7022'  
    ```  
  
     プリンシパル サーバーでこのステートメントを入力すると、データベース ミラーリング セッションが開始されます。  
  
6.  既定ではセッションでのトランザクションの安全性が "完全" に設定され (SAFETY が FULL に設定された状態)、同期セッションが自動フェールオーバーを伴わない高い安全性モードで開始されます。 セッションは、次のように自動フェールオーバーを伴う高い安全性モードか、非同期の高パフォーマンス モードで実行するように再構成できます。  
  
    -   **自動フェールオーバーを伴う高い安全性モード**  
  
         自動フェールオーバーをサポートするために高い安全性モードでセッションを実行する場合は、ミラーリング監視サーバー インスタンスを追加します。 詳細については、「[Windows 認証の使用によるデータベースのミラーリング監視の追加 &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)」を参照してください。  
  
    -   **高パフォーマンス モード**  
  
         自動フェールオーバーを行わず、高可用性よりパフォーマンスを重視する場合は、トランザクションの安全性を無効にします。 詳細については、｢[データベース ミラーリング セッションでのトランザクションの安全性の変更 &#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)」を参照してください。  
  
        > [!NOTE]  
        >  高パフォーマンス モードでは、WITNESS を OFF に設定してください。 詳細については、「[クォーラム: データベースの可用性にミラーリング監視サーバーが与える影響 &#40;データベース ミラーリング&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md)」を参照してください。  
  
## <a name="example"></a>例  
  
> [!NOTE]  
>  次の例では、既存のミラー データベースのためにパートナー間にデータベース ミラーリング セッションを確立します。 ミラー データベースを作成する方法の詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)」を参照してください。  
  
 ミラーリング監視サーバーを使用せずにデータベース ミラーリング セッションを作成するための基本的な手順を示します。 2 つのパートナーは、2 台のコンピューター システムにある既定のサーバー インスタンスです (PARTNERHOST1 および PARTNERHOST5)。 2 つのパートナー インスタンスは、同一の Windows ドメイン ユーザー アカウント (MYDOMAIN\dbousername) で実行されます。  
  
1.  プリンシパル サーバー インスタンス (PARTNERHOST1 の既定のインスタンス) で、ポート 7022 を使用するすべてのロールをサポートするエンドポイントを作成します。  
  
    ```  
    --create an endpoint for this instance  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    ```  
  
    > [!NOTE]  
    >  ログインをセットアップする方法の例は、「 [Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md)のすべてのエディションで使用できるわけではありません。  
  
2.  ミラー サーバー インスタンス (PARTNERHOST5 の既定のインスタンス) で、ポート 7022 を使用するすべてのロールをサポートするエンドポイントを作成します。  
  
    ```  
    --create an endpoint for this instance  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    ```  
  
3.  プリンシパル サーバー インスタンス (PARTNERHOST1) で、データベースをバックアップします。  
  
    ```  
    BACKUP DATABASE AdventureWorks   
        TO DISK = 'C:\AdvWorks_dbmirror.bak'   
        WITH FORMAT  
    GO  
    ```  
  
4.  ミラー サーバー インスタンス ( `PARTNERHOST5`) で、データベースを復元します。  
  
    ```  
    RESTORE DATABASE AdventureWorks   
        FROM DISK = 'Z:\AdvWorks_dbmirror.bak'   
        WITH NORECOVERY  
    GO  
    ```  
  
5.  完全データベース バックアップを作成した後、プリンシパル データベースでログ バックアップを作成する必要があります。 たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、前回の完全データベース バックアップで使用したものと同じファイルにログをバックアップします。  
  
    ```  
    BACKUP LOG AdventureWorks   
        TO DISK = 'C:\AdventureWorks.bak'   
    GO  
    ```  
  
6.  ミラーリングを開始する前に、必要なログ バックアップ (および、それ以降のログ バックアップ) を適用する必要があります。  
  
     たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは C:\AdventureWorks.bak から最初のログを復元します。  
  
    ```  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\ AdventureWorks.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  ミラー サーバー インスタンスで、PARTNERHOST1 のサーバー インスタンスをパートナーとして設定します (初期プリンシパル サーバーにします)。  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks   
        SET PARTNER =   
        'TCP://PARTNERHOST1:7022'  
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  既定でデータベース ミラーリング セッションは、トランザクションの安全性が「完全」に設定された (SAFETY が FULL に設定された) 状態の同期モードで実行されます。 セッションを非同期の高パフォーマンス モードで実行するには、SAFETY を OFF にします。 詳しくは、「 [Database Mirroring Operating Modes](database-mirroring-operating-modes.md)」をご覧ください。  
  
8.  プリンシパル サーバー インスタンスで、 `PARTNERHOST5` のサーバー インスタンスをパートナーとして設定します (初期ミラー サーバーにします)。  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://PARTNERHOST5:7022'  
    GO  
    ```  
  
9. 自動フェールオーバーを伴う高い安全性モードを使用する場合、必要に応じてミラーリング監視サーバー インスタンスを設定します。 詳細については、「[Windows 認証の使用によるデータベースのミラーリング監視の追加 &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  セキュリティの設定、ミラー データベースの準備、パートナーの設定、およびミラーリング監視サーバーの追加をすべて含む例については、「[データベース ミラーリングの設定 &#40;SQL Server&#41;](database-mirroring-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングの設定 &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md)   
 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [データベース ミラーリングとログ配布 &#40;SQL Server&#41;](database-mirroring-and-log-shipping-sql-server.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [データベース ミラーリングとレプリケーション &#40;SQL Server&#41;](database-mirroring-and-replication-sql-server.md)   
 [データベース ミラーリングの設定 &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](specify-a-server-network-address-database-mirroring.md)   
 [Database Mirroring Operating Modes](database-mirroring-operating-modes.md)  
  
  
