---
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d3968c5c8f04cba8581dfdd44ac847f7010de994
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595627"
---
# <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md)では、エンクレーブ対応キーを導入することによって、[Always Encrypted](always-encrypted-database-engine.md) のキー管理が拡張されています。 

- **エンクレーブ対応の列マスター キー** - データベース内の列マスター キー メタデータ オブジェクトで `ENCLAVE_COMPUTATIONS` プロパティを指定して作成された列マスター キー。 
- **エンクレーブ対応列暗号化キー**: エンクレーブ対応列マスター キーで暗号化された列暗号化キーです。 サーバー側のセキュリティで保護されたエンクレーブ内での計算に使用できるのは、エンクレーブ対応の列暗号化キーだけです。 

[Always Encrypted キーの管理](overview-of-key-management-for-always-encrypted.md)に関する一般的なガイドラインとプロセスが、エンクレーブ対応キーの管理にも適用されます。 

## <a name="managing-keys"></a>キーの管理

次の記事では、エンクレーブ対応キーの管理に固有の部分が説明されています。

- [エンクレーブ対応キーをプロビジョニングする](always-encrypted-enclaves-provision-keys.md)
- [エンクレーブ対応キーをローテーションする](always-encrypted-enclaves-rotate-keys.md)

## <a name="next-steps"></a>Next Steps
- [エンクレーブ対応キーをプロビジョニングする](always-encrypted-enclaves-provision-keys.md)

## <a name="see-also"></a>参照  
- [Always Encrypted のキー管理の概要](overview-of-key-management-for-always-encrypted.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
