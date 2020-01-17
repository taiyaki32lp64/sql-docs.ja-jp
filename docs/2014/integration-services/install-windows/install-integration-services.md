---
title: Integration Services のインストール | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 678b14b224f994c834630a398767fee1ea360870
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768222"
---
# <a name="install-integration-services"></a>Integration Services のインストール
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を含む任意またはすべてのコンポーネントを 1 つのセットアップ プログラムでインストールできます。 セットアップによって、他の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントと共にまたは単独で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を 1 台のコンピューターにインストールできます。  
  
 このトピックでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]をインストールする前に知っておく必要がある重要な注意点について説明します。 このトピックの情報を参考にして各インストール オプションを評価することにより、インストール時に適切な選択を行うことができます。  
  
 セットアップの開始、セットアップ ウィザードの使用、またはコマンド ラインからのセットアップの実行の手順については、ここでは扱いません。 インストールするには、セットアップと選択のコンポーネントを起動する方法の詳しい手順については、「 [SQL Server 2014 インストールのクイック スタート](../../getting-started/quick-start-installation-of-sql-server-2014.md)します。 インストールするためのコマンド ライン オプションについて[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を参照してください[コマンド プロンプトから SQL Server 2014 のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)します。  
  
## <a name="preparing-to-install-integration-services"></a>Integration Services をインストールする準備  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]をインストールする前に、次の要件を確認してください。  
  
-   [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [システム構成チェッカーの検査パラメーター](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)  
  
-   [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
## <a name="selecting-an-integration-services-configuration"></a>Integration Services の構成の選択  
 次の構成で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールできます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の以前のインスタンスが存在しないコンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールできます。  
  
-   [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] は、 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] または [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]の既存のインスタンスとサイド バイ サイドでインストールできます。  
  
     [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] の以前のバージョンのいずれかが既にインストールされているコンピューターで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] にアップグレードすると、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] は以前のバージョンに対してサイド バイ サイドでインストールされます。  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のアップグレードの詳細については、「 [Integration Services のアップグレード](upgrade-integration-services.md)」を参照してください。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]の旧バージョンとの互換性については、「 [Integration Services の旧バージョンとの互換性](../integration-services-backward-compatibility.md)」を参照してください。  
  
## <a name="installing-integration-services"></a>Integration Services のインストール  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール要件を検討し、コンピューターがそれらの要件を満たしていることを確認したら、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のインストールの準備は完了です。  
  
> [!NOTE]  
>  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールすると、既定で Users グループの全ユーザーが [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスにアクセスできました。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]をインストールした場合、ユーザーは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスにアクセスできません。 このサービスは既定で保護されます。 後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]がインストールされている、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理者に DCOM 構成ツール (Dcomcnfg.exe) を特定のユーザーのアクセスを付与するを実行する必要があります**SQL Server Integration Services 12.0**します。  
>   
>  アクセス許可を付与する方法については、「 [Grant Permissions to Integration Services Service](../grant-permissions-to-integration-services-service.md)」を参照してください。  
  
 セットアップ ウィザードを使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]をインストールする場合は、一連のページを使用してコンポーネントとオプションを指定します。 次に、選択したオプションに影響のインストール、セットアップ ウィザードのページ[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]選択範囲の推奨事項。  
  
