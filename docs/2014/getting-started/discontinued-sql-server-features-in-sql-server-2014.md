---
title: SQL Server 2014 | の SQL Server 廃止された機能Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 0678bfbc-5d3f-44f4-89c0-13e8e52404da
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8f7ab6cdbc1b6e0e3dc7d26fb579943a0c8fa95
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637770"
---
# <a name="discontinued-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 で提供が中止された機能
  このトピックでは、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] にアップグレードした後で使用できなくなる機能について説明します。  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] で提供が中止された機能はありません。  
  
## <a name="discontinued-features-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="discontinued-active-directory-helper-service"></a>Active Directory Helper サービスの提供中止  
 Active Directory Helper サービスおよびその関連コンポーネントは、削除されました。 次の表は、削除された関連コンポーネントの一覧を示しています。  
  
|カテゴリ|提供が中止された機能|代替|  
|--------------|--------------------------|-----------------|  
|システム ストアド プロシージャ|sp_ActiveDirectory_Obj<br /><br /> sp_ActiveDirectory_SCP<br /><br /> sp_ActiveDirectory_Start|置き換えることはできません|  
  
## <a name="discontinued-features-in-sql-server-2008-r2"></a>SQL Server 2008 R2 で提供が中止された機能  
  
### <a name="64-bit-platform-support-in-reporting-services"></a>Reporting Services での 64 ビット プラットフォームのサポート  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 以降の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] コンポーネントでは、Windows Server 2003 または Windows Server 2003 R2 を実行している Itanium ベースのサーバーがサポートされなくなりました。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、Itanium ベース システム用の Windows Server 2008 や Itanium ベース システム用の Windows Server 2008 R2 などの他の 64 ビット オペレーティング システムは引き続きサポートされます。 Windows Server 2003 または Windows Server 2003 R2 の Itanium ベース システム エディションにインストールされた [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] を [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] にアップグレードするには、まずオペレーティング システムをアップグレードする必要があります。  
  
## <a name="discontinued-features-in-sql-server-2008"></a>SQL Server 2008 で提供が中止された機能  
  
### <a name="discontinued-sql-dmo-from-sql-server-express-installation"></a>SQL Server Express で提供が中止された SQL-DMO  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の SQL-DMO が [!INCLUDE[ssExpressEd10](../includes/ssexpressed10-md.md)] から削除されました。 この機能を現在使用しているアプリケーションはできるだけ早く変更することをお勧めします。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 用の sql-dmo をサポートする必要がある場合は、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=24793)から [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] feature Pack から旧バージョンとの互換性コンポーネントをインストールしてください。 新しい開発作業では、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) を使用してください。  
  
### <a name="discontinued-option-for-web-assistant"></a>廃止された Web Assistant オプション  
 `sp_configure` では、Web Assistant を有効にする [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] オプションが削除されました。 代わりに [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] を使用することをお勧めします。  
  
### <a name="surface-area-configuration-tool"></a>セキュリティ構成ツール  
 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]では、セキュリティ構成ツールは廃止されました。 以下の表に、このリリースの設定、オプション、およびコンポーネントの機能を構成する際に使用できる方法を示します。  
  
|置換設定とコンポーネントの機能|構成方法|  
|-------------------------------------------------|----------------------|  
|プロトコル、接続、およびスタートアップオプション|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを使用します。|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] 機能|ポリシー ベースの管理、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のプロパティ設定、または sp_configure を使用します。|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 機能|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のプロパティ設定を使用します。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-EnableIntegrated Security プロパティ|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のプロパティ設定を使用します。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-"イベントのスケジュールとレポートの配信" および "Web サービスおよび HTTP アクセス"|RSReportServer.config 構成ファイルを編集します。|  
|コマンドラインオプション|このリリースではサポートされません。|  
|SOAP および [!INCLUDE[ssSB](../includes/sssb-md.md)] のエンドポイント|[CREATE endpoint](/sql/t-sql/statements/create-endpoint-transact-sql)と[ALTER endpoint](/sql/t-sql/statements/alter-endpoint-transact-sql)を使用します。|  
  
### <a name="discontinued-command-prompt-parameters-for-sql-server-setup"></a>SQL Server のセットアップで廃止されたコマンド プロンプト パラメーター  
 次の表に、以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のセットアップ コマンド プロンプト パラメーターのうち、[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] でサポートされていないものを示します。  
  
|廃止されたパラメーター|新しいパラメーター|  
|----------------------------|---------------------------|  
|ADDLOCAL|/ACTION=Uninstall および /FEATURES|  
|DISABLENETWORKPROTOCOLS|/Tcpenabled/tcp/ip<sup>1</sup>|  
|DISABLENETWORKPROTOCOLS|名前付きパイプの/NPENABLED<sup>1</sup>|  
|INSTALLSQLDATADIR|/SQLUSERDBDIR<br /><br /> /SQLUSERDBLOGDIR<br /><br /> /SQLBACKUPDIR<br /><br /> /SQLTEMPDBDIR<br /><br /> /SQLTEMPDBLOGDIR|  
|REINSTALL|このリリースに該当する機能はありません。|  
|REINSTALLMODE|このリリースに該当する機能はありません。|  
|REMOVE|/ACTION=Uninstall および /FEATURES|  
|SAMPLEDATABASE|このリリースに該当する機能はありません。|  
|SAVESYSDB|このリリースに該当する機能はありません。|  
|SKUUPGRADE<sup>2</sup>|このリリースに該当する機能はありません。|  
|UPGRADE|/ACTION=Upgrade および /FEATURES|  
|USESYSDB|このリリースに該当する機能はありません。|  
  
 <sup>1</sup>これらのパラメーターは、インストールに対してのみ有効です。  
  
 <sup>2</sup>[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]を開始するには、/Action = EditionUpgrade を指定して、既存のエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を、元のインストールメディアを使用せずに、いつでも別のエディションにアップグレードします。 サポートされるバージョンとエディションのアップグレードについては、「 [Supported Version and Edition Upgrades](../database-engine/install-windows/supported-version-and-edition-upgrades.md)」を参照してください。  
  
 詳細については、「[コマンド プロンプトからの SQL Server 2014 のインストール](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)」を参照してください。  
  
  
