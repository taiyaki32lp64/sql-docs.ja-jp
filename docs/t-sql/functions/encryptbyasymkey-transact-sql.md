---
title: ENCRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1de142260dc0724656ca4cfdf286370d16def4b5
ms.sourcegitcommit: a24f6e12357979f1134a54a036ebc58049484a4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314601"
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は非対称キーでデータを暗号化します。  
  
 ![記事のリンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事のリンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>引数  
*asym_key_ID*  
データベース内の非対称キーの ID。 *asym_key_ID* には、**int** データ型が与えられます。  
  
*cleartext*  
`ENCRYPTBYASYMKEY` が非対称キーで暗号化するデータの文字列。 *cleartext* のデータ型には
 
+ **binary**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
内の複数の
  
+ **varchar**
 
があります。  
  
**\@plaintext**  
`ENCRYPTBYASYMKEY` が非対称キーで暗号化する値を保持する変数。 **\@plaintext** のデータ型には
  
+ **binary**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
内の複数の
  
+ **varchar**
 
があります。  
  
## <a name="return-types"></a>戻り値の型  
最大サイズが 8,000 バイトの **varbinary**。  
  
## <a name="remarks"></a>Remarks  
非対称キーを使用する暗号化操作と復号操作は大量のリソースを消費します。そのため、対称キーの暗号化と復号に比べ、高くつきます。 データベース テーブルに格納されているユーザー データ データベースなど、データセットが大規模になる場合、非対称キーで暗号化/復号することは開発者にお勧めしていません。 代わりに、強力な対称キーでデータを暗号化し、その対称キーを非対称キーで暗号化することをお勧めしています。  
  
アルゴリズムにもよりますが、`ENCRYPTBYASYMKEY` は、入力が特定のバイト数を超えると、**NULL** を返します。 具体的な制限:

+ 512 ビット RSA キーで暗号化できるのは 53 バイトまで
+ 1024 ビット キーで暗号化できるのは 117 バイトまで
+ 2048 ビット キーで暗号化できるのは 245 バイトまで

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、証明書と非対称キーの両方が RSA キーのラッパーとして機能します。  
  
## <a name="examples"></a>使用例  
この例では、`@cleartext` に格納されているテキストを非対称キー `JanainaAsymKey02` を使用して暗号化します。 このステートメントは、`ProtectedData04` テーブルに暗号化されたデータを挿入します。  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
