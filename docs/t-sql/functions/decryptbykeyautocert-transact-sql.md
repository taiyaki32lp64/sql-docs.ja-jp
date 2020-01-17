---
title: DECRYPTBYKEYAUTOCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a8772e2e1ecb001b26db02750ae134f545180113
ms.sourcegitcommit: a24f6e12357979f1134a54a036ebc58049484a4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314565"
---
# <a name="decryptbykeyautocert-transact-sql"></a>DECRYPTBYKEYAUTOCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

この関数は、対称キーでデータを復号します。 その対称キーは、証明書で自動的に復号されます。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *cert_ID*  
対称キーの保護に使用されている証明書の ID。 *cert_ID* には、**int** データ型が与えられます。  
  
*cert_password*  
証明書の秘密キーの復号に使用されるパスワード。 データベース マスター キーによって秘密キーが保護される場合、`NULL` 値を設定できます。 *cert_password* には、**nvarchar** データ型が与えられます。  

'*ciphertext*'  
キーで暗号化されたデータの文字列。 *ciphertext* には、**varbinary** データ型が与えられます。  

@ciphertext  
キーで暗号化されたデータを含む、型 **varbinary** の変数。  

*add_authenticator*  
元の暗号化プロセスにプレーンテキストと共に認証子が含まれ、認証子が暗号化されたかどうかを示します。 データ暗号化プロセス中、[ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に渡された値に一致する必要があります。 *add_authenticator* には、暗号化プロセスで認証子が使用された場合、値 1 が与えられます。 *add_authenticator* には、**int** データ型が与えられます。  
  
@add_authenticator  
元の暗号化プロセスにプレーンテキストと共に認証子が含まれ、認証子が暗号化されたかどうかを示す変数。 データ暗号化プロセス中、[ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に渡された値に一致する必要があります。 *\@add_authenticator* には、**int** データ型が与えられます。  
  
*authenticator*  
認証子の生成の基礎として使用されるデータ。 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に与えられた値と一致する必要があります。 *authenticator* には、**sysname** データ型が与えられます。  
  
@authenticator  
認証子の生成元となるデータを含む変数。 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に与えられた値と一致する必要があります。 *\@authenticator* には、**sysname** データ型が与えられます。  
  
## <a name="return-types"></a>戻り値の型  
最大サイズが 8,000 バイトの **varbinary**。  
  
## <a name="remarks"></a>Remarks  
`DECRYPTBYKEYAUTOCERT` には、`OPEN SYMMETRIC KEY` と `DECRYPTBYKEY` の機能が組み合わされています。 1 つの操作で、最初に非対称キーが復号され、そのキーで暗号化テキストが復号されます。  
  
## <a name="permissions"></a>アクセス許可  
対称キーに対する `VIEW DEFINITION` 権限と、証明書に対する `CONTROL` 権限が必要です。   
  
## <a name="examples"></a>使用例  
この例では、`DECRYPTBYKEYAUTOCERT` が復号コードを簡略化するしくみを確認できます。 このコードは、データベース マスター キーが存在しない [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで実行する必要があります。  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE CERTIFICATE HumanResources037   
   WITH SUBJECT = 'Sammamish HR',   
   EXPIRY_DATE = '10/31/2009';  
CREATE SYMMETRIC KEY SSN_Key_01 WITH ALGORITHM = DES  
    ENCRYPTION BY CERTIFICATE HumanResources037;  
GO  
----Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037 ;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
--  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key  
--2. Decrypt the data  
--3. Close the symmetric key  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
SELECT NationalIDNumber, EncryptedNationalIDNumber    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--OPTION TWO, using DecryptByKeyAutoCert()  
SELECT NationalIDNumber, EncryptedNationalIDNumber   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoCert ( cert_ID('HumanResources037') , NULL ,EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
```  
  
## <a name="see-also"></a>参照  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
