---
title: SQL Server 2014 | をインストールするためのハードウェアおよびソフトウェアの要件Microsoft Docs
ms.custom: ''
ms.date: 07/10/2018
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: ce6cef69abe7c2461552229363c8334ca56555b4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245663"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server-2014"></a>SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア

 > - **[無料の Developer edition](https://my.visualstudio.com/Downloads?q=SQL%20Server%20Developer)をインストールして、SQL Server 2016 をお試しください。**  
  
## <a name="considerations"></a>考慮事項 
  
-   NTFS ファイル形式[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のコンピューターでを実行することをお勧めします。 FAT32 ファイルシステムはサポートされていますが、NTFS ファイルシステムよりも安全性が低いため、推奨されません。  
  
-   読み取り専用、マップ、または圧縮されたドライブにをインストールすることはできません。  
  
-   Visual Studio コンポーネントが正しくインストールされるように[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]するには、で更新プログラムをインストールする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]この更新プログラムが存在するかどうかを確認するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インストールを続行する前に、更新プログラムをダウンロードしてインストールする必要があります。 セットアップ中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に中断されないようにするには、次に示すように、**セットアップを実行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する前に**更新プログラムをダウンロードしてインストールします (または、Windows Update で利用可能な .net 3.5 SP1 のすべての更新プログラムをインストールします)。  
  
    -   SP2 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]の場合は、[ここで](https://go.microsoft.com/fwlink/?LinkId=198093)必要な更新プログラムを入手してください。  
  
    -   その他のサポートされているオペレーティングシステムでは、この更新プログラムは含まれています。  
  
-   ターミナル サービス クライアントからの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップの起動はサポートされていません。 ターミナルサービスクライアントからセットアップを起動した場合、インストールは失敗します。   
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行すると、製品に必要な以下のソフトウェア コンポーネントがインストールされます。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セットアップサポートファイル  
  
-   または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[win8srv](../../includes/win8srv-md.md)] [!INCLUDE[win8](../../includes/win8-md.md)]にインストールするための最小バージョン要件については、「 [windows Server 2012 または windows 8 に SQL Server をインストール](https://support.microsoft.com/kb/2681562)する」 (https://support.microsoft.com/kb/2681562)を参照してください。  
  
 このトピックには、次のセクションが含まれます。  
  
-   [ハードウェアとソフトウェアの要件](hardware-and-software-requirements-for-installing-sql-server.md#hwswr)  
  
-   [プロセッサ、メモリ、およびオペレーティングシステムの要件](hardware-and-software-requirements-for-installing-sql-server.md#pmosr)  
  
-   [言語間サポート](hardware-and-software-requirements-for-installing-sql-server.md#CrossLanguageSupport)  
  
-   [拡張システムのサポート](hardware-and-software-requirements-for-installing-sql-server.md#ess)  
  
-   [必要なハード ディスク空き容量 (32 ビットおよび 64 ビット)](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)  
  
-   [データファイルのストレージの種類](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)  
  
-   [ドメインコントローラーへの SQL Server のインストール](hardware-and-software-requirements-for-installing-sql-server.md#DC_support)  
  
##  <a name="hwswr"></a>ハードウェアとソフトウェアの要件  
 次の要件は、すべての [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインストールに適用されます。  
  
|コンポーネント|要件|  
|---------------|-----------------|  
|.NET Framework|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、Replication、または [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]を選択した場合、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]には .NET 3.5 SP1 が必要です。このコンポーネントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップではインストールされなくなりました。 <br />-セットアップを実行していて、.NET 3.5 SP1 が[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インストールされていない場合、セットアップでは、インストールを続行する前に .net 3.5 sp1 をダウンロードしてインストールする必要があります。 ( [Microsoft .NET Framework 3.5 Service Pack 1](https://www.microsoft.com/download/details.aspx?id=22)から .NET 3.5 SP1 をインストールします)。エラーメッセージには、ダウンロードセンターへのリンクが含まれています。または、Windows Update から .NET 3.5 SP1 をダウンロードすることもできます。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップが中断されないようにするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行する前に .NET 3.5 SP1 をダウンロードしてインストールします。<br />-Sp1 または[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] [!INCLUDE[win8](../../includes/win8-md.md)]がインストールされているコンピューターでセットアップを実行する場合は、をインストール[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]する前に .NET Framework 3.5 SP1 を有効にする必要があります。<br />-インターネットにアクセスできない場合は、セットアップを実行して前述のコンポーネントのいずれかをインストールする前に .NET Framework 3.5 SP1 をダウンロードしてインストールする必要があります。 [!INCLUDE[win8](../../includes/win8-md.md)]および[!INCLUDE[win8srv](../../includes/win8srv-md.md)]で .NET Framework 3.5 を取得して有効にする方法に関する推奨事項とガイダンスの詳細については、「https://msdn.microsoft.com/library/windows/hardware/hh975396) [Microsoft .NET Framework 3.5 の展開に関する考慮事項](https://msdn.microsoft.com/library/windows/hardware/hh975396)」 (を参照してください。<br /><br /> .NET 4.0 は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では必須です。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、機能のインストール手順で .NET 4.0 がインストールされます。<br />-の[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]エディションをインストールする場合は、コンピューターでインターネット接続が使用可能であることを確認します。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、.NET Framework 4 がダウンロードされインストールされます。これは、.NET Framework 4 が [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] メディアに含まれていないためです。<br />-[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]では、SP1 または[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] [!INCLUDE[win8srv](../../includes/win8srv-md.md)]の Server Core モードに .net 4.0 がインストールされません。 
  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] SP1 または [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] の Server Core インストールに [!INCLUDE[win8srv](../../includes/win8srv-md.md)]をインストールする場合は、事前に .NET 4.0 をインストールしておく必要があります。|  
|Windows PowerShell|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では Windows PowerShell 2.0 のインストールおよび有効化は行われませんが、Windows PowerShell 2.0 は [!INCLUDE[ssDE](../../includes/ssde-md.md)] コンポーネントおよび [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の前提条件です。 セットアップ中に Windows PowerShell 2.0 がインストールされていないと報告された場合は、「 [Windows 管理フレームワーク](https://go.microsoft.com/fwlink/?LinkId=186214) 」ページの手順に従ってインストールまたは有効化することができます。|  
|ネットワーク ソフトウェア|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] でサポートされるオペレーティング システムにはネットワーク ソフトウェアが組み込まれています。 スタンドアロン インストールの名前付きインスタンスおよび既定のインスタンスは、次のネットワーク プロトコルをサポートします: 共有メモリ、名前付きパイプ、TCP/IP、および VIA。<br /><br /> 注: VIA プロトコルはフェールオーバー クラスターではサポートされません。 SQL Server インスタンスと同じフェールオーバー クラスターのノード上で実行されているクライアントまたはアプリケーションは、そのローカル パイプ アドレスを使用して SQL Server に接続するために、共有メモリ プロトコルを使用することができます。 ただし、この種の接続はクラスターに対応しないため、インスタンスのフェールオーバー後に失敗します。 したがって、これは非推奨であり、非常に限られたシナリオでのみ使用する必要があります。 VIA プロトコルは非推奨とされます。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br /><br /> ネットワーク プロトコルとネットワーク ライブラリの詳細については、「 [Network Protocols and Network Libraries](network-protocols-and-network-libraries.md)」を参照してください。|  
|仮想化|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] は、以下の Hyper-V ロールで実行される仮想マシン環境でサポートされます。<br />-<br />                    
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard、Enterprise、および Datacenter Edition<br />-[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard、Enterprise、Datacenter の各エディション。<br />-<br />                    
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter および Standard Edition。<br /><br /> 親パーティションに必要なリソースに加えて、各仮想マシン (子パーティション) には [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インスタンス用に十分なプロセッサ リソース、メモリ、およびディスク リソースが必要です。 要件はこのトピックの後半に記載されています。\*<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 または [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 の Hyper-V ロール内では、最大 4 つの仮想プロセッサを、 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 の 32 ビットまたは 64 ビット エディション、または [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 の 64 ビット、または [!INCLUDE[win8srv](../../includes/win8srv-md.md)] の 64 ビット エディションを実行する仮想マシンに割り当てることができます。<br /><br /> Hyper-v ロール内[!INCLUDE[win8srv](../../includes/win8srv-md.md)]:<br />
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 32/64 ビットを実行する仮想マシンには、最大 8 個の仮想プロセッサを割り当てることができます。<br />
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 ビットまたは [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 ビット エディションを実行する仮想マシンには、最大 64 個の仮想プロセッサを割り当てることができます。<br /><br /> の各エディションの計算容量の制限と、ハイパー [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]スレッドプロセッサを使用した物理環境と仮想化環境での違いの詳細については、「 [SQL Server のエディション別の計算容量制限](../compute-capacity-limits-by-edition-of-sql-server.md)」を参照してください。 Hyper-V ロールの詳細については、 [Windows Server 2008 の Web サイト](https://go.microsoft.com/fwlink/?LinkId=182820)を参照してください。<br /><br /> ** \*重要\* \* **では、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ゲストフェールオーバークラスタリングがサポートされています。 ゲスト フェールオーバー クラスタリングをサポートする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] およびオペレーティング システムのバージョンの詳細については、「 [ハードウェア仮想化環境で Microsoft SQL Server 製品を実行する場合のサポート ポリシー](https://go.microsoft.com/fwlink/?LinkId=151676)」を参照してください。|  
|ハード ディスク|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では 6 GB 以上のハード ディスク空き容量が必要です。<br /><br /> 必要となるディスク空き容量は、インストールする [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のコンポーネントに応じて異なります。 詳細については、このトピックの「 [Hard Disk Space Requirements (32-Bit and 64 Bit)](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) 」を参照してください。 データ ファイルでサポートされているストレージの種類の詳細については、「 [Storage Types for Data Files](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)」を参照してください。|  
|ドライブ|ディスクからインストールする場合は、DVD ドライブが必要です。|  
|監視|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では Super-VGA (800x600) 以上の解像度のモニターが必要です。|  
|インターネット|インターネット機能にはインターネット アクセス (有料) が必要です。|  
  
 * 仮想[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]マシンで実行されるのは、仮想化のオーバーヘッドのためにネイティブで実行する場合よりも遅くなります。  
  
##  <a name="pmosr"></a>プロセッサ、メモリ、およびオペレーティングシステムの要件  
 次に示すメモリおよびプロセッサの要件は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のすべてのエディションに適用されます。  
  
|コンポーネント|要件|  
|---------------|-----------------|  
|メモリ<sup>[1]</sup>|**以降**<br /><br /> Express Edition: 512 MB<br /><br /> その他すべてのエディション: 1 GB<br /><br /> **しない**<br /><br /> Express Edition: 1 GB<br /><br /> 他のすべてのエディション: 4 GB 以上。最適なパフォーマンスを確保するために、データベースのサイズが大きくなるにつれて増やす必要があります。|  
|プロセッサの速度|**以降**<br /><br /> x86 プロセッサ: 1.0 GHz<br /><br /> x64 プロセッサ: 1.4 GHz<br /><br /> **推奨:** 2.0 GHz 以上|  
|プロセッサの種類|x64 Processor: AMD Opteron、AMD Athlon 64、Intel EM64T 対応の Intel Xeon、EM64T 対応の Intel Pentium IV<br /><br /> x86 プロセッサ: Pentium III 互換プロセッサ以上|  
  
 <sup>[1]</sup>(DQS) で[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]コンポーネントをインストールするために必要な最小メモリは 2 GB の RAM で、これは[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]最小メモリ要件とは異なります。 DQS のインストールの詳細については、「 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)」を参照してください。  
  
 **WOW64 のサポート:**  
  
 WOW64 (Windows 32-bit on Windows 64-bit) は 64 ビット版 Windows の機能で、32 ビット アプリケーションをネイティブの 32 ビット モードで実行することができます。 つまり、基盤となるオペレーティング システムが 64 ビット オペレーティング システムであっても、アプリケーションは 32 ビット モードで動作します。  
  
-   サポートされている 64 ビット オペレーティング システムでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 ビット エディションを、64 ビット サーバーの WOW64 32 ビット サブシステムにインストールできます。 WOW64 は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のスタンドアロン インスタンスでのみサポートされています。 WOW64 は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インストールではサポートされていません。  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 ビット エディションが、サポートされている 64 ビット オペレーティング システムにインストールされている場合、管理ツールは WOW64 でサポートされます。 サポートされているオペレーティング システムの詳細を表示するには、以下の各セクションから [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のエディションを選択してください。  
  
 **Server Core のサポート:**  

 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] は Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016、および Windows Server 2019 の Server Core インストールでサポートされています。 


  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインストールは、次のエディションの Windows Server の Server Core モードでサポートされます。

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| Windows Server 2012 R2 Standard | Windows Server 2012 R2 Datacenter|
| Windows Server 2012 Standard | Windows Server 2012 Datacenter |
| Windows Server 2008 R2 SP1 Standard | Windows Server 2008 R2 SP1 Datacenter |
| Windows Server 2008 R2 SP1 Enterprise | Windows Server 2008 R2 SP1 Web|
   | &nbsp; | &nbsp; |
  
 Server Core へのの[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]インストールの詳細については、「 [Install SQL Server 2014 on server core](../../database-engine/install-windows/install-sql-server-on-server-core.md)」を参照してください。  
  
   >[!NOTE]
   > 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 ビット x64 Standard Edition でサポートされている [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] の各エディションは、[!INCLUDE[sbs_2](../../includes/sbs-2-md.md)] 64 ビット x64 でもサポートされています。  
  
 **オペレーティングシステムのサポート:**  
  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のエディションは次のように分類されます。  
  
-   [SQL Server 2014 のプリンシパル エディション](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [SQL Server 2014 の特別エディション](hardware-and-software-requirements-for-installing-sql-server.md#TOP_SP)  
  
-   [SQL Server 2014 の拡張エディション](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
###  <a name="TOP_Principal"></a>プリンシパルエディションのオペレーティングシステムの要件  
 次の表は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のプリンシパル エディションのオペレーティング システム要件を示しています。  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Edition|32 ビット|64 ビット|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 ビット|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ビジネスインテリジェンス|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 ビット|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|Windows 10 Home 64 ビット<br /><br /> Windows 10 Professional 64 ビット<br /><br /> Windows 10 Enterprise 64 ビット<br /><br /> Windows 10 Home 32 ビット<br /><br /> Windows 10 Professional 32 ビット<br /><br /> Windows 10 Enterprise 32 ビット<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32ビット<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32ビット<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32ビット<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32ビット<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32ビット<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32ビット<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)].SP1 Professional 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)].SP1 Professional 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 ビット|Windows 10 Home 64 ビット<br /><br /> Windows 10 Professional 64 ビット<br /><br /> Windows 10 Enterprise 64 ビット<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)].SP1 Professional 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット| 
  
###  <a name="TOP_SP"></a>特別なエディションのオペレーティングシステム要件  
 次の表は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の特別エディションのオペレーティング システム要件を示しています。  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Edition|32 ビット|64 ビット|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|Windows 10 Home 64 ビット<br /><br /> Windows 10 Professional 64 ビット<br /><br /> Windows 10 Enterprise 64 ビット<br /><br /> Windows 10 Home 32 ビット<br /><br /> Windows 10 Professional 32 ビット<br /><br /> Windows 10 Enterprise 32 ビット<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 ビット|Windows 10 Home 64 ビット<br /><br /> Windows 10 Professional 64 ビット<br /><br /> Windows 10 Enterprise 64 ビット<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット| 
  
###  <a name="TOP_Breadth"></a>広範なエディションのオペレーティングシステム要件
 次の表は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の拡張エディションのオペレーティング システム要件を示しています。  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Edition|32 ビット|64 ビット|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|Windows 10 Home 64 ビット<br /><br /> Windows 10 Professional 64 ビット<br /><br /> Windows 10 Enterprise 64 ビット<br /><br /> Windows 10 Home 32 ビット<br /><br /> Windows 10 Professional 32 ビット<br /><br /> Windows 10 Enterprise 32 ビット<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32ビット<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32ビット<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32ビット<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32ビット<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32ビット<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32ビット<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)].SP1 Professional 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)].SP1 Professional 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 ビット|Windows 10 Home 64 ビット<br /><br /> Windows 10 Professional 64 ビット<br /><br /> Windows 10 Enterprise 64 ビット<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br />
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)].SP1 Professional 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|Windows 10 Home 64 ビット<br /><br /> Windows 10 Professional 64 ビット<br /><br /> Windows 10 Enterprise 64 ビット<br /><br /> Windows 10 Home 32 ビット<br /><br /> Windows 10 Professional 32 ビット<br /><br /> Windows 10 Enterprise 32 ビット<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32ビット<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32ビット<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32ビット<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32ビット<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32ビット<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32ビット<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)].SP1 Professional 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)].SP1 Professional 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 32 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 32 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 ビット|Windows 10 Home 64 ビット<br /><br /> Windows 10 Professional 64 ビット<br /><br /> Windows 10 Enterprise 64 ビット<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 ビット<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Standard 64-bit<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 ビット<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Enterprise 64 ビット<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard 64-bit<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 ビット<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64ビット<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Ultimate 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)].SP1 Professional 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Premium 64 ビット<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 Home Basic 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Datacenter 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Foundation 64 ビット<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 64 ビット|  
  
