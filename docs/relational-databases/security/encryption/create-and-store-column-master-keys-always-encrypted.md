---
title: Always Encrypted の列マスター キーを作成して保存する
description: キー ストアを選択し、SQL Server Always Encrypted の列マスター キーを作成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 856e8061-c604-4ce4-b89f-a11876dd6c88
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 63be7df50b6dd590d0ec90346d27f6601e15cf45
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557839"
---
# <a name="create-and-store-column-master-keys-for-always-encrypted"></a>Always Encrypted の列マスター キーを作成して保存する
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

*列マスター キー* は、Always Encrypted で列暗号化キーの暗号化に使用される、キー保護用キーです。 列マスター キーは信頼できるキー ストアに格納する必要があり、キーはデータの暗号化または暗号化解除に必要なアプリケーション、および Always Encrypted の構成および Always Encrypted キーの管理のためのツールにアクセスできる必要があります。

この記事では、キー ストアの選択、および Always Encrypted の列マスター キーの作成について説明します。 詳細な概要については、「 [Overview of Key Management for Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)」(Always Encrypted のキー管理の概要) を参照してください。

## <a name="selecting-a-key-store-for-your-column-master-key"></a>列マスター キーのキー ストアを選択する

Always Encrypted は、Always Encrypted の列マスター キーを格納するための複数のキー ストアをサポートしています。 サポートされるキー ストアは、使用しているドライバーとバージョンによって異なります。

キー ストアでは 2 つの大きなカテゴリを考慮する必要があります。 *ローカル キー ストア*と、 *集中型キー ストア*です。

###  <a name="local-or-centralized-key-store"></a>ローカル キー ストアと集中型キー ストアとは?

* **ローカル キー ストア** - ローカル キー ストアを含むコンピューター上のアプリケーションでのみ使用できます。 つまり、キー ストアおよびキーを、アプリケーションを実行している各コンピューターに複製する必要があります。 ローカル キー ストアの例が、Windows 証明書ストアです。 ローカル キー ストアを使用する場合は、キー ストアがアプリケーションをホストしている各コンピューターに存在していること、およびアプリケーションが Always Encrypted を使用して保護されたデータにアクセスするために必要な列マスター キーがそのコンピューターに含まれていることを確認する必要があります。 初めて列マスター キーを指定した場合、またはキーを変更 (回転) した場合は、アプリケーションをホストしているすべてのコンピューターにキーが展開されていることを確認する必要があります。

* **集中型キー ストア** - 複数のコンピューター上でアプリケーションを提供します。 集中型キー ストアの例が、 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/)です。 通常は、集中型キー ストアによりキー管理が容易になります。これは、複数のコンピューターにある列マスター キーの複数のコピーを維持する必要がないためです。 アプリケーションが集中型キー ストアに接続するように構成されていることを確認します。

### <a name="which-key-stores-are-supported-in-always-encrypted-enabled-client-drivers"></a>Always Encrypted が有効なクライアント ドライバーではどのキー ストアがサポートされていますか?

Always Encrypted が有効なクライアント ドライバーは Always Encrypted をクライアント アプリケーションに組み込むためのサポートが組み込まれた SQL Server クライアント ドライバーです。 Always Encrypted が有効なドライバーには、一般的なキー ストアの組み込みのプロバイダーがいくつか含まれています。 ドライバーによっては、プロバイダーが組み込まれていなくても任意のキー ストアを使用できるように、カスタム列マスター キー ストアのプロバイダーを実装して登録することが求められる場合もあります。 組み込みのプロバイダーとカスタムのプロバイダーのどちらにするかを決める場合、通常は組み込みのプロバイダーを使用した方が、アプリケーションへの変更が少なくなることに留意してください (場合によっては、データベース接続文字列の変更のみが必要となります)。

利用可能な組み込みのプロバイダーは、選択されているドライバー、ドライバーのバージョン、オペレーティング システムによって異なります。  追加設定なしでサポートされるキー ストアがどれか、ドライバーがカスタム キー ストアのプロバイダーをサポートしているかどうかを判断するには、Always Encrypted のドキュメントでお使いのドライバーについて確認してください ([Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)」)。

### <a name="which-key-stores-are-supported-in-sql-tools"></a>SQL ツールではどのキー ストアがサポートされていますか?
SQL Server Management Studio および SqlServer PowerShell モジュールでは、Azure Key Vault、Windows 証明書ストア、および Cryptography Next Generation (CNG) API または Cryptography API (CAPI) を提供するキー ストアに格納されている列マスター キーのみが、サポートされています。 

## <a name="creating-column-master-keys-in-windows-certificate-store"></a>Windows 証明書ストアで列マスター キーを作成する    

