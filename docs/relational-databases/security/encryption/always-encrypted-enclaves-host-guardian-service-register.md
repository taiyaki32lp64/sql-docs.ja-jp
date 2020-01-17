---
title: ホスト ガーディアン サービスにコンピューターを登録する
description: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するために、SQL Server コンピューターをホスト ガーディアン サービスに登録します。
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 06db927ec2d77f07e82a9647239f87bc46e8a953
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74320065"
---
# <a name="register-computer-with-host-guardian-service"></a>ホスト ガーディアン サービスにコンピューターを登録する

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

この記事では、ホスト ガーディアン サービス (HGS) で証明する [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターを登録する方法について説明します。

開始する前に、少なくとも 1 台の HGS コンピューターがデプロイされ、構成証明サービスが設定されていることを確認してください。
詳細については、「[Deploy the Host Guardian Service for [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]](./always-encrypted-enclaves-host-guardian-service-deploy.md)」 (SQL Server のホスト ガーディアン サービスを展開する) を参照してください。

## <a name="step-1-install-the-attestation-client-components"></a>手順 1:構成証明クライアント コンポーネントをインストールする

SQL クライアントが、信頼できる [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターと通信しているかどうかを確認できるようにするには、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターがホスト ガーディアン サービスで正しく証明されている必要があります。
構成証明プロセスは、HGS クライアントと呼ばれるオプションの Windows コンポーネントによって管理されます。
次の手順は、このコンポーネントをインストールして証明を開始するのに役立ちます。

1. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターが [HGS の計画に関する Doc で概説されている前提条件](./always-encrypted-enclaves-host-guardian-service-plan.md#prerequisites)を満たしていることを確認します。

2. 管理者特権の PowerShell コンソールで次のコマンドを実行して、ホスト ガーディアン Hyper-V サポート機能をインストールします。これには、HGS クライアントと構成証明コンポーネントが含まれています。

    ```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
    ```

3. 再起動してインストールを完了します。

## <a name="step-2-verify-virtualization-based-security-is-running"></a>手順 2:仮想化ベースのセキュリティが実行されていることを確認する

ホスト ガーディアン Hyper-V サポート機能をインストールすると、仮想化ベースのセキュリティ (VBS) が自動的に構成され、有効化されます。
[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] Always Encrypted のエンクレーブは、VBS によって保護され、VBS 環境内で実行されます。
コンピューターに IOMMU デバイスがインストールされ、有効化されていない場合、VBS は起動しない可能性があります。
VBS が実行されているかどうかを確認するには、`msinfo32.exe`を実行してシステム情報ツールを開き、[システムの概要] の下部に表示されている `Virtualization-based security` の項目を見つけます。

![仮想化ベースのセキュリティの状態と構成を表示した [システム情報] のスクリーンショット](./media/always-encrypted-enclaves/msinfo32-vbs-status.png)

最初に確認する項目は、`Virtualization-based security`です。次の 3 つの値のいずれかが表示されます。

- `Running` は、VBS が正しく構成されており、正常に開始できたことを意味します。 コンピューターがこの状態を示す場合、手順 3 に進むことができます。
- `Enabled but not running`は、VBS を実行するように構成されていますが、ハードウェアが、VBS を実行するための最小限のセキュリティ要件を満たしていないことを意味します。 BIOS または UEFI でハードウェアの構成を変更して、IOMMU などのオプションのプロセッサ機能を有効にする必要があります。また、ハードウェアが本当に必要な機能をサポートしていない場合は、VBS のセキュリティ要件を低減させることが必要になる可能性があります。 詳細については、このセクションを引き続き参照してください。
- `Not enabled` は、VBS を実行するように構成されていないことを意味します。 VBS はホスト ガーデン Hyper-V 機能によって自動的に有効化されるため、この状態が表示された場合は手順 1 を繰り返します。

コンピューターで VBS が実行されていない場合は、`Virtualization-based security` プロパティを確認します。 `Required Security Properties` 項目の値と、`Available Security Properties` 項目の値を比較します。
VBS を実行するには、必須プロパティが、使用可能なセキュリティ プロパティと等しいか、そのサブセットである必要があります。

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] エンクレーブの証明については、セキュリティ プロパティに次のような重要な意味があります。

- `Base virtualization support` は常に必須です。これは、ハイパーバイザーを実行するために最小限必要なハードウェア機能を表します。
- `Secure Boot` が推奨されますが、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] Always Encrypted の場合、必須ではありません。 セキュア ブートは、UEFI の初期化が完了した直後に Microsoft によって署名されたブートローダーを要求して、ルートキットから保護します。 トラステッド プラットフォーム モジュール (TPM) 構成証明を使用する場合、VBS がセキュア ブートを要求するように構成されているかどうかに関係なく、セキュア ブートの有効化が測定され、適用されます。
- `DMA Protection` が推奨されますが、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] Always Encrypted の場合、必須ではありません。 DMA 保護は、IOMMU を使用してダイレクト メモリ アクセス攻撃から VBS とエンクレーブ メモリを保護します。 運用環境では、DMA 保護を備えたコンピューターを常に使用する必要があります。 開発またはテスト環境では、DMA 保護の要件を削除することができます。 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] インスタンスが仮想化されている場合、DMA 保護を使用できない可能性が高いため、VBS を実行するための要件を削除する必要があります。 VM で実行する場合のセキュリティ保証の低下については、「[信頼モデル](./always-encrypted-enclaves-host-guardian-service-plan.md#trust-model)」を参照してください。

VBS の必須セキュリティ機能を低減する前に、OEM またはクラウド サービス プロバイダーに問い合わせて、不足しているプラットフォーム要件を UEFI または BIOS で有効にする方法 (たとえば、セキュア ブート、Intel VT-d、または AMD IOV の有効化など) があるかどうかを確認してください。

VBS の必須プラットフォーム セキュリティ機能を変更するには、管理者特権の PowerShell コンソールで次のコマンドを実行します。

```powershell
# Value 0 = No security features required (use this for Azure VMs)
# Value 1 = Only Secure Boot is required
# Value 2 = Only DMA protection is required (default configuration)
# Value 3 = Both Secure Boot and DMA protection are required
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name RequirePlatformSecurityFeatures -Value 0
```

レジストリを変更した後、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターを再起動して、VBS が実行されているかどうかを再度確認します。

コンピューターが会社で管理されている場合、再起動後に、グループ ポリシーまたは Microsoft エンドポイント マネージャーによって、これらのレジストリ キーの変更がオーバーライドされる可能性があります。
IT ヘルプ デスクに問い合わせて、VBS 構成を管理するポリシーがデプロイされているかどうかを確認してください。

## <a name="step-3-configure-the-attestation-url"></a>手順 3:構成証明 URL を構成する

次に、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターに HGS 構成証明サービスの URL を構成します。

管理者特権の PowerShell コンソールで次のコマンドを更新して実行し、構成証明 URL を構成します。

- `hgs.bastion.local` を HGS クラスター名に置き換えます
- クラスター名を取得するには、HGS コンピューターで `Get-HgsServer` を実行します
- 構成証明 URL は常に `/Attestation`で終わる必要があります
- SQL Server は HGS のキー保護機能を利用しないため、`http://localhost` などのダミー URL を `-KeyProtectionServerUrl`に指定します

```powershell
Set-HgsClientConfiguration -AttestationServerUrl "https://hgs.bastion.local/Attestation" -KeyProtectionServerUrl "http://localhost"
```

このコンピューターが HGS にあらかじめ登録されている場合を除いて、このコマンドは構成証明の失敗を報告します。 この結果は正常です。

コマンドレットの出力の `AttestationMode` フィールドは、HGS が使用する構成証明モードを示します。

コンピューターを TPM モードで登録する場合は、[手順 4A](#step-4a-register-a-computer-in-tpm-mode) に進みます。また、コンピューターをホスト キー モードで登録する場合は、[手順 4B](#step-4b-register-a-computer-in-host-key-mode) に進みます。

## <a name="step-4a-register-a-computer-in-tpm-mode"></a>手順 4A: コンピューターを TPM モードで登録する

この手順では、コンピューターの TPM 状態に関する情報を収集して、それを HGS に登録します。

ホスト キー モードを使用するように HGS 構成証明サービスを構成する場合は、[手順 4B](#step-4b-register-a-computer-in-host-key-mode) に進んでください。

TPM の測定値の収集を開始する前に、既知の正常な構成の [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターで作業していることを確認します。
コンピューターには、必要なハードウェアがすべてインストールされ、最新のファームウェアとソフトウェアが適用されている必要があります。
HGS は、証明する際、このベースラインに対してコンピューターを測定します。このため、TPM 測定値を収集する際には、可能な限り最も安全で意図した状態にすることが重要です。

TPM の構成証明では、次の 3 つのデータ ファイルが収集されます。これらの一部は、同じ構成のコンピューターを使用する場合に再利用できます。

| 構成証明の成果物 | 測定の対象 | 一意性 |
| -------------------- | ---------------- | ---------- |
| プラットフォーム識別子  | コンピューターの TPM の公開保証キーと、TPM 製造元からの保証キーの証明書。 | コンピューターごとに 1 個 |
| TPM ベースライン | ブート プロセス中に読み込まれるファームウェアと OS の構成を測定する TPM のプラットフォーム制御レジスタ (PCR)。 たとえば、セキュア ブートの状態や、クラッシュ ダンプが暗号化されるかどうかなどがあります。 | 固有のコンピューター構成ごとに 1 つのベースライン (同じハードウェアとソフトウェアは同じベースラインを使用できます) |
| コードの整合性ポリシー | コンピューターを保護するための信頼する[Windows Defender アプリケーション制御](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)ポリシー | コンピューターにデプロイされた固有の CI ポリシーごとに 1 つ。 |

HGS で各構成証明の成果物を複数構成して、ハードウェアとソフトウェアのさまざまな組み合わせをサポートすることができます。
HGS では、証明するコンピューターは各ポリシー カテゴリの 1 つのポリシーとのみ一致する必要があります。
たとえば、HGS で 3 つの TPM ベースラインが登録されている場合、コンピューターの測定値は、これらのベースラインのいずれか 1 つと一致すれば、ポリシー要件を満たすことができます。

### <a name="configure-a-code-integrity-policy"></a>コードの整合性ポリシーを構成する

HGS では、TPM モードで証明するすべてのコンピューターに Windows Defender アプリケーション制御 (WDAC) ポリシーが適用されている必要があります。
WDAC コードの整合性ポリシーは、コードを実行しようとする各プロセスを、信頼された発行元とファイル ハッシュの一覧と照合することで、コンピューターで実行できるソフトウェアを制限します。
[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] のユース ケースの場合、エンクレーブは、仮想化ベースのセキュリティによって保護され、ホスト OS から変更することはできません。このため、WDAC ポリシーの厳格℉は、暗号化されたクエリのセキュリティに影響しません。
そのため、システムに追加の制限を課すことなく構成証明要件を満たすために、単純な監査モード ポリシーを [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターにデプロイすることをお勧めします。

コンピューターで既にカスタムの WDAC コードの整合性ポリシーを使用して、OS 構成を強化している場合、「[TPM の構成証明の情報を収集する](#collect-tpm-attestation-information)」に進んでください。

1. Windows Server 2019、Windows 10 バージョン 1809 以降のすべてのオペレーティング システムで使用できる作成済みのポリシー例があります。 `AllowAll` ポリシーを使用すると、制限されることなくコンピューターでソフトウェアを実行できます。 このポリシーを使用するには、OS および HGS で理解されるバイナリー形式に変換します。 管理者特権の PowerShell コンソールで次のコマンドを実行して、`AllowAll` ポリシーをコンパイルします。

    ```powershell
    # We are changing the policy to disable enforcement and user mode code protection before compiling
    $temppolicy = "$HOME\Desktop\allowall_edited.xml"
    Copy-Item -Path "$env:SystemRoot\schemas\CodeIntegrity\ExamplePolicies\AllowAll.xml" -Destination $temppolicy
    Set-RuleOption -FilePath $temppolicy -Option 0 -Delete
    Set-RuleOption -FilePath $temppolicy -Option 3

    ConvertFrom-CIPolicy -XmlFilePath $temppolicy -BinaryFilePath "$HOME\Desktop\allowall_cipolicy.bin"
    ```

2. 「[Windows Defender アプリケーション制御展開ガイド](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)」のガイダンスに従って、[グループ ポリシー](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-group-policy)を使用して `allowall_cipolicy.bin` ファイルを [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターにデプロイします。 ワークグループ コンピューターの場合は、ローカル グループ ポリシー エディター (`gpedit.msc`) を使用して同じプロセスを実行します。

3. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターで `gpupdate /force` を実行して、新しいコードの整合性ポリシーを構成し、コンピューターを再起動してポリシーを適用します。

### <a name="collect-tpm-attestation-information"></a>TPM の構成証明の情報を収集する

HGS で証明する [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターごとに次の手順を繰り返します。

1. コンピューターが既知の正常な状態にある場合に、PowerShell で次のコマンドを実行して TPM の構成証明の情報を収集します。

    ```powershell
    # Collects the TPM EKpub and EKcert
    $name = $env:computername
    $path = "$HOME\Desktop"
    (Get-PlatformIdentifier -Name $name).Save("$path\$name-EK.xml")

    # Collects the TPM baseline (current PCR values)
    Get-HgsAttestationBaselinePolicy -Path "$path\$name.tcglog" -SkipValidation

    # Collects the applied CI policy, if one exists
    Copy-Item -Path "$env:SystemRoot\System32\CodeIntegrity\SIPolicy.p7b" -Destination "$path\$name-CIpolicy.bin"
    ```

2. 3 つの構成証明ファイルを HGS サーバーにコピーします。

3. HGS サーバーの管理者特権の PowerShell コンソールで次のコマンドを実行して、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターを登録します。

    ```powershell
    # TIP: REMEMBER TO CHANGE THE FILENAMES
    # Registers the unique TPM with HGS (required for every computer)
    Add-HgsAttestationTpmHost -Path "C:\temp\SQL01-EK.xml"

    # Registers the TPM baseline (required ONCE for each unique hardware and software configuration)
    Add-HgsAttestationTpmPolicy -Name "MyHWSoftwareConfig" -Path "C:\temp\SQL01.tcglog"

    # Registers the CI policy (required ONCE for each unique CI policy)
    Add-HgsAttestationCiPolicy -Name "AllowAll" -Path "C:\temp\SQL01-CIpolicy.bin"
    ```

    > [!TIP]
    > 一意の TPM 識別子を登録しようとしてエラーが発生した場合は、使用している HGS コンピューターに [TPM の中間証明書とルート証明書がインポートされている](./always-encrypted-enclaves-host-guardian-service-deploy.md#switch-to-tpm-attestation)かどうかを確認してください。

プラットフォーム識別子、TPM ベースライン、コードの整合性ポリシーに加えて、HGS によって構成および適用された組み込みポリシーがあり、これらの変更が必要になる場合があります。
これらの組み込みポリシーは、サーバーから収集されたベースラインから測定され、コンピューターを保護するために有効にする必要があるさまざまなセキュリティ設定を表します。
DMA 攻撃から保護するための IOMMU がないコンピューター (たとえば、VM) がある場合、IOMMU ポリシーを無効にする必要があります。

IOMMU 要件を無効にするには、HGS サーバーで次のコマンドを実行します。

```powershell
Disable-HgsAttestationPolicy Hgs_IommuEnabled
```

> [!NOTE]
> IOMMU ポリシーを無効にした場合、HGS で証明するコンピューターに IOMMU は必要ありません。
> 1 台のコンピューターに対してのみ IOMMU ポリシーを無効にすることはできません。

登録済みの TPM ホストとポリシーの一覧を確認するには、次の PowerShell コマンドを使用します。

```powershell
Get-HgsAttestationTpmHost
Get-HgsAttestationTpmPolicy
```

## <a name="step-4b-register-a-computer-in-host-key-mode"></a>手順 4B: コンピューターをホスト キー モードで登録する

この手順では、ホストの一意のキーを生成して、それを HGS に登録するプロセスについて説明します。
TPM モードを使用するように HGS 構成証明サービスを構成する場合は、[手順 4A](#step-4a-register-a-computer-in-tpm-mode) のガイダンスに従ってください。

ホスト キーの構成証明は、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターで非対称キー ペアを生成して、そのキーの半分の公開部分を HGS に提供することで機能します。
キー ペアを生成するには、管理者特権の PowerShell コンソールで次のコマンドを実行します。

```powershell
Set-HgsClientHostKey
Get-HgsClientHostKey -Path "$HOME\Desktop\$env:computername-key.cer"
```

既にホスト キーを作成していて、新しいキー ペアを生成する場合は、代わりに次のコマンドを使用します。

```powershell
Remove-HgsClientHostKey
Set-HgsClientHostKey
Get-HgsClientHostKey -Path "$HOME\Desktop\$env:computername-key.cer"
```

ホスト キーを生成したら、証明書ファイルを HGS サーバーにコピーし、管理者特権の PowerShell コンソールで次のコマンドを実行して、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターを登録します。

```powershell
Add-HgsAttestationHostKey -Name "YourComputerName" -Path "C:\temp\yourcomputername.cer"
```

HGS で証明する [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターごとに手順 4B を繰り返します。

## <a name="step-5-confirm-the-host-can-attest-successfully"></a>手順 5:ホストが正常に証明できることを確認する

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターを HGS に登録した後 (TPM モードの場合は[手順 4A](#step-4a-register-a-computer-in-tpm-mode)、ホスト キー モードの場合は[手順 4B](#step-4b-register-a-computer-in-host-key-mode))、正常に証明できることを確認する必要があります。

[Get-HgsClientConfiguration](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsclientconfiguration?view=win10-ps) を使用するといつでも、HGS 構成証明クライアントの構成を確認して、構成証明を試行できます。
このコマンドの出力は、次のようになります。

```
PS C:\> Get-HgsClientConfiguration


IsHostGuarded                  : True
Mode                           : HostGuardianService
KeyProtectionServerUrl         : http://localhost
AttestationServerUrl           : http://hgs.bastion.local/Attestation
AttestationOperationMode       : HostKey
AttestationStatus              : Passed
AttestationSubstatus           : NoInformation
FallbackKeyProtectionServerUrl :
FallbackAttestationServerUrl   :
IsFallbackInUse                : False
```

出力で最も重要な 2 つのフィールドは、`AttestationStatus`(コンピューターが構成証明を通過したかどうかを示します) と `AttestationSubStatus`(コンピューターが構成証明に失敗した場合にコンピューターがどのポリシーで失敗したかを説明します) です。

以下では、`AttestationStatus` に表示される可能性のある最も一般的な値について説明します。

| `AttestationStatus` | 説明 |
| ----------------- | ----------- |
| 有効期限切れ | ホストは以前に構成証明を通過しましたが、発行された正常性証明書の有効期限が切れています。 ホストと HGS の時刻が同期されていることを確認してください。 |
| `InsecureHostConfiguration` | コンピューターは、HGS サーバーで構成された構成証明ポリシーの 1 つ以上を満たしていませんでした。 詳細については、`AttestationSubStatus` を参照してください。 |
| NotConfigured | コンピューターに構成証明 URL が構成されていません。 [構成証明 URL を構成](#step-3-configure-the-attestation-url)してください。 |
| Passed | コンピューターは構成証明を通過し、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] エンクレーブを実行するために信頼されています。 |
| `TransientError` | 一時的なエラーが原因で、構成証明の試行が失敗しました。 このエラーは通常、ネットワークを介した HGS の接続に問題が発生したことを意味します。 ネットワーク接続を確認して、コンピューターが HGS サービス名を解決し、ルーティングできるようにしてください。 |
| `TpmError` | コンピューターの TPM デバイスが、構成証明の試行中にエラーを報告しました。 詳細については、TPM のログを参照してください。 TPM をクリアすると、問題が解決される可能性がありますが、TPM をクリアする前に、BitLocker と、TPM に依存する他のサービスを一時停止する必要があります。 |
| `UnauthorizedHost` | ホスト キーが HGS に認識されていません。 [手順 4B](#step-4b-register-a-computer-in-host-key-mode) の手順に従って、コンピューターを HGS に登録してください。 |

`AttestationStatus` に `InsecureHostConfiguration`が表示される場合、`AttestationSubStatus` フィールドには、1 つ以上の失敗したポリシー名が入力されます。
次の表では、最も一般的な値とエラーの修復方法について説明します。

| AttestationSubStatus | 意味と対処法 |
| -------------------- | ---------------------------- |
| CodeIntegrityPolicy | コンピューターのコードの整合性ポリシーが HGS に登録されていないか、*または*コンピューターが現在コードの整合性ポリシーを使用していません。 ガイダンスについては、「[コードの整合性ポリシーを構成する](#configure-a-code-integrity-policy)」を参照してください。 |
| DumpsEnabled | コンピューターはクラッシュ ダンプを許可するように構成されていますが、Hgs_DumpsEnabled ポリシーでダンプが許可されていません。 このコンピューターでダンプを無効にするか、Hgs_DumpsEnabled ポリシーを無効にして続行してください。 |
| FullBoot | コンピューターがスリープ状態または休止状態から再開されたため、TPM の測定値が変更されました。 クリーンな TPM の測定値を生成するためにコンピューターを再起動してください。 |
| HibernationEnabled | コンピューターが、休止状態ファイルを暗号化しない休止状態を許可するように構成されています。 この問題を解決するには、コンピューターで休止状態を無効にしてください。 |
| HypervisorEnforcedCodeIntegrityPolicy | コンピューターが、コードの整合性ポリシーを使用するように構成されていません。 [グループ ポリシー] または [ローカル グループ ポリシー] > [コンピューターの構成] > [管理用テンプレート] > [システム] > [Device Guard] > [仮想化ベースのセキュリティを有効にする] > [コードの整合性に対する仮想化ベースの保護] を確認してください。 このポリシー項目は、[UEFI ロックなしで有効にする] に設定する必要があります。 |
| Iommu | このコンピューターでは、IOMMU デバイスが有効になっていません。 物理コンピューターの場合、UEFI 構成メニューで IOMMU を有効にします。 仮想マシンで、IOMMU を使用できない場合、HGS サーバーで `Disable-HgsAttestationPolicy Hgs_IommuEnabled` を実行します。 |
| SecureBoot | このコンピューターでは、セキュア ブートが有効になっていません。 この問題を解決するには、UEFI 構成メニューでセキュア ブートを有効にします。 |
| VirtualSecureMode | このコンピューターでは、仮想化ベースのセキュリティが実行されていません。 「[手順 2: 仮想化ベースのセキュリティが実行されていることを確認する](#step-2-verify-virtualization-based-security-is-running)」のガイダンスに従ってください。 |
