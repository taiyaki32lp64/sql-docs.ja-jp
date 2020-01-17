---
title: SQL Server Management Studio を使用した Always Encrypted キーのプロビジョニング | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 13bb5944c5907f3bebc9f01eb969b4b8979f8c97
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595757"
---
# <a name="provision-always-encrypted-keys-using-sql-server-management-studio"></a>SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

この記事では、[SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md) を使用して、Always Encrypted の列マスター キーと列暗号化キーをプロビジョニングするための手順について説明します。

推奨されるベスト プラクティスやセキュリティ上の重要な考慮事項など、Always Encrypted のキー管理の概要については、「[Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)」をご覧ください。

<a name="provisioncmk"></a>
## <a name="provision-column-master-keys-with-the-new-column-master-key-dialog"></a>[新しい列マスター キー] ダイアログを使用して列マスター キーをプロビジョニングする

**[新しい列マスター キー]** ダイアログでは、列マスター キーを生成することも、キー ストア内の既存のキーを選択することもできます。さらに、作成または選択したキーに対して列マスター キーのメタデータをデータベースに作成することができます。

1.  **オブジェクト エクスプローラー**を使用し、データベースの下の **[セキュリティ]、[Always Encrypted キー]** の順にアクセスします。
2.  **[列マスター キー]** フォルダーを右クリックし、**[新しい列マスター キー...]** を選択します。 
3.  **[新しい列マスター キー]** ダイアログで、列マスター キーのメタデータ オブジェクトの名前を入力します。
4.  キー ストアを選択します。
    - **証明書ストア - 現在のユーザー** - Windows 証明書ストアでの現在のユーザーの証明書ストアの場所を示します。これは個人的なストアです。 
    - **証明書ストア - ローカル コンピューター** - Windows 証明書ストアでのローカル コンピューターの証明書ストアの場所を示します。 
    - **Azure Key Vault** - Azure にサインインする必要があります (**[サインイン]** をクリック)。 サインインすると、ご自分の Azure サブスクリプションのいずれかと、キー コンテナーを選択できるようになります。
    - **キー ストア プロバイダー (KSP)** - Cryptography Next Generation (CNG) API を実装するキー ストア プロバイダー (KSP) を介してアクセスできるキー ストアを示します。 通常、この種のストアは、ハードウェア セキュリティ モジュール (HSM) となります。 このオプションを選択したら、KSP を選択する必要があります。 既定では、**Microsoft ソフトウェア キー ストア プロバイダー** が選択されます。 HSM に格納されている列マスター キーを使用する場合は、デバイス用の KSP を選択します (ダイアログを開く前に、コンピューターにインストールし、構成しておく必要があります)。
    -   **暗号化サービス プロバイダー (CSP)** - 暗号化 API (CAPI) を実装する暗号化サービス プロバイダー (CSP) を介してアクセスできるキー ストアです。 通常、そのようなストアは、ハードウェア セキュリティ モジュール (HSM) です。 このオプションを選択したら、CSP を選択する必要があります。  HSM に格納されている列マスター キーを使用する場合は、デバイス用の CSP を選択します (ダイアログを開く前に、コンピューターにインストールし、構成しておく必要があります)。
    
    > [!NOTE]
    > CAPI は非推奨の API であるため、既定では暗号化サービス プロバイダー (CAPI) オプションは無効になります。 これを有効にするには、Windows レジストリの **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** キーの下に CAPI Provider Enabled DWORD 値を作成し、これを 1 に設定します。 キー ストアで CNG がサポートされていない場合は、CAPI ではなく CNG を使用する必要があります。
   
    上記のキー ストアの詳細については、「[Always Encrypted の列マスター キーの作成と保存](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)」をご覧ください。

5. お客様が [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] を使用していて、お使いの SQL Server インスタンスがセキュア エンクレーブを使って構成されている場合は、**[エンクレーブ計算を許可する]** チェックボックスをオンにして、マスター キーをエンクレーブ対応にすることができます。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](always-encrypted-enclaves.md)」をご覧ください。 

    > [!NOTE]
    > お使いの SQL Server インスタンスがセキュア エンクレーブを使って正しく構成されていない場合は、**[エンクレーブ計算を許可する]** チェックボックスは表示されません。

6.  キー ストアにある既存のキーを選択するか、あるいは **[キーの生成]** ボタンまたは **[証明書の生成]** ボタンをクリックしてキー ストアにキーを作成します。 
7.  **[OK]** をクリックします。新しいキーが一覧に表示されます。 

ダイアログを完了すると、SQL Server Management Studio によって、データベースに列マスター キーのメタデータが作成されます。 ダイアログでこれを実現するには、 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) ステートメントを生成し発行します。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

エンクレーブ対応の列マスター キーを構成する場合は、SSMS により、そのメタデータも列マスター キーを使って署名されます。 

::: moniker-end

### <a name="permissions-for-provisioning-a-column-master-key"></a>列マスター キーをプロビジョニングするための権限

