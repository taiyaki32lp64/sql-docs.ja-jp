---
title: SIGNBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SIGNBYASYMKEY_TSQL
- SIGNBYASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- text signing [SQL Server]
- encryption [SQL Server], asymmetric keys
- signing text [SQL Server]
- SIGNBYASYMKEY function
- asymmetric keys [SQL Server], SIGNBYASYMKEY function
- cryptography [SQL Server], asymmetric keys
- clear text signing
ms.assetid: b1c46159-cc76-4205-a841-8f4a71742f80
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 804f8c1f2f7c59edec2c4e40c7d47f99ac71b5e7
ms.sourcegitcommit: a24f6e12357979f1134a54a036ebc58049484a4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314553"
---
# <a name="signbyasymkey-transact-sql"></a>SIGNBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  プレーン テキストに非対称キーで署名する  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SignByAsymKey( Asym_Key_ID , @plaintext [ , 'password' ] )  
```  
  
## <a name="arguments"></a>引数  
 *Asym_Key_ID*  
 現在のデータベース内の非対称キーの ID を指定します。 *Asym_Key_ID* は**int**です。  
  
 **\@plaintext**  
 非対称キーを使って署名するデータを格納する **nvarchar**、**char**、**varchar**、または **nchar** 型の変数を指定します。  
  
 *password*  
 秘密キーを保護するパスワードを指定します。 *password* は **nvarchar (128)** です。  
  
## <a name="return-types"></a>戻り値の型  
 **varbinary** 8,000 バイトの最大サイズ。  
  
## <a name="remarks"></a>Remarks  
 非対称キーに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、プレーン テキストとその署名を格納するテーブル `SignedData04` を作成し、 次に、非対称キー `PrimeKey` を使用して署名したレコードをテーブルに挿入します。このキーは最初にパスワード `'pGFD4bb925DGvbd2439587y'` で暗号化解除されます。  
  
```  
-- Create a table in which to store the data  
CREATE TABLE [SignedData04](Description nvarchar(max), Data nvarchar(max), DataSignature varbinary(8000));  
GO  
-- Store data together with its signature  
DECLARE @clear_text_data nvarchar(max);  
set @clear_text_data = N'Important numbers 2, 3, 5, 7, 11, 13, 17,   
      19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79,  
      83, 89, 97';  
INSERT INTO [SignedData04]   
    VALUES( N'data encrypted by asymmetric key ''PrimeKey''',  
    @clear_text_data, SignByAsymKey( AsymKey_Id( 'PrimeKey' ),  
    @clear_text_data, N'pGFD4bb925DGvbd2439587y' ));  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [VERIFYSIGNEDBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
