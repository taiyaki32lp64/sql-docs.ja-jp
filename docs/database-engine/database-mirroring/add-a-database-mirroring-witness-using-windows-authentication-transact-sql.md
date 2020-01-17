---
title: ミラーリング監視の構成
description: 'Transact-SQL を使用して Windows 認証でデータベース ミラーリング監視を構成する方法について説明します。 '
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], establishing
- Windows authentication [SQL Server]
- database mirroring [SQL Server], witness
ms.assetid: bf5e87df-91a4-49f9-ae88-2a6dcf644510
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4616e2c10657e1af8db9c706c518fdf690618303
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822299"
---
# <a name="add-a-database-mirroring-witness-using-windows-authentication-transact-sql"></a>Windows 認証の使用によるデータベースのミラーリング監視の追加 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  データベースのミラーリング監視を設定するには、データベース所有者が、データベース エンジンのインスタンスをミラーリング監視サーバーの役割に割り当てます。 ミラーリング監視サーバーのインスタンスは、プリンシパル サーバーまたはミラー サーバーのインスタンスと同じコンピューターで実行できますが、このようにすると、自動フェールオーバーの堅牢性が大幅に低下します。  
  
 ミラーリング監視は独立したコンピューターに常駐させることを強くお勧めします。 特定のサーバーを、同じパートナーまたは別のパートナーを含む複数の同時実行データベース ミラーリング セッションに参加させることができます。 また、特定のサーバーを、あるセッションではパートナーとし、別のセッションではミラーリング監視にすることができます。  
  
 ミラーリング監視は、自動フェールオーバーを伴う高い安全性モードでの使用だけが想定されています。 ミラーリング監視を設定する前に、SAFETY プロパティが現在 FULL に設定されていることを確認するよう強くお勧めします。  
  
> [!IMPORTANT]  
>  構成はパフォーマンスに影響する場合があるので、データベース ミラーリングの構成はピーク タイム以外の時間に行うことをお勧めします。  
  
## <a name="establish-a-witness"></a>ミラーリング監視サーバーの確立  
  
