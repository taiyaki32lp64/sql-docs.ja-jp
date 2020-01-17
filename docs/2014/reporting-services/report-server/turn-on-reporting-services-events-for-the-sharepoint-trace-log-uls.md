---
title: Turn on Reporting Services events for the SharePoint trace log (ULS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 81110ef6-4289-405c-a931-e7e9f49e69ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8b9cbd080a138b939224d6bb88218b46e52a23f4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255449"
---
# <a name="turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls"></a>Turn on Reporting Services events for the SharePoint trace log (ULS)
  
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]以降では、SharePoint モードの [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サーバーから SharePoint 統合ログ サービス (ULS) のトレース ログに [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] イベントを書き込むことができます。 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 固有のカテゴリは、SharePoint サーバーの全体管理の [監視] ページで利用できます。  
  
 このトピックの内容  
  
-   [ULS ログの一般的な推奨事項](#bkmk_general)  
  
-   [Reporting Services カテゴリのイベント Reporting Services をオンまたはオフにするには](#bkmk_turnon)  
  
-   [推奨される構成](#bkmk_recommended)  
  
-   [ログエントリを読み取っています](#bkmk_readentries)  
  
-   [SQL Server Reporting Services イベントの一覧](#bkmk_list)  
  
-   [PowerShell を使用したログファイルの表示](#bkmk_powershell)  
  
-   [トレースログの場所](#bkmk_trace)  
  
##  <a name="bkmk_general"></a>ULS ログの一般的な推奨事項  
 次の表は、イベントのカテゴリの一覧です。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 環境を監視する場合の推奨されるレベルも記載されています。 イベントをログに記録した場合、各エントリには、イベントが記録された時刻、プロセス名、およびスレッド ID が記録されます。  
  
|Category|レベル|説明|  
|--------------|-----------|-----------------|  
|データベース|Verbose|データベース アクセスに関連するイベントが記録されます。|  
|全般|Verbose|次の項目へのアクセスを伴うイベントが記録されます。<br /><br /> [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]Web ページ<br /><br /> レポート ビューアーの HTTP ハンドラー<br /><br /> レポート アクセス (.rdl ファイル)<br /><br /> データ ソース (.rsds ファイル)<br /><br /> SharePoint サイト上の URL (.smdl ファイル)|  
|Office Server 全般|Exception|ログオンの失敗が記録されます。|  
|トポロジ|Verbose|現在のユーザー情報が記録されます。|  
|Web パーツ|Verbose|レポート ビューアー Web パーツへのアクセスを伴うイベントが記録されます。|  
  
##  <a name="bkmk_turnon"></a>Reporting Services カテゴリのイベント Reporting Services をオンまたはオフにするには  
  
1.  SharePoint サーバーの全体管理で、以下の操作を行います。  
  
2.  
  **[監視]** をクリックします。  
  
3.  
  **[レポート]** グループの **[診断ログの構成]** をクリックします。  
  
4.  カテゴリの一覧で **[SQL Server Reporting Services]** を探します。  
  
5.  プラス記号 (+) をクリックして、 **[SQL Server Reporting Services]** の下のサブカテゴリを展開します。  
  
6.  トレース ログに追加するサブカテゴリを選択します。  
  
7.  カテゴリの一覧の下部で、 **[トレース ログの記録対象となる重要度の最も低いイベント]** のイベント レベルを選択します。 トレースを無効にするには、 **[なし]** を選択します。  
  
> [!NOTE]  
>  
  **[イベント ログの記録対象となる重要度の最も低いイベント]** オプションは、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]ではサポートされません。 オプションは無視されます。  
  
##  <a name="bkmk_recommended"></a>推奨される構成  
 次のログ オプションが標準構成として推奨されます。  
  
-   **HTTP リダイレクター**  
  
-   **SOAP クライアント プロキシ**  
  
-   構成に関する問題が発生する場合は、 **[構成ページ]** を追加します。  
  
 現在のファームの診断ログ設定は、すべて次の PowerShell コマンドレットで確認できます。  
  
```powershell
Get-SPDiagnosticConfig  
```  
  
##  <a name="bkmk_readentries"></a>ログエントリを読み取っています  
 ログ内の [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] エントリは、次の方法で書式設定されます。  
  
1.  **製品: SQL Server Reporting Services**  
  
2.  **カテゴリ:** サーバーに関連するイベントの名前の先頭には、"Report Server" という文字が表示されます。 例: "Report Server Alerting Runtime"。これらのイベントは、レポート サーバーのログ ファイルにも記録されます。  
  
3.  **カテゴリ:** Web フロントエンドコンポーネントに関連するイベントまたは web フロントエンドコンポーネントと通信するイベントには、"レポートサーバー" は含まれません。 例: "Service Application Proxy" "Report Server Alerting Runtime"。 WFE エントリには CorrelationID が含まれますが、サーバー エントリには含まれません。  
  
##  <a name="bkmk_list"></a>SQL Server Reporting Services イベントの一覧  
 次の表に示すのは、SQL Server Reporting Services カテゴリに含まれるイベントの一覧です。  
  
|領域の名前|説明またはサンプルのエントリ|  
|---------------|-----------------------------------|  
|[構成ページ]||  
|HTTP リダイレクター||  
|ローカル モード処理||  
|ローカル モード表示||  
|SOAP クライアント プロキシ||  
|UI ページ||  
|Power View|
  **LogClientTraceEvents** API に書き込まれたログ エントリ。 これらのエントリは、Enterprise Edition 用の[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]アドインの[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]機能など、クライアントアプリケーションから[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]供給されています。<br /><br /> LogClientTraceEvents API からのすべてのログ エントリは、"SQL Server Reporting Services" の **Category** および "Power View" の **Area** に記録されます。<br /><br /> "Power View" の Area に記録されるエントリの内容は、クライアント アプリケーションによって異なります。|  
|Report Server Alerting Runtime||  
|レポート サーバー アプリケーション ドメイン マネージャー||  
|レポート サーバー バッファー済み応答||  
|レポート サーバー キャッシュ||  
|レポート サーバー カタログ||  
|レポート サーバー チャンク||  
|レポート サーバー クリーンアップ||  
|レポート サーバー構成マネージャー|サンプルのエントリ:<br /><br /> MediumUsing レポート サーバーの内部 URL http://localhost:80/ReportServer。<br /><br /> UnexpectedMissing または無効な ExtendedProtectionLevel 設定です|  
|レポート サーバー Crypto||  
|レポート サーバー データ拡張機能||  
|レポート サーバー DB ポーリング||  
|レポート サーバーの既定値||  
|レポート サーバー電子メール拡張機能||  
|レポート サーバー Excel レンダラー||  
|レポート サーバー拡張機能ファクトリ||  
|レポート サーバー HTTP ランタイム||  
|レポート サーバー画像レンダラー||  
|レポート サーバー メモリ監視||  
|レポート サーバー通知||  
|レポート サーバー処理||  
|レポート サーバー プロバイダー||  
|レポート サーバー レンダリング||  
|レポート サーバー レポート プレビュー||  
|レポート サーバー リソース ユーティリティ|サンプルのエントリ:<br /><br /> MediumReporting Services starting SKU: Evaluation<br /><br /> MediumEvaluation コピー: 180 日間残っています|  
|レポート サーバー実行中ジョブ||  
|レポート サーバー実行中要求||  
|レポート サーバー スケジュール||  
|レポート サーバー セキュリティ||  
|レポート サーバー サービス コントローラー||  
|レポート サーバー セッション||  
|レポート サーバー サブスクリプション||  
|レポート サーバー WCF ランタイム||  
|レポート サーバー Web サーバー||  
|サービス アプリケーション プロキシ||  
|共有サービス|サンプルのエントリ:<br /><br /> MediumUpdating ReportingWebServiceApplication<br /><br /> コンテンツ データベースへの MediumGranting アクセス。<br /><br /> ReportingWebServiceApplication の MediumProvisioning インスタンス<br /><br /> ReportingWebServiceApplication の MediumProcessing サービス アカウントの変更<br /><br /> MediumSetting データベース権限。|  
  
##  <a name="bkmk_powershell"></a>PowerShell を使用したログファイルの表示  
 ![PowerShell 関連コンテンツ](../media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")PowerShell を使用して[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 、ULS ログファイルから関連イベントの一覧を返すことができます。 SharePoint 2010 管理シェルから次のコマンドを入力すると、ULS ログ ファイル UESQL11SPOINT-20110606-1530.log から、"**sql server reporting services**" を含む行のフィルターされたリストが返されます。  
  
```powershell
Get-Content -Path "C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS\UESQL11SPOINT-20110606-1530.log" | Select-String "sql server reporting services"  
```  
  
 ULS ログの読み取りに使用できるツールは他にも多数提供されており、ダウンロードして使用できます。 たとえば、 [SharePoint LogViewer](https://sharepointlogviewer.codeplex.com/) や [SharePoint ULS Log Viewer](http://ulsviewer.codeplex.com/workitem/list/basic)などがあります。 これらはいずれも、CodePlex から入手できます。  
  
 PowerShell を使用してログ データを表示する方法の詳細については、「 [診断ログを表示する (SharePoint Server 2010)](https://technet.microsoft.com/library/ff463595.aspx)」を参照してください。  
  
##  <a name="bkmk_trace"></a>トレースログの場所  
 トレース ログ ファイルは通常、 **c:\Program Files\Common files\Microsoft Shared\Web Server Extensions\14\logs** フォルダーにありますが、SharePoint サーバーの全体管理の **[診断ログ]** ページから、パスを確認または変更することもできます。  
  
