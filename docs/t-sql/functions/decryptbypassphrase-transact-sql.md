---
title: DECRYPTBYPASSPHRASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYPASSPHRASE
- DECRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], DECRYPTBYPASSPHRASE function
- DECRYPTBYPASSPHRASE function
ms.assetid: ca34b5cd-07b3-4dca-b66a-ed8c6a826c95
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9791a9672965757f5b86cbae60241ef7528ae565
ms.sourcegitcommit: a24f6e12357979f1134a54a036ebc58049484a4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314520"
---
# <a name="decryptbypassphrase-transact-sql"></a>DECRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は、もともとパスフレーズで暗号化されたデータを復号します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DecryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>引数  
 *passphrase*  
復号キーの生成に使用されるパスフレーズ。  
  
 @passphrase  
復号キーの生成に使用されるパスフレーズを含む型

+ **char**
+ **nchar**
+ **nvarchar**

内の複数の

+ **varchar**

の変数。  
  
'*ciphertext*'  
キーで暗号化されたデータの文字列。 *ciphertext* には、**varbinary** データ型が与えられます。  
 
@ciphertext  
キーで暗号化されたデータを含む、型 **varbinary** の変数。 *\@ciphertext* 変数の最大サイズは 8,000 バイトです。  
  
*add_authenticator*  
元の暗号化プロセスにプレーンテキストと共に認証子が含まれ、認証子が暗号化されたかどうかを示します。 *add_authenticator* には、暗号化プロセスで認証子が使用された場合、値 1 が与えられます。 *add_authenticator* には、**int** データ型が与えられます。  
  
@add_authenticator  
元の暗号化プロセスにプレーンテキストと共に認証子が含まれ、認証子が暗号化されたかどうかを示す変数。 *\@add_authenticator* には、暗号化プロセスで認証子が使用された場合、値 1 が与えられます。 *\@add_authenticator* には、**int** データ型が与えられます。  

*authenticator*  
認証子の生成の基礎として使用されるデータ。 *authenticator* には、**sysname** データ型が与えられます。  
  
@authenticator  
認証子の生成の基礎として使用されるデータを含む変数。 *\@authenticator* には、**sysname** データ型が与えられます。  
  
## <a name="return-types"></a>戻り値の型  
最大サイズが 8,000 バイトの **varbinary**。  
  
## <a name="remarks"></a>Remarks  
`DECRYPTBYPASSPHRASE` は、その実行にアクセス許可を必要としません。 `DECRYPTBYPASSPHRASE` は、間違ったパスフレーズまたは認証子情報を受け取ると、NULL を返します。  
  
`DECRYPTBYPASSPHRASE` はパスフレーズを使用し、復号キーを生成します。 この復号キーは永続ではありません。  
  
暗号化テキストの暗号化時に認証子が含まれた場合、`DECRYPTBYPASSPHRASE` は、復号プロセスのためにその同じ認証子を受け取らなければなりません。 復号プロセスのために与えられた認証子値がデータの暗号化に使用された認証子値に一致しない場合、`DECRYPTBYPASSPHRASE` 操作は失敗します。  
  
## <a name="examples"></a>使用例  
この例では、[EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md) で更新されたレコードを復号します。  
  
```  
USE AdventureWorks2012;  
-- Get the pass phrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
= 'A little learning is a dangerous thing!';  
  
-- Decrypt the encrypted record.  
SELECT CardNumber, CardNumber_EncryptedbyPassphrase   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByPassphrase(@PassphraseEnteredByUser, CardNumber_EncryptedbyPassphrase, 1   
    , CONVERT(varbinary, CreditCardID)))  
    AS 'Decrypted card number' FROM Sales.CreditCard   
    WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
  
  
