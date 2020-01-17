---
title: 例:証明書を使用したデータベース ミラーリング (T-SQL)
description: Transact-SQL を使用して証明書で SQL Server データベース ミラーリングを構成する例です。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: df489ecd-deee-465c-a26a-6d1bef6d7b66
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5e7c3a2fd690b7a19f7d94de7e8d4fbbd9cac355
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253593"
---
# <a name="example-setting-up-database-mirroring-using-certificates-transact-sql"></a>例:証明書を使用したデータベース ミラーリングの設定 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  この例では、証明書ベースの認証を使用してデータベース ミラーリング セッションを作成するために必要なすべての段階について説明します。 このトピックの例では、 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用します。 ネットワークがセキュリティで保護されていることを保証できる場合を除いて、データベース ミラーリング接続に対して暗号化を使用することをお勧めします。  
  
 証明書を別のシステムにコピーする場合は、セキュリティで保護されたコピー方法を使用してください。 すべての証明書をセキュリティで保護された状態で保管するよう十分に注意してください。  
  
##  <a name="ExampleH2"></a> 例  
 以下の例は、HOST_A に存在するパートナーで実行する必要のある処理を示しています。 この例では、2 つのパートナーが、3 つのコンピューター システムの既定のサーバー インスタンスです。 2 つのサーバー インスタンスは、信頼されていない Windows ドメインで実行されているため、証明書ベースの認証が必要です。  
  
 初期プリンシパル ロールは HOST_A によって取得され、ミラー ロールは HOST_B によって取得されます。  
  
 証明書を使用したデータベース ミラーリングの設定には、一般的な段階が 4 つあり、そのうちの 3 つの段階 (1、2、および 4) をこの例に示します。 これらの段階は次のとおりです。  
  
