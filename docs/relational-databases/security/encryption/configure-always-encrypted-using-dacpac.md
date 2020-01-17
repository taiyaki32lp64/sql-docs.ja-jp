---
title: DAC パッケージでの Always Encrypted を使用した列暗号化の構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: df18a2ca6f79982db41b5188283bf1721b518e31
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595747"
---
# <a name="configure-column-encryption-using-always-encrypted-with-a-dac-package"></a>DAC パッケージでの Always Encrypted を使用した列暗号化の構成 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[データ層アプリケーション (DAC) パッケージ](../../data-tier-applications/data-tier-applications.md) (DACPAC とも呼ばれます) は、テーブル内のテーブルや列を含むすべての SQL Server オブジェクトを定義する SQL Server データベースのデプロイの移植可能な単位です。 DACPAC をデータベースに発行する場合 (DACPAC を使用してデータベースをアップグレードする場合)、ターゲット データベースのスキーマは、DACPAC のスキーマに一致するように更新されます。 SQL Server Management Studio、[PowerShell](../../data-tier-applications/upgrade-a-data-tier-application.md#UpgradeDACPowerShell)、または [sqlpackage](../../../tools/sqlpackage.md#publish-parameters-properties-and-sqlcmd-variables) の[データ層アプリケーションのアップグレード ウィザード](../../data-tier-applications/upgrade-a-data-tier-application.md#UsingDACUpgradeWizard)を使用して、DACPAC を発行できます。

この記事では、DACPAC またはターゲット データベースに [Always Encrypted](always-encrypted-database-engine.md) で保護された列が含まれる場合に、データベースをアップグレードするための特別な考慮事項について説明します。 DACPAC 内の列の暗号化スキームが、ターゲット データベースの既存の列の暗号化スキームと異なる場合、DACPAC を発行すると、列に格納されているデータの暗号化、暗号化解除、または再暗号化が行われます。 詳細については、次の表を参照してください。

| 条件|操作|
|:---|:---|
|列は、DACPAC では暗号化され、データベースでは暗号化されていません。| 列のデータは暗号化されます。|
|列は、DACPAC では暗号化されておらず、データベースでは暗号化されています。| 列のデータは暗号化解除されます (列の暗号化は解除されます)。|
| DACPAC とデータベースの両方で列は暗号化されていますが、DACPAC の列で使用される暗号化の種類および/または列暗号化キーは、データベースの対応する列の場合と異なっています。|列のデータは暗号化解除され、DACPAC の暗号化の構成に一致するように再び暗号化されます。|

また、DAC パッケージをデプロイすると、Always Encrypted の列マスター キーまたは列暗号化キーのメタデータ オブジェクトが作成または削除されることがあります。

## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項
暗号化操作を実行するには、DACPAC をデプロイするために使用するツールにより、データをデータベースから移動する必要があります。 このツールでは、データベース内で必要な暗号化構成を使用して新しい 1 つまたは複数のテーブルが作成され、元のテーブルからすべてのデータが読み込まれ、要求された暗号化操作が実行され、データを新しいテーブルにアップロードされた後、元のテーブルが新しいテーブルに入れ替えられます。 暗号化操作の実行には時間がかかる場合があります。 その間、データベースでトランザクションを書き込むことはできません。 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] を使用し、SQL Server インスタンスがセキュア エンクレーブで構成されている場合は、データベースからデータを移動せずに、暗号化操作をインプレースで実行できます。 「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)」を参照してください。 DACPAC のデプロイでは、インプレース暗号化は使用できないことに注意してください。

::: moniker-end

## <a name="permissions-for-publishing-a-dac-package-if-always-encrypted-is-set-up"></a>Always Encrypted がセットアップされている場合に DAC パッケージを発行するための権限

DACPAC またはターゲット データベースで Always Encrypted がセットアップされている場合に DAC パッケージを発行するには、DACPAC 内のスキーマとターゲット データベースのスキーマとの違いに応じて、次に示す権限の一部またはすべてが必要になる場合があります。

*ALTER ANY COLUMN MASTER KEY*、 *ALTER ANY COLUMN ENCRYPTION KEY*、 *VIEW ANY COLUMN MASTER KEY DEFINITION*、 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*

アップグレード操作によってデータ暗号化操作がトリガーされる場合、影響を受ける列に対して構成された列マスター キーにアクセスできることも必要です。

- **証明書ストア – ローカル コンピューター** - 列マスター キーとして使用される証明書への読み取りアクセス権を持っているか、コンピューターの管理者である必要があります。
- **Azure Key Vault** - 列マスター キーが格納されている資格情報コンテナーに対する *create*、*get*、*unwrapKey*、*wrapKey*、*sign*、および *verify* 権限が必要です。
- **キー ストア プロバイダー (CNG)** - キー ストアまたはキーを使用する際には、ストアと KSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。
- **暗号化サービス プロバイダー (CAPI)** - キー ストアまたはキーを使用する際には、ストアと CSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。

詳細については、 [列マスター キーの作成と格納 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) を参照してください。 

 
## <a name="next-steps"></a>Next Steps
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)
- [SQL Server Management Studio で Always Encrypted を使用した列にクエリを実行する](always-encrypted-query-columns-ssms.md)

## <a name="see-also"></a>参照  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Always Encrypted のキー管理の概要](overview-of-key-management-for-always-encrypted.md) 
 - [SQL Server Management Studio を使用した Always Encrypted の構成](configure-always-encrypted-using-sql-server-management-studio.md)
 - [Always Encrypted ウィザードを使用した列暗号化の構成](always-encrypted-wizard.md)
 - [PowerShell での Always Encrypted を使用した列暗号化の構成](configure-column-encryption-using-powershell.md)
 
