---
title: サポートされているバージョンとエディションのアップグレード - SQL Server 2019 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 6cff48da9e251fedd56d676349480e350c88bcae
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531535"
---
# <a name="supported-version-and-edition-upgrades-for-sql-server-2019"></a>SQL Server 2019 のサポートされているバージョンとエディションのアップグレード

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、[!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]、および [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] からアップグレードできます。 この記事では、これらの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンからのサポートされているアップグレード パスと、サポートされている [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] へのエディションのアップグレードを示します。  
  
## <a name="pre-upgrade-checklist"></a>アップグレード前のチェック リスト  

- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] のいずれかのエディションから別のエディションへアップグレードする前に、現在使用している機能が移動先のエディションでサポートされているかどうかを確認します。  
- サポートされている[ハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)を確認する。
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアップグレードする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの Windows 認証を有効にし、既定の構成 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサービス アカウントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin グループのメンバーであること) を確認してください。
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] にアップグレードするには、サポート対象のオペレーティング システムを実行している必要があります。 詳細については、「[SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)」を参照してください。  
- 再起動を保留している場合はアップグレードがブロックされます。  
- Windows インストーラー サービスが実行されていない場合は、アップグレードがブロックされます。

## <a name="unsupported-scenarios"></a>サポートされていないシナリオ

- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] の複数バージョンにまたがるインスタンスの使用はサポートされていません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] コンポーネントのバージョン番号は、[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] のインスタンス内で同一である必要があります。  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] は、64 ビット プラットフォームでのみ利用できます。 クロスプラットフォームのアップグレードはサポートされていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 32 ビット インスタンスをネイティブ 64 ビットにアップグレードすることはできません。 ただし、データベースがレプリケーションでパブリッシュされていない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の 32 ビット インスタンスのデータベースをバックアップまたはデタッチしてから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンス (64 ビット) に復元またはアタッチすることができます。 master、msdb、および model の各システム データベースにある、すべてのログインとその他のユーザー オブジェクトを再作成する必要があります。  
  
- 既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスのアップグレード中は、新しい機能を追加できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] にアップグレードした後、[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] のセットアップを使用して機能を追加できます。 詳細については、「[SQL Server のインスタンスへの機能の追加 &#40;セットアップ&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)」を参照してください。  
 
## <a name="upgrades-from-earlier-versions-to-includesssqlv15-mdincludessssqlv15-mdmd"></a>以前のバージョンから [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]  
 
[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] では、次のバージョンの SQL Server からのアップグレードがサポートされます。

- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 以降
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP3 以降
- [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] SP2 以降
- [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]

次の表に示すのは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]への、サポートされるアップグレード シナリオです。  
  
|アップグレード元|サポートされているアップグレード パス|  
|:------|:------|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/>[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] リリース候補 * |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise |  
|[!INCLUDE[sssqlv15_md](../../includes/sssqlv15-md.md)] Developer |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise | 

 \* Microsoft では、特に早期導入者プログラムに参加したお客様向けに、リリース候補版ソフトウェアからのアップグレードをサポートしています。

## <a name="migrate-to-sql-server-2019"></a>SQL Server 2019 への移行

古いバージョンのデータベースを移行することができます。 たとえば、[!INCLUDE [sskilimanjaro-md](../../includes/sskilimanjaro-md.md)] から SQL Server 2019 にデータベースを移行できます。

詳細については、[Azure データベースの移行ガイド](https://datamigration.microsoft.com/scenario/sql-to-sqlserver)に関するページを参照してください。

次のヒントとツールは、移行の計画と実装に役立ちます。

- 移行ツール:移行は [Data Migration Assistant (DMA)](https://aka.ms/dma) を通じてサポートされます。
- バックアップと復元:SQL Server 2008 または SQL Server 2008 R2 で作成されたバックアップは、SQL Server 2019 に復元できます。
- ログ配布:ログ配布は、プライマリが SQL Server 2008 SP3 以降、または SQL Server 2008 R2 SP2 以降を実行していて、セカンダリが SQL Server 2019 で実行されている場合にサポートされます。 

   > [!WARNING]
   > 自動または手動フェールオーバーが発生し、SQL Server 2019 インスタンスがプライマリになった場合は、SQL Server 2008 または SQL Server 2008 R2 インスタンスはセカンダリになり、プライマリから変更を受け取ることはできません。

- 一括読み込み:テーブルは、SQL Server 2008 または SQL Server 2008 R2 から SQL Server 2019 に一括コピーすることができます。

## <a name="includesssqlv15-mdincludessssqlv15-mdmd-edition-upgrade"></a>[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] エディションのアップグレード 

次の表に示すのは、 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]でサポートされるエディションのアップグレード シナリオです。  

エディションのアップグレードを実行する手順については、「[Upgrade to a Different Edition of SQL Server &#40;Setup&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)」 (SQL Server の別のエディションへのアップグレード &#40;セットアップ&#41;) を参照してください。  
  
|アップグレード元|アップグレード先|  
|------------------|----------------|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Server+CAL および Core)**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise |  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation Enterprise**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> Evaluation (無償エディション) からいずれかの有償エディションへのアップグレードは、スタンドアロン インストールではサポートされていますが、クラスター化インストールではサポートされていません。|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Server+CAL または Core ライセンス)|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express*|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
  
 さらに、 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Server+CAL ライセンス) と [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Core License) の間でエディションのアップグレードも実行できます。  
  
|エディションのアップグレード元|エディションのアップグレード先|  
|--------------------------|------------------------|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Server+CAL ライセンス)**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Core ライセンス)|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Core ライセンス)|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Server+CAL ライセンス)|  
  
 \*[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express with Tools および [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express with Advanced Services についても同様です。  
  
 ** [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] のクラスター化されたインスタンスのエディションの変更は制限されています。 次のシナリオは、 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] フェールオーバー クラスターではサポートされていません。  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise から [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer、Standard、または Evaluation への変更  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer から [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard または Evaluation への変更  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard から [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation への変更  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation から [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard への変更  
  
## <a name="see-also"></a>参照  

 [[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] の各エディションとサポートされる機能](../../sql-server/editions-and-components-of-sql-server-version-15.md)

 [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)

 [SQL Server のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)  
