---
title: サポートされるバージョンとエディションのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 4a245aab71292e1482bd5a17bd32a27bded640ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775224"
---
# <a name="supported-version-and-edition-upgrades"></a>サポートされるバージョンとエディションのアップグレード
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、および [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] からアップグレードできます。 このトピックでは、これらの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンからのサポートされているアップグレード パスと、サポートされている [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]へのエディションのアップグレードを示します。  
  
## <a name="pre-upgrade-checklist"></a>アップグレード前のチェック リスト  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] のいずれかのエディションから別のエディションへアップグレードする前に、現在使用している機能が移動先のエディションでサポートされているかどうかを確認します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアップグレードする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの Windows 認証を有効にし、既定の構成 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサービス アカウントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin グループのメンバーであること) を確認してください。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]にアップグレードするには、サポート対象のオペレーティング システムを実行している必要があります。 詳細については、「 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」をご参照ください。  
  
-   再起動を保留している場合はアップグレードがブロックされます。  
  
-   Windows インストーラー サービスが実行されていない場合は、アップグレードがブロックされます。  
  
## <a name="unsupported-scenarios"></a>サポートされていないシナリオ  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] の複数バージョンにまたがるインスタンスの使用はサポートされていません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントのバージョン番号は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンス内で同一であることが必要です。  
  
-   クロスプラットフォームのアップグレードはサポートされていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 32 ビット インスタンスをネイティブ 64 ビットにアップグレードすることはできません。 ただし、データベースがレプリケーションでパブリッシュされていない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の 32 ビット インスタンスのデータベースをバックアップまたはデタッチしてから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンス (64 ビット) に復元またはアタッチすることができます。 master、msdb、および model の各システム データベースにある、すべてのログインとその他のユーザー オブジェクトを再作成する必要があります。  
  
-   既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスのアップグレード中は、新しい機能を追加できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードした後、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のセットアップを使用して機能を追加できます。 詳細については、次を参照してください。 [、インスタンスの SQL Server 2014 への機能の追加&#40;セットアップ&#41;](add-features-to-an-instance-of-sql-server-setup.md)します。  
  
-   フェールオーバー クラスターは、WOW モードでサポートされていません。  
  
-   以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Evaluation Edition からのアップグレードはサポートされていません。  
  
## <a name="upgrades-from-earlier-versions-to-includesssql14includessssql14-mdmd"></a>以前のバージョンから [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のサポート状況は、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 'に対する ' [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のサポートを取り扱う次のセクションで詳細に説明します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 ビット エディションは 64 ビット サーバーの 32 ビット サブシステム (WOW64) 上の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードできます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 ビット エディションは [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 ビット サーバーにのみアップグレードできます。  
  
> [!NOTE]  
>  アップグレードすると[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]の以前のバージョンから[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise edition、Enterprise Edition を選択します。コアベース ライセンスの Enterprise エディションのいずれかを選ぶことができます。 これらの Enterprise Edition は、ライセンス モードとサポートされるコアの最大数のみが異なります。 詳細については、「 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)」を参照してください。  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] では、次のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からのアップグレードがサポートされます。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 以降  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 以降  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 以降  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 以降  
  
 次の表に示すのは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] への、サポートされるアップグレード シナリオです。  
  
|アップグレード元|サポートされているアップグレード パス|  
|------------------|----------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express、<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Tools、および<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express、<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Tools、および<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Datacenter|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express、<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Tools、および<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express、<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Tools、および<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express Management Studio、および<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
  
### <a name="includesssql14includessssql14-mdmd-support-for-includessversion2005includesssversion2005-mdmd"></a>[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] に対する [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] のサポート  
 ここでは、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] に対する [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のサポートについて説明します。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]では、次の作業を実行できます。  
  
-   インストール ウィザードを使用するか、コマンド プロンプトから . [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] セットアップを実行して、データベース エンジンの [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] インスタンスを [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] にアップグレードします。  
  
-   データベース エンジンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] データベース (mdf/ldf ファイル) をアタッチします。  
  
-   バックアップからデータベース エンジンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] データベースを復元します。  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] パッケージを [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]にアップグレードします。 自動化されたインプレース アップグレードを使用してパッケージを実行します。  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] セットアップを実行して、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] を [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] にアップグレードします。  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] キューブをバックアップし、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]に復元します。  
  
-   [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] セットアップを実行して、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] を [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] にアップグレードします。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]2014 を使用して [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] に接続します。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースを [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] にアップグレードすると、そのデータベースの互換性レベルは 90 から 100 に変更されます ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] のデータベース互換性レベルの有効な値は 100、110、120 です。)[ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) は、互換性レベルの変更が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アプリケーションに与える影響について説明します。  
  
 上記の一覧で説明されていないどのシナリオもサポートされていませんが、以下のシナリオに限定されるものではありません。  
  
-   同じコンピューターへの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] と [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] の (サイド バイ サイド) インストール。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに参加するレプリケーション トポロジのメンバーとして [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] インスタンスを使用する。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのデータベース ミラーリングの構成。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのログ配布によるトランザクション ログのバックアップ。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのリンク サーバーの構成。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Management Studio からの [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] インスタンスの管理。  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] Management Studio 内での [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] キューブのアタッチ。  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio から [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] への接続  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio からの [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] サービスの管理。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のサード パーティのカスタム Integration Services コンポーネントに対するサポート (実行とアップグレードなど)。  
  
## <a name="includesssql14includessssql14-mdmd-edition-upgrade"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] エディションのアップグレード  
 次の表に示すのは、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]でサポートされるエディションのアップグレード シナリオです。  
  
 エディションのアップグレードを実行する方法の詳しい手順については、「 [、さまざまなエディションの SQL Server 2014 にアップグレード&#40;セットアップ&#41;](upgrade-to-a-different-edition-of-sql-server-setup.md)します。  
  
|アップグレード元|アップグレード先|  
|------------------|----------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (SERVER+CAL および Core) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL または Core ライセンス)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation Enterprise <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL または Core ライセンス)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> Evaluation Enterprise (無償エディション) からいずれかの有償エディションへのアップグレードは、スタンドアロン インストールではサポートされていますが、クラスター化インストールではサポートされていません。|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 標準<sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL または Core ライセンス)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 開発者<sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL または Core ライセンス)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL または Core ライセンス)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express <sup>1</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL または Core ライセンス)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
  
 さらに、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL ライセンス) と [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Core License) の間でエディションのアップグレードも実行できます。  
  
|エディションのアップグレード元|エディションのアップグレード先|  
|--------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (SERVER+CAL ライセンス) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Core ライセンス)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Core ライセンス)|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL ライセンス)|  
  
 <sup>1</sup>にも適用されます[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]Express with Tools と[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]Express with Advanced Services。  
  
 <sup>2</sup>のエディションの変更、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]フェイル オーバー クラスターは制限されています。 次のシナリオは、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] フェールオーバー クラスターではサポートされていません。  
  
-   SQL Server 2014 Enterprise から SQL Server 2014 Developer、Standard、または Enterprise Evaluation へ。  
  
-   SQL Server 2014 Developer から SQL Server 2014 Standard または Enterprise Evaluation へ。  
  
-   SQL Server 2014 Standard から SQL Server 2014 Enterprise Evaluation へ。  
  
-   SQL Server 2014 Enterprise Evaluation から SQL Server 2014 Standard へ。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 のエディションでサポートされる機能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [SQL Server 2014 へのアップグレード](upgrade-sql-server.md)   
 [アップグレード アドバイザーを使用したアップグレードの準備](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
  
