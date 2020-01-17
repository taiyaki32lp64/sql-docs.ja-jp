---
title: チュートリアル:SSMS を使用したセキュリティで保護されたエンクレーブが設定された Always Encrypted
description: このチュートリアルでは、セキュリティで保護されたエンクレーブが設定された基本的な Always Encrypted を作成する方法、インプレースでデータを暗号化する方法、SQL Server Management Studio (SSMS) を利用し、暗号化された列に対して高度なクエリを実行する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: a01b55cb67332617ea2e326756fb8ad6fc7bcf42
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557502"
---
# <a name="tutorial-always-encrypted-with-secure-enclaves-using-ssms"></a>チュートリアル:SSMS を使用したセキュリティで保護されたエンクレーブが設定された Always Encrypted
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

このチュートリアルでは、[セキュア エンクレーブを使用する Always Encrypted](encryption/always-encrypted-enclaves.md) の開始方法について説明します。 次のことを示します。
- セキュア エンクレーブを使用する Always Encrypted をテストおよび評価する基本的な環境を作成する方法。
- SQL Server Management Studio (SSMS) を使用して、データのインプレース暗号化を行い、暗号化された列に対して高度なクエリを実行する方法。

## <a name="prerequisites"></a>前提条件

セキュア エンクレーブを使用する Always Encrypted を開始するには、少なくとも 2 台のコンピューター (仮想マシンも可) が必要です。

- SQL Server と SSMS をホストする SQL Server コンピューター。
- エンクレーブの構成証明に必要なホスト ガーディアン サービスを実行する HGS コンピューター。

### <a name="sql-server-computer-requirements"></a>SQL Server コンピューターの要件

