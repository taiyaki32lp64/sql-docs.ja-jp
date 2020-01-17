---
title: OPEN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPEN MASTER KEY DECRYPTION BY PASSWORD
- OPEN_MASTER_KEY_DECRYPTION_BY_PASSWORD_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- OPEN_MASTER_KEY_TSQL
- MASTER KEY DECRYPTION
- OPEN MASTER KEY
- MASTER_KEY_DECRYPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- opening Database Master Keys
- encryption [SQL Server], Database Master Key
- cryptography [SQL Server], Database Master Key
- master key decryption
- OPEN MASTER KEY statement
- database master key [SQL Server], opening
ms.assetid: 1674753e-ca1e-4913-9ba4-b442e7106121
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fd9510f28c1cdfda1f0ff9303c77df946bf5b9d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129432"
---
# <a name="open-master-key-transact-sql"></a>OPEN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在のデータベースのデータベース マスター キーを開きます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>引数  
 '*password*'  
 データベース マスター キーを暗号化するときに使用するパスワードを指定します。  
  
## <a name="remarks"></a>Remarks  
 データベース マスター キーがサービス マスター キーで暗号化された場合、データベース マスター キーは、暗号化解除または暗号化の必要が生じたときに、自動的に開かれます。 この場合、**OPEN MASTER KEY** ステートメントを使う必要はありません。  
  
 データベースが最初に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の新しいインスタンスにアタッチまたは復元されるとき、データベース マスター キー (サービス マスター キーにより暗号化されたもの) のコピーはまだサーバーに格納されていません。 **OPEN MASTER KEY** を使用して、データベース マスター キー (DMK) を暗号化解除する必要があります。 DMK の暗号化が解除されると、 **ALTER MASTER KEY REGENERATE** ステートメントを使用して、サービス マスター キー (SMK) で暗号化された DMK のコピーをサーバーに提供することにより、将来、自動的に暗号化解除することも可能となります。 データベースを以前のバージョンからアップグレードした場合、新しい AES アルゴリズムを使用するように DMK を再作成する必要があります。 DMK を再作成する方法については、「[ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)」を参照してください。 DMK キーを再作成して AES にアップグレードするのに必要な時間は、DMK によって保護されているオブジェクトの数によって異なります。 DMK キーを再作成して AES にアップグレードする作業は、1 回限りで済み、今後のキー ローテーション方法には影響を与えません。  
  
 DROP ENCRYPTION BY SERVICE MASTER KEY オプションと共に ALTER MASTER KEY ステートメントを使用することにより、特定のデータベースのデータベース マスター キーを自動キー管理から除外することができます。 その後は、パスワードにより明示的にデータベース マスター キーを開く必要があります。  
  
 データベース マスター キーが明示的に開かれるトランザクションがロールバックされると、キーは開いたままとなります。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、パスワードにより暗号化された `AdventureWorks2012` データベースのデータベース マスター キーを開きます。  
  
```  
USE AdventureWorks2012;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、パスワードで暗号化されているデータベース マスターを開きます。  
  
```  
USE master;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO  
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