列マスター キーを、Windows 証明書ストアに格納された証明書にすることができます。 Always Encrypted が有効なドライバーを使うと、有効期限や証明機関チェーンは検証されません。 証明書は、単に公開および秘密キーで構成されるキーのペアとして使用されます。

有効な列マスター キーであるためには、証明書が次を満たす必要があります。
* X.509 証明書である。
* が、2 つの証明書ストアの場所 ( *ローカル コンピューター* または *現在のユーザー*) のどちらかに保存されている (証明書をローカル コンピューターの証明書ストアの場所に作成するには、対象のコンピューターの管理者である必要があります)。
* 秘密キーを含む (証明書のキーで推奨される長さは 2048 ビット以上)。
* が、キー交換のために作成されている。


有効な列マスター キーである証明書を作成する方法はいくつかありますが、最も簡単なオプションは、自己署名証明書を作成する方法です。


### <a name="create-a-self-signed-certificate-using-powershell"></a>PowerShell を使用して自己署名証明書を作成する

[New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate) コマンドレットを使用して、自己署名証明書を作成します。 次の例は、Always Encrypted の列マスター キーとして使用できる証明書を生成する方法を示します。

```
# New-SelfSignedCertificate is a Windows PowerShell cmdlet that creates a self-signed certificate. The below examples show how to generate a certificate that can be used as a column master key for Always Encrypted.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048 

# To create a certificate in the local machine certificate store location you need to run the cmdlet as an administrator.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:LocalMachine\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048
```

### <a name="create-a-self-signed-certificate-using-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) を使用して自己署名証明書を作成する

詳しくは、「[SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)」をご覧ください。
SSMS を使用し、Windows 証明書ストアに Always Encrypted キーを格納するためのチュートリアルは、「 [Always Encrypted - データベース暗号化を使用して SQL Database で機密データを保護し、Windows 証明書ストアで暗号化キーを格納する](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)」を参照してください。


### <a name="making-certificates-available-to-applications-and-users"></a>証明書をアプリケーションとユーザーが使用できるようにする

列マスター キーが *ローカル コンピューター* の証明書ストアの場所に格納された証明書である場合、秘密キーを使用して証明書をエクスポートしてから、暗号化された列に格納されたデータの暗号化または暗号化解除を行うアプリケーション、または Always Encrypted の構成および Always Encrypted キーの管理を行うツールをホストするすべてのコンピューターに証明書をインポートする必要があります。 また、証明書を列マスター キーとして使用できるように、ローカル コンピューターの証明書ストアの場所に格納された証明書に対する読み取りアクセス許可を各ユーザーに付与する必要があります。

列マスター キーが *現在のユーザー* の証明書ストアの場所に格納された証明書である場合、秘密キーを使用して証明書をエクスポートしてから、暗号化された列に格納されたデータの暗号化または暗号化解除を行うアプリケーション、または Always Encrypted の構成および Always Encrypted キーの管理を行うツールを実行しているすべてのユーザー アカウントの、(該当するアプリケーション/ツールを含むすべてのコンピューター上の) 現在のユーザーの証明書ストアの場所に、証明書をインポートする必要があります。 アクセス許可の構成は不要です。コンピューターにログオンしたら、ユーザーは現在のユーザーの証明書ストアの場所にあるすべての証明書にアクセスすることができます。

#### <a name="using-powershell"></a>PowerShell の使用
証明書のインポートとエクスポートには、 [Import-PfxCertificate](/powershell/module/pkiclient/import-pfxcertificate) と [Export-PfxCertificate](/powershell/module/pkiclient/export-pfxcertificate) コマンドレットを使用します。

#### <a name="using-microsoft-management-console"></a>Microsoft 管理コンソールを使用する 

ユーザーに、ローカル コンピューターの証明書ストアの場所に格納されている証明書に対する *読み取り* アクセス許可を付与するには、次の手順を実行します。

1.  コマンド プロンプトを開き、「 **mmc**」と入力します。
2.  MMC コンソールの **[ファイル]** メニューで、 **[スナップインの追加と削除]** をクリックします。
3.  **[スナップインの追加と削除]** ダイアログ ボックスで **[追加]** をクリックします。
4.  **[スタンドアロン スナップインの追加]** ダイアログ ボックスで **[証明書]** をクリックし、次に **[追加]** をクリックします。
5.  **[証明書スナップイン]** ダイアログ ボックスで **[コンピューター アカウント]** をクリックし、 **[完了]** をクリックします。
6.  **[スタンドアロン スナップインの追加]** ダイアログ ボックスで **[閉じる]** をクリックします。
7.  **[スナップインの追加と削除]** ダイアログ ボックスで **[OK]** をクリックします。
8.  **[証明書]** スナップインで、 **[証明書] > [個人]** フォルダーで証明書を探し、その証明書を右クリックします。次に **[すべてのタスク]** をポイントし、 **[秘密キーの管理]** をクリックします。
9.  **[セキュリティ]** ダイアログ ボックスで、必要に応じてユーザー アカウントの読み取りアクセス許可を追加します。

