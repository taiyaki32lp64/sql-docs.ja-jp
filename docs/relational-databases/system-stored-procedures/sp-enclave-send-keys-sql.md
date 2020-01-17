---
title: sp_enclave_send_keys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enclave_send_keys
- sp_enclave_send_keys_TSQL
- sys.sp_enclave_send_keys
- sys.sp_enclave_send_keys_TSQL
helpviewer_keywords:
- sp_enclave_send_keys
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: ca6e7485e85665f06c2410438b902fa0647418ae
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593758"
---
# <a name="sp_enclave_send_keys-transact-sql"></a>sp_enclave_send_keys (Transact-sql)
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

データベースで定義されている列暗号化キーを、 [Always Encrypted with secure enclaves と](../security/encryption/always-encrypted-enclaves.md)共に使用されるサーバー側の secure エンクレーブに送信します。

`sp_enclave_send_keys` は、エンクレーブが有効なキーのみを送信し、ランダム化された暗号化を使用してインデックスを持つ列を暗号化します。 通常のユーザークエリの場合、クライアントドライバーは、クエリの計算に必要なキーをエンクレーブに提供します。 `sp_enclave_send_keys` は、データベースで定義され、暗号化された列のインデックスに使用されるすべての列暗号化キーを送信します。 

`sp_enclave_send_keys` を使用すると、キーをエンクレーブに送信し、それ以降のインデックス作成操作のために列暗号化キーキャッシュを設定できます。 `sp_enclave_send_keys` を使用して有効にします。
- DBA が列マスターキーにアクセスできない場合に、暗号化されたデータベース列のインデックスまたは統計を再構築または変更するための DBA。 「[キャッシュ列暗号化キーを使用したインデックス作成操作の呼び出し」を](../security/encryption/always-encrypted-enclaves-create-use-indexes.md#invoke-indexing-operations-using-cached-column-encryption-keys)参照してください。
- 暗号化された列のインデックスの復旧を完了するために [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] します。 「[データベースの復旧](../security/encryption/always-encrypted-enclaves.md#database-recovery)」を参照してください。
- 暗号化された列にデータを一括読み込みする SQL Server の .NET Framework Data Provider を使用するアプリケーション。

`sp_enclave_send_keys`を正常に呼び出すには、データベース接続に対して有効になっている Always Encrypted とエンクレーブ計算を使用してデータベースに接続する必要があります。 また、列のマスターキーにアクセスし、列の暗号化キーを保護し、送信する必要があります。また、データベース内の Always Encrypted キーメタデータにアクセスするためのアクセス許可が必要です。 

## <a name="syntax"></a>構文  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>引数

このストアドプロシージャには引数がありません。

## <a name="return-value"></a>戻り値

このストアドプロシージャには戻り値がありません。
  
## <a name="result-sets"></a>結果セット

このストアドプロシージャには結果セットがありません。
  
## <a name="permissions"></a>アクセス許可

 データベースの `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` と `VIEW ANY COLUMN MASTER KEY DEFINITION` のアクセス許可が必要です。  
  
## <a name="examples"></a>使用例  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>参照
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../security/encryption/always-encrypted-enclaves.md) 
 
- [Always Encrypted と secure enclaves を使用して列にインデックスを作成して使用する](../security/encryption/always-encrypted-enclaves-create-use-indexes.md)

- [チュートリアル: ランダム化された暗号化を使用してエンクレーブ対応の列にインデックスを作成して使用する](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)
