---
title: Always Encrypted ウィザードを使用して列暗号化を構成する | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.alwaysencryptedwizard.encryption.f1
- sql13.swb.alwaysencryptedwizard.f1
- sql13.swb.alwaysencryptedwizard.masterkey.f1
helpviewer_keywords:
- Wizard, Always Encrypted
ms.assetid: 68daddc9-ce48-49aa-917f-6dec86ad5af5
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 71df93e5e7d628fadf5839e980f42a92138a5e0c
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594505"
---
# <a name="configure-column-encryption-using-always-encrypted-wizard"></a>Always Encrypted ウィザードを使用して列暗号化を構成する
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Always Encrypted ウィザードは、選択したデータベースの列に対して目的の [Always Encrypted](always-encrypted-database-engine.md) の構成を設定することができる強力なツールです。 現在の構成と目的の構成に応じて、ウィザードでは、列を暗号化したり、列の暗号化を解除したり (解読)、列を再暗号化 (たとえば、新しい列暗号化キーの使用や、列に構成された現在のものとは種類が異なる暗号化の使用) したりできます。 ウィザードの 1 回の実行で、複数の列を構成することができます。

ウィザードを使うと、既存の列暗号化キーを使用して列を暗号化したり、新しい列暗号化キーまたは新しい列暗号化キーと新しい列マスター キーの両方を生成したりすることもできます。 

ウィザードにより、データはデータベースの外に移動されて、SSMS プロセス内で暗号化操作を実行されます。 このウィザードでは、データベース内で必要な暗号化構成を使用して新しい 1 つまたは複数のテーブルが作成され、元のテーブルからすべてのデータが読み込まれ、要求された暗号化操作が実行され、データを新しいテーブルにアップロードされた後、元のテーブルが新しいテーブルに入れ替えられます。

> [!NOTE]
> 暗号化操作の実行には時間がかかる場合があります。 その間、データベースでトランザクションを書き込むことはできません。 大きなテーブルに対する暗号化操作には、PowerShell が推奨されるツールです。 「[PowerShell での Always Encrypted を使用した列暗号化の構成](configure-column-encryption-using-powershell.md)」をご覧ください。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] を使用していて、お使いの SQL Server インスタンスがセキュリティで保護されたエンクレーブで構成されている場合は、データベースからデータを移動せずに、暗号化操作をインプレースで実行できます。 「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)」を参照してください。 ウィザードでは、インプレース暗号化がサポートされていないことに注意してください。

::: moniker-end