## <a name="creating-column-master-keys-in-azure-key-vault"></a>Azure Key Vault で列マスター キーを作成する

Azure Key Vault は、暗号化キーやシークレットの保護に役立ちます。特に、アプリケーションが Azure でホストされている場合、Always Encrypted の列マスター キーの格納には便利なオプションです。 [Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)でキーを作成するには、 [Azure サブスクリプション](https://azure.microsoft.com/free/) および Azure Key Vault が必要です。

### <a name="using-powershell"></a>PowerShell の使用

次の例は、新しい Azure Key Vault とキーを作成し、目的のユーザーにアクセス許可を付与しています。

```
# Create a column master key in Azure Key Vault.
Connect-AzAccount
$SubscriptionId = "<Azure subscription ID>"
$resourceGroup = "<resource group name>"
$azureLocation = "<key vault location>"
$akvName = "<key vault name>"
$akvKeyName = "<column master key name>"
$azureCtx = Set-AzContext -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation -SKU premium # Creates a new key vault - skip if your vault already exists.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey, unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination HSM
```

### <a name="using-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) の使用

SSMS を使用して Azure Key Vault で列マスター キーを作成する方法について詳しくは、「[SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)」をご覧ください。
SSMS を使用し、Azure Key Vault に Always Encrypted キーを格納するためのチュートリアルは、「 [Always Encrypted - データベース暗号化を使用して SQL Database で機密データを保護し、Windows 証明書ストアで暗号化キーを格納する](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault)」を参照してください。

### <a name="making-azure-key-vault-keys-available-to-applications-and-users"></a>Azure Key Vault のキーをアプリケーションとユーザーが使用できるようにする

Azure Key Vault のキーを列のマスター キーとして使用する場合、アプリケーションが Azure を認証し、アプリケーションの ID がキー コンテナーに対する次の権限を持っている必要があります: *get*、*unwrapKey*、*verify*。 

Azure Key Vault に格納されている列マスター キーで保護されている列暗号化キーをプロビジョニングするには、 *get*、 *unwrapKey*、 *wrapKey*、 *sign*、および *verify* の権限が必要です。 さらに、Azure Key Vault に新しいキーを作成するには *create* の権限、Key Vault の内容を一覧するには *list* の権限が必要です。

#### <a name="using-powershell"></a>PowerShell の使用

Azure Key Vault 内の実際のキーへのユーザーおよびアプリケーションによるアクセスを有効にするには、コンテナーのアクセス ポリシーを設定する必要があります ([Set-AzKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy))。

```
$vaultName = "<vault name>"
$resourceGroupName = "<resource group name>"
$userPrincipalName = "<user to grant access to>"
$clientId = "<client Id>"

# grant users permissions to the keys:
Set-AzKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
# grant applications permissions to the keys:
Set-AzKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list
```

## <a name="creating-column-master-keys-in-hardware-security-modules-using-cng"></a>CNG を使用してハードウェア セキュリティ モジュールに列マスター キーを作成する

Always Encrypted の列マスター キーは、Cryptography Next Generation (CNG) API を実装するキー ストアに格納することができます。 通常、この種のストアは、ハードウェア セキュリティ モジュール (HSM) となります。 HSM はデジタルのキーを安全に管理し、暗号化処理を提供する物理デバイスです。 HSM は、プラグイン カードまたはコンピューター (ローカルの HSM) またはネットワークサーバーに直接接続する外部デバイスの形で提供されることになっています。

特定のコンピューターのアプリケーションから HSM を使用できるようにするには、CNG を実装するキー記憶域プロバイダー (KSP) をコンピューターにインストールして構成する必要があります。 Always Encrypted のクライアント ドライバー (ドライバー内部の列マスター キー ストア プロバイダー) は KSP を使用して、キー ストアに格納された列マスター キーで保護されている列暗号化キーを暗号化および暗号化解除します。

Windows にはソフトウェアベースの KSP である Microsoft ソフトウェア キー記憶域プロバイダーが含まれており、テスト目的で使用することができます。 「 [CNG Key Storage Providers](/windows/desktop/SecCertEnroll/cng-key-storage-providers)」(CNG キー記憶域プロバイダー) を参照してください。

### <a name="creating-column-master-keys-in-a-key-store-using-cngksp"></a>CNG/KSP を使用してキー ストア内の列マスター キーを作成する

列マスター キーは、RSA アルゴリズムを使用する非対称キー (公開/秘密キーのペア) にする必要があります。 推奨されるキーの長さは 2048 文字以上です。

#### <a name="using-hsm-specific-tools"></a>HSM 固有ツールの使用
HSM のドキュメントを参照してください。

#### <a name="using-powershell"></a>PowerShell の使用

.NET API を使用すると、PowerShell で CNG を使用してキー ストアにキーを作成することができます。


```
$cngProviderName = "Microsoft Software Key Storage Provider" # If you have an HSM, you can use a KSP for your HSM instead of a Microsoft KSP
$cngAlgorithmName = "RSA"
$cngKeySize = 2048 # Recommended key size for Always Encrypted column master keys
$cngKeyName = "AlwaysEncryptedKey" # Name identifying your new key in the KSP
$cngProvider = New-Object System.Security.Cryptography.CngProvider($cngProviderName)
$cngKeyParams = New-Object System.Security.Cryptography.CngKeyCreationParameters
$cngKeyParams.provider = $cngProvider
$cngKeyParams.KeyCreationOptions = [System.Security.Cryptography.CngKeyCreationOptions]::OverwriteExistingKey
$keySizeProperty = New-Object System.Security.Cryptography.CngProperty("Length", [System.BitConverter]::GetBytes($cngKeySize), [System.Security.Cryptography.CngPropertyOptions]::None);
$cngKeyParams.Parameters.Add($keySizeProperty)
$cngAlgorithm = New-Object System.Security.Cryptography.CngAlgorithm($cngAlgorithmName)
$cngKey = [System.Security.Cryptography.CngKey]::Create($cngAlgorithm, $cngKeyName, $cngKeyParams)
```

#### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio を使用する

「[SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)」をご覧ください。

### <a name="making-cng-keys-available-to-applications-and-users"></a>CNG のキーをアプリケーションとユーザーが使用できるようにする

コンピューターに KSP を構成する方法、およびアプリケーションとユーザーに HSM へのアクセス権を付与する方法については、HSM および KSP のドキュメントを参照してください。

## <a name="creating-column-master-keys-in-hardware-security-modules-using-capi"></a>CAPI を使用してハードウェア セキュリティ モジュールに列マスター キーを作成する

Always Encrypted の列マスター キーは、Cryptography API (CAPI) を実装するキー ストアに格納することができます。 通常は、デジタルのキーを安全に管理し、暗号化処理を提供する物理デバイスであるハードウェア セキュリティ モジュール (HSM) のようなストアがこれに含まれます。 HSM は、プラグイン カードまたはコンピューター (ローカルの HSM) またはネットワークサーバーに直接接続する外部デバイスの形で提供されることになっています。

特定のコンピューターのアプリケーションから HSM を使用できるようにするには、CAPI を実装する Cryptography Service Provider (CSP) をコンピューターにインストールして構成する必要があります。 Always Encrypted のクライアント ドライバー (ドライバー内部の列マスター キー ストア プロバイダー) は CSP を使用して、キー ストアに格納された列マスター キーで保護されている列暗号化キーを暗号化および暗号化解除します。 

> [!NOTE]
> CAPI は、非推奨のレガシ API です。 HSM で KSP を使用できる場合、CSP/CAPI ではなく KSP を使用する必要があります。

CSP は、Always Encrypted で使用される RSA アルゴリズムをサポートする必要があります。

Windows には RSA をサポートし、テスト目的で使用できる、(HSM ではサポートされない) 次のソフトウェアベースの CSP が含まれています:Microsoft Enhanced RSA および AES Cryptographic Provider。

### <a name="creating-column-master-keys-in-a-key-store-using-capicsp"></a>CAPI/CSP を使用してキー ストア内の列マスター キーを作成する

列マスター キーは、RSA アルゴリズムを使用する非対称キー (公開/秘密キーのペア) にする必要があります。 推奨されるキーの長さは 2048 文字以上です。

#### <a name="using-hsm-specific-tools"></a>HSM 固有ツールの使用
HSM のドキュメントを参照してください。

#### <a name="using-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) の使用
「[SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)」をご覧ください。

### <a name="making-cng-keys-available-to-applications-and-users"></a>CNG のキーをアプリケーションとユーザーが使用できるようにする
コンピューターで CSP を構成する方法、およびアプリケーションとユーザーに HSM へのアクセス権を付与する方法については、お使いの HSM および CSP のドキュメントをご覧ください。
 
## <a name="next-steps"></a>次の手順  
- [SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)
- [PowerShell を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-powershell.md)
  
## <a name="see-also"></a>参照 
- [常に暗号化](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)  
