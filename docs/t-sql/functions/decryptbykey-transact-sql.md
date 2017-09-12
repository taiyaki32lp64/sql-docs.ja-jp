---
title: "DECRYPTBYKEY (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0debd61d7a6c43c076f2e868379e85db65e90ab1
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  対称キーを使用してデータを暗号化解除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>引数  
 *暗号化テキスト*  
 キーで暗号化されたデータを指定します。 *暗号化テキスト*は**varbinary**です。  
  
 **@ciphertext**  
 型の変数は、 **varbinary**キーで暗号化されたデータが含まれます。  
  
 *add_authenticator*  
 認証子がプレーン テキストと共に暗号化されているかどうかを示します。 この値は、データの暗号化時に EncryptByKey に渡された値と同じである必要があります。 *add_authenticator*は**int**です。  
  
 *認証子*  
 認証子を生成する基のデータを指定します。 EncryptByKey に渡された値と一致する必要があります。 *認証子*は**sysname**です。  
  
 **@authenticator**  
 認証子の生成元のデータを含む変数を指定します。 EncryptByKey に渡された値と一致する必要があります。  
  
## <a name="return-types"></a>戻り値の型  
 **varbinary** 8,000 バイトの最大サイズ。  
  
## <a name="remarks"></a>解説  
 DecryptByKey では対称キーが使用されます。 この対称キーはデータベースで開かれている必要があります。 複数のキーを同時に開いておくことができます。 暗号化テキストの暗号化解除をする直前にキーを開く必要はありません。  
  
 対称キーの暗号化と暗号化解除は比較的高速なので、データが大きい場合に適しています。  
  
## <a name="permissions"></a>Permissions  
 対称キーが現在のセッションで開かれている必要があります。 詳細については、次を参照してください。 [OPEN SYMMETRIC KEY & #40 です。TRANSACT-SQL と #41 です。](../../t-sql/statements/open-symmetric-key-transact-sql.md).  
  
## <a name="examples"></a>使用例  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>A. 対称キーを使用して暗号化解除する  
 次の例では、対称キーを使用して暗号化テキストを暗号化解除します。  
  
```  
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
 次の例では、認証子と共に暗号化されたデータを暗号化解除します。  
  
```  
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
  
## <a name="see-also"></a>参照  
 [ENCRYPTBYKEY & #40 です。TRANSACT-SQL と #41 です。](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  