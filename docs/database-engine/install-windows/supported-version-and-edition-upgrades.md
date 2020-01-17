---
title: サポートされるバージョンとエディションのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 06/27/2016
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
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 99b6522316928fcd7397d27c1a5c85d927a8e0b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934861"
---
# <a name="supported-version-and-edition-upgrades"></a>サポートされるバージョンとエディションのアップグレード

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、および [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] からアップグレードできます。 この記事では、これらの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンからのサポートされているアップグレード パスと、サポートされている [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] へのエディションのアップグレードを示します。  
  
## <a name="pre-upgrade-checklist"></a>アップグレード前のチェック リスト  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] のいずれかのエディションから別のエディションへアップグレードする前に、現在使用している機能が移動先のエディションでサポートされているかどうかを確認します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアップグレードする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの Windows 認証を有効にし、既定の構成 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサービス アカウントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin グループのメンバーであること) を確認してください。  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]にアップグレードするには、サポート対象のオペレーティング システムを実行している必要があります。 詳細については、「 [SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」を参照してください。  
  
-   再起動を保留している場合はアップグレードがブロックされます。  
  
-   Windows インストーラー サービスが実行されていない場合は、アップグレードがブロックされます。  
  
## <a name="unsupported-scenarios"></a>サポートされていないシナリオ  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] の複数バージョンにまたがるインスタンスの使用はサポートされていません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントのバージョン番号は [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]のインスタンス内で同一であることが必要です。  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] は、64 ビット プラットフォームでのみ利用できます。 クロスプラットフォームのアップグレードはサポートされていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 32 ビット インスタンスをネイティブ 64 ビットにアップグレードすることはできません。 ただし、データベースがレプリケーションでパブリッシュされていない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の 32 ビット インスタンスのデータベースをバックアップまたはデタッチしてから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンス (64 ビット) に復元またはアタッチすることができます。 master、msdb、および model の各システム データベースにある、すべてのログインとその他のユーザー オブジェクトを再作成する必要があります。  
  
-   既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスのアップグレード中は、新しい機能を追加できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] にアップグレードした後、[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] のセットアップを使用して機能を追加できます。 詳細については、「[SQL Server 2016 のインスタンスへの機能の追加 &#40;セットアップ&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)」を参照してください。  
 
-   フェールオーバー クラスターは、WOW モードでサポートされていません。  
  
-   以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Evaluation Edition からのアップグレードはサポートされていません。

-   SQL Server 2016 RC1 以前のバージョンから RC3 以降のバージョンにアップグレードする場合、アップグレード前に PolyBase をアンインストールし、アップグレード後に再インストールする必要があります。
  
## <a name="upgrades-from-earlier-versions-to-includesssql15-mdincludessssql15-mdmd"></a>以前のバージョンから [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]  
 
SQL Server 2016 では、次のバージョンの SQL Server からのアップグレードがサポートされます。
 
- [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] SP4 以降
- [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP3 以降
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 以降
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降 
 
> [!NOTE]  
> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] でデータベースをアップグレードするには、 [2005 のサポート](#SupportFor2005)を参照してください。  
  
次の表に示すのは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]への、サポートされるアップグレード シナリオです。  
  
|アップグレード元|サポートされているアップグレード パス|  
|------------------|----------------------------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Small Business|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Workgroup|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Datacenter|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Small Business|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Workgroup|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Business Intelligence|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Evaluation|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] リリース候補 * |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise |  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] Developer |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise | 

 \* Microsoft では、特に Technology Adoption Program (TAP) に参加したお客様向けに、リリース候補版ソフトウェアからのアップグレードをサポートしています。 
   
###  <a name="SupportFor2005"></a> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] サポート対象 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
ここでは、 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] に対する [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のサポートについて説明します。 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]では、次の作業を実行できます。  
  
-   データベース エンジンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに、 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] データベース (mdf/ldf ファイル) をアタッチします。  
  
-   バックアップからデータベース エンジンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] データベースを復元します。  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] キューブをバックアップし、 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]に復元します。  
  
> [!NOTE]  
> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースを [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] にアップグレードすると、そのデータベースの互換性レベルは 90 から 100 に変更されます [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] のデータベース互換性レベルの有効な値は 100、110、120、および 130 です。 [ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) は、互換性レベルの変更が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アプリケーションに与える影響について説明します。  
  
上記の一覧で説明されていないどのシナリオもサポートされていませんが、以下のシナリオに限定されるものではありません。  
  
-   同じコンピューターへの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] と [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] の (サイド バイ サイド) インストール。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに参加するレプリケーション トポロジのメンバーとして [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] インスタンスを使用する。  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのデータベース ミラーリングの構成。  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのログ配布によるトランザクション ログのバックアップ。  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのリンク サーバーの構成。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Management Studio からの [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] インスタンスの管理。  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] Management Studio 内での [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] キューブのアタッチ。  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio から [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] への接続  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio からの [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] サービスの管理。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のサード パーティのカスタム Integration Services コンポーネントに対するサポート (実行とアップグレードなど)。  
  
## <a name="includesssql15-mdincludessssql15-mdmd-edition-upgrade"></a>[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] エディションのアップグレード  
次の表に示すのは、 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]でサポートされるエディションのアップグレード シナリオです。  
  
エディションのアップグレードを実行する手順については、「[SQL Server 2016 の別のエディションへのアップグレード &#40;セットアップ&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)」を参照してください。  
  
|アップグレード元|アップグレード先|  
|------------------|----------------|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL および Core)**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise |  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation Enterprise**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> Evaluation (無償エディション) からいずれかの有償エディションへのアップグレードは、スタンドアロン インストールではサポートされていますが、クラスター化インストールではサポートされていません。|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL または Core ライセンス)|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express*|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
  
さらに、 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL ライセンス) と [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Core License) の間でエディションのアップグレードも実行できます。  
  
|エディションのアップグレード元|エディションのアップグレード先|  
|--------------------------|------------------------|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL ライセンス)**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Core ライセンス)|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Core ライセンス)|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL ライセンス)|  
  
 \*[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express with Tools および [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express with Advanced Services についても同様です。  
  
 ** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] フェールオーバー クラスターのエディションの変更は制限されています。 次のシナリオは、 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] フェールオーバー クラスターではサポートされていません。  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise から [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer、Standard、または Evaluation への変更  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer から [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard または Evaluation への変更  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard から [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation への変更  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation から [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard への変更  
  
## <a name="see-also"></a>参照  

[SQL Server 2016 のエディションとサポートされている機能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)     
[SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)     
[SQL Server 2016 へのアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)    
  
  