1.  [発信接続の構成](#ConfiguringOutboundConnections)  
  
     この例では次の手順を示します。  
  
    1.  発信接続用の Host_A の構成。  
  
    2.  発信接続用の Host_B の構成。  
  
     データベース ミラーリングの設定のこの段階の詳細については、「 [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)を使用します。  
  
2.  [着信接続の構成](#ConfigureInboundConnections)  
  
     この例では次の手順を示します。  
  
    1.  着信接続用の Host_A の構成。  
  
    2.  着信接続用の Host_B の構成。  
  
     データベース ミラーリングの設定のこの段階の詳細については、「 [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)を使用します。  
  
3.  ミラー データベースの作成  
  
     ミラー データベースを作成する方法の詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)を使用します。  
  
4.  [ミラーリング パートナーの構成](#ConfigureMirroringPartners)  
  
###  <a name="ConfiguringOutboundConnections"></a> 発信接続の構成  
 **発信接続用に Host_A を構成するには**  
  
1.  master データベースで、必要な場合はデータベース マスター キーを作成します。  
  
    ```  
    USE master;  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<1_Strong_Password!>';  
    GO  
    ```  
  
2.  このサーバー インスタンスに対する証明書を作成します。  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_A_cert   
       WITH SUBJECT = 'HOST_A certificate';  
    GO  
    ```  
  
3.  作成した証明書を使用して、サーバー インスタンスのミラーリング エンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_A_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
4.  HOST_A の証明書をバックアップし、他のシステム HOST_B にコピーします。  
  
    ```  
    BACKUP CERTIFICATE HOST_A_cert TO FILE = 'C:\HOST_A_cert.cer';  
    GO  
    ```  
  
5.  安全なコピー方法を使用して、C:\HOST_A_cert.cer を HOST_B にコピーします。  
  
 **発信接続用に Host_B を構成するには**  
  
1.  master データベースで、必要な場合はデータベース マスター キーを作成します。  
  
    ```  
    USE master;  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Strong_Password_#2>';  
    GO  
    ```  
  
2.  HOST_B サーバー インスタンスで証明書を作成します。  
  
    ```  
    CREATE CERTIFICATE HOST_B_cert   
       WITH SUBJECT = 'HOST_B certificate for database mirroring';  
    GO  
    ```  
  
3.  HOST_B のサーバー インスタンスに対するミラーリング エンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_B_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
4.  HOST_B の証明書をバックアップします。  
  
    ```  
    BACKUP CERTIFICATE HOST_B_cert TO FILE = 'C:\HOST_B_cert.cer';  
    GO   
    ```  
  
5.  安全なコピー方法を使用して、C:\HOST_B_cert.cer を HOST_A にコピーします。  
  
 詳細については、「 [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)を使用します。  
  
 [&#91;例の先頭に戻る&#93;](#ExampleH2)  
  
###  <a name="ConfigureInboundConnections"></a> 着信接続の構成  
 **着信接続用に Host_A を構成するには**  
  
1.  HOST_B に対するログインを HOST_A に作成します。  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_B_login WITH PASSWORD = '1Sample_Strong_Password!@#';  
    GO  
    ```  
  
2.  そのログインのユーザー名を作成します。  
  
    ```  
    CREATE USER HOST_B_user FOR LOGIN HOST_B_login;  
    GO  
    ```  
  
3.  証明書をユーザーと関連付けます。  
  
    ```  
    CREATE CERTIFICATE HOST_B_cert  
       AUTHORIZATION HOST_B_user  
       FROM FILE = 'C:\HOST_B_cert.cer'  
    GO  
    ```  
  
4.  リモート ミラーリング エンドポイント用のログインに CONNECT 権限を許可します。  
  
    ```  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_B_login];  
    GO  
    ```  
  
 **着信接続用に Host_B を構成するには**  
  
1.  HOST_A に対するログインを HOST_B に作成します。  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_A_login WITH PASSWORD = '=Sample#2_Strong_Password2';  
    GO  
    ```  
  
2.  そのログインのユーザー名を作成します。  
  
    ```  
    CREATE USER HOST_A_user FOR LOGIN HOST_A_login;  
    GO  
    ```  
  
3.  証明書をユーザーと関連付けます。  
  
    ```  
    CREATE CERTIFICATE HOST_A_cert  
       AUTHORIZATION HOST_A_user  
       FROM FILE = 'C:\HOST_A_cert.cer'  
    GO  
    ```  
  
4.  リモート ミラーリング エンドポイント用のログインに CONNECT 権限を許可します。  
  
    ```  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_A_login];  
    GO  
    ```  
  
> [!IMPORTANT]  
>  自動フェールオーバーを伴う高い安全性モードで実行する場合、発信接続と着信接続の両方で、ミラーリング監視サーバーを構成する同じ手順を繰り返す必要があります。 ミラーリング監視サーバーを利用する着信接続を設定する場合は、両方のパートナーでミラーリング監視サーバー用にログインとユーザーを設定し、ミラーリング監視サーバーで両方のパートナー用にログインとユーザーを設定する必要があります。  
  
 詳細については、「 [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)を使用します。  
  
 [&#91;例の先頭に戻る&#93;](#ExampleH2)  
  
### <a name="creating-the-mirror-database"></a>ミラー データベースの作成  
 ミラー データベースを作成する方法の詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)を使用します。  
  
###  <a name="ConfigureMirroringPartners"></a> ミラーリング パートナーの構成  
  
1.  HOST_B のミラー サーバー インスタンスで、HOST_A のサーバー インスタンスをパートナー (最初のプリンシパル サーバー インスタンス) として設定します。 `TCP://HOST_A.Mydomain.Corp.Adventure-Works``.com:7024`の部分を有効なネットワーク アドレスに置き換えます。 詳細については、「 [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)を使用します。  
  
    ```  
    --At HOST_B, set server instance on HOST_A as partner (principal server):  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://HOST_A.Mydomain.Corp.Adventure-Works.com:7024';  
    GO  
    ```  
  
2.  HOST_A のプリンシパル サーバー インスタンスで、HOST_B のサーバー インスタンスをパートナー (最初のミラー サーバー インスタンス) として設定します。 `TCP://HOST_B.Mydomain.Corp.Adventure-Works.com:7024`の部分を有効なネットワーク アドレスに置き換えます。  
  
    ```  
    --At HOST_A, set server instance on HOST_B as partner (mirror server).  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://HOST_B.Mydomain.Corp.Adventure-Works.com:7024';  
    GO  
    ```  
  
3.  この例では、セッションが高パフォーマンス モードで実行されると仮定します。 このセッションの実行モードを高パフォーマンス モードに構成するには、HOST_A のプリンシパル サーバー インスタンスでトランザクションの安全性を OFF に設定します。  
  
    ```  
    --Change to high-performance mode by turning off transacton safety.  
    ALTER DATABASE AdventureWorks   
        SET PARTNER SAFETY OFF  
    GO  
    ```  
  
    > [!NOTE]  
    >  自動フェールオーバーを伴う高い安全性モードで実行する場合は、トランザクションの安全性を FULL (既定の設定) のままにし、2 番目の SET PARTNER **'** _partner_server_ **'** ステートメントの実行後、できる限り早い段階でミラーリング監視サーバーを追加します。 ただし、まずミラーリング監視サーバーが発信接続と着信接続用に構成されている必要があります。  
  
 [&#91;例の先頭に戻る&#93;](#ExampleH2)  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [役割の交代後のログインとジョブの管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
-   [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md) (SQL Server)  
  
-   [データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングと Always On 可用性グループのトランスポート セキュリティ &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
