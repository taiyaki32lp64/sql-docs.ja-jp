---
title: SQL Server のインストールに必要なハードウェアおよびソフトウェア | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 553c01ea02c83a57370e596d67ad077b43328d9b
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056801"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>SQL Server のインストールに必要なハードウェアおよびソフトウェア
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、Windows オペレーティング システムでの [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] のインストールと実行に必要な最低限のハードウェア要件とソフトウェア要件について説明します。 

[!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)] では、Linux での [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] が新たにサポートされました。 詳細については、[Linux での [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールに必要なハードウェアおよびソフトウェア](../../linux/sql-server-linux-setup.md#system)に関するページを参照してください。 

  
**お試しください:**  
  
-   [**Evaluation Center**](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)から SQL Server をダウンロードします。 
  
-   [**SQL Server 2017**](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) がインストール済みの仮想マシンをすぐにご利用いただけます。  
  
**すべてのエディションに次の考慮事項が適用されます。**  
  
-   [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] は NTFS または ReFS ファイル形式のコンピューターで実行することをお勧めします。 FAT32 ファイル システムのコンピューターへの [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] のインストールはサポートされていますが、NTFS または ReFS ファイル システムよりも安全性が低いためお勧めしません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、読み取り専用ドライブ、マップされたドライブ、または圧縮されたドライブでのインストールがブロックされます。  
  
-   リモート デスクトップ接続で、RDC クライアントのローカル リソースのメディアを使用して、セットアップを起動した場合、インストールは失敗します。 リモートでインストールするには、メディアをネットワーク共有に配置するか、物理または仮想マシンのローカルに配置する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール メディアは、ネットワーク共有、マッピングされたドライブ、またはローカル ドライブに配置するか、仮想マシンに ISO として配置する必要があります。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のインストールでは、前提条件として .NET 4.6.1 をインストールする必要があります。 .NET 4.6.1 は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の選択時のセットアップに応じて自動的にインストールされます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行すると、製品に必要な以下のソフトウェア コンポーネントがインストールされます。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ サポート ファイル  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を [!INCLUDE[win8srv](../../includes/win8srv-md.md)] または [!INCLUDE[win8](../../includes/win8-md.md)] にインストールするための最低限のバージョン要件については、[ Windows Server 2012 または Windows 8 への SQL Server のインストール](https://support.microsoft.com/kb/2681562)に関するページを参照してください。  
  
##  <a name="hwswr"></a> ハードウェアとソフトウェアの要件  
次の要件は、すべてのインストールに適用されます。  
  
|コンポーネント|要件|  
|---------------|-----------------|  
|.NET Framework|[!INCLUDE[sql2016](../../includes/sssql15-md.md)] RC1 以降では、データベース エンジン、マスター データ サービス、レプリケーションのために [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 が必要になります。 SQL Server セットアップで [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] が自動的にインストールされます。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Microsoft .NET Framework 4.6 (Web Installer) for Windows [から](https://support.microsoft.com/kb/3045560)を手動でインストールすることもできます。<br/><br/>[!INCLUDE[sql2019](../../includes/sssqlv15-md.md)] では .NET Framework 4.6.2 が必要です。 [ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=53344)から入手できます<br/><br/> [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 の詳細、推奨事項、ガイダンスについては、「 [.NET Framework 配置ガイド (開発者向け)](https://msdn.microsoft.com/library/ee942965\(v=vs.110\).aspx)」を参照してください。<br/><br/>[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 をインストールするには、[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)] と [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)] に [KB2919355](https://support.microsoft.com/kb/2919355) が必要になります。|  
|ネットワーク ソフトウェア|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] でサポートされるオペレーティング システムにはネットワーク ソフトウェアが組み込まれています。 スタンドアロン インストールの名前付きおよび既定のインスタンスでは、次のネットワーク プロトコルがサポートされています。共有メモリ、名前付きパイプ、TCP/IP、および VIA。<br/><br/> **注:** VIA プロトコルはフェールオーバー クラスターではサポートされません。 SQL Server インスタンスと同じフェールオーバー クラスターのノード上で実行されているクライアントまたはアプリケーションは、そのローカル パイプ アドレスを使用して SQL Server に接続するために、共有メモリ プロトコルを使用することができます。 ただし、この種の接続はクラスターに対応しないため、インスタンスのフェールオーバー後に失敗します。 したがって、これは非推奨であり、非常に限られたシナリオでのみ使用する必要があります。<br/><br/> **重要:** VIA プロトコルは非推奨とされます。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br/><br/> ネットワーク プロトコルとネットワーク ライブラリの詳細については、「 [Network Protocols and Network Libraries](../../sql-server/install/network-protocols-and-network-libraries.md)」を参照してください。|  
|ハード ディスク|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] では 6 GB 以上のハード ディスク空き容量が必要です。<br/><br/> 必要となるディスク空き容量は、インストールする [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] のコンポーネントに応じて異なります。 詳細については、この記事で後述する「[必要なハード ディスク空き容量](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)」を参照してください。 データ ファイルでサポートされているストレージの種類の詳細については、「 [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)」を参照してください。|  
|ドライブ|ディスクからインストールする場合は、DVD ドライブが必要です。|  
|モニター|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] では Super-VGA (800x600) 以上の解像度のモニターが必要です。|  
|インターネット|インターネット機能にはインターネット アクセス (有料) が必要です。|  
  
> [!NOTE]
> 仮想マシンで [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] を実行すると、仮想化のオーバーヘッドのために、ネイティブで実行した場合よりも遅くなります。  
  
> [!IMPORTANT]
> PolyBase 機能には、ハードウェアとソフトウェアに追加の要件があります。 詳細については、「 [PolyBase 入門](../../relational-databases/polybase/get-started-with-polybase.md)」を参照してください。  
  
##  <a name="pmosr"></a> プロセッサ、メモリ、およびオペレーティング システムの要件  
 次に示すメモリおよびプロセッサの要件は [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]のすべてのエディションに適用されます。  
  
|コンポーネント|要件|  
|---------------|-----------------|  
|メモリ \*|**最小:**<br/><br/> Express Edition: 512 MB<br/><br/> 他のすべてのエディション: 1 GB<br/><br/> **推奨:**<br/><br/> Express Edition: 1 GB<br/><br/> 他のすべてのエディション: 4 GB 以上。最適なパフォーマンスを確保するために、データベースのサイズが大きくなるにつれて増やす必要があります。|  
|プロセッサの速度|**最小:** x64 プロセッサ:1.4 GHz<br/><br/> **推奨:** 2.0 GHz 以上|  
|プロセッサの種類|x64 プロセッサ: AMD Opteron、AMD Athlon 64、Intel Xeon (Intel EM64T 対応)、Intel Pentium IV (EM64T 対応)|  
  
> [!NOTE]  
> [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] は x64 プロセッサでのみイントールできます。 X86 プロセッサではインストールできません。  
  
 \* [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) の [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンポーネントをインストールする場合の最小メモリ要件は 2 GB の RAM で、[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] の最小メモリ要件とは異なります。 DQS のインストールの詳細については、「 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)」を参照してください。  
  
 **WOW64 サポート:**  
  
 WOW64 (Windows 32-bit on Windows 64-bit) は 64 ビット版 Windows の機能で、32 ビット アプリケーションをネイティブの 32 ビット モードで実行することができます。 つまり、基盤となるオペレーティング システムが 64 ビット オペレーティング システムであっても、アプリケーションは 32 ビット モードで動作します。 WOW64 は、 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] インストールではサポートされていません。 ただし、管理ツールは WOW64 でサポートされています。  


**Server Core サポート:**

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 

SQL Server 2019 の Server Core モードでのインストールは、次のエディションの Windows Server でサポートされます。

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
   | &nbsp; | &nbsp; |

::: moniker-end

::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"

SQL Server 2016 および 2017 の Server Core モードでのインストールは、次のエディションの Windows Server でサポートされます。

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| Windows Server 2012 R2 Standard | Windows Server 2012 R2 Datacenter|
| Windows Server 2012 Standard | Windows Server 2012 Datacenter |
| &nbsp; | &nbsp; |
::: moniker-end

Server Core への SQL Server のインストールの詳細については、「[Server Core への SQL Server のインストール](../../database-engine/install-windows/install-sql-server-on-server-core.md)」を参照してください。  

  
### <a name="features-supported-on-32-bit-client-operating-systems"></a>32 ビット クライアント オペレーティング システムでサポートされている機能  
 Windows 10 や Windows 8.1 など、Windows クライアント オペレーティング システムは 32 ビットまたは 64 ビットのアーキテクチャとして利用できます。   すべての SQL Server 機能は 64 ビット クライアント オペレーティング システムでサポートされています。 サポートされている 32 ビット クライアント オペレーティング システムでは、マイクロソフトは次の機能をサポートします。  
  
-   Data Quality クライアント
-   クライアント ツール接続
-   Integration Services
-   クライアント ツールの旧バージョンとの互換性
-   クライアント ツール SDK
-   Documentation コンポーネント
-   分散再生コンポーネント
-   分散再生コントローラー
-   分散再生クライアント
-   SQL クライアント接続 SDK
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 以降のサーバー オペレーティング システムは 32 ビットのアーキテクチャとして利用できません。 サポートされているサーバー オペレーティング システムはすべて 64 ビットのみを利用できます。 すべての機能は 64 ビット サーバー オペレーティング システムでサポートされています。  
  
###  <a name="TOP_Principal"></a> OS の互換性   

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 
次の表では、Windows のバージョンと SQL Server 2019 のエディションとの互換性を示します。  
  

| SQL Server のエディション:               | Enterprise | Developer | Standard | Web | Express |  
| :------------------------         | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2019 Standard      |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2019 Essentials    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2016 Datacenter    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2016 Standard      |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2016 Essentials    |    はい     |    はい    |    はい   | はい |   はい   |
| &nbsp; | &nbsp; |
::: moniker-end

::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"

次の表では、Windows のバージョンと SQL Server 2016 と 2017 のエディションとの互換性を示します。  
  
| SQL Server のエディション:               | Enterprise | Developer | Standard | Web | Express |  
| :------------------------         | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2019 Standard      |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2019 Essentials    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2016 Datacenter    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2016 Standard      |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2016 Essentials    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 R2 Datacenter |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 R2 Standard   |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 R2 Essentials |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 R2 Foundation |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 Datacenter    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 Standard      |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 Essentials    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows Server 2012 Foundation    |    はい     |    はい    |    はい   | はい |   はい   |
| Windows 10 IoT Enterprise         |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 10 Enterprise             |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 10 Professional           |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 10 Home                   |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8.1 Enterprise            |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8.1 Pro                   |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8.1 Enterprise            |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8 Pro                     |    いいえ      |    はい    |    はい   | いいえ  |   はい   |
| Windows 8                         |    いいえ      |    はい    |    はい   | いいえ  |   はい   | 

> [!NOTE]  
> このセクションで注記されているオペレーティング システム サポートの例外は、以下の [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以前の Business Intelligence 機能です。これは Windows Server 2008 R2 SP1 以降にインストールできます。  
>  
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint  
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 製品用アドイン  
::: moniker-end


  
##  <a name="CrossLanguageSupport"></a> 言語間サポート  
 各言語にローカライズされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールする場合の言語間サポートと注意点の詳細については、「 [SQL Server のローカル言語版](../../sql-server/install/local-language-versions-in-sql-server.md)」を参照してください。  
  
##  <a name="HardDiskSpace"></a> 必要なハード ディスク空き容量  
 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]のインストール中は、Windows インストーラーによってシステム ドライブ上に一時ファイルが作成されます。 したがって、セットアップを実行して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールまたはアップグレードする前に、これらの一時ファイル用に 6.0 GB 以上の空き容量がシステム ドライブにあることを確認してください。 この要件は、既定以外のドライブに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントをインストールする場合にも適用されます。  
  
 実際に必要なハード ディスク空き容量は、システム構成と、インストールする機能によって異なります。 次の表は、 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] の各コンポーネントに必要なディスク空き容量を示しています。  
  