-   **機能の選択**  
  
     **サービスをインストールしてデザイン環境外部でパッケージを実行するには、** [Integration Services] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を選択します。  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]の完全インストール (パッケージの開発と管理に必要なツールやドキュメントを含んだインストール) を実行するには、 **[Integration Services]** と次の **[共有機能]** の両方を選択します。  
  
    -   **[[SQL Server Data Tools]]** : パッケージをデザインするためのツールをインストールします。  
  
    -   **[管理ツール - 完全]** : パッケージを管理するための [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] をインストールします。  
  
    -   **[クライアント ツール SDK]** : [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プログラミング用にマネージド アセンブリをインストールします。  
  
     多くのデータ ウェアハウジング ソリューションでは、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  など、その他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントもインストールする必要があります。  
  
    > [!NOTE]  
    >  セットアップ ウィザードの **[機能の選択]** ページでインストールを選ぶことができる一部の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントで、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントのサブセットの一部がインストールされます。 これらのコンポーネントを使用して一部のタスクを実行することは可能ですが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のすべての機能は使用できません。 たとえば、 **[データベース エンジン サービス]** オプションを選択すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] インポートおよびエクスポート ウィザードに必要な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントがインストールされます。 **[SQL Server Data Tools]** オプションを選択すると、パッケージのデザインに必要な [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントはインストールされますが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスはインストールされないので、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]外でパッケージを実行することはできません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を完全にインストールするには、 **[機能の選択]** ページで **[Integration Services]** を選択する必要があります。  
  
     **64 ビット コンピューターでのインストール** 64 ビット コンピューターでは、 **[Integration Services]** を選択すると、64 ビットのランタイムとツールのみがインストールされます。 パッケージを 32 ビット モードで実行する必要がある場合は、追加のオプションを選択して 32 ビットのランタイムとツールもインストールする必要があります。  
  
    -   64 ビット コンピューターで x86 オペレーティング システムが実行されている場合は、選択**SQL Server Data Tools**または**管理ツール - 完全**します。  
  
    -   64 ビット コンピューターで実行している場合、[!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]オペレーティング システムで、**管理ツール - 完全**します。  
  
     **ETL 専用のサーバーでのインストール** ETL (抽出、変換、読み込み) プロセス専用のサーバーを使用するには、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインストール時に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のローカル インスタンスをインストールすることをお勧めします。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、通常、パッケージを [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに格納し、このパッケージのスケジュールを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントに依存して設定します。 ETL サーバーに [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスが存在しない場合は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスが存在するサーバーからパッケージのスケジュール設定や実行を行う必要があります。 つまり、パッケージは、ETL サーバーではなく、パッケージが開始されたサーバーで実行されます。 その結果、専用の ETL サーバーのリソースは意図したとおりに使用されません。 さらに、他のサーバーのリソースが実行中の ETL プロセスによって使用される場合もあります。  
  
-   **インスタンスの構成**  
  
     **[インスタンスの構成]** ページで行う選択は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] または [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスに影響しません。  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのインスタンスは 1 台のコンピューターに 1 つだけインストールできます。 サービスに接続するには、コンピューター名を使用します。  
  
     既定では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、 **と同時にインストールされるデータベース エンジンのインスタンスの** msdb [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]データベースに格納されているパッケージを管理するように構成されます。 データベース エンジンのインスタンスが [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]と同時にインストールされない場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、 **の既定のローカル インスタンスの** msdb [!INCLUDE[ssDE](../../includes/ssde-md.md)]データベースに格納されているパッケージを管理するように構成されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の名前付きインスタンスまたはリモート インスタンス、あるいは [!INCLUDE[ssDE](../../includes/ssde-md.md)]の複数のインスタンスに格納されているパッケージを管理するには、構成ファイルを変更する必要があります。 この構成ファイルを変更する方法については、「[Integration Services サービスの構成 &#40;SSIS サービス&#41;](../service/integration-services-service-ssis-service.md)」を参照してください。  
  
-   **サーバー構成**  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [サーバーの構成] **ページの** [サービス アカウント] **タブで、** サービスの設定を確認します。  
  
     Windows 7 または Windows Server 2008 R2 がインストールされている場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] NT \msdtsserver120 の仮想アカウントで実行するサービスが登録されていると、**スタートアップの種類**は**自動**します。  仮想アカウントのパスワードを入力する必要はありません。 Microsoft Vista または Windows Server 2008 がインストールされている場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、ネットワーク サービス ビルトイン アカウントを使用して実行するように登録されており、 **[スタートアップの種類]** は **[自動]** になっています。 ネットワーク サービス ビルトイン アカウントのパスワードを入力する必要はありません。  
  
 既定では、新規インストールで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] はパッケージの実行に関連するイベントをアプリケーション イベント ログに記録しないように構成されます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のデータ コレクター機能を使用すると、この設定により、大量のイベント ログ エントリは生成されません。 ログに記録されないイベントは、EventID 12288 の "パッケージが起動されました。" や EventID 12289 の "パッケージが正常に完了しました。" です。 これらのイベントをアプリケーション イベント ログに記録するには、レジストリを編集用に開きます。 次に、レジストリ内で HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS ノードを見つけ、LogPackageExecutionToEventLog 設定の DWORD 値を 0 から 1 に変更します。  
  
## <a name="understanding-the-integration-services-service"></a>Integration Services サービスについて  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスがインストールされます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [機能の選択] **ページで** [Integration Services] **オプションを選択すると、** サービスがインストールされます。 **[サーバーの構成]** ページで既定の設定をそのまま使用すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが有効になり、その **[スタートアップの種類]** が **[自動]** になります。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのインスタンスは 1 台のコンピューターに 1 つだけインストールできます。 このサービスは、データベース エンジンの特定のインスタンスに固有ではありません。 サービスに接続するには、サービスが実行されているコンピューターの名前を使用します。  
  
## <a name="installing-integration-services-on-64-bit-computers"></a>64 ビット コンピューターへの Integration Services のインストール  
  
### <a name="integration-services-features-installed-on-64-bit-computers"></a>64 ビット コンピューターにインストールされる Integration Services 機能  
 セットアップにより、選択したセットアップ オプションに基づいてさまざまな [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 機能がインストールされます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールし、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールするように選択した場合、使用可能な 64 ビットの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 機能とツールがすべてインストールされます。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデザイン時機能が必要な場合は、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]もインストールする必要があります。  
  
-   特定のパッケージを 32 ビット モードで実行するために 32 ビット版の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ランタイムおよびツールが必要な場合は、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]もインストールする必要があります。  
  
 64 ビット バージョンの機能は、 **Program Files** ディレクトリに格納されます。32 ビット バージョンの機能は、 **Program Files (x86)** ディレクトリに別個にインストールされます。 この動作は [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に固有の動作ではありません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの 32 ビット開発環境であるは、 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 64 ビット オペレーティング システムではサポートされていないので、 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] サーバーにはインストールされません。  
  
  
