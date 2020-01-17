---
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを実行する | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d0a522d6deb01169189d6f5faaf7ba2f189d1522
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595507"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを実行する
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

このチュートリアルでは、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) に対してサーバー側のセキュリティで保護されたエンクレーブを使用して、暗号化された列に対するクエリを実行する場合の、一般的な考慮事項について説明します。 

次の種類のクエリには、セキュリティで保護されたエンクレーブの使用が含まれます。
- エンクレーブ対応キーを使用するインプレース暗号化操作をトリガーするクエリ。「[Transact-SQL を使用してインプレースでの列の暗号化を構成する](always-encrypted-enclaves-configure-encryption-tsql.md)」をご覧ください。
- *高度なクエリ* - ランダム化された暗号化およびエンクレーブ対応キーを使用して暗号化された列に対する範囲比較またはパターン マッチング操作。
- ランダム化された暗号化およびエンクレーブ対応キーを使用して、暗号化された列のインデックスを作成または更新するクエリ。 詳細については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列でインデックスを作成して使用する](always-encrypted-enclaves-create-use-indexes.md)」を参照してください。

> [!NOTE]
> 高度なクエリとインデックスは、ランダム化された暗号化を使用するエンクレーブ対応列 (エンクレーブ対応列の暗号化キーで暗号化された列) でのみサポートされています。 決定論的暗号化では、高度なクエリやインデックスはサポートされていません。

> [!NOTE]
> 暗号化された文字列型の列で高度なクエリを使用するには、バイナリ 2 並べ替え順序 (BIN2 照合順序) による照合順序が列で使用されている必要があります。 


## <a name="next-steps"></a>Next Steps
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを SSMS で実行する](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="see-also"></a>参照
- [チュートリアル: SSMS を使用したセキュリティで保護されたエンクレーブを持つ Always Encrypted の概要](../tutorial-getting-started-with-always-encrypted-enclaves.md)

