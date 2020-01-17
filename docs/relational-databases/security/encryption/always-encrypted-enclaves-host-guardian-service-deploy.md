---
title: ホスト ガーディアン サービスを展開する
description: セキュリティで保護されたエンクレーブが設定された Always Encrypted にホスト ガーディアン サービスを展開します。
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6794f5fd57d1c89e7c1989e79b5072a8c15cf43e
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74320055"
---
# <a name="deploy-the-host-guardian-service-for-include-ssnoversion-mdincludesssnoversion-mdmd"></a>[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] のホスト ガーディアン サービスを展開する

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

この記事では、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] の構成証明サービスとしてホスト ガーディアン サービス (HGS) を展開する方法について説明します。
開始する前に、前提条件とアーキテクチャに関するガイダンスの完全な一覧について、「[ホスト ガーディアン サービスの構成証明の計画](./always-encrypted-enclaves-host-guardian-service-plan.md)」を参照してください。

## <a name="step-1-set-up-the-first-hgs-computer"></a>手順 1:1 台目の HGS コンピューターを設定する

ホスト ガーディアン サービス (HGS) は、1 台または複数のコンピューター上でクラスター化されたサービスとして実行されます。
この手順では、1 台目のコンピューターに新しい HGS クラスターを設定します。
既に HGS クラスターがあり、高可用性を実現するため、それにコンピューターを追加する場合は、「[手順 2:HGS コンピューターをクラスターに追加する](#step-2-add-more-hgs-computers-to-the-cluster)」に進みます。

開始する前に、使用しているコンピューターで Windows Server 2019 Standard または Datacenter Edition を実行していること、ローカル管理者特権があること、コンピューターが Active Directory ドメインにまだ参加していないことを確認します。

1. 1 台目の HGS コンピューターにローカル管理者としてサインインし、管理者特権の Windows PowerShell コンソールを開きます。 次のコマンドを実行して、ホスト ガーディアン サービス ロールをインストールします。 コンピューターが自動的に再起動され、変更が適用されます。

    ```powershell
    Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
    ```

2. HGS コンピューターを再起動した後、管理者特権の Windows PowerShell コンソールで次のコマンドを実行して、新しい Active Directory フォレストをインストールします。

    ```powershell
    # Select the name for your new Active Directory root domain.
    # Make sure the name does not conflict with, and is not subordinate to, any existing domains on your network.
    $HGSDomainName = 'bastion.local'

    # Specify a Directory Services Restore Mode password that can be used to recover your domain in safe mode.
    # This password is not, and will not change, your admin account password.
    # Save this password somewhere safe and include it in your disaster recovery plan.
    $DSRMPassword = Read-Host -AsSecureString -Prompt "Directory Services Restore Mode Password"

    Install-HgsServer -HgsDomainName $HgsDomainName -SafeModeAdministratorPassword $DSRMPassword -Restart
    ```

    HGS コンピューターが再起動され、Active Directory フォレストの構成が完了します。 次回のログイン時に、お使いの管理者アカウントがドメイン管理者アカウントになります。 新しいフォレストの管理とセキュリティ保護の詳細については、[Active Directory Domain Services 操作に関するドキュメント](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/ad-ds-operations)を参照することをお勧めします。

3. 次に、管理者特権の Windows PowerShell コンソールで次のコマンドを実行して、HGS クラスターを設定し、構成証明サービスをインストールします。

    ```powershell
    # Note: the name you provide here will be shared by all HGS nodes and used to point your SQL Server computers to the HGS cluster.
    # For example, if you provide "attsvc" here, a DNS record for "attsvc.yourdomain.com" will be created for every HGS computer.
    Initialize-HgsAttestation -HgsServiceName 'hgs'
    ```

## <a name="step-2-add-more-hgs-computers-to-the-cluster"></a>手順 2:HGS コンピューターをクラスターにさらに追加する

1 台目の HGS コンピューターとクラスターを設定したら、さらに HGS サーバーを追加して高可用性を実現できます。
HGS サーバーを 1 台だけ設定する場合 (開発/テスト環境など) は、手順 3 に進むことができます。

1 台目の HGS コンピューターと同様、クラスターに参加するコンピューターで Windows Server 2019 Standard または Datacenter Edition を実行していること、ローカル管理者特権があること、コンピューターが Active Directory ドメインにまだ参加していないことを確認します。

1. コンピューターにローカル管理者としてサインインし、管理者特権の Windows PowerShell コンソールを開きます。 次のコマンドを実行して、ホスト ガーディアン サービス ロールをインストールします。 コンピューターが自動的に再起動され、変更が適用されます。

    ```powershell
    Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
    ```

2. コンピューターの DNS クライアントの構成を調べて、HGS ドメインを解決できることを確認します。 次のコマンドは、HGS サーバーの IP アドレスを返します。 HGS ドメインを解決できない場合は、名前解決に HGS DNS サーバーを使用するように、ネットワーク アダプターの DNS サーバー情報を更新することが必要になる可能性があります。

    ```powershell
    # Change 'bastion.local' to the domain name you specified in Step 1.2
    nslookup bastion.local

    # If it fails, use sconfig.exe, option 8, to set the first HGS computer as your preferred DNS server.
    ```

3. コンピューターが再起動したら、管理者特権の Windows PowerShell コンソールで次のコマンドを実行して、1 台目の HGS サーバーによって作成された Active Directory ドメインにコンピューターを参加させます。 このコマンドを実行するには、AD ドメインのドメイン管理者資格情報が必要です。 コマンドが完了すると、コンピューターが再起動され、コンピューターが HGS ドメインの Active Directory ドメイン コントローラーになります。

    ```powershell
    # Provide the fully qualified HGS domain name
    $HGSDomainName = 'bastion.local'

    # Provide a domain administrator's credential for the HGS domain
    $DomainAdminCred = Get-Credential

    # Specify a Directory Services Restore Mode password that can be used to recover your domain in safe mode.
    # This password is not, and will not change, your admin account password.
    # Save this password somewhere safe and include it in your disaster recovery plan.
    $DSRMPassword = Read-Host -AsSecureString -Prompt "Directory Services Restore Mode Password"

    Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $DomainAdminCred -SafeModeAdministratorPassword $DSRMPassword -Restart
    ```

4. コンピューターの再起動後に、ドメイン管理者資格情報でログインします。 管理者特権の Windows PowerShell コンソールを開き、次のコマンドを実行して構成証明サービスを構成します。 構成証明サービスはクラスター対応であるため、他のクラスター メンバーから構成をレプリケートします。 任意の HGS ノードで構成証明ポリシーに加えられた変更は、他のすべてのノードに適用されます。

    ```powershell
    # Provide the IP address of an existing, initialized HGS server
    # If you are using separate networks for cluster and application traffic, choose an IP address on the cluster network.
    # You can find the IP address of your HGS server by signing in and running "ipconfig /all"
    Initialize-HgsAttestation -HgsServerIPAddress '172.16.10.20'
    ```

5. HGS クラスターに追加するすべてのコンピューターに対して、手順 2 を繰り返します。

## <a name="step-3-configure-a-dns-forwarder-to-your-hgs-cluster"></a>手順 3:HGS クラスターへの DNS フォワーダーを構成する

HGS では、独自の DNS サーバーが実行されます。このサーバーには、構成証明サービスの解決に必要な名前レコードが含まれます。
お使いの SQL Server コンピューターでは、HGS DNS サーバーに要求を転送するようにネットワークの DNS サーバーを構成するまで、これらのレコードを解決することができません。

DNS フォワーダーを構成するプロセスはベンダーによって異なります。そのため、特定のネットワークの正しいガイダンスについては、ネットワーク管理者に問い合わせることをお勧めします。

企業ネットワークで Windows Server DNS サーバー のロールを使用している場合、DNS 管理者は、HGS ドメインへの条件付きフォワーダーを作成して、HGS ドメインに対する要求のみが転送されるようにできます。
たとえば、HGS サーバーで "bastion.local" ドメイン名を使用し、172.16.10.20、172.16.10.21、172.16.10.22 の IP アドレスがある場合、企業 DNS サーバーで次のコマンドを実行して条件付きフォワーダーを構成できます。

```powershell
# Tip: make sure to provide every HGS server's IP address
# If you use separate NICs for cluster and application traffic, use the application traffic NIC IP addresses here
Add-DnsServerConditionalForwarderZone -Name 'bastion.local' -ReplicationScope "Forest" -MasterServers "172.16.10.20", "172.16.10.21", "172.16.10.22"
```

## <a name="step-4-configure-the-attestation-service"></a>手順 4:構成証明サービスを構成する

HGS では、2 つの構成証明モードをサポートしています。各 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターの整合性と ID の暗号化検証のための TPM 構成証明と、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターの ID を簡単に検証するためのホスト キーの構成証明です。
構成証明モードをまだ選択していない場合は、各モードのセキュリティ保証とユース ケースの詳細について[計画ガイド](./always-encrypted-enclaves-host-guardian-service-plan.md#attestation-modes)の構成証明書の情報を確認してください。

このセクションの手順では、特定の構成証明モードの基本構成証明ポリシーを構成します。
手順 4 では、ホスト固有の情報を登録します。
将来、構成証明モードを変更する必要がある場合は、必要な構成証明モードを使用して手順 3 と 4 を繰り返します。

### <a name="switch-to-tpm-attestation"></a>TPM 構成証明に切り替える

HGS で TPM 構成証明を構成するには、インターネットにアクセスできるコンピューターと、TPM 2.0 rev 1.16 チップを搭載した少なくとも 1 台の [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターが必要です。

TPM モードを使用するように HGS を構成するには、管理者特権の PowerShell コンソールを開き、次のコマンドを実行します。

```powershell
Set-HgsServer -TrustTpm
```

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターで証明を試みるときに、クラスター内のすべての HGS コンピューターで TPM モードが使用されるようになります。

HGS を使用して SQL Server コンピューターから TPM 情報を登録する前に、TPM ベンダーから保証キー (EK) ルート証明書をインストールする必要があります。
各物理 TPM は、製造元を識別する保証キー証明書が付いている一意の保証キーを使用して、ファクトリで構成されます。
この証明書により、TPM が本物であることが保証されます。
HGS では、信頼されるルート証明書の一覧と証明書チェーンを比較して、新しい TPM を HGS に登録するときに、保証キー証明書を検証します。

Microsoft は、HGS の信頼される TPM ルート証明書ストアにインポートできる既知の適切な TPM ベンダー ルート証明書の一覧を公開します。
SQL Server のコンピューターが仮想化されている場合、仮想 TPM の保証キーの証明書チェーンを取得する方法については、クラウド サービス プロバイダーまたは仮想化プラットフォーム ベンダーに問い合わせる必要があります。

信頼される TPM ルート証明書パッケージを物理 TPM 用に Microsoft からダウンロードするには、次の手順を行います。

1. インターネットにアクセスできるコンピューターで、最新の TPM ルート証明書パッケージを [https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925) からダウンロードします

2. cab ファイルの署名を検証して、それが本物であることを確認します。

    ```powershell
    # Note: replace the path below with the correct one to the file you downloaded in step 1
    Get-AuthenticodeSignature ".\TrustedTpm.cab"
    ```

    > [!WARNING]
    > 署名が無効な場合は続行せず、Microsoft サポートにお問い合わせください。

3. cab ファイルを新しいディレクトリに展開します。

    ```powershell
    mkdir .\TrustedTpmCertificates
    expand.exe -F:* ".\TrustedTpm.cab" ".\TrustedTpmCertificates"
    ```

4. 新しいディレクトリに、各 TPM ベンダーのディレクトリが表示されます。 使用しないベンダーのディレクトリは削除できます。

5. "TrustedTpmCertificates" ディレクトリ全体を HGS サーバーにコピーします。

6. HGS サーバーで管理者特権の PowerShell コンソールを開き、次のコマンドを実行して、すべての TPM ルート証明書と中間証明書をインポートします。

    ```powershell
    # Note: replace the path below with the correct location of the TrustedTpmCertificates folder on your HGS computer
    cd "C:\scratch\TrustedTpmCertificates"
    .\setup.cmd
    ```

7. HGS コンピューターごとに、手順 5 と 6 を繰り返します。

OEM、クラウド サービス プロバイダー、または仮想化プラットフォーム ベンダーから中間証明書とルート CA 証明書を取得している場合は、各ローカル コンピューターの証明書ストア (`TrustedHgs_RootCA` または `TrustedHgs_IntermediateCA`) に証明書を直接インポートすることができます。 たとえば、PowerShell で以下を実行します。

```powershell
# Imports MyCustomTpmVendor_Root.cer to the local machine's "TrustedHgs_RootCA" store
Import-Certificate -FilePath ".\MyCustomTpmVendor_Root.cer" -CertStoreLocation "Cert:\LocalMachine\TrustedHgs_RootCA"
```

### <a name="switch-to-host-key-attestation"></a>ホスト キーの構成証明に切り替える

ホスト キーの構成証明を使用するには、管理者特権の PowerShell コンソールで、HGS サーバー上で次のコマンドを実行します。

```powershell
Set-HgsServer -TrustHostKey
```

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターで証明を試みるときに、クラスター内のすべての HGS コンピューターでホスト キー モードが使用されるようになります。

## <a name="step-5-configure-the-hgs-https-binding"></a>手順 5:HGS HTTPS バインドを構成する

既定のインストールでは、HGS により、HTTP (ポート 80) バインドのみが公開されます。
HTTPS (ポート 443) バインドを構成して、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターと HGS 間のすべての通信を暗号化できます。
HGS のすべての実稼働インスタンスで HTTPS バインドを使用することをお勧めします。

1. 手順 1.3 の完全修飾 HGS サービス名をサブジェクト名として使用して、証明機関から TLS 証明書を取得します。 サービス名がわからない場合は、任意の HGS コンピューターで `Get-HgsServer` を実行して確認できます。 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターが別の DNS 名を使用して HGS クラスターに接続している場合 (たとえば、HGS が異なるアドレスを持つネットワーク ロード バランサーの後ろにある場合)、代替 DNS 名をサブジェクト代替名の一覧に追加できます。

2. HGS コンピューターで [Set-HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/set-hgsserver) を使用して HTTPS バインドを有効にし、前の手順で取得した TLS 証明書を指定します。 ローカル証明書ストアのコンピューターに証明書が既にインストールされている場合は、次のコマンドを使用して HGS に登録します。

    ```powershell
    # Note: you'll need to know the thumbprint for your certificate to configure HGS this way
    Set-HgsServer -Http -Https -HttpsCertificateThumbprint "54A043386555EB5118DB367CFE38776F82F4A181"
    ```

    パスワードで保護された PFX ファイルに証明書 (秘密キーを含む) をエクスポートした場合は、次のコマンドを実行して HGS に証明書を登録できます。

    ```powershell
    $PFXPassword = Read-Host -AsSecureString -Prompt "PFX Password"
    Set-HgsServer -Http -Https -HttpsCertificatePath "C:\path\to\hgs_tls.pfx" -HttpsCertificatePassword $PFXPassword
    ```

3. クラスター内の各 HGS コンピューターに対して、手順 1 と 2 を繰り返します。 TLS 証明書は、HGS ノード間で自動的にレプリケートされません。 さらに、各 HGS コンピューターは、サブジェクトが HGS サービス名と一致する限り、独自の一意の TLS 証明書を持つことができます。

## <a name="next-steps"></a>次のステップ

- [HGS にコンピューターを登録する](./always-encrypted-enclaves-host-guardian-service-register.md)
