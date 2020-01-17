---
title: サポートされているバージョンとエディションのアップグレード
titleSuffix: SQL Server 2017
ms.custom: seo-lt-2019
ms.date: 12/13/2019
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
ms.openlocfilehash: 4dba820ec4e353fff15b0695b97f940441caf802
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258834"
---
# <a name="supported-version-and-edition-upgrades-for-sql-server-2017"></a>SQL Server 2017 のサポートされているバージョンとエディションのアップグレード

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、および [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] からアップグレードできます。 この記事では、これらの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンからのサポートされているアップグレード パスと、サポートされている [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] へのエディションのアップグレードを示します。  
  
## <a name="pre-upgrade-checklist"></a>アップグレード前のチェック リスト  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] のいずれかのエディションから別のエディションへアップグレードする前に、現在使用している機能が移動先のエディションでサポートされているかどうかを確認します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアップグレードする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの Windows 認証を有効にし、既定の構成 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサービス アカウントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin グループのメンバーであること) を確認してください。  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]にアップグレードするには、サポート対象のオペレーティング システムを実行している必要があります。 詳細については、「[SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」を参照してください。  
  
-   再起動を保留している場合はアップグレードがブロックされます。  
  
-   Windows インストーラー サービスが実行されていない場合は、アップグレードがブロックされます。  
  
## <a name="unsupported-scenarios"></a>サポートされないシナリオ  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] の複数バージョンにまたがるインスタンスの使用はサポートされていません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] コンポーネントのバージョン番号は、[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] のインスタンス内で同一である必要があります。  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] は、64 ビット プラットフォームでのみ利用できます。 クロスプラットフォームのアップグレードはサポートされていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 32 ビット インスタンスをネイティブ 64 ビットにアップグレードすることはできません。 ただし、データベースがレプリケーションでパブリッシュされていない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の 32 ビット インスタンスのデータベースをバックアップまたはデタッチしてから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンス (64 ビット) に復元またはアタッチすることができます。 master、msdb、および model の各システム データベースにある、すべてのログインとその他のユーザー オブジェクトを再作成する必要があります。  
  
-   既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスのアップグレード中は、新しい機能を追加できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] にアップグレードした後、[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] のセットアップを使用して機能を追加できます。 詳細については、「[SQL Server のインスタンスへの機能の追加 &#40;セットアップ&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)」を参照してください。  
 
-   フェールオーバー クラスターは、WOW モードでサポートされていません。  
    
## <a name="upgrades-from-earlier-versions-to-includesssqlv14-mdincludessssqlv14-mdmd"></a>以前のバージョンから [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]  
 
[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] では、次のバージョンの SQL Server からのアップグレードがサポートされます。
 
- SQL Server 2008 SP4 以降
- SQL Server 2008 R2 SP3 以降
- SQL Server 2012 SP2 以降
- SQL Server 2014 以降 
- SQL Server 2016 以降
 

  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] でデータベースをアップグレードするには、 [2005 のサポート](#SupportFor2005)を参照してください。  
  
 次の表に示すのは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]への、サポートされるアップグレード シナリオです。  
  
|アップグレード元|サポートされているアップグレード パス|  
|:------|:------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Small Business|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Workgroup|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Datacenter|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Small Business|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Workgroup|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Evaluation|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Evaluation|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] リリース候補 * |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise |  
|[!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)] Developer |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise | 

 \* Microsoft では、特に Technology Adoption Program (TAP) に参加したお客様向けに、リリース候補版ソフトウェアからのアップグレードをサポートしています。 

   
###  <a name="SupportFor2005"></a> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] に対する [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] のサポート  
 ここでは、 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] に対する [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のサポートについて説明します。 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]では、次の作業を実行できます。  
  
-   データベース エンジンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに、 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] データベース (mdf/ldf ファイル) をアタッチします。  
  
-   バックアップからデータベース エンジンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] データベースを復元します。  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] キューブをバックアップし、[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] で復元します。  
  
[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースを [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] にアップグレードすると、そのデータベースの互換性レベルは 90 から 100 に変更されます ([!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] のデータベース互換性レベルの有効な値は 100、110、120、130、および 140 です)。[ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) は、互換性レベルの変更が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アプリケーションに与える影響について説明します。  
  
上記の一覧で説明されていないどのシナリオもサポートされていませんが、以下のシナリオに限定されるものではありません。  
  
- 同じコンピューターへの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] と [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] の (サイド バイ サイド) インストール。  
  
- [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスに参加するレプリケーション トポロジのメンバーとして [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] インスタンスを使用する。  
  
- [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのデータベース ミラーリングの構成。  
  
- [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのログ配布によるトランザクション ログのバックアップ。  
  
- [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] インスタンスと [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] インスタンスの間でのリンク サーバーの構成。  
  
- [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Management Studio からの [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] インスタンスの管理。  
  
- [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] Management Studio 内での [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] キューブのアタッチ。  
  
- [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio から [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] への接続  
  
- [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio からの [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] サービスの管理。  
  
- [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のサード パーティのカスタム Integration Services コンポーネントに対するサポート (実行とアップグレードなど)。  
  
## <a name="includesssqlv14-mdincludessssqlv14-mdmd-edition-upgrade"></a>[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] エディションのアップグレード  
次の表に示すのは、 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]でサポートされるエディションのアップグレード シナリオです。  
  
エディションのアップグレードを実行する手順については、「[Upgrade to a Different Edition of SQL Server &#40;Setup&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)」 (SQL Server の別のエディションへのアップグレード &#40;セットアップ&#41;) を参照してください。  
  
|アップグレード元|アップグレード先|  
|------------------|----------------|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL および Core)**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise |  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation Enterprise**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> Evaluation (無償エディション) からいずれかの有償エディションへのアップグレードは、スタンドアロン インストールではサポートされていますが、クラスター化インストールではサポートされていません。|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL または Core ライセンス)|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express*|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL または Core ライセンス) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
  
 さらに、 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL ライセンス) と [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Core License) の間でエディションのアップグレードも実行できます。  
  
|エディションのアップグレード元|エディションのアップグレード先|  
|--------------------------|------------------------|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL ライセンス)**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Core ライセンス)|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Core ライセンス)|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL ライセンス)|  
  
 \*[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express with Tools および [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express with Advanced Services についても同様です。  
  
 ** [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] フェールオーバー クラスターのエディションの変更は制限されています。 次のシナリオは、 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] フェールオーバー クラスターではサポートされていません。  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise から [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer、Standard、または Evaluation への変更  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer から [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard または Evaluation への変更  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard から [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation への変更  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation から [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard への変更  
  
## <a name="see-also"></a>参照  

 [SQL Server 2017 の各エディションとサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2017.md)
 
 [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 
 [SQL Server のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)  
  
  
