---
title: DECRYPTBYKEYAUTOASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOASYMKEY_TSQL
- DECRYPTBYKEYAUTOASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOASYMSKEY function
ms.assetid: 5521d4cf-740c-4ede-98b6-4ba90b84e32d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 14668b9fac1ba05d458bdedc038faaf2883dc9c1
ms.sourcegitcommit: a24f6e12357979f1134a54a036ebc58049484a4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314568"
---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

この関数によって、暗号化データが復号されます。 これを行うために、最初に別個の非対称キーで対称キーが復号され、次に最初の "手順" で抽出された対称キーで暗号化データが復号されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DecryptByKeyAutoAsymKey ( akey_ID , akey_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *akey_ID*  
対称キーの暗号化に使用されている非対称キーの ID。 *akey_ID* には、**int** データ型が与えられます。  
  
 *akey_password*  
非対称キーを保護するパスワード。 *akey_password* には、データベース マスター キーによって非対称プライベート キーが保護される場合、NULL 値を設定できます。 *akey_password* には、**nvarchar** データ型が与えられます。  
  
 *ciphertext* はキーによって暗号化されたデータです。 *ciphertext* には、**varbinary** データ型が与えられます。  
  
 @ciphertext  
対称キーで暗号化されたデータを含む、型 **varbinary** の変数。  
  
 *add_authenticator*  
元の暗号化プロセスにプレーンテキストと共に認証子が含まれ、認証子が暗号化されたかどうかを示します。 データ暗号化プロセス中、[ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に渡された値に一致する必要があります。 *add_authenticator* には、暗号化プロセスで認証子が使用された場合、値 1 が与えられます。 *add_authenticator* には、**int** データ型が与えられます。  
  
 @add_authenticator  
元の暗号化プロセスにプレーンテキストと共に認証子が含まれ、認証子が暗号化されたかどうかを示す変数。 データ暗号化プロセス中、[ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に渡された値に一致する必要があります。 *\@add_authenticator* には、**int** データ型が与えられます。
  
 *authenticator*  
認証子の生成の基礎として使用されるデータ。 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に与えられた値と一致する必要があります。 *authenticator* には、**sysname** データ型が与えられます。  
  
 @authenticator  
認証子の生成元となるデータを含む変数。 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に与えられた値と一致する必要があります。 *\@authenticator* には、**sysname** データ型が与えられます。  
  
@add_authenticator  
元の暗号化プロセスにプレーンテキストと共に認証子が含まれ、認証子が暗号化されたかどうかを示す変数。 データ暗号化プロセス中、[ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に渡された値に一致する必要があります。 *\@add_authenticator* には、**int** データ型が与えられます。  

*authenticator*  
認証子の生成の基礎として使用されるデータ。 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に与えられた値と一致する必要があります。 *authenticator* には、**sysname** データ型が与えられます。

@authenticator  
認証子の生成元となるデータを含む変数。 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) に与えられた値と一致する必要があります。 *\@authenticator* には、**sysname** データ型が与えられます。  

## <a name="return-types"></a>戻り値の型  
最大サイズが 8,000 バイトの **varbinary**。  
  
## <a name="remarks"></a>Remarks  
`DECRYPTBYKEYAUTOASYMKEY` には、`OPEN SYMMETRIC KEY` と `DECRYPTBYKEY` の両方の機能が組み合わされています。 1 つの操作で、最初に非対称キーが復号され、そのキーで暗号化テキストが復号されます。  
  
## <a name="permissions"></a>アクセス許可  
対称キーに対する `VIEW DEFINITION` 権限と、非対称キーに対する `CONTROL` 権限が必要です。  
  
## <a name="examples"></a>使用例
この例では、`DECRYPTBYKEYAUTOASYMKEY` が復号コードを簡略化するしくみを確認できます。 このコードは、データベース マスター キーが存在しない [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで実行する必要があります。  

```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE ASYMMETRIC KEY SSN_AKey   
    WITH ALGORITHM = RSA_2048 ;   
GO  
CREATE SYMMETRIC KEY SSN_Key_02 WITH ALGORITHM = DES  
    ENCRYPTION BY ASYMMETRIC KEY SSN_AKey;  
GO  
--  
--Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber2 varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber2  
    = EncryptByKey(Key_GUID('SSN_Key_02'), NationalIDNumber);  
GO  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key.  
--2. Decrypt the data.  
--3. Close the symmetric key.  
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
SELECT NationalIDNumber, EncryptedNationalIDNumber2    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--OPTION TWO, using DecryptByKeyAutoAsymKey()  
SELECT NationalIDNumber, EncryptedNationalIDNumber2   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoAsymKey ( AsymKey_ID('SSN_AKey') , NULL ,EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
