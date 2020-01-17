---
title: DECRYPTBYKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DecryptByKey_TSQL
- DECRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], DecryptByKey function
- decryption [SQL Server], keys
- decryption [SQL Server], symmetric keys
- DECRYPTBYKEY function
ms.assetid: 6edf121f-ac62-4dae-90e6-6938f32603c9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9ca108b3336a77becc605040b12c0361db4ac903
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251379"
---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は対称キーを使用してデータを復号します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>引数  
*ciphertext*  
キーで暗号化されたデータを含む、型 **varbinary** の変数。  
  
**\@ciphertext**  
キーで暗号化されたデータを含む、型 **varbinary** の変数。  
  
 *add_authenticator*  
元の暗号化プロセスにプレーンテキストと共に認証子が含まれ、認証子が暗号化されたかどうかを示します。 データ暗号化プロセス中、[ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に渡された値に一致する必要があります。 *add_authenticator* には、**int** データ型が与えられます。  
  
 *authenticator*  
認証子の生成の基礎として使用されるデータ。 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に与えられた値と一致する必要があります。 *authenticator* には、**sysname** データ型が与えられます。  

**\@authenticator**  
認証子の生成元となるデータを含む変数。 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に与えられた値と一致する必要があります。 *\@authenticator* には、**sysname** データ型が与えられます。  

## <a name="return-types"></a>戻り値の型  
最大サイズが 8,000 バイトの **varbinary**。 `DECRYPTBYKEY` は、データの暗号化に使用する対称キーが開いていない場合か、*ciphertext* が NULL の場合、NULL を返します。  
  
## <a name="remarks"></a>Remarks  
`DECRYPTBYKEY` は対称キーを使用します。 データベースでは、この対称キーを既に開いている必要があります。 `DECRYPTBYKEY` では、複数のキーを同時に開いておくことができます。 暗号化テキストの復号する直前にキーを開く必要はありません。  
  
対称暗号化/復号は通常、比較的すぐに動作します。大量のデータが含まれる操作で効率的に動作します。  

`DECRYPTBYKEY` 呼び出しは、暗号化キーを含むデータベースのコンテキストで行う必要があります。 これを保証するには、データベース内に存在するオブジェクト (ビュー、ストアド プロシージャ、関数など) から `DECRYPTBYKEY` を呼び出します。 
  
## <a name="permissions"></a>アクセス許可  
対称キーは現在のセッションで開かれている必要があります。 詳細については、「[OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>A. 対称キーを使用して暗号化解除する  
この例では、対称キーで暗号化テキストを復号します。  
  
```sql  
-- First, open the symmetric key with which to decrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
GO  
  
-- Now list the original ID, the encrypted ID, and the   
-- decrypted ciphertext. If the decryption worked, the original  
-- and the decrypted ID will match.  
SELECT NationalIDNumber, EncryptedNationalID   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalID))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-decrypting-by-using-a-symmetric-key-and-an-authenticating-hash"></a>B. 対称キーと認証ハッシュを使用して暗号化解除する  
この例では、認証子と共に、最初に暗号化されたデータを復号します。  
  
```sql  
-- First, open the symmetric key with which to decrypt the data  
OPEN SYMMETRIC KEY CreditCards_Key11  
   DECRYPTION BY CERTIFICATE Sales09;  
GO  
  
-- Now list the original card number, the encrypted card number,  
-- and the decrypted ciphertext. If the decryption worked,   
-- the original number will match the decrypted number.  
SELECT CardNumber, CardNumber_Encrypted   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByKey(CardNumber_Encrypted, 1 ,   
    HashBytes('SHA1', CONVERT(varbinary, CreditCardID))))   
    AS 'Decrypted card number' FROM Sales.CreditCard;  
GO  
  
```  

### <a name="c-fail-to-decrypt-when-not-in-the-context-of-database-with-key"></a>C. キーを持つデータベースのコンテキストではないときに復号化に失敗する
次の例は、キーが含まれるデータベースのコンテキストで `DECRYPTBYKEY` を実行する必要があること示しています。 `DECRYPTBYKEY` がマスター データベースで実行されると、行は復号化されず、結果は NULL になります。 

```sql
-- Create the database
CREATE DATABASE TestingDecryptByKey
GO

USE [TestingDecryptByKey]

-- Create the table and view
CREATE TABLE TestingDecryptByKey.dbo.Test(val VARBINARY(8000) NOT NULL);
GO
CREATE VIEW dbo.TestView AS SELECT CAST(DecryptByKey(val) AS VARCHAR(30)) AS DecryptedVal FROM TestingDecryptByKey.dbo.Test;
GO

-- Create the key, and certificate
USE TestingDecryptByKey;
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'ItIsreallyLong1AndSecured!Passsword#';
CREATE CERTIFICATE TestEncryptionCertificate WITH SUBJECT = 'TestEncryption';
CREATE SYMMETRIC KEY TestEncryptSymmmetricKey WITH ALGORITHM = AES_256, IDENTITY_VALUE = 'It is place for test',
KEY_SOURCE = 'It is source for test' ENCRYPTION BY CERTIFICATE TestEncryptionCertificate;

-- Insert rows into the table
DECLARE @var VARBINARY(8000), @Val VARCHAR(30);
SELECT @Val = '000-123-4567';
OPEN SYMMETRIC KEY TestEncryptSymmmetricKey DECRYPTION BY CERTIFICATE TestEncryptionCertificate;
SELECT @var = EncryptByKey(Key_GUID('TestEncryptSymmmetricKey'), @Val);
SELECT CAST(DecryptByKey(@var) AS VARCHAR(30)), @Val;
INSERT INTO dbo.Test VALUES(@var);
GO

-- Switch to master
USE [Master];
GO

-- Results show the date inserted
SELECT DecryptedVal FROM TestingDecryptByKey.dbo.TestView;

-- Results are NULL because we are not in the context of the TestingDecryptByKey Database
SELECT CAST(DecryptByKey(val) AS VARCHAR(30)) AS DecryptedVal FROM TestingDecryptByKey.dbo.Test;
GO

-- Clean up resources
USE TestingDecryptByKey;

DROP SYMMETRIC KEY TestEncryptSymmmetricKey REMOVE PROVIDER KEY;
DROP CERTIFICATE TestEncryptionCertificate;

Use [Master]
DROP DATABASE TestingDecryptByKey;
GO
```

  
## <a name="see-also"></a>参照  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