|**機能**|**必要なディスク空き容量**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] とデータ ファイル、レプリケーション、フルテキスト検索、および Data Quality Services|1480 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (上記と同じ) と R Services (データベース内)|2744 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (上記と同じ) と外部データ用 PolyBase クエリ サービス|4194 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] およびデータ ファイル|698 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (スタンドアロン)|280 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|1203 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 製品用アドイン|325 MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 MB|  
|クライアント ツール接続|328 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 MB|  
|クライアント コンポーネント ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブック コンポーネントと Integration Services ツール以外)|445 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブック コンポーネント (ヘルプ コンテンツを表示し、管理する)*|27 MB|  
|すべての機能|8030 MB|  
  
 *ダウンロードされるオンライン ブック コンテンツに必要なディスク領域は 200 MB です。  
  
##  <a name="StorageTypes"></a> データ ファイルのストレージの種類  
 データ ファイルでサポートされているストレージの種類は、次のとおりです。  
  
-   ローカル ディスク 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は現在、標準のネイティブ セクター サイズである 512 バイトと 4 KB のディスク ドライブに対応しています。  ハード ディスクのセクター サイズが 4 KB を超える場合、それに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ファイルを格納しようとするとエラーが発生することがあります。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされているハード ディスク セクターのサイズに関する詳細については、[SQL Server でのハード ディスク ドライブ セクターのサイズのサポート範囲](https://support.microsoft.com/kb/926930)に関するページを参照してください。 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインストールでは、tempdb ファイルをインストールする場合のみローカル ディスクがサポートされます。 tempdb のデータ ファイルおよびログ ファイルに指定されたパスが、すべてのクラスター ノードで有効であることを確認してください。 フェールオーバー中に、tempdb のディレクトリがフェールオーバーのターゲット ノード上で利用できない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースはオンラインへの移行に失敗します。
-   ストレージの共有  
-   [記憶域スペース ダイレクト \(S2D\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)  
-   SMB ファイル共有  
    - スタンドアロン インストールやクラスター化されたインストールでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ファイルに対して SMB ストレージはサポートされていません。 代わりに、直接アタッチされたストレージ、ストレージ エリア ネットワーク、または S2D を使用してください。 
    - SMB ストレージは、Windows ファイル サーバーまたはサード パーティ SMB ストレージ デバイスによってホストされます。 Windows ファイル サーバーが使用される場合、Windows ファイル サーバーのバージョンは 2008 以降である必要があります。 ストレージ オプションとして SMB ファイル共有をとして使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールの詳細については、「 [SQL Server をストレージ オプションとして SMB ファイル共有にインストールする](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)のインストールおよび実行に必要な最低限のハードウェア要件とソフトウェア要件について説明します。  
  
  
  
##  <a name="DC_support"></a>ドメイン コントローラーへの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール  
 セキュリティ上の理由から、ドメイン コントローラーには [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] をインストールしないことをお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時にインストールが中止されることはありませんが、次の制限事項が適用されます。  
  
-   ローカル サービス アカウントを使用して、ドメイン コントローラー上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを実行することはできません。    
-   コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールした後で、そのコンピューターをドメイン メンバーからドメイン コントローラーに変更することはできません。 ホスト コンピューターをドメイン コントローラーに変更する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールする必要があります。    
-   コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールした後で、そのコンピューターをドメイン コントローラーからドメイン メンバーに変更することはできません。 ホスト コンピューターをドメイン メンバーに変更する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールする必要があります。   
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスは、クラスター ノードがドメイン コントローラーの場合はサポートされません。   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、読み取り専用ドメイン コントローラーではサポートされません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、読み取り専用ドメイン コントローラーにセキュリティ グループを作成したり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを準備したりすることはできません。 この場合、セットアップは失敗します。 

  > [!NOTE]
  > この制限は、ドメイン メンバー ノードへのインストールにも適用されます。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスは、読み取り専用ドメイン コントローラーのみにアクセスできる環境ではサポートされません。 

  > [!NOTE]
  > この制限は、ドメイン メンバー ノードへのインストールにも適用されます。
  
## <a name="see-also"></a>参照  
 [SQL Server のインストール計画](../../sql-server/install/planning-a-sql-server-installation.md)   
 [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   

