---
title: DECRYPTBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DecryptByCert_TSQL
- DECRYPTBYCERT
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], decryption
- decryption [SQL Server], certificates
- DECRYPTBYCERT function
ms.assetid: 4950d787-40fa-4e26-bce8-2cb2ceca12fb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9653e799a543dd95a7d6fb033e0a8d5b9a4484a8
ms.sourcegitcommit: a24f6e12357979f1134a54a036ebc58049484a4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314531"
---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は証明書の秘密キーを使用し、暗号化データを復号します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>引数  
 *certificate_ID*  
データベース内の証明書の ID。 *certificate_ID* には、**int** データ型が与えられます。  
  
 *ciphertext*  
証明書の公開キーで暗号化されているデータの文字列。  
  
 @ciphertext  
証明書で暗号化されたデータを含む、型 **varbinary** の変数。  
  
 *cert_password*  
証明書の秘密キーの復号に使用されるパスワード。 *cert_password* のデータ形式は Unicode にする必要があります。  
  
 @cert_password  
証明書の秘密キーの復号に使用されるパスワードを含む、型 **nchar** または **nvarchar** の変数。 *\@cert_password* のデータ形式は Unicode にする必要があります。  

## <a name="return-types"></a>戻り値の型  
最大サイズが 8,000 バイトの **varbinary**。  
  
## <a name="remarks"></a>Remarks  
この関数では、証明書の秘密キーを使ってデータの暗号化を解除します。 非対称キーを使用する暗号化変換では、リソースが大幅に消費されます。 そのため、日常的なユーザー データの暗号化/復号については、[ENCRYPTBYCERT](./encryptbycert-transact-sql.md) と DECRYPTBYCERT の使用を避けるように開発者に提案しています。  

## <a name="permissions"></a>アクセス許可  
`DECRYPTBYCERT` には、証明書に対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
この例では、証明書 `JanainaCert02` によって最初に暗号化されたデータとしてマークされている、`[AdventureWorks2012].[ProtectedData04]` からの行が選択されます。 最初に、証明書 `pGFD4bb925DGvbd2439587y` のパスワードで証明書 `JanainaCert02` の秘密キーが復号されます。 次に、この秘密キーで暗号化テキストが復号されます。 暗号化データが **varbinary** から **nvarchar** に変換されます。  

```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ENCRYPTBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