## <a name="minimum-sql-server-version-requirements-for-windows-10"></a>Windows 10 の SQL Server バージョンの最小要件  
 Windows 10 を実行しているコンピューターに SQL Server をインストールする前に、次の最小要件を満たしていることを確認する必要があります。  
  
-   SQL Server 2014 では、SQL Server 2014 の Service Pack 1 以降の更新プログラムを適用する必要があります。 詳しくは、「 [SQL Server 2014 の最新のサービス パックの入手方法](https://support.microsoft.com/kb/2958069)」をご覧ください。  
  
-   SQL Server 2012 では、SQL Server 2012 Service Pack 2 以降の更新プログラムを適用する必要があります。 詳しくは、「 [SQL Server 2012 の最新のサービス パックの入手方法](https://support.microsoft.com/kb/2755533)」をご覧ください。  
  
-   SQL Server 2008 R2  
    と SQL Server 2008 は、Windows 10 ではサポートされていません。  
  
##  <a name="CrossLanguageSupport"></a>言語間サポート  
 各言語にローカライズされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールする場合の言語間サポートと注意点の詳細については、「 [SQL Server のローカル言語版](local-language-versions-in-sql-server.md)」を参照してください。  
  
##  <a name="ess"></a>拡張システムサポート  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 ビット版は、WOW64 (Windows 32-bit on Windows 64-bit) という拡張システムをサポートしています。 WOW64 は 64 ビット版 Windows の機能であり、これによって 32 ビット アプリケーションをネイティブの 32 ビット モードで実行することが可能になります。 つまり、基盤となるオペレーティング システムが 64 ビットでも、アプリケーションは 32 ビット モードで動作します。  
  
##  <a name="HardDiskSpace"></a>ハードディスク領域の要件 (32 ビットおよび64ビット)  
 インストール中 Windows インストーラーは、システムドライブ上に一時ファイルを作成します。 セットアップを実行してインストールまたは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]アップグレードする前に、これらのファイルについて、少なくとも**6.0 GB**の空きディスク領域がシステムドライブにあることを確認してください。 この要件は、既定以外のドライブにコンポーネントをインストールした場合でも適用されます。  
  
 実際に必要なハード ディスク空き容量は、システム構成と、インストールする機能によって異なります。 の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各エディションでサポートされる機能の一覧については、「 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」を参照してください。 次の表は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の各コンポーネントに必要なディスク空き容量を示しています。  
  
|**機能**|**必要なディスク領域**|  
|-----------------|--------------------------------|  
|
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] とデータ ファイル、レプリケーション、フルテキスト検索、および Data Quality Services|811 MB|  
|
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] およびデータ ファイル|345 MB|  
|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] およびレポート マネージャー|304 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|591 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|243 MB|  
|クライアント コンポーネント ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブック コンポーネントと Integration Services ツール以外)|1823 MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ヘルプコンテンツを表示および管理するためのオンラインブックコンポーネント<sup>1</sup>|375 KB|  
  
 <sup>1</sup>ダウンロードしたオンラインブックコンテンツに必要なディスク領域は、200 MB です。  
  