ダイアログを使って列マスター キーを作成するためには、そのデータベースで、*ALTER ANY COLUMN MASTER KEY* データベース権限が必要です。 ダイアログを使用して新しい列マスター キーを作成するか、キー ストア作成の既存のキーを使用する場合は、キー ストアやキーに対する権限が必要になることがあります。
- **証明書ストア - ローカル コンピューター** - 列マスター キーとして使用される証明書への読み取りアクセス権を持っているか、コンピューターの管理者である必要があります。
- **Azure Key Vault** - キーを選択して使用するための *get* および *list* 権限と、新しいキーを作成するための *create* 権限が必要です。 エンクレーブ対応の列マスター キーを構成する場合は、キーのメタデータの署名を生成するための *sign* 権限も必要です。
- **キー ストア プロバイダー (CNG)** - キー ストアまたはキーを使用する際には、ストアと KSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。
- **暗号化サービス プロバイダー (CAPI)** - キー ストアまたはキーを使用する際には、ストアと CSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。

詳細については、「[Always Encrypted の列マスター キーの作成と保存](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)」をご覧ください。

<a name="provisioncek"></a> 
## <a name="provision-column-encryption-keys-with-the-new-column-encryption-key-dialog"></a>[新しい列の暗号化キー] ダイアログを使用して列の暗号化キーをプロビジョニングする

**[新しい列の暗号化キー]** ダイアログでは、列暗号化キーを生成し、それを列マスター キーで暗号化し、データベースに列暗号化キーのメタデータを作成することができます。

1.  **オブジェクト エクスプローラー**を使用して、データベースの下にあるフォルダーを **[セキュリティ]、[Always Encrypted キー]** の順に移動します。
2.  **[列暗号化キー]** フォルダーを右クリックし、**[新しい列の暗号化キー...]** を選択します。 
3.  **[新しい列の暗号化キー]** ダイアログで、列暗号化キーのメタデータ オブジェクトの名前を入力します。
4.  データベースの列マスター キーを表すメタデータ オブジェクトを選択します。
5.  [**OK**] をクリックします。 

ダイアログを完了すると、SQL Server Management Studio によって新しい列暗号化キーが生成され、選択した列マスター キーのメタデータがデータベースから取得されます。 次に、SSMS では、列マスター キーのメタデータを使って、その列マスター キーを含むキー ストアとの交信が行われ、列暗号化キーが暗号化されます。 最後に、[CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) ステートメントを生成して発行することで、SSMS によって新しい列暗号化のメタデータ データがデータベースに作成されます。

### <a name="permissions-for-provisioning-a-column-encryption-key"></a>列暗号化キーをプロビジョニングするためのアクセス許可

ダイアログを使って列暗号化キーのメタデータを作成し、列マスター キーのメタデータにアクセスするには、*ALTER ANY COLUMN ENCRYPTION KEY* および *VIEW ANY COLUMN MASTER KEY DEFINITION* データベース権限が必要です。
キー ストアにアクセスして、列マスター キーを使用するには、キー ストアとキーの両方、またはそのいずれかに対する権限が必要な場合があります。
- **証明書ストア - ローカル コンピューター** - 列マスター キーとして使用される証明書への読み取りアクセス権を持っているか、コンピューターの管理者である必要があります。
- **Azure Key Vault** - 列マスター キーが格納されている資格情報コンテナーに対して *get*、*unwrapKey*、*wrapKey*、*sign*、および *verify* の権限が必要です。
- **キー ストア プロバイダー (CNG)** - キー ストアまたはキーを使用する際には、ストアと KSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。
- **暗号化サービス プロバイダー (CAPI)** - キー ストアまたはキーを使用する際には、ストアと CSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。

詳細については、[列マスター キーの作成と保存 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) に関する記事をご覧ください。

## <a name="provision-always-encrypted-keys-using-the-always-encrypted-wizard"></a>Always Encrypted ウィザードを使って Always Encrypted キーをプロビジョニングする

[Always Encrypted ウィザード](../../../relational-databases/security/encryption/always-encrypted-wizard.md)は、選択したデータベースの列の暗号化、暗号化解除、および再暗号化を行うためのツールです。 そこでは、既に構成されているキーを使用できますが、新しい列マスター キーと新しい列暗号化を生成することもできます。 

## <a name="next-steps"></a>Next Steps
- [Always Encrypted ウィザードを使用した列暗号化の構成](always-encrypted-wizard.md)
- [DAC パッケージでの Always Encrypted を使用した列暗号化の構成](configure-always-encrypted-using-dacpac.md)
- [SQL Server Management Studio を使用して Always Encrypted キーを交換する](rotate-always-encrypted-keys-using-ssms.md)
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)
- [SQL Server インポートおよびエクスポート ウィザードでの Always Encrypted を使用した列間でのデータの移行](always-encrypted-migrate-using-import-export-wizard.md)

## <a name="see-also"></a>参照
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Always Encrypted の列マスター キーの作成と保存](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [SQL Server Management Studio を使用した Always Encrypted の構成](configure-always-encrypted-using-sql-server-management-studio.md)
- [PowerShell を使用した Always Encrypted キーのプロビジョニング](configure-always-encrypted-keys-using-powershell.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