- [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] 以降。
- Windows 10 Enterprise バージョン 1809 以降、または Windows Server 2019 Datacenter エディション。 Windows 10 および Windows Server の他のエディションでは、HGS を使用した構成証明はサポートされていません。
- 仮想化テクノロジの CPU サポート:
  - Extended Page Tables を備えた Intel VT-x。
  - Rapid Virtualization Indexing を備えた AMD-V。
  - VM で [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] を実行する場合、ハイパーバイザーおよび物理 CPU には入れ子になった仮想化機能が用意されている必要があります。 
    - Hyper-V 2016 以降では、VM プロセッサ上で[入れ子にされた仮想化拡張機能](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization#configure-nested-virtualization)を有効にします。
    - Azure では、入れ子になった仮想化をサポートする VM サイズを選択します。 これには、Dv3 や Ev3 など、すべての v3 シリーズの VM が含まれます。 [入れ子対応の Azure VM の作成](https://docs.microsoft.com/azure/virtual-machines/windows/nested-virtualization#create-a-nesting-capable-azure-vm)に関するページを参照してください。
    - VMWare vSphere 6.7 以降では、[VMware のドキュメント](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.vm_admin.doc/GUID-C2E78F3E-9DE2-44DB-9B0A-11440800AADD.html)の説明に従って、仮想化ベースのセキュリティによる VM のサポートを有効にします。
    - 他のハイパーバイザーおよびパブリック クラウドでは、VBS エンクレーブが設定された Always Encrypted を有効にする入れ子になった仮想化機能がサポートされている場合もあります。 互換性と構成手順については、仮想化ソリューションのドキュメントを確認してください。
- [SQL Server Management Studio (SSMS) 18.3 以降](../../ssms/download-sql-server-management-studio-ssms.md)。

代わりに、別のコンピューター上に SSMS をインストールすることができます。

> [!WARNING]
> 運用環境では、SSMS またはその他のツールを使用して Always Encrypted キーを管理したり、SQL Server コンピューター上の暗号化されたデータに対してクエリを実行したりしないでください。これらの操作を行うと、Always Encrypted の使用目的が一部または完全に達成されなくなることがあります。 詳しくは、「[ キー管理のセキュリティに関する考慮事項](encryption/overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)」をご覧ください。

### <a name="hgs-computer-requirements"></a>HGS コンピューターの要件

- Windows Server 2019 Standard または Datacenter Edition
- 2 つの CPU
- 8 GB RAM
- 100 GB ストレージ

> [!NOTE]
> 開始する前に、HGS コンピューターがドメインに参加していてはなりません。

## <a name="step-1-configure-the-hgs-computer"></a>手順 1:HGS コンピューターを構成する

この手順では、ホスト キーの構成証明をサポートしているホスト ガーディアン サービスを実行するように HGS コンピューターを構成します。

1. HGS コンピューターに管理者 (ローカル管理者) としてサインインし、管理者特権の Windows PowerShell コンソールを開き、次のコマンドを実行してホスト ガーディアン サービスの役割を追加します。

   ```powershell
   Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
   ```

2. HGS コンピューターが再起動した後、管理者アカウントでもう一度サインインし、管理者特権の Windows PowerShell コンソールを開きます。次のコマンドを実行してホスト ガーディアン サービスをインストールし、そのドメインを構成します。 ここで指定したパスワードは、Active Directory のディレクトリ サービスの修復モード パスワードに対してのみ適用されます、管理者アカウントのログイン パスワードは変更されません。 -HgsDomainName に対して任意のドメイン名を指定できます。

   ```powershell
   $adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force
   Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
   ```

3. コンピューターが再起動したら、管理者アカウント (今回もドメイン管理者) でサインインし、管理者特権の Windows PowerShell コンソールを開いて、HGS インスタンスのホスト キーの構成証明を構成します。 

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey  
   ```

4. 次のコマンドを実行して、HGS コンピューターの IP アドレスを検索します。 後の手順で使用するために、この IP アドレスを保存します。

   ```powershell
   Get-NetIPAddress  
   ```

> [!NOTE]
> または、HGS コンピューターを DNS 名によって参照する場合は、企業の DNS サーバーから新しい HGS ドメイン コントローラーにフォワーダーを設定できます。  

## <a name="step-2-configure-the-sql-server-computer-as-a-guarded-host"></a>手順 2:SQL Server コンピューターを保護されたホストとして構成する
この手順では、ホスト キーの構成証明を使用して、HGS に登録されている保護されたホストとして SQL Server コンピューターを構成します。

> [!WARNING]
> ホスト キーの構成証明はテスト環境でのみ使用することをお勧めします。 運用環境では、TPM 構成証明を使用してください。

1. 管理者として SQL Server コンピューターにサインインし、管理者特権で Windows PowerShell コンソールを開き、computername 変数にアクセスしてコンピューターの名前を取得します。

   ```powershell
   $env:computername 
   ```

2. 保護されたホスト機能をインストールします。Hyper-V もインストールされます (まだインストールされていない)。

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
   ```

3. Hyper-V のインストールを完了するように求められたら、SQL Server コンピューターを再起動します。

4. 使用している SQL Server コンピューターが仮想マシンの場合、または UEFI セキュア ブートをサポートしていないか IOMMU が搭載されていない従来の物理マシンの場合は、プラットフォームのセキュリティ機能に関する VBS 要件を削除する必要があります。
    1. Windows レジストリの要件を削除します。

        ```powershell
       Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name RequirePlatformSecurityFeatures -Value 0
       ```

    1. コンピューターを再起動し、要件を低くして VBS をオンラインにします。

        ```powershell
       Restart-Computer
       ```

5. もう一度 SQL Server コンピューターに管理者としてサインインし、管理者特権の Windows PowerShell コンソールを開きます。一意のホスト キーを生成し、結果の公開キーをファイルにエクスポートします。

   ```powershell
   Set-HgsClientHostKey 
   Get-HgsClientHostKey -Path $HOME\Desktop\hostkey.cer
   ```

6. 前の手順で生成したホスト キー ファイルを HGS マシンに手動でコピーします。 次の手順では、ファイル名が hostkey.cer で、これを HGS マシン上のデスクトップにコピーすることを想定しています。

7. HGS コンピューター上で、管理者特権の Windows PowerShell コンソールを開き、SQL Server コンピューターのホスト キーを HGS に登録します。

   ```powershell
   Add-HgsAttestationHostKey -Name <your SQL Server computer name> -Path $HOME\Desktop\hostkey.cer
   ```

8. SQL Server コンピューター上で、管理者特権の Windows PowerShell コンソール内で次のコマンドを実行して、SQL Server コンピューターに証明する場所を指示します。 両方のアドレスの場所で HGS コンピューターの IP アドレスまたは DNS 名を必ず指定します。 

   ```powershell
   # use http, and not https
   Set-HgsClientConfiguration -AttestationServerUrl http://<IP address or DNS name>/Attestation -KeyProtectionServerUrl http://<IP address or DNS name>/KeyProtection/  
   ```

上記のコマンドの結果として、AttestationStatus = Passed と表示されます。

HostUnreachable エラーが発生する場合、SQL Server コンピューターが HGS と通信できないことを意味します。 HGS コンピューターに対して ping を実行できることを確認します。

UnauthorizedHost エラーは、公開キーが HGS サーバーに登録されていないことを示します。手順 5. と 6. を繰り返してエラーを解決します。

他のすべてに失敗した場合は、Remove-HgsClientHostKey を実行し、手順 4. から 7. を繰り返します。

## <a name="step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server"></a>手順 3:SQL Server 上でセキュア エンクレーブを使用する Always Encrypted を有効にする

この手順では、SQL Server インスタンス上でエンクレーブを使用する Always Encrypted の機能を有効にします。

1. SSMS を使用し、データベース接続の Always Encrypted を有効に**しないで**、sysadmin として SQL Server インスタンスに接続します。
    1. SSMS を起動します。
    1. **[サーバーへの接続]** ダイアログで、サーバーの名前を指定し、認証方法を選択して、資格情報を指定します。
    1. **[オプション >>]** をクリックして、 **[Always Encrypted]** タブを選択します。
    1. **[Always Encrypted を有効にする (列の暗号化)]** チェック ボックスがオンになって**いない**ことを確認します。
    1. **[接続]** を選択します。

2. 新しいクエリ ウィンドウを開き、次のステートメントを実行して、セキュリティで保護されたエンクレーブの型を仮想化ベースのセキュリティ (VBS) に設定します。

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1;
   RECONFIGURE;
   ```

3. SQL Server インスタンスを再起動して、前の変更を反映します。 SSMS でインスタンスを再起動するには、オブジェクト エクスプローラー上でそのインスタンスを右クリックし、[再起動] を選択します。 インスタンスの再起動後に、再接続します。

4. 次のクエリを実行して、セキュア エンクレーブが読み込まれていることを確認します。

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```

    クエリでは、次の結果が返されるはずです。  

    | name                           | value | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | 列暗号化エンクレーブの型 | 1     | 1              |

5. 暗号化された列に対して高度な計算を有効にするには、次のクエリを実行します。

   ```sql
   DBCC traceon(127,-1);
   ```

    > [!NOTE]
    > [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] では、高度な計算が既定で無効になります。 これらは、SQL Server インスタンスを再起動するたびに、上記のステートメントを使用して有効にする必要があります。

## <a name="step-4-create-a-sample-database"></a>手順 4:サンプル データベースの作成
この手順では、いくつかのサンプル データを含むデータベースを作成し、その後暗号化します。

1. 前の手順の SSMS インスタンスを使用し、クエリ ウィンドウで次のステートメントを実行して、**ContosoHR** という名前の新しいデータベースを作成します。

    ```sql
    CREATE DATABASE [ContosoHR];
    ```

1. **Employees** という名前の新しいテーブルを作成します。

    ```sql
    USE [ContosoHR];
    GO

    CREATE TABLE [dbo].[Employees]
    (
        [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
        [SSN] [char](11) NOT NULL,
        [FirstName] [nvarchar](50) NOT NULL,
        [LastName] [nvarchar](50) NOT NULL,
        [Salary] [money] NOT NULL
    ) ON [PRIMARY];
    ```

1. いくつかの従業員レコードを **Employees** テーブルに追加します。

    ```sql
    USE [ContosoHR];
    GO

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('795-73-9838'
            , N'Catherine'
            , N'Abel'
            , $31692);

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('990-00-6818'
            , N'Kim'
            , N'Abercrombie'
            , $55415);
    ```

## <a name="step-5-provision-enclave-enabled-keys"></a>手順 5:エンクレーブ対応キーをプロビジョニングする

この手順では、エンクレーブ計算を許可する列マスター キーと列暗号化キーを作成します。

1. 前の手順の SSMS インスタンスを使用し、**オブジェクト エクスプローラー**でデータベースを展開して、 **[セキュリティ]**  >  **[Always Encrypted キー]** に移動します。
1. エンクレーブ対応の列マスター キーをプロビジョニングします。
    1. **[Always Encrypted キー]** を右クリックし、 **[新しい列マスター キー...]** を選択します。
    2. 列マスター キー名**CMK1** を選択します。
    3. **[Windows 証明書ストア -現在のユーザー] または [Windows 証明書ストア - ローカル コンピューター]** か、 **[Azure Key Vault]** を選択します。
    4. **[エンクレーブ計算を許可する]** を選択します。
    5. [Azure Key Vault] を選択した場合は、Azure にサインインし、キー コンテナーを選択します。 Always Encrypted のキー コンテナーを作成する方法について詳しくは、「[Manage your key vaults from Azure portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/)」(Azure portal からキー コンテナーを管理する) を参照してください。
    6. 証明書または Azure Key Value キーが既に存在する場合はそれを選択します。または、 **[証明書の生成]** ボタンをクリックして新しい証明書を作成します。
    7. **[OK]** を選択します。

        ![エンクレーブ計算を許可する](encryption/media/always-encrypted-enclaves/allow-enclave-computations.png)

1. 新しいエンクレーブ対応の列暗号化キーを作成します。

    1. **[Always Encrypted キー]** を右クリックし、 **[新しい列の暗号化キー]** を選択します。
    2. 新しい列暗号化キーの名前「**CEK1**」を入力します。
    3. **[列マスター キー]** ドロップダウンで、前の手順で作成した列マスター キーを選択します。
    4. **[OK]** を選択します。

## <a name="step-6-encrypt-some-columns-in-place"></a>手順 6:一部の列のインプレース暗号化を行う

この手順では、サーバー側エンクレーブ内の **SSN** 列と **Salary** に格納されたデータを暗号化し、データの SELECT クエリをテストします。

1. SSMS を開き、データベース接続の Always Encrypted を有効に**して**、SQL Server インスタンスに接続します。
    1. SSMS の新しいインスタンスを開始します。
    1. **[サーバーへの接続]** ダイアログで、サーバーの名前を指定し、認証方法を選択して、資格情報を指定します。
    1. **[オプション >>]** をクリックして、 **[Always Encrypted]** タブを選択します。
    1. **[Always Encrypted を有効にする (列の暗号化)]** チェック ボックスをオンにして、エンクレーブ構成証明 URL (たとえば、ht<span>tp://</span>hgs.bastion.local/Attestation) を指定します。
    1. **[接続]** を選択します。
    1. Always Encrypted クエリのパラメーター化を有効にすることの確認を求められたら、 **[有効]** を選択します。

1. 同じ SSMS インスタンス (Always Encrypted が有効) を使用して、新しいクエリ ウィンドウを開き、下のクエリを実行して **SSN** 列と **Salary** 列を暗号化します。

    ```sql
    USE [ContosoHR];
    GO

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [SSN] [char] (11) COLLATE Latin1_General_BIN2
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [Salary] [money]
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);

    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```

    > [!NOTE]
    > 上記のスクリプト内でデータベース用のクエリ プラン キャッシュをクリアする ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ステートメントに注目してください。 テーブルを変更したら、テーブルにアクセスするすべてのバッチおよびストアド プロシージャのプランをクリアして、パラメーター暗号化情報を更新する必要があります。 

1. **SSN** 列と **Salary** 列が暗号化されたことを確認するには、データベース接続の Always Encrypted が有効になって**いない** SSMS インスタンスで新しいクエリ ウィンドウを開き、下のステートメントを実行します。 クエリ ウィンドウで、**SSN** 列と **Salary** 列に暗号化された値が返される必要があります。 Always Encrypted が有効な SSMS インスタンスを使用して同じクエリを実行した場合は、復号化されたデータが表示されます。

    ```sql
    SELECT * FROM [dbo].[Employees];
    ```

## <a name="step-7-run-rich-queries-against-encrypted-columns"></a>手順 7:暗号化された列に対して高度なクエリを実行する

ここで、暗号化された列に対して高度なクエリを実行できます。 いくつかのクエリ処理は、サーバー側エンクレーブ内で実行されます。 

1. Always Encrypted が有効になって**いる** SSMS インスタンスで、Always Encrypted のパラメーター化も有効になっていることを確認します。
    1. SSMS のメイン メニューから **[ツール]** を選択します。
    2. **[オプション...]** を選択します。
    3. **[クエリ実行]**  >  **[SQL Server]**  >  **[詳細]** の順に移動します。
    4. **[Always Encrypted のパラメーター化を有効にする]** がオンであることを確認します。
    5. **[OK]** を選択します。
2. 新しいクエリ ウィンドウを開き、下のクエリを貼り付けて実行します。 クエリでは、指定した検索条件を満たすプレーンテキスト値と行が返されます。

    ```sql
    DECLARE @SSNPattern [char](11) = '%6818';
    DECLARE @MinSalary [money] = $1000;
    SELECT * FROM [dbo].[Employees]
    WHERE SSN LIKE @SSNPattern AND [Salary] >= @MinSalary;
    ```

3. Always Encrypted が有効になっていない SSMS インスタンスで同じクエリをもう一度試し、発生するエラーに注意します。

## <a name="next-steps"></a>次の手順
このチュートリアルを完了すると、次のいずれかのチュートリアルに進むことができます。
- [チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET Framework アプリケーションの開発](tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)
- [チュートリアル:ランダム化された暗号化を使用してエンクレーブ対応の列でインデックスを作成して使用する](./tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)

## <a name="see-also"></a>参照
- [Always Encrypted サーバー構成オプションのエンクレーブの種類を構成する](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
- [エンクレーブ対応キーをプロビジョニングする](encryption/always-encrypted-enclaves-provision-keys.md)
- [Transact-SQL を使用してインプレースでの列の暗号化を構成する](encryption/always-encrypted-enclaves-configure-encryption-tsql.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを実行する](encryption/always-encrypted-enclaves-query-columns.md)