---
title: データベース ミラーリング エンドポイントで発信接続 (Transact SQL) の証明書の使用を許可する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- certificates [SQL Server], database mirroring
- outbound connections [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 464c9096-10d6-4c5e-8bb1-19acba27ad9e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43a55174bae1bb03034ea005749055701884848f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806875"
---
# <a name="allow-a-database-mirroring-endpoint-to-use-certificates-for-outbound-connections-transact-sql"></a>データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする (Transact-SQL)
  このトピックでは、データベース ミラーリングの発信接続を認証する際に証明書を使用するようにサーバー インスタンスを構成する手順について説明します。 着信接続を設定する前に、発信接続を構成する必要があります。  
  
> [!NOTE]  
>  1 つのサーバー インスタンス上のすべてのミラーリング接続では、1 つのデータベース ミラーリング エンドポイントが使用されます。そのため、エンドポイントを作成する際にサーバー インスタンスの認証方法を指定する必要があります。  
  
 発信接続を構成する処理には、次の一般的な手順が含まれます。  
  
1.  **master** データベースで、データベース マスター キーを作成します。  
  
2.  **master** データベースで、暗号化された証明書をサーバー インスタンスに作成します。  
  
3.  作成した証明書を使用して、サーバー インスタンスのエンドポイントを作成します。  
  
4.  証明書をファイルにバックアップし、そのファイルをセキュリティで保護された状態で他のシステムにコピーします。  
  
 パートナーおよびミラーリング監視サーバーがある場合は、それぞれで上記の手順を完了する必要があります。  
  
 次の手順では、上記の手順について詳しく説明します。 各手順では、HOST_A という名前のシステムでサーバー インスタンスを構成するための例を示します。 その後に続く「例」では、HOST_B という名前のシステム上の別のサーバー インスタンスに対する同じ手順について説明します。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-configure-server-instances-for-outbound-mirroring-connections-on-hosta"></a>ミラーリングの発信接続用に (HOST_A 上で) サーバー インスタンスを構成するには  
  
1.  **master** データベースで、データベース マスター キーが存在しない場合は作成します。 データベースの既存のキーを表示するには、 [sys.symmetric_keys](/sql/relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql) カタログ ビューを使用します。  
  
     データベース マスター キーを作成するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを使用します。  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<1_Strong_Password!>';  
    GO  
    ```  
  
     複雑で一意なパスワードを使用し、作成したキーを安全な場所に記録します。  
  
     詳細については、「[CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)」と「[データベース マスター キーの作成](../../relational-databases/security/encryption/create-a-database-master-key.md)」を参照してください。  
  
2.  **master** データベースで、データベース ミラーリングの発信接続に使用する、暗号化された証明書をサーバー インスタンスに作成します。  
  
     たとえば、HOST_A システム用の証明書を作成するには、次のステートメントを使用します。  
  
    > [!IMPORTANT]  
    >  証明書の使用期間が 1 年を超える場合は、CREATE CERTIFICATE ステートメントの EXPIRY_DATE オプションを使用して、有効期限を UTC 時間で指定してください。 また、証明書の有効期限が近いことを知らせるポリシー ベースの管理ルールを SQL Server Management Studio で作成することをお勧めします。 ポリシー管理の **[新しい条件の作成]** ダイアログ ボックスを使用し、 **@ExpirationDate** ファセットの **[@ExpirationDate]** フィールドでこのルールを作成します。 詳細については、「 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md) 」と「 [SQL Server の保護](../../relational-databases/security/securing-sql-server.md)」を参照してください。  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_A_cert   
       WITH SUBJECT = 'HOST_A certificate for database mirroring',   
       EXPIRY_DATE = '11/30/2013';  
    GO  
    ```  
  
     詳細については、「[CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)」を参照してください。  
  
     **master** データベースの証明書を表示するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用できます。  
  
    ```  
    USE master;  
    SELECT * FROM sys.certificates;  
    ```  
  
     詳細については、「[sys.certificates &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-certificates-transact-sql)」を参照してください。  
  
3.  各サーバー インスタンスにデータベース ミラーリング エンドポイントがあることを確認します。  
  
     サーバー インスタンスにデータベース ミラーリング エンドポイントが既に存在する場合、サーバー インスタンス上で確立するその他のセッションにそのエンドポイントを再利用する必要があります。 データベース ミラーリング エンドポイントがサーバー インスタンスに存在するかどうかを確認し、その構成を表示するには、次のステートメントを使用します。  
  
    ```  
    SELECT name, role_desc, state_desc, connection_auth_desc, encryption_algorithm_desc   
       FROM sys.database_mirroring_endpoints;  
    ```  
  
     エンドポイントが存在しない場合、発信接続にこの証明書を使用し、他のシステムでの検証にその証明書の資格情報を使用するエンドポイントを作成します。 これは、サーバー全体のエンドポイントであり、サーバー インスタンスが参加するすべてのミラーリング セッションで使用されます。  
  
     たとえば、HOST_A 上のサーバー インスタンスの例にミラーリング エンドポイントを作成するには、次のステートメントを使用します。  
  
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
  
     詳細については、「[CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)」を参照してください。  
  
4.  証明書をバックアップし、他のシステムにコピーします。 この操作は、他のシステムで着信接続を構成するために必要です。  
  
    ```  
    BACKUP CERTIFICATE HOST_A_cert TO FILE = 'C:\HOST_A_cert.cer';  
    GO  
    ```  
  
     詳細については、「[BACKUP CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)」を参照してください。  
  
     任意の安全な方法を使用し、この証明書をコピーします。 すべての証明書をセキュリティで保護された状態で保管するよう十分に注意してください。  
  
 上記の手順のコード例では、HOST_A の発信接続を構成します。  
  
 ここで、HOST_B の着信接続を構成するために同じ手順を実行する必要があります。 この手順については、次の「例」で説明します。  
  
## <a name="example"></a>例  
 次の例では、発信接続用に HOST_B を構成する方法について示します。  
  
```  
USE master;  
--Create the database Master Key, if needed.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Strong_Password_#2>';  
GO  
-- Make a certifcate on HOST_B server instance.  
CREATE CERTIFICATE HOST_B_cert   
   WITH SUBJECT = 'HOST_B certificate for database mirroring',   
   EXPIRY_DATE = '11/30/2013';  
GO  
--Create a mirroring endpoint for the server instance on HOST_B.  
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
--Backup HOST_B certificate.  
BACKUP CERTIFICATE HOST_B_cert TO FILE = 'C:\HOST_B_cert.cer';  
GO   
--Using any secure copy method, copy C:\HOST_B_cert.cer to HOST_A.  
```  
  
 任意の安全な方法を使用し、証明書を他のシステムにコピーします。 すべての証明書をセキュリティで保護された状態で保管するよう十分に注意してください。  
  
> [!IMPORTANT]  
>  発信接続を設定した後、各サーバー インスタンスの着信接続を他のサーバー インスタンス用に構成する必要があります。 詳細については、「[データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)」を参照してください。  
  
 Transact-SQL の例を含む、ミラー データベースを作成する方法の詳細については、「[ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)」を参照してください。  
  
 高パフォーマンス モード セッションを確立する TRANSACT-SQL 例では、次を参照してください。[例。データベース ミラーリングを使用して証明書設定&#40;TRANSACT-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)します。  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
 ネットワークがセキュリティで保護されていることを保証できる場合を除いて、データベース ミラーリング接続に対して暗号化を使用することをお勧めします。  
  
 証明書を別のシステムにコピーする場合は、セキュリティで保護されたコピー方法を使用してください。  
  
## <a name="see-also"></a>関連項目  
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)   
 [例:データベース ミラーリングを使用して証明書設定&#40;TRANSACT-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [暗号化されたミラー データベースの設定](set-up-an-encrypted-mirror-database.md)  
  
  
