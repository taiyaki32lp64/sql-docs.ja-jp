---
title: データベース ミラーリング構成のトラブルシューティング (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- endpoints [SQL Server], database mirroring
- database mirroring [SQL Server], troubleshooting
- troubleshooting [SQL Server], database mirroring
ms.assetid: 87d3801b-dc52-419e-9316-8b1f1490946c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b99fb881fc6bf09aa848bd41a42f8254e5f3acd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754210"
---
# <a name="troubleshoot-database-mirroring-configuration-sql-server"></a>データベース ミラーリング構成のトラブルシューティング (SQL Server)
  ここでは、データベース ミラーリング セッションの設定時に発生する問題のトラブルシューティングに役立つ情報を提供します。  
  
> [!NOTE]  
>  [データベース ミラーリングの前提条件](prerequisites-restrictions-and-recommendations-for-database-mirroring.md)をすべて満たす必要があります。  
  
|問題点|まとめ|  
|-----------|-------------|  
|エラー メッセージ 1418|この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メッセージは、サーバー ネットワーク アドレスに到達できないか、そのアドレスが存在しないことを意味し、ネットワーク アドレス名を確認してコマンドを再実行するように示しています。 詳細については、「 [MSSQLSERVER_1418](../../relational-databases/errors-events/mssqlserver-1418-database-engine-error.md) 」を参照してください。|  
|[Accounts](#Accounts)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているアカウントを適切に構成するための要件について説明します。|  
|[エンドポイント](#Endpoints)|各サーバー インスタンスのデータベース ミラーリング エンドポイントを適切に構成するための要件について説明します。|  
|[システム アドレス](#SystemAddress)|データベース ミラーリング構成でサーバー インスタンスのシステム名を指定するためのその他の方法について概要を説明します。|  
|[ネットワーク アクセス](#NetworkAccess)|各サーバー インスタンスが他のサーバー インスタンスのポートに TCP 経由でアクセスできるという要件について説明します。|  
|[ミラー データベースの準備](#MirrorDbPrep)|ミラーリングを開始できるようにミラー データベースを準備する際の要件について概要を説明します。|  
|[失敗したファイル作成操作](#FailedCreateFileOp)|失敗したファイル作成操作の対処方法について説明します。|  
|[Transact-SQL を使用したミラーリングの開始](#StartDbm)|ALTER DATABASE *database_name* SET PARTNER **='***partner_server***'** ステートメントを実行する際に必要な順序について説明します。|  
|[複数データベースにまたがるトランザクション](#CrossDbTxns)|自動フェールオーバーにより、状態が不明なトランザクションが自動的に解決されることがあります。ただし、この解決は不適切な場合があります。 このため、データベース ミラーリングでは複数データベースにまたがるトランザクションをサポートしていません。|  
  
##  <a name="Accounts"></a> Accounts  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の実行に使用するアカウントは、正しく構成されている必要があります。  
  
1.  アカウントに適切な権限が与えられていることを確認します。  
  
    1.  アカウントが同じドメインで実行されている場合、アカウントの構成が不適切になる可能性は低くなります。  
  
    2.  アカウントが別のドメインで実行されているか、またはドメイン アカウントではない場合、もう一方のコンピューターの **master** データベースにアカウントのログインを作成する必要があります。また、そのログインには、エンドポイントに対して CONNECT 権限を与える必要があります。 詳細については、「 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)」を参照してください。 これには、ネットワーク サービス アカウントも含まれます。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がローカル システム アカウントを使用しているサービスとして実行されている場合、認証には証明書を使用する必要があります。 詳細については、「[データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)」を参照してください。  
  
##  <a name="Endpoints"></a> エンドポイント  
 エンドポイントが正しく構成されている必要があります。  
  
1.  各サーバー インスタンス (プリンシパル サーバー、ミラー サーバー、およびミラーリング監視サーバー (存在する場合)) にデータベース ミラーリング エンドポイントがあることを確認します。 詳細については、「[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)」、および、認証形式によって、「[Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)」もしくは「[データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)」のいずれかを参照してください。  
  
2.  ポート番号が適切であることを確認します。  
  
     サーバー インスタンスのデータベース ミラーリング エンドポイントに現在関連付けられているポートを識別するには、 [sys.database_mirroring_endpoints](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql) カタログ ビューおよび [sys.tcp_endpoints](/sql/relational-databases/system-catalog-views/sys-tcp-endpoints-transact-sql) カタログ ビューを使用します。  
  
3.  説明が困難なデータベース ミラーリングのセットアップに関する問題については、各サーバー インスタンスを調査して、それぞれが正しいポートでリッスンしているかどうかを確認することをお勧めします。 ポートの可用性の検証については、「 [MSSQLSERVER_1418](../../relational-databases/errors-events/mssqlserver-1418-database-engine-error.md)」を参照してください。  
  
4.  エンドポイントが開始されていること (STATE = STARTED) を確認します。 各サーバー インスタンスで、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    SELECT state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
     **state_desc** 列の詳細については、「[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)」を参照してください。  
  
     エンドポイントを開始するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    ALTER ENDPOINT Endpoint_Mirroring   
    STATE = STARTED   
    AS TCP (LISTENER_PORT = <port_number>)  
    FOR database_mirroring (ROLE = ALL);  
    GO  
    ```  
  
     詳細については、「 [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)」を参照してください。  
  
5.  ROLE の設定が正しいことを確認します。 各サーバー インスタンスで、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    SELECT role FROM sys.database_mirroring_endpoints;  
    GO  
    ```  
  
     詳細については、「[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)」を参照してください。  
  
6.  他のサーバー インスタンスからサービス アカウントにログインするには、CONNECT 権限が必要です。 他のサーバーからのログインに、CONNECT 権限があることを確認します。 あるエンドポイントに対して CONNECT 権限のあるユーザーを確認するには、各サーバー インスタンスで、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    SELECT 'Metadata Check';  
    SELECT EP.name, SP.STATE,   
       CONVERT(nvarchar(38), suser_name(SP.grantor_principal_id))   
          AS GRANTOR,   
       SP.TYPE AS PERMISSION,  
       CONVERT(nvarchar(46),suser_name(SP.grantee_principal_id))   
          AS GRANTEE   
       FROM sys.server_permissions SP , sys.endpoints EP  
       WHERE SP.major_id = EP.endpoint_id  
       ORDER BY Permission,grantor, grantee;   
    GO  
  
    ```  
  
##  <a name="SystemAddress"></a> システム アドレス  
 データベース ミラーリング構成におけるサーバー インスタンスのシステム名には、システムを明確に識別できる任意の名前を使用できます。 サーバー アドレスには、システム名 (システムが同じドメインに存在する場合)、完全修飾ドメイン名、または IP アドレス (可能であれば静的 IP アドレス) を使用できます。 完全修飾ドメイン名を使用すると動作が保証されます。 詳細については、「[サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](specify-a-server-network-address-database-mirroring.md)」を参照してください。  
  
##  <a name="NetworkAccess"></a> Network Access  
 各サーバー インスタンスは、他のサーバー インスタンスのポートに TCP 経由でアクセスできる必要があります。 これは、サーバー インスタンスが相互に信頼関係を持たない別のドメイン (信頼されていないドメイン) に存在する場合に特に重要になります。 このような状況では、サーバー インスタンス間の通信の大半が制限されます。  
  
##  <a name="MirrorDbPrep"></a> Mirror Database Preparation  
 ミラーリングを初めて開始する場合も、ミラーリングを削除した後に再度開始する場合も、ミラー データベースがミラーリング用に準備されていることを確認します。  
  
 ミラー サーバーにミラー データベースを作成する際には、同じデータベース名と WITH NORECOVERY オプションを指定して、プリンシパル データベースのバックアップを復元する必要があります。 また、このバックアップが実行された後で作成されたすべてのログ バックアップについても、WITH NORECOVERY を指定して適用する必要があります。  
  
 また、可能であれば、ミラー データベースのファイル パス (ドライブ文字を含む) を、プリンシパル データベースと同一のパスにすることが推奨されています。 ファイルのパスが異なる場合、たとえば、プリンシパル データベースが "F:" ドライブに存在する一方で、ミラー システムに "F:" ドライブがない場合には、RESTORE ステートメントに MOVE オプションを含める必要があります。  
  
> [!IMPORTANT]  
>  ミラー データベースの作成時にデータベース ファイルを移動した場合、そのミラー データベースに後でファイルを追加する際に、ミラーリングの中断が必要になる場合があります。  
  
 データベース ミラーリングが停止している場合にミラーリングを再開するには、停止後にプリンシパル データベースで作成されたすべてのログ バックアップをミラー データベースに適用する必要があります。  
  
 詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)」を参照してください。  
  
##  <a name="FailedCreateFileOp"></a> Failed Create-File Operation  
 ミラーリング セッションに影響を与えずにファイルを追加するには、追加するファイルのパスが両方のサーバーに存在する必要があります。 したがって、ミラー データベースの作成時にデータベース ファイルを移動し、その後でミラー データベースにファイルを追加しようとした場合、ファイルの追加操作が失敗し、ミラーリングが中断されることがあります。  
  
 この問題を解決するには、データベース所有者が次の操作を行う必要があります。  
  
1.  ミラーリング セッションを削除し、追加されたファイルを含むファイル グループの完全バックアップを復元します。  
  
2.  次に、ファイルを追加する操作を含むログをプリンシパル サーバーでバックアップし、WITH NORECOVERY オプションと WITH MOVE オプションを使用して、そのログ バックアップをミラー データベースに手動で復元します。 この操作を行うと、指定したファイル パスがミラー サーバーに作成され、その場所に新しいファイルが復元されます。  
  
3.  新しいミラーリング セッションのためにデータベースを準備するには、WITH NORECOVERY オプションを使用して、プリンシパル サーバーでバックアップした他の未処理のログをすべて復元する必要もあります。  
  
 詳細については、「[データベース ミラーリングの削除 &#40;SQL Server&#41;](database-mirroring-sql-server.md)」、「[ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)」、「[Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)」、「[データベース ミラーリング エンドポイントでの証明書の使用&#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)」、「[Windows 認証を使用してデータベース ミラーリング セッションを確立する方法 &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)」のいずれかを参照してください。  
  
##  <a name="StartDbm"></a> Transact-SQL を使用したミラーリングの開始  
 ALTER DATABASE *database_name* SET PARTNER **='***partner_server***'** ステートメントを実行する際は、順序が非常に重要です。  
  
1.  最初のステートメントは、ミラー サーバーで実行する必要があります。 このステートメントの実行時に、ミラー サーバーでは他のサーバー インスタンスへの接続は試行されません。 ミラー サーバーは自身のデータベースに対し、プリンシパル サーバーからそのミラー サーバーへの接続が行われるまで待機するように指示します。  
  
2.  2 番目の ALTER DATABASE ステートメントはプリンシパル サーバーで実行する必要があります。 このステートメントにより、プリンシパル サーバーはミラー サーバーへの接続を試みます。 この接続が確立されると、ミラー サーバーは、さらに別の接続でプリンシパル サーバーへの接続を試みます。  
  
 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してミラーリングを開始する方法の詳細については、「[Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)」を参照してください。  
  
##  <a name="CrossDbTxns"></a> 複数データベースにまたがるトランザクション  
 データベースが自動フェールオーバーを伴う高い安全性モードでミラー化されている場合、自動フェールオーバーにより、状態が不明なトランザクションが自動的に解決されることがあります。ただし、この解決は不適切な場合があります。 複数データベースにまたがるトランザクションがコミットされているときに、いずれかのデータベースで自動フェールオーバーが発生すると、データベース間で論理的な不一致が発生することがあります。  
  
 自動フェールオーバーの影響を受ける可能性がある、複数データベースにまたがるトランザクションには、次の種類があります。  
  
-   同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスで複数のデータベースを更新するトランザクション。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) を使用するトランザクション。  
  
 詳細については、「[データベース ミラーリングまたは AlwaysOn 可用性グループではサポートされない複数データベースにまたがるトランザクション &#40;SQL Server&#41;](../availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングの設定 &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md)   
 [データベース ミラーリングと AlwaysOn 可用性グループのトランスポート セキュリティ&#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)  
  
  
