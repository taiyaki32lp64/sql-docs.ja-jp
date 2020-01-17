---
title: CREATE DATABASE ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATABASE_ENCRYPTION_KEY_TSQL
- ENCRYPTION_KEY_TSQL
- sql13.swb.dbencryptionkeyo.f1
- ENCRYPTION KEY
- DATABASE ENCRYPTION KEY
- CREATE_DATABASE_ENCRYPTION_KEY_TSQL
- CREATE DATABASE ENCRYPTION KEY
- sql13.swb.dbencryptionkeyg.f1
- CREATE DATABASE ENCRYPTION
- CREATE_DATABASE_ENCRYPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database encryption key
- CREATE DATABASE ENCRYPTION KEY statement
- database encryption key, create
ms.assetid: 2ee95a32-5140-41bd-9ab3-a947b9990688
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: da59f10213eab84f52b764f41625d6f9361f0a40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060991"
---
# <a name="create-database-encryption-key-transact-sql"></a>CREATE DATABASE ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

 データベースを透過的に暗号化するために使用する暗号化キーを作成します。 透過的データベース暗号化について詳しくは、「[透過的なデータ暗号化 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」をご覧ください。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server  

CREATE DATABASE ENCRYPTION KEY  
       WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   ENCRYPTION BY SERVER   
    {  
        CERTIFICATE Encryptor_Name |  
        ASYMMETRIC KEY Encryptor_Name  
    }  
[ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  

CREATE DATABASE ENCRYPTION KEY  
       WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY  }  
暗号化キーに使用する暗号化アルゴリズムを指定します。   
> [!NOTE]
>    SQL Server 2016以降、AES_128、AES_192、AES_256 以外のすべてのアルゴリズムが非推奨とされました。 古いアルゴリズムを使用する場合は (推奨されません)、データベース互換性レベルを 120 以下に設定する必要があります。  
  
ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name  
データベース暗号化キーを暗号化するために使用する暗号化処理方法の名前を指定します。  
  
ENCRYPTION BY SERVER ASYMMETRIC KEY Encryptor_Name  
データベース暗号化キーを暗号化するために使用する非対称キーの名前を指定します。 非対称キーでデータベース暗号化キーを暗号化するには、非対称キーが拡張キー管理プロバイダーに存在している必要があります。  
  
## <a name="remarks"></a>Remarks  
*Transparent Data Encryption* (TDE) を使ってデータベースを暗号化するには、事前にデータベース暗号化キーが必要です。 データベースを透過的に暗号化すると、特別にコードを変更することなく、データベース全体がファイル レベルで暗号化されます。 データベース暗号化キーの暗号化に使用する証明書または非対称キーは、マスター システム データベースに配置されている必要があります。  
  
データベース暗号化ステートメントは、ユーザー データベースでのみ使用できます。  
  
データベース暗号化キーは、データベースからエクスポートできません。 このキーを使用できるのは、システム、サーバーでのデバッグ権限を持つユーザー、およびデータベース暗号化キーを暗号化および暗号化解除する証明書へのアクセス権を持つユーザーに限られています。  
  
データベース所有者 (dbo) が変わっても、データベース暗号化キーを再生成する必要はありません。  
  
データベース暗号化キーは、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] データベース用に自動的に作成されます。 CREATE DATABASE ENCRYPTION KEY ステートメントを使用してキーを作成する必要はありません。  
  
## <a name="permissions"></a>アクセス許可  
データベースに対する CONTROL 権限と、データベース暗号化キーの暗号化に使用する証明書または非対称キーに対する VIEW DEFINITION 権限が必要です。  
  
## <a name="examples"></a>使用例  
TDE の使用に関する他の例については、「[Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」、「[EKM の使用による TDE の有効化](../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)」、および「[Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)」をご覧ください。  
  
次の例では、`AES_256` アルゴリズムを使用してデータベース暗号化キーを作成し、`MyServerCert` という証明書で秘密キーを保護します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
```  
  
## <a name="see-also"></a>参照  
[透過的なデータ暗号化 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
[SQL Server の暗号化](../../relational-databases/security/encryption/sql-server-encryption.md)   
[SQL Server とデータベースの暗号化キー &#40;データベース エンジン&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
[暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
[ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)   
[sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)  
    
