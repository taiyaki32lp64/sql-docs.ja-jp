---
title: SQL Server の各エディションでサポートされる SQL Server Reporting Services の機能
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 06/20/2019
ms.openlocfilehash: 3e61381c2298a197be698ed82c247023ad708789
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893281"
---
# <a name="sql-server-reporting-services-features-supported-by-its-editions"></a>SQL Server の各エディションでサポートされる SQL Server Reporting Services の機能

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

このトピックでは、SQL Server のさまざまなエディションでサポートされる SQL Server Reporting Services (SSRS) 機能の詳細について説明します。 180 日の試用期間中、SQL Server Evaluation Edition をご利用いただけます。  
  
 最新の SQL Server リリース ノートについては、「[SQL Server 2017 リリース ノート](../sql-server/sql-server-2017-release-notes.md)」を参照してください。 新機能に関する最新情報については、「[SQL Server Reporting Services (SSRS) の新機能](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)」をご覧ください。

 ## <a name="try-sql-server-2017"></a>SQL Server 2017 をお試す

> [![SQL Server 2017 をダウンロードする](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?LinkID=829477) **[Evaluation Center から SQL Server 2017 をダウンロードする](https://go.microsoft.com/fwlink/?LinkID=829477)**    
>
> ![Azure Virtual Machine のアイコン](https://docs.microsoft.com/analysis-services/analysis-services/media/azure-virtual-machine-small.png) **[SQL Server 2017 がインストール済みの Virtual Machine をすぐにご利用いただけます](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    

Evaluation Edition および Developer Edition でサポートされている機能については、次の表の SQL Server Enterprise Edition の列を参照してください。

##  <a name="SSRS"></a> SQL Server Reporting Services (SQL Server Reporting Services)  
  
|機能名|Enterprise|Standard|Web|Express with Advanced Services|Developer|  
|------------------|---------|------------------------------------|------------------------|-------------|---------------|  
|モバイル レポートと分析|はい||||はい|  
|サポートされているカタログ データベースの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|Standard 以上|Standard 以上|Web|Express|Standard 以上|  
|サポートされているデータ ソースの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|すべての   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|すべての [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|Web|Express|すべての [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|  
|レポート サーバー|はい|はい|はい|はい|はい|  
|レポート デザイナー|はい|はい|はい|はい|はい|  
|レポート デザイナー Web ポータル|はい|はい|はい|はい|はい|  
|ロール ベース セキュリティ|はい|はい|はい|はい|はい|  
|Excel、PowerPoint、Word、PDF、およびイメージへのエクスポート|はい|はい|はい|はい|はい|  
|強化されたゲージとグラフ|はい|はい|はい|はい|はい|  
|[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] ダッシュボードへのレポート アイテムのピン留め|はい|はい|はい|はい|はい|  
|カスタム認証|はい|はい|はい||はい|  
|データ フィードとしてのレポート|はい|はい|はい|はい|はい|  
|モデルのサポート|はい|はい|はい||はい|  
|ロールベースのセキュリティのカスタム ロールの作成|はい|はい|||はい|  
|モデル アイテムのセキュリティ|はい|はい|||はい|  
|無限クリック スルー|はい|はい|||はい|  
|共有コンポーネント ライブラリ|はい|はい|||はい|  
|電子メールおよびファイル共有のサブスクリプションとスケジュール設定|はい|はい|||はい|  
|レポート履歴、実行スナップショット、およびキャッシュ|はい|はい|||はい|  
|SharePoint 統合<sup>2</sup>|はい|はい|||はい|  
|リモートおよび非 SQL データ ソースのサポート<sup>1</sup>|はい|はい|||はい|  
|データ ソース、配信およびレンダリング、RDCE の拡張性|はい|はい|||はい|  
|カスタム ブランド化|はい||||はい|  
|データ ドリブン レポートのサブスクリプション|はい||||はい|  
|スケール アウト配置 (Web ファーム)|はい||||はい|  
|警告<sup>2</sup> (SSRS 2016) |はい||||はい|  
|Power View<sup>2</sup> (SSRS 2016) |はい||||はい| 
|コメント<sup>3</sup> |はい|はい|はい|はい|はい|  

 <sup>1</sup> SQL Server Reporting Services (SSRS) でサポートされるデータ ソースの詳細については、「[Reporting Services でサポートされるデータ ソース (SSRS)](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)」を参照してください。  
  
 <sup>2</sup> SharePoint モードの SQL Server 2016 Reporting Services が必要です。 詳細については、[SharePoint モードでの SQL Server Reporting Services のインストール](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)に関するページを参照してください。 SQL Server 2017 Reporting Services 以降では、SharePoint との統合は使用できません。 

<sup>3</sup> Power BI Report Server と SQL Server 2017 Reporting Services 以降のみ。

> [!NOTE]
> SQL Server Express with Tools および SQL Server Express では、SQL Server Reporting Services はサポートされていません。
  
## <a name="edition-requirements-for-the-report-server-database"></a>レポート サーバー データベースのエディションの要件
 レポート サーバー データベースを作成するときは、SQL Server [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のすべてのエディションでデータベースをホストできるわけではないことに注意してください。 次の表に、SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の特定のエディションで使用できる [!INCLUDE[ssDE](../includes/ssde-md.md)] のエディションを示します。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services のエディション|データベースをホストするために使用するデータベース エンジン インスタンスのエディション|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Enterprise Edition または Standard Edition (ローカルまたはリモート)|  
|Standard|Enterprise Edition または Standard Edition (ローカルまたはリモート)|  
|Web|Web Edition (ローカルのみ)|  
|Express with Advanced Services|Express with Advanced Services (ローカルのみ)|  
|Evaluation|Evaluation|  
  
##  <a name="BIC"></a> Business Intelligence クライアント  
次のソフトウェア クライアント アプリケーションは、Microsoft ダウンロード センターで入手できます。 これらは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス上で実行されるビジネス インテリジェンス ドキュメントの作成に役立ちます。 作成したドキュメントをサーバー環境でホストする場合は、そのドキュメントの種類をサポートする [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のエディションを使用してください。 これらのクライアント アプリケーションで作成したドキュメントをホストするのに必要なサーバー機能を備えた [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディションを次の表に示します。  
  
|ツール名|Enterprise|Standard|Web|Express with Advanced Services|Developer|  
|---------------|----------------|--------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]、 **.rdl**、 **.rds**|はい|はい|はい|はい|はい|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)]、 **.rsmobile**|はい||||はい|  
|モバイル デバイス (iOS、Windows 10、Android) 用 Power BI アプリ、 **.rsmobile**|はい||||はい|  
  
> [!NOTE]  
> * 上記の表では、これらのクライアント ツールを有効にするために必要な [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディションが示されています。 ただし、これらのツールは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の任意のエディションでホストされているデータにアクセスできます。  
> * [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] モバイル レポートの作成の単一ポイントです。 SSRS サーバーに接続してデータ ソースにアクセスし、レポートを作成します。 次に、それらを SSRS サーバーにパブリッシュすることで、組織内の他のユーザーがサーバーまたはモバイル デバイスでアクセスできるようにします。 ローカル データ ソースの場合は、[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] スタンド アロンを使用することもできます。  
> * オンプレミスの [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]、クラウドの [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]、またはその両方のいずれをレポート配信ソリューションとして使用しても、モバイル デバイスでダッシュボードおよびモバイル レポートにアクセスするために必要なのは、1 つのモバイル アプリのみです。 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] アプリは Windows、iOS、または Android アプリ ストアからダウンロードできます。  

## <a name="next-steps"></a>次の手順

* [SQL Server 2017 の各エディションでサポートされている機能](~/sql-server/editions-and-components-of-sql-server-2017.md)を確認する。 

* [SQL Server のインストールを計画する](../sql-server/install/planning-a-sql-server-installation.md)。

* その他の質問 [SQL Server Reporting Services フォーラム](https://go.microsoft.com/fwlink/?LinkId=620231)で質問する。
