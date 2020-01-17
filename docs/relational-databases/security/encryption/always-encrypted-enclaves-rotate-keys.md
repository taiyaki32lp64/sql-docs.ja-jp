---
title: 交換 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 39d90da404fd6bc230a3308c76b48fdc26da2b8f
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595817"
---
# <a name="rotate-enclave-enabled-keys"></a>エンクレーブ対応キーの交換
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Always Encrypted では、キーの交換は、既存の列マスター キーまたは列暗号化キーを新しいキーに置き換える処理です。 この記事では、初期キーまたはターゲット (新しい) キーのどちらか一方または両方がエンクレーブが有効なキーである場合に、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) に固有のキー ローテーションのユースケースと考慮事項について説明します。 Always Encrypted キーを管理するための一般的なガイドラインとプロセスについては、「[Always Encrypted のキー管理の概要](overview-of-key-management-for-always-encrypted.md)」を参照してください。 

セキュリティまたはコンプライアンス上の理由から、キーの交換が必要になる場合があります。 キーが侵害された場合や、組織のポリシーでキーを定期的に交換する必要がある場合などです。 さらに、セキュリティで保護されたエンクレーブが設定された Always Encrypted のキー ローテーションでは、暗号化された列に対してサーバー側のセキュア エンクレーブの機能を有効または無効にすることができます。
- エンクレーブが有効でないキーをエンクレーブが有効なキーで置き換える場合は、キーで保護された 1 つまたは複数の列へのクエリに対するセキュア エンクレーブの機能をロック解除します。 「[既存の暗号化された列に対してセキュリティで保護されたエンクレーブが設定された Always Encrypted の有効化](always-encrypted-enclaves-enable-for-encrypted-columns.md)」をご覧ください。
 - エンクレーブが有効なキーをエンクレーブが有効でないキーで置き換える場合は、キーで保護された 1 つまたは複数の列へのクエリに対するセキュア エンクレーブの機能を無効にします。

セキュリティまたはコンプライアンス上の理由だけでキーを交換し、列のエンクレーブ計算を有効または無効にしない場合は、ターゲット キーのエンクレーブに関する構成がソース キーと同じであることを確認してください。 たとえば、ソース キーのエンクレーブが有効な場合、ターゲット キーもエンクレーブが有効になっている必要があります。

以下の大まかな手順には、目的の交換シナリオに応じた詳細な記事へのリンクが含まれています。

1. 新しいキーを (列マスター キーまたは列暗号化キー) をプロビジョニングします。
    - 新しいエンクレーブ対応キーをプロビジョニングするには、「[エンクレーブ対応キーをプロビジョニングする](always-encrypted-enclaves-provision-keys.md)」を参照してください。
    - エンクレーブが有効でないキーをプロビジョニングするには、「[SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)」および「[PowerShell を使用した Always Encrypted キーのプロビジョニング](configure-always-encrypted-keys-using-powershell.md)」を参照してください。
2. 既存のキーを新しいキーで置き換えます。
    - 列暗号化キーを交換し、ソース キーとターゲット キーの両方のエンクレーブが有効になっている場合は、インプレースで交換を実行できます (データの再暗号化を含む)。 「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)」を参照してください。
    - キーのローテーションの詳細な手順については、「[SQL Server Management Studio を使用した Always Encrypted キーの交換](rotate-always-encrypted-keys-using-ssms.md)」および「[PowerShell を使用した Always Encrypted キーの交換](rotate-always-encrypted-keys-using-powershell.md)」をご覧ください。

    
## <a name="next-steps"></a>Next Steps
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリ](always-encrypted-enclaves-query-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)
- [既存の暗号化された列に対してセキュリティで保護されたエンクレーブが設定された Always Encrypted の有効化](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションの開発](always-encrypted-enclaves-client-development.md)  

## <a name="see-also"></a>参照  
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーの管理](always-encrypted-enclaves-manage-keys.md)