PowerShell を使用することをお勧めします 

 - ウィザードを使用して Always Encrypted を構成し、それをクライアント アプリケーションで使用する方法を説明したエンドツーエンドのチュートリアルについては、以下の Azure SQL Database チュートリアルをご覧ください。
    - [Always Encrypted と Windows 証明書ストアの列マスター キーを使用して Azure SQL Database 内の機密データを保護する](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)
    - [Always Encrypted と Azure Key Vault の列マスター キーを使用して Azure SQL Database 内の機密データを保護する](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted-azure-key-vault)

 - ウィザードの利用方法を含む動画が必要な場合、「 [Keeping Sensitive Data Secure with Always Encrypted (Always Encrypted で機密データを守る)](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)」をご覧ください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セキュリティ チームのブログ「 [SSMS Encryption Wizard - Enabling Always Encrypted in a Few Easy Steps](https://techcommunity.microsoft.com/t5/SQL-Server/SSMS-Encryption-Wizard-Enabling-Always-Encrypted-in-a-Few-Easy/ba-p/384545)」(SSMS 暗号化ウィザード - 数回の手順で Always Encrypted を有効にする) も参照してください。  
 - Always Encrypted キーについて詳しくは、「[Always Encrypted のキー管理の概要](overview-of-key-management-for-always-encrypted.md)」をご覧ください。
 - Always Encrypted でサポートされる暗号化の種類について詳しくは、「[明確な暗号化またはランダム化された暗号化の選択](always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)」をご覧ください。
 
 ## <a name="permissions"></a>アクセス許可
ウィザードを使って暗号化操作を実行するには、**VIEW ANY COLUMN MASTER KEY DEFINITION** および **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** のアクセス許可が必要です。 また、キーが保持されているキー ストア内にある、使用している列マスター キーにアクセスするためのアクセス許可も必要です。
- **証明書ストア – ローカル コンピューター** - 列マスター キーとして使用される証明書への読み取りアクセス権を持っているか、コンピューターの管理者である必要があります。
- **Azure Key Vault** - 列マスター キーが格納されている資格情報コンテナーに対する get、unwrapKey、および verify の権限が必要です。
- **キー ストア プロバイダー (CNG)** - キー ストアまたはキーを使用する際には、ストアと KSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。
- **暗号化サービス プロバイダー (CAPI)** - キー ストアまたはキーを使用する際には、ストアと CSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。

さらに、ウィザードを使用して新しいキーを作成する場合は、「[[新しい列マスター キー] ダイアログを使用して列マスター キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)」および「[[新しい列の暗号化キー] ダイアログを使用して列の暗号化キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)」の一覧で示されている追加のアクセス許可が必要です。

## <a name="open-the-always-encrypted-wizard"></a>Always Encrypted ウィザードを開く
3 つの異なるレベルでウィザードを起動できます。 
- データベース レベル - 異なるテーブルに存在する複数の列を暗号化する場合。
- テーブル レベル - 同じテーブルに存在する複数の列を暗号化する場合。
- 列レベル - 1 つの特定の列を暗号化する場合。
 
 1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のオブジェクト エクスプローラー コンポーネントで [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]に接続します。  
   
 2. 暗号化を行います。
     1. 1 つのデータベースの異なるテーブルに存在する複数の列を暗号化するには、データベースを右クリックし、 **[タスク]** をポイントして、 **[列の暗号化]** を選択します。
     1. 同じテーブルに存在する複数の列を暗号化するには、テーブルに移動して右クリックし、 **[列の暗号化]** を選択します。
     1. 個々の列を暗号化するには、列に移動して右クリックし、 **[列の暗号化]** を選択します。


   
 ## <a name="column-selection-page"></a>列の選択ページ
このページでは、暗号化、再暗号化、または暗号化解除する列を選択し、選択した列に対するターゲットの暗号化構成を定義します。

プレーンテキスト列 (暗号化されていない列) を暗号化するには、列の暗号化の種類 ( **[決定論的]** または **[ランダム化]** ) と暗号化キーを選択します。 

既に暗号化されている列の暗号化の種類を変更したり、列暗号化キーをローテーション (変更) したりするには、目的の暗号化の種類とキーを選択します。 

ウィザードで新しい列暗号化キーを使用して 1 つまたは複数の列を暗号化または再暗号化する場合は、名前に **(New)** が含まれるキーを選択します。 ウィザードによってキーが生成されます。

現在暗号化されている列の暗号化を解除するには、暗号化の種類として **[プレーン テキスト]** を選択します。


> [!NOTE]
> ウィザードでは、テンポラル テーブルとインメモリ テーブルに対する暗号化操作はサポートされていません。 Transact-SQL を使って空のテンポラル テーブルまたはインメモリ テーブルを作成し、アプリケーションを使ってデータを挿入できます。

## <a name="master-key-configuration-page"></a>マスター キーの構成ページ
前のページでいずれかの列に対して自動生成された列暗号化キーを選択した場合、このページでは、既存の列マスター キーを選択するか、列暗号化キーを暗号化する新しい列マスター キーを構成する必要があります。 

新しい列マスター キーを構成するときは、Windows 証明書ストアまたは Azure Key Vault で既存のキーを選択し、ウィザードを使ってデータベース内のキーに対するメタデータ オブジェクトだけを作成するか、キーとデータベース内のキーを記述するメタデータ オブジェクトの両方を生成することができます。 

列マスター キーを作成し、Windows 証明書ストア、Azure Key Vault、または他のキー ストアに格納する方法について詳しくは、「[Always Encrypted の列マスター キーを作成して保存する](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)」をご覧ください。

> [!TIP]
> このウィザードでは、Windows 証明書ストアおよび Azure Key Vault のキーだけを参照および作成できます。 また、新しいキーとキーを記述するデータベース メタデータ オブジェクトの両方の名前が自動生成されます。 キーのプロビジョニング方法をより詳細に制御する必要がある場合 (および列マスター キーを格納したキー ストアの選択肢がもっと必要である場合) は、 **[新しい列マスター キー]** ダイアログと **[新しい列の暗号化キー]** ダイアログを使用して最初にキーを作成した後、ウィザードを実行して作成したキーを選択します。 「[[新しい列マスター キー] ダイアログを使用して列マスター キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)」および「[[新しい列の暗号化キー] ダイアログを使用して列の暗号化キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)」をご覧ください。 

## <a name="next-steps"></a>Next Steps
- [SQL Server Management Studio で Always Encrypted を使用した列のクエリを実行する](always-encrypted-query-columns-ssms.md)
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)

## <a name="see-also"></a>参照  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Always Encrypted のキー管理の概要](overview-of-key-management-for-always-encrypted.md) 
 - [SQL Server Management Studio を使用した Always Encrypted の構成](configure-always-encrypted-using-sql-server-management-studio.md)
 - [PowerShell を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-powershell.md)
 - [PowerShell での Always Encrypted を使用した列暗号化の構成](configure-column-encryption-using-powershell.md)
 - [DAC パッケージでの Always Encrypted を使用した列暗号化の構成](configure-always-encrypted-using-dacpac.md)
