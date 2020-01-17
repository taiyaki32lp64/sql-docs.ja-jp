---
title: 着信接続に証明書を使用する
description: データベース ミラーリングの着信接続を認証する際に証明書を使用するようにサーバー インスタンスを構成する手順について説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- certificates [SQL Server], database mirroring
- inbound connections
- database mirroring [SQL Server], security
ms.assetid: 5d48bb98-61f0-4b99-8f1a-b53f831d63d0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 145c182323d3de702ce1e7d4bfcc4e966c5928c2
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822271"
---
# <a name="database-mirroring---use-certificates-for-inbound-connections"></a>データベース ミラーリング - 着信接続に証明書を使用する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、データベース ミラーリングの着信接続を認証する際に証明書を使用するようにサーバー インスタンスを構成する手順について説明します。 着信接続を設定する前に、各サーバー インスタンスで発信接続を構成する必要があります。 詳細については、「 [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)を使用します。  
  
 着信接続を構成する処理には、次の一般的な手順が含まれます。  
  
1.  他のシステムへのログインを作成します。  
  
2.  そのログインのユーザー名を作成します。  
  
3.  他のサーバー インスタンスのミラーリング エンドポイント用の証明書を入手します。  
  
4.  手順 2. で作成したユーザーに証明書を関連付けます。  
  
5.  ミラーリング エンドポイント用のログインに CONNECT 権限を許可します。  
  
 ミラーリング監視サーバーがある場合は、このサーバーでも着信接続の構成を行う必要があります。 この場合、どちらのパートナーのミラーリング監視サーバーでも、相手のログイン、ユーザー、証明書が必要です。  
  
 次の手順では、上記の手順について詳しく説明します。 各手順では、HOST_A という名前のシステムでサーバー インスタンスを構成するための例を示します。 その後に続く「例」では、HOST_B という名前のシステム上の別のサーバー インスタンスに対する同じ手順について説明します。  
  
### <a name="to-configure-server-instances-for-inbound-mirroring-connections-on-host_a"></a>ミラーリングの着信接続用に (HOST_A 上で) サーバー インスタンスを構成するには  
  
1.  他のシステムへのログインを作成します。  
  
     次の例では、システム HOST_B のログインを HOST_A のサーバー インスタンスの **master** データベースに作成します。この例では、このログインに `HOST_B_login`という名前が付けられています。 サンプルのパスワードは、独自のパスワードに置き換えてください。  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_B_login   
       WITH PASSWORD = '1Sample_Strong_Password!@#';  
    GO  
    ```  
  
     詳細については、「[CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)」を参照してください。  
  
     このサーバー インスタンスのログインを表示するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用できます。  
  
    ```  
    SELECT * FROM sys.server_principals  
    ```  
  
     詳細については、「[sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)」を参照してください。  
  
2.  そのログインのユーザー名を作成します。  
  
     次の例では、上記の手順で作成したログイン用のユーザー `HOST_B_user` を作成します。  
  
    ```  
    USE master;  
    CREATE USER HOST_B_user FOR LOGIN HOST_B_login;  
    GO  
    ```  
  
     詳細については、「[CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)」を参照してください。  
  
     このサーバー インスタンスのユーザーを表示するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用できます。  
  
    ```  
    SELECT * FROM sys.sysusers;  
    ```  
  
     詳細については、「[sys.sysusers &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md)」を参照してください。  
  
3.  他のサーバー インスタンスのミラーリング エンドポイント用の証明書を入手します。  
  
     発信接続の構成時にリモート サーバー インスタンスのミラーリング エンドポイント用の証明書のコピーを入手していない場合は、これを入手します。 これを行うには、「[データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)」の説明に従って、そのサーバー インスタンスの証明書をバックアップします。 証明書を別のシステムにコピーする場合は、セキュリティで保護されたコピー方法を使用してください。 すべての証明書をセキュリティで保護された状態で保管するよう十分に注意してください。  
  
     詳細については、「[BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)」を参照してください。  
  
4.  手順 2. で作成したユーザーに証明書を関連付けます。  
  
     次の例では、HOST_B の証明書と HOST_B のユーザーを HOST_A で関連付けています。  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_B_cert  
       AUTHORIZATION HOST_B_user  
       FROM FILE = 'C:\HOST_B_cert.cer'  
    GO  
    ```  
  
     詳細については、「[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)」を参照してください。  
  
     このサーバー インスタンスの証明書を表示するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    SELECT * FROM sys.certificates  
    ```  
  
     詳細については、「[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)」を参照してください。  
  
5.  リモート ミラーリング エンドポイント用のログインに CONNECT 権限を許可します。  
  
     たとえば、HOST_A に対する権限を HOST_B 上のリモート サーバー インスタンスに許可し、このローカル ログインに接続 (つまり、`HOST_B_login` に接続) するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    USE master;  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_B_login];  
    GO  
    ```  
  
     詳細については、「 [GRANT (エンドポイントの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)」を参照してください。  
  
 これで、HOST_A にログインするための HOST_B の証明書認証の設定が完了します。  
  
 ここで、HOST_B で HOST_A 用の着信接続を構成するために同じ手順を実行する必要があります。 この手順については、次の「例」のサンプル コードで着信接続の設定部分を参照してください。  
  
## <a name="example"></a>例  
 次の例では、HOST_B の着信接続を構成する方法について示します。  
  
> [!NOTE]  
>  この例では、「[データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)」のコード スニペットによって作成される HOST_A 証明書を含む証明書ファイルを使用します。  
  
```  
USE master;  
--On HOST_B, create a login for HOST_A.  
CREATE LOGIN HOST_A_login WITH PASSWORD = 'AStrongPassword!@#';  
GO  
--Create a user, HOST_A_user, for that login.  
CREATE USER HOST_A_user FOR LOGIN HOST_A_login  
GO  
--Obtain HOST_A certificate. (See the note   
--   preceding this example.)  
--Asscociate this certificate with the user, HOST_A_user.  
CREATE CERTIFICATE HOST_A_cert  
   AUTHORIZATION HOST_A_user  
   FROM FILE = 'C:\HOST_A_cert.cer';  
GO  
--Grant CONNECT permission for the server instance on HOST_A.  
GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO HOST_A_login  
GO  
```  
  
 自動フェールオーバーを伴う高い安全性モードで実行する場合、発信接続と着信接続の両方に対応するようミラーリング監視サーバーを構成する手順を繰り返す必要があります。  
  
 Transact-SQL の例を含む、ミラー データベースを作成する方法の詳細については、「[ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)」を参照してください。  
  
 高パフォーマンス モードのセッションを確立する Transact-SQL の例については、「[証明書を使用したデータベース ミラーリングの設定の例 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)」を参照してください。  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
 証明書を別のシステムにコピーする場合は、セキュリティで保護されたコピー方法を使用してください。 すべての証明書をセキュリティで保護された状態で保管するよう十分に注意してください。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングと Always On 可用性グループのトランスポート セキュリティ &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [GRANT (エンドポイントのアクセス許可の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [暗号化されたミラー データベースの設定](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