1.  ミラーリング監視サーバーのインスタンスで、データベース ミラーリングのエンドポイントが存在することを確認します。 サポートされるミラーリング セッションの数に関係なく、サーバー インスタンスにはデータベース ミラーリング エンドポイントが 1 つだけ存在する必要があります。 このサーバー インスタンスをデータベース ミラーリング セッションのミラーリング監視専用に使用する場合、ミラーリング監視の役割をエンドポイントに割り当てます (ROLE **=** WITNESS)。 このサーバー インスタンスを 1 つ以上の他のデータベース ミラーリング セッションのパートナーとして使用する場合、エンドポイントの役割を ALL に割り当てます。  
  
     SET WITNESS ステートメントを実行するには、データベース ミラーリング セッションが (パートナー間で) 既に開始されていて、ミラーリング監視のエンドポイントの STATE が STARTED に設定されている必要があります。  
  
     ミラーリング監視サーバーのインスタンスにデータベース ミラーリング エンドポイントがあるかどうかを把握し、そのエンドポイントの役割と状態を把握するには、インスタンスで次の Transact-SQL ステートメントを使用します。  
  
    ```  
    SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
    > [!IMPORTANT]  
    >  データベース ミラーリング エンドポイントが存在し、既に使用されている場合、サーバー インスタンスのすべてのセッションでそのエンドポイントを使用することをお勧めします。 使用中のエンドポイントを削除すると、既存のセッションの接続が切断されます。 セッションにミラーリング監視サーバーが設定されている場合、データベース ミラーリングのエンドポイントを削除すると、そのセッションのプリンシパル サーバーがクォーラムを失う可能性があります。プリンシパル サーバーがクォーラムを失うと、データベースがオフラインになりユーザー接続が切断されます。 詳細については、「[クォーラム: データベースの可用性にミラーリング監視サーバーが与える影響 (データベース ミラーリング)](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)」を参照してください。  
  
     ミラーリング監視にエンドポイントが存在しない場合は、「[Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)」を参照してください。  
  
2.  パートナー インスタンスが異なるドメイン ユーザー アカウントで実行されている場合、各インスタンスの master データベースに別のアカウントのログインを作成します。 詳細については、「 [Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)」を参照してください。  
  
3.  プリンシパル サーバーに接続し、次のステートメントを実行します。  
  
     ALTER DATABASE *<database_name>* SET WITNESS **=** _<server_network_address>_  
  
     *<database_name>* はミラー化するデータベースの名前 (両方のパートナーで同一の名前にします)、 *<server_network_address>* はミラーリング監視サーバー インスタンスのサーバー ネットワーク アドレスです。  
  
     サーバー ネットワーク アドレスの構文は次のとおりです。  
  
     TCP<b>://</b> _\<system-address>_ <b>:</b> _\<port>_  
  
     \<*system-address*> は目的のコンピューター システムを明確に指定する文字列です。また、\<*port>* はパートナー サーバー インスタンスのミラーリング エンドポイントが使用するポート番号です。 詳細については、「 [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)を使用します。  
  
     たとえば、プリンシパル サーバー インスタンスでは、次の ALTER DATABASE ステートメントでミラーリング監視を設定します。 データベース名は **AdventureWorks**、システム アドレスは DBSERVER3 (ミラーリング監視システムの名前)、ミラーリング監視のデータベース ミラーリング エンドポイントが使用するポートは `7022` です。  
  
    ```  
    ALTER DATABASE AdventureWorks   
      SET WITNESS = 'TCP://DBSERVER3:7022'  
    ```  
  
## <a name="example"></a>例  
 次の例では、データのミラーリング監視を確立します。 ミラーリング監視サーバー インスタンス ( `WITNESSHOST4`の既定のインスタンス) で、次の手順を実行します。  
  
1.  `7022`を使用する WITNESS の役割だけにこのサーバー インスタンスのエンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=WITNESS)  
    GO  
    ```  
  
2.  パートナー インスタンスのドメイン ユーザー アカウントが異なる場合は、そのログインを作成します。たとえば、ミラーリング監視サーバーが `SOMEDOMAIN\witnessuser`で実行されていて、パートナーが `MYDOMAIN\dbousername`で実行されている場合などです。 パートナーのログインを作成するには、以下のステートメントを実行します。  
  
    ```  
    --Create a login for the partner server instances,  
    --which are both running as MYDOMAIN\dbousername:  
    USE master ;  
    GO  
    CREATE LOGIN [MYDOMAIN\dbousername] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account   
    --of partners  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [MYDOMAIN\dbousername];  
    GO  
    ```  
  
3.  各パートナー サーバー インスタンスで、ミラーリング監視サーバー インスタンスのログインを作成します。  
  
    ```  
    --Create a login for the witness server instance,  
    --which is running as SOMEDOMAIN\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [SOMEDOMAIN\witnessuser] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account   
    --of partners  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [SOMEDOMAIN\witnessuser];  
    GO  
    ```  
  
4.  プリンシパル サーバーで、ミラーリング監視サーバー ( `WITNESSHOST4`) を設定します。  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET WITNESS =   
        'TCP://WITNESSHOST4:7022'  
    GO  
    ```  
  
> [!NOTE]  
>  サーバー ネットワーク アドレスはターゲット サーバー インスタンスを、インスタンスのミラーリング エンドポイントにマップされるポート番号で示します。  
  
 セキュリティの設定、ミラー データベースの準備、パートナーの設定、およびミラーリング監視サーバーの追加をすべて含む例については、「[データベース ミラーリングの設定 &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)   
 [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Windows 認証を使用してデータベース ミラーリング セッションを確立する方法 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)   
 [データベース ミラーリング セッションからのミラーリング監視サーバーの削除 &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)   
 [データベース ミラーリング監視サーバー](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
