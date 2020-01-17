---
title: データベース ミラーリング エンドポイントで着信接続 (Transact SQL) の証明書の使用を許可する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 3f70ddfc241a902a59dff989323a75b17f7af55e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807561"
---
# <a name="allow-a-database-mirroring-endpoint-to-use-certificates-for-inbound-connections-transact-sql"></a>データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする (Transact-SQL)
  このトピックでは、データベース ミラーリングの着信接続を認証する際に証明書を使用するようにサーバー インスタンスを構成する手順について説明します。 着信接続を設定する前に、各サーバー インスタンスで発信接続を構成する必要があります。 詳細については、「[データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)」を参照してください。  
  
 着信接続を構成する処理には、次の一般的な手順が含まれます。  
  
1.  他のシステムへのログインを作成します。  
  
2.  そのログインのユーザー名を作成します。  
  
3.  他のサーバー インスタンスのミラーリング エンドポイント用の証明書を入手します。  
  
4.  手順 2. で作成したユーザーに証明書を関連付けます。  
  
5.  ミラーリング エンドポイント用のログインに CONNECT 権限を許可します。  
  
 ミラーリング監視サーバーがある場合は、このサーバーでも着信接続の構成を行う必要があります。 この場合、どちらのパートナーのミラーリング監視サーバーでも、相手のログイン、ユーザー、証明書が必要です。  
  
 次の手順では、上記の手順について詳しく説明します。 各手順では、HOST_A という名前のシステムでサーバー インスタンスを構成するための例を示します。 その後に続く「例」では、HOST_B という名前のシステム上の別のサーバー インスタンスに対する同じ手順について説明します。  
  
### <a name="to-configure-server-instances-for-inbound-mirroring-connections-on-hosta"></a>ミラーリングの着信接続用に (HOST_A 上で) サーバー インスタンスを構成するには  
  
1.  他のシステムへのログインを作成します。  
  
     次の例では、システム HOST_B のログインを HOST_A のサーバー インスタンスの **master** データベースに作成します。この例では、このログインに `HOST_B_login`という名前が付けられています。 サンプルのパスワードは、独自のパスワードに置き換えてください。  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_B_login   
       WITH PASSWORD = '1Sample_Strong_Password!@#';  
    GO  
    ```  
  
     詳細については、「[CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)」を参照してください。  
  
     このサーバー インスタンスのログインを表示するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用できます。  
  
    ```  
    SELECT * FROM sys.server_principals  
    ```  
  
     詳細については、「[sys.server_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)」を参照してください。  
  
2.  そのログインのユーザー名を作成します。  
  
     次の例では、上記の手順で作成したログイン用のユーザー `HOST_B_user` を作成します。  
  
    ```  
    USE master;  
    CREATE USER HOST_B_user FOR LOGIN HOST_B_login;  
    GO  
    ```  
  
     詳細については、「[CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)」を参照してください。  
  
     このサーバー インスタンスのユーザーを表示するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用できます。  
  
    ```  
    SELECT * FROM sys.sysusers;  
    ```  
  
     詳細については、「[sys.sysusers &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysusers-transact-sql)」を参照してください。  
  
3.  他のサーバー インスタンスのミラーリング エンドポイント用の証明書を入手します。  
  
     発信接続の構成時にリモート サーバー インスタンスのミラーリング エンドポイント用の証明書のコピーを入手していない場合は、これを入手します。 これを行うには、「[データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする&#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)」の説明に従って、そのサーバー インスタンスの証明書をバックアップします。 証明書を別のシステムにコピーする場合は、セキュリティで保護されたコピー方法を使用してください。 すべての証明書をセキュリティで保護された状態で保管するよう十分に注意してください。  
  
     詳細については、「[BACKUP CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)」を参照してください。  
  
4.  手順 2. で作成したユーザーに証明書を関連付けます。  
  
     次の例では、HOST_B の証明書と HOST_B のユーザーを HOST_A で関連付けています。  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_B_cert  
       AUTHORIZATION HOST_B_user  
       FROM FILE = 'C:\HOST_B_cert.cer'  
    GO  
    ```  
  
     詳細については、「[CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)」を参照してください。  
  
     このサーバー インスタンスの証明書を表示するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    SELECT * FROM sys.certificates  
    ```  
  
     詳細については、「[sys.certificates &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-certificates-transact-sql)」を参照してください。  
  
5.  リモート ミラーリング エンドポイント用のログインに CONNECT 権限を許可します。  
  
     たとえば、HOST_A に対する権限を HOST_B 上のリモート サーバー インスタンスに許可し、このローカル ログインに接続 (つまり、`HOST_B_login` に接続) するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    USE master;  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_B_login];  
    GO  
    ```  
  
     詳細については、「 [GRANT (エンドポイントの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)」を参照してください。  
  
 これで、HOST_A にログインするための HOST_B の証明書認証の設定が完了します。  
  
 ここで、HOST_B で HOST_A 用の着信接続を構成するために同じ手順を実行する必要があります。 この手順については、次の「例」のサンプル コードで着信接続の設定部分を参照してください。  
  
## <a name="example"></a>例  
 次の例では、HOST_B の着信接続を構成する方法について示します。  
  
> [!NOTE]  
>  この例では、「[データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)」のコード スニペットによって作成される HOST_A 証明書を含む証明書ファイルを使用します。  
  
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
  
 Transact-SQL の例を含む、ミラー データベースを作成する方法の詳細については、「[ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)」を参照してください。  
  
 高パフォーマンス モード セッションを確立する TRANSACT-SQL 例では、次を参照してください。[例。データベース ミラーリングを使用して証明書設定&#40;TRANSACT-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)します。  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
 証明書を別のシステムにコピーする場合は、セキュリティで保護されたコピー方法を使用してください。 すべての証明書をセキュリティで保護された状態で保管するよう十分に注意してください。  
  
## <a name="see-also"></a>関連項目  
 [データベース ミラーリングと AlwaysOn 可用性グループのトランスポート セキュリティ&#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [GRANT (エンドポイントのアクセス許可の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)   
 [暗号化されたミラー データベースの設定](set-up-an-encrypted-mirror-database.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
