---
title: VERIFYSIGNEDBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VERIFYSIGNEDBYASYMKEY_TSQL
- VERIFYSIGNEDBYASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- verifying digitally signed data for changes
- VERIFYSIGNEDBYASYMKEY
- testing digitally signed data for changes
- checking digitally signed data for changes
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 9f7c6e0b-5ba4-4dbb-994d-5bd59f4908de
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 414c5df86e58472bc1aa3f5df9ee25a54f8bc590
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927547"
---
# <a name="verifysignedbyasymkey-transact-sql"></a>VERIFYSIGNEDBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  デジタル署名付きデータが、署名された後に変更されているかどうかをテストします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
VerifySignedByAsymKey( Asym_Key_ID , clear_text , signature )  
```  
  
## <a name="arguments"></a>引数  
 *Asym_Key_ID*  
 データベース内の非対称キー証明書の ID を指定します。  
  
 *clear_text*  
 検証するクリア テキスト データを指定します。  
  
 *signature*  
 署名付きデータにアタッチされた署名を指定します。 *signature* は **varbinary** です。  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
 署名が一致する場合は 1 が返されます。それ以外の場合は 0 が返されます。  
  
## <a name="remarks"></a>Remarks  
 **VerifySignedByAsymKey** は、指定された非対称キーの公開キーを使用してデータの署名を復号化し、新しく計算されたデータの MD5 ハッシュと比較します。 値が一致すると、その署名が有効であることが確認されます。  
  
## <a name="permissions"></a>アクセス許可  
 非対称キーに対する VIEW DEFINITION 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-testing-for-data-with-a-valid-signature"></a>A. データの署名が有効かどうかをテストする  
 次の例では、選択したデータが非対称キー `WillisKey74` で署名された後に変更されていない場合は 1 が返されます。 この例では、データが変更されている場合は 0 が返されます。  
  
```  
SELECT Data,  
     VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), SignedData,  
     DataSignature ) as IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
RETURN;  
```  
  
### <a name="b-returning-a-result-set-that-contains-data-with-a-valid-signature"></a>B. 有効な署名が添付されたデータを含む結果セットを返す  
 次の例では、`SignedData04` 内の行で、非対称キー `WillisKey74` で署名された後に変更されていないデータを含む行が返されます。 この例では、データベースから非対称キーの ID を取得するため関数 `AsymKey_ID` を呼び出します。  
  
```  
SELECT Data   
FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), Data,  
     DataSignature ) = 1  
AND Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