##  <a name="StorageTypes"></a>データファイルのストレージの種類  
 データ ファイルでサポートされているストレージの種類は、次のとおりです。  
  
-   ローカル ディスク  
  
-   ストレージの共有  
  
-   SMB ファイル共有  
  
    > **注:** SMB 記憶域は、スタンドアロン[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インストールまたはクラスター化インストールのデータファイルに対してはサポートされていません。 代わりに、直接アタッチされたストレージまたはストレージ エリア ネットワークを使用してください。  
  
    > **大事な！！** SMB ストレージは、Windows ファイル サーバーまたはサード パーティ SMB ストレージ デバイスによってホストされます。 Windows ファイル サーバーが使用される場合、Windows ファイル サーバーのバージョンは 2008 以降である必要があります。 ストレージ オプションとして SMB ファイル共有をとして使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールの詳細については、「 [SQL Server をストレージ オプションとして SMB ファイル共有にインストールする](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)のインストールおよび実行に必要な最低限のハードウェア要件とソフトウェア要件について説明します。  
  
    > **警告!!!!**  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインストールでは、tempdb ファイルをインストールする場合のみローカル ディスクがサポートされます。 Tempdb のデータファイルとログファイルに指定されたパスが、**すべて**のクラスターノードで有効であることを確認してください。 フェールオーバー中に、tempdb のディレクトリがフェールオーバーのターゲット ノード上で利用できない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースはオンラインへの移行に失敗します。  
  
##  <a name="DC_support"></a>ドメイン[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]コントローラーへののインストール-制限事項  
 セキュリティ上の理由から、ドメイン コントローラーには [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] をインストールしないことをお勧めします。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時にインストールが中止されることはありませんが、次の制限事項が適用されます。  
  
-   ローカル サービス アカウントを使用して、ドメイン コントローラー上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを実行することはできません。  
  
-   コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールした後で、そのコンピューターをドメイン メンバーからドメイン コントローラーに変更することはできません。 ホスト コンピューターをドメイン コントローラーに変更する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールする必要があります。  
  
-   コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールした後で、そのコンピューターをドメイン コントローラーからドメイン メンバーに変更することはできません。 ホスト コンピューターをドメイン メンバーに変更する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールする必要があります。  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスは、クラスター ノードがドメイン コントローラーの場合はサポートされません。  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、読み取り専用ドメイン コントローラーにセキュリティ グループを作成したり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを準備したりすることはできません。 この場合、セットアップは失敗します。  
  
## <a name="see-also"></a>参照  
 [SQL Server インストールの計画](planning-a-sql-server-installation.md)   
 [SQL Server インストールのセキュリティに関する考慮事項](security-considerations-for-a-sql-server-installation.md)   
 [SQL Server 2014 の製品仕様](../../getting-started/sql-server-2014-product-specifications.md)  
