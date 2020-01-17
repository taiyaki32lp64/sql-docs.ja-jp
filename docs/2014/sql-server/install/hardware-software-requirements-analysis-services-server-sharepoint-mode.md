---
title: SharePoint モードの Analysis Services Server のハードウェアとソフトウェアの要件 (SQL Server 2014) |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 8f645ca9bdb6176505a6277af0f0482be5b62f09
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245608"
---
# <a name="hardware-and-software-requirements-for-analysis-services-server-in-sharepoint-mode-sql-server-2014"></a>SharePoint モードの Analysis Services サーバーのハードウェアとソフトウェアの要件 (SQL Server 2014)


  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] は、SharePoint 2010 と SharePoint 2013 の両方をサポートしています。 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 は SharePoint ファームの外部で実行されますが、SharePoint サーバー上にインストールすることもできます。 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 は、SharePoint 2010 ファーム内のアプリケーション サーバー上で動作し、SharePoint の機能とインフラストラクチャを使用してサーバー操作をサポートします。 SharePoint のいずれかのバージョンの [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をインストールするには、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストール ウィザードを使用します。 インストール後に、次の手順を完了します。  
  
- SharePoint のバージョンに応じた、適切なバージョンの [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 構成ツールを実行します。  
  
- SharePoint 2013 の場合は、 [sharepoint 2013&#41;&#40;PowerPivot for SharePoint アドインをインストールまたはアンインストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)します。  

##  <a name="bkmk_sqleditions"></a>SQL Server エディションの要件  
 ビジネス インテリジェンス機能は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のすべてのエディションで利用できるわけではありません。 詳細については、 [SQL Server 2014 の各エディションがサポートする機能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」および[SQL Server 2014 の各エディションとコンポーネント](../editions-and-components-of-sql-server-2016.md)に関する説明を参照してください。  
  
 最新のリリースノートについては、 [Microsoft SQL Server 2014 のリリースノート](https://go.microsoft.com/fwlink/?LinkID=296445)を参照してください。  
  

  
##  <a name="bkmk_sqllicense"></a>SQL Server ライセンス  
 SQL Server のライセンスの詳細については、以下を参照してください。  
  
-   [SQL Server 2014 ライセンスデータシート](https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf)(https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf))。  
  
-   [購入方法: SQL Server のライセンスモデル](https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2)ではhttps://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2)、() がサポートされます。  
  
##  <a name="bkmk_ssas__sharepoint_2013"></a>SharePoint 2013 にインストールされた Analysis Services  
 Analysis Services サーバーだけを SharePoint モードでサーバーにインストールする場合、最小システム要件は、SharePoint サーバーの要件ではなく [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に基づきます。  
  
 [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](hardware-and-software-requirements-for-installing-sql-server.md)  
  
 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint は、RAM のしきい値と処理能力が高い新世代のビジネス サーバー上で最適に動作します。 メモリへの [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データの格納には大量の RAM が使用されます。 RAM は構造の変化に対応できる機能をサポートしています。 追加のプロセッサでは、未処理の集計されていないデータの長時間スキャンがサポートされます。 このデータの構造は、ユーザーが Excel クライアントやフロントエンド インターフェイスを使用して開始したデータ分析に応じて動的に変化します。  
  
> [!TIP]  
>  
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint では、L2 キャッシュと L3 キャッシュを使用します。 パフォーマンスを向上させるには、大容量の L2 および L3 キャッシュが搭載されたプロセッサを使用することを検討してください。  
  
 次の表では、SharePoint ファームの一部ではないスタンドアロン [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] サーバーの最小ハードウェア構成と推奨構成を示しています。  
  
|コンポーネント|最小値|推奨|  
|---------------|-------------|-----------------|  
|プロセッサ|64 ビット デュアルコア プロセッサ、3 GHz|16 コア|  
|RAM|8 GB の RAM|64 GB の RAM|  
|Storage|80 GB のストレージ|80 GB 以上|  
  
 Analysis Services サーバーを SharePoint モードで SharePoint ファームのサーバーにインストールする場合は、以下のリンクで、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サーバーと SharePoint サーバー両方の最小システム要件を確認してください。  
  
-   [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [SharePoint 2013 のハードウェアとソフトウェアの要件](https://technet.microsoft.com/library/cc262485\(office.15\).aspx)。  
  
 SharePoint 2013 のハードウェアおよびソフトウェアの標準の推奨構成は、ワークグループまたはチーム向けの Web ベースのドキュメント管理ソリューション用の構成です。 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 処理ではデータが集中的に使用されますが、ワークロード全体の数が少ない場合 (たとえば、ユーザー数またはブック数が 100 件未満の場合) は、標準の推奨設定で十分です。 大規模な [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] の配置を行う場合は、さらに高い処理能力が必要です。  
  
##  <a name="bkmk_ssas__sharepoint_2010"></a>SharePoint 2010 サーバーにインストールされている Analysis Services  
 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 は、SharePoint 2010 ファーム内のアプリケーション サーバー上で動作し、SharePoint の機能とインフラストラクチャを使用してサーバー操作をサポートします。 次の表は、 SharePoint 2010 の配置に関連する要件をまとめたものです。  
  
|コンポーネント|要件|  
|---------------|-----------------|  
|SharePoint バージョン|同じサーバー ファーム内で Excel Services、Secure Store Service、および Claims to Windows Token Service が構成された SharePoint 2010 Enterprise。<br /><br /> SharePoint は、SharePoint セットアップでサーバー ファーム オプションを使用してインストールされている必要があります (SharePoint のスタンドアロン インストール オプションはサポートされていません)。 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] には、管理アクセスおよびデータ アクセスをサポートするサーバー ファーム インフラストラクチャが必要です。 スタンドアロン インストールではこれらのサービスは提供されません。<br /><br /> 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] サーバーのインストールでは、Windows 7 または Windows Vista 上で動作する Developer Edition はサポートされません。|  
|サービス パック|SharePoint Server 2010 Service Pack 1 (SP1) が必要です。<br /><br /> 機能には、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] SharePoint 2010 Service Pack 1 が必要です。<br /><br /> 以前のバージョンの [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] から [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] にアップグレードする場合は、SharePoint 2010 の 2010 年 8 月の累積的な更新プログラム、またはそれ以降の更新プログラムが必要です。 2010 年 8 月の累積的な更新プログラム、またはそれ以降の更新プログラムは、SharePoint Service Pack 1 のインストール後にインストールする必要があります。 の[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]新規インストールでは、累積的な更新プログラムは必要ありません。 詳細については、「 [2010 年8月の SharePoint の累積的な更新プログラムのリリース](https://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx)」を参照してください。|  
|SharePoint Web アプリケーション|
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2010 は、クラシック モード認証用に構成された SharePoint Web アプリケーションのみをサポートします。 既存のファームに [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint を追加する場合は、使用する予定の Web アプリケーションがクラシック モード認証用に構成されていることを確認してください。 認証モードを確認する方法については、「 [SharePoint への PowerPivot ソリューションの配置](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)」の「Web アプリケーションでクラシックモード認証が使用されていることを確認する」を参照してください。|  
|
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] サーバー側のデータ更新に必要なデータ プロバイダー|サーバー側のデータの更新を行うと、最初にデータをインポートするために使用したのと同じデータ取得手順が繰り返されます。 これは、クライアント ワークステーションでデータのインポートに使用されるデータ プロバイダーが、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint サーバーにも存在する必要があることを示します。<br /><br /> また、SharePoint サーバー上のデータ フィードを使用するには、ADO.NET Data Services が必要です。 SharePoint の必須コンポーネントのインストーラー プログラムでは、このコンポーネントはインストールされません。 次のソフトウェアを手動でインストールする必要があります。<br /><br /> ADO.NET Data Services 3.5 SP1 ランタイム アセンブリ。このアセンブリは、SharePoint リストをデータ フィードとしてエクスポートするために使用します。 使用しているオペレーティング システムに対応するバージョンをダウンロードしてインストールしてください。<br /><br /> Windows Server 2008 R2 の場合は、 [windows 7 および Windows server 2008 r2 用の .NET Framework 3.5 SP1 用に ADO.NET Data Services Update](https://www.microsoft.com/download/details.aspx?id=2343)を使用します。 Windows Server 2008 R2 **SP1**には、更新されたプロバイダーが既に含まれています。<br /><br /> Windows Server 2008 の場合は、 [windows 2000、Windows server 2003、WINDOWS XP、Windows Vista、および Windows Server 2008 (https://go.microsoft.com/fwlink/?LinkId=158125)) に対して、.NET Framework 3.5 SP1 用の ADO.NET Data Services Update](https://www.microsoft.com/download/details.aspx?id=22734)を使用します。|  
  
 [ハードウェアとソフトウェアの要件の決定 (SharePoint 2010) (https://go.microsoft.com/fwlink/?LinkId=169734)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
## <a name="additional-information"></a>追加情報  

