---
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d887e428773e6901544422edcb6960e6e9ae0580
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595517"
---
# <a name="configure-column-encryption-in-place-using-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する 
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) を使うと、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のセキュリティで保護されたエンクレーブ内で、データベースの列に対するインプレースでの暗号化操作がサポートされます。 インプレース暗号化を使うと、そのような操作のためにデータをデータベースの外部に移動する必要がなくなり、暗号化操作の速度と信頼性が向上します。 

> [!NOTE]
> インプレース暗号化のパフォーマンス上の利点にもかかわらず、大きなテーブルの暗号化操作には時間がかかり、大量のリソースが消費され、アプリケーションのパフォーマンスと可用性が低下する可能性があります。

インプレース暗号化を使うと、[ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) ステートメントを使用して暗号化操作をトリガーすることもできます。これは、エンクレーブなしでは実行できません。

## <a name="prerequisites"></a>Prerequisites
サポートされている暗号化操作と、操作に使用される列暗号化キーの要件は、次のとおりです。
- プレーンテキスト列の暗号化。 列の暗号化に使用される列暗号化キーは、エンクレーブ対応である必要があります。
- 新しい暗号化の種類と新しい列暗号化キーの一方または両方を使用した、暗号化された列の再暗号化。 現在の列暗号化キーと新しい列暗号化キー (現在のキーと異なる場合) の両方が、エンクレーブ対応である必要があります。
- 暗号化された列の暗号化解除。列を保護している列暗号化キーは、エンクレーブ対応である必要があります。

列暗号化キーがエンクレーブ対応であることを確認する方法については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](always-encrypted-enclaves-manage-keys.md)」を参照してください。

また、インプレース暗号化には、セキュリティで保護されたエンクレーブが正しく初期化されている SQL Server インスタンスも必要です。 「[Always Encrypted サーバー構成オプションのエンクレーブの種類を構成する](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)」をご覧ください。

暗号化操作をトリガーするユーザーまたはアプリケーションには、影響を受ける列を含むテーブルでスキーマを変更し、操作に関係する列マスター キーとデータベース内の関連するキー メタデータにアクセスするための、アクセス許可が必要です。

SQL Server Management Studio またはカスタム アプリケーションから [ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) を使用することによってのみ、インプレース暗号化をトリガーできます。 「[Transact-SQL を使用してインプレースでの列の暗号化を構成する](always-encrypted-enclaves-configure-encryption-tsql.md)」をご覧ください。

> [!NOTE]
> 現時点では、[Always Encrypted ウィザード](always-encrypted-wizard.md)および [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/module/sqlserver/set-sqlcolumnencryption) コマンドレットではインプレース暗号化はサポートされておらず、構成が上記の要件を満たしている場合でも、データは暗号化操作のために常にダウンロードされます。 

## <a name="next-steps"></a>Next Steps
- [Transact-SQL を使用してインプレースでの列の暗号化を構成する](always-encrypted-enclaves-configure-encryption-tsql.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列でインデックスを作成して使用する](always-encrypted-enclaves-create-use-indexes.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)
