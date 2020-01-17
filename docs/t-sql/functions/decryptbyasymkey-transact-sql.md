---
title: DECRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c187caf0dc0027d6d7fa86cbd1bee09e76f0228d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118959"
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は非対称キーを使用して暗号化データを復号します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>引数  
 *Asym_Key_ID*  
データベース内の非対称キーの ID。 *Asym_Key_ID* には、**int** データ型が与えられます。  
  
 *ciphertext*  
非対称キーで暗号化するデータの文字列。  
  
 @ciphertext  
非対称キーで暗号化されたデータを含む、型 **varbinary** の変数。  
  
 *Asym_Key_Password*  
データベース内の非対称キーの暗号化に使用されたパスワード。  
  
## <a name="return-types"></a>戻り値の型  
最大サイズが 8,000 バイトの **varbinary**。  
  
## <a name="remarks"></a>Remarks  
対称暗号化/復号と比べると、非対称キーの暗号化/復号はコストが高くなります。 テーブルに保存されているユーザー データなど、大量のデータセットを扱うとき、非対称キーの暗号化/復号は回避するように開発者には提案しています。  
  
## <a name="permissions"></a>アクセス許可  
`DECRYPTBYASYMKEY` には、非対称キーに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
この例では、非対称キー `JanainaAsymKey02` で最初に暗号化された暗号化テキストが復号されます。 `AdventureWorks2012.ProtectedData04` によって、この非対称キーが格納されました。 返されたデータが非対称キー `JanainaAsymKey02` で復号されました。 パスワード `pGFD4bb925DGvbd2439587y` を使用し、この非対称キーが復号されました。 返されたプレーンテキストが型 **nvarchar** に変換されました。  
  
```  
SELECT CONVERT(nvarchar(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2012].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
