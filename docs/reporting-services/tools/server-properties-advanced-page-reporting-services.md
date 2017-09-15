---
title: "[サーバーのプロパティ] ([詳細設定] ページ) - Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 0626dc829e6ae2cd4212dc05deb406740592dc40
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---

# <a name="server-properties-advanced-page---reporting-services"></a>[サーバーのプロパティ]\([詳細設定] ページ) - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

このページを使用して、レポート サーバーのシステム プロパティを設定します。 システム プロパティを設定する方法はいくつかあります。 このツールにはグラフィカル ユーザー インターフェイスが用意されているので、コードを記述しなくてもプロパティを設定できます。

このページを開くには、SQL Server Management Studio を起動、レポート サーバー インスタンスに接続、レポート サーバーの名前を右クリックし、選択**プロパティ**です。 選択**詳細**をこのページを開きます。

## <a name="options"></a>オプション

**EnableMyReports**  
個人用レポート機能が有効になっているかどうかを指定します。 値 **true** は、機能が有効になっていることを示します。  

**MyReportsRole**  
ユーザーの個人用レポート フォルダーに、セキュリティ ポリシーを作成する際に使用するロールの名前。 既定値は **My Reports Role**です。  

**EnableClientPrinting**  
レポート サーバーからのダウンロードに RSClientPrint ActiveX コントロールが使用可能かどうかを示します。 有効値は **true** および **false**です。 既定値は **true**です。 このコントロールに必要な追加設定に関する詳細については、「 [Reporting Services のクライアント側印刷機能の有効化と無効化](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)」を参照してください。  

**EnableExecutionLogging**  
レポート実行のログ記録が有効になっているかどうかを示します。 既定値は **true**です。 レポート サーバー実行ログの詳細については、「 [レポート サーバー ExecutionLog と ExecutionLog3 ビュー](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)」を参照してください。  

**ExecutionLogDaysKept**  
レポート実行情報を実行ログに保持する日数。 このプロパティの有効値は、 **-1** - **2**、**147**、**483**、**647**です。 値が **-1** の場合、エントリは実行ログ テーブルから削除されません。 既定値は **60**です。  

> [!NOTE] 
> **0** の値を設定すると、実行ログからすべてのエントリが*削除*されます。 **-1** の値を設定すると、実行ログのエントリは保持され、削除されません。

**SessionTimeout**  
セッションがアクティブな状態になっている期間 (秒単位)。 既定値は **600**です。  

**SharePointIntegratedMode**  
これは、サーバー モードを示す読み取り専用プロパティです。 この値が False の場合、レポート サーバーはネイティブ モードで実行されます。  

**SiteName**  
Web ポータルのページ タイトルに表示されるレポート サーバー サイトの名前。 既定値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]です。 このプロパティには空の文字列を指定できます。 最大長は 8,000 文字です。  

**StoredParametersLifetime**  
保存したパラメーターを保持できる最大日数を指定します。 有効値は **-1**、 **+1** ～ **2,147,483,647**です。 既定値は **180** 日です。  

**StoredParametersThreshold**  
レポート サーバーが保存できるパラメーター値の最大数を指定します。 有効値は **-1**、 **+1** ～ **2,147,483,647**です。 既定値は **1500**です。  

**UseSessionCookies**  
レポート サーバーがクライアント ブラウザーとの通信時にセッションクッキーを使用する必要があるかどうかを指定します。 既定値は **true**です。  

**ExternalImagesTimeout**  
この時間以内に外部画像ファイルを取得しないと接続がタイムアウトになる時間の長さを指定します。既定値は **600** 秒です。  

**SnapshotCompression**  
スナップショットの圧縮方法を定義します。 既定値は **SQL**です。 有効な値は次のとおりです。

|値|Description|
|---------|---------|
|**SQL**|レポート サーバー データベースに格納されているときに、スナップショットは圧縮されます。 これは現在の動作です。|
|**なし**|スナップショットは圧縮されません。|
|**すべて**|レポート サーバー データベースまたはファイル システムを含む、すべての記憶域オプションのスナップショットが圧縮されます。|

**SystemReportTimeout**  
レポート サーバー名前空間で管理されているすべてのレポートの既定のレポート処理タイムアウト値 (秒単位)。 この値はレポート レベルでオーバーライドできます。 このプロパティを設定すると、レポート サーバーは指定された時間が経過した後、レポートの処理を停止しようとします。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値に **-1**を設定すると、名前空間内のレポートが処理中にタイムアウトしません。 既定値は **1800**です。  

**SystemSnapshotLimit**  
レポートに格納されるスナップショットの最大数。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値が **-1**の場合、スナップショットに制限はありません。  

**EnableIntegratedSecurity**  
Windows 統合セキュリティをレポート データ ソース接続でサポートするかどうかを決定します。 既定値は **True**です。 有効な値は次のとおりです。

|値|Description|
|---------|---------|
|**True**|Windows 統合セキュリティが有効になっているとします。|
|**False**|Windows 統合セキュリティが無効です。 Windows 統合セキュリティを使用するように構成されているレポート データ ソースは実行されません。|

**EnableLoadReportDefinition**  
ユーザーがレポート ビルダーのレポートからアドホック レポートを実行できるかどうかを指定するには、このオプションを選択します。 このオプションをオンにすると、レポート サーバーの **EnableLoadReportDefinition** プロパティが設定されます。  

このオプションをオフにするとプロパティが False に設定され、データ ソースとしてレポート モデルを使用するレポートのクリックスルー レポートは生成されません。 LoadReportDefinition メソッドへの呼び出しをブロックします。  

この機能を無効にすることで、悪意のあるユーザーが LoadReportDefinition 要求でレポート サーバーを過負荷にするサービス拒否攻撃の脅威を軽減することができます。  

**EnableRemoteErrors**  
リモート コンピューターからレポートを要求したユーザーに返されるエラー メッセージに、外部エラー情報 (レポート データ ソースに関するエラー情報など) を含めます。 有効値は **true** および **false**です。 既定値は **false**です。 詳細については、「[リモート エラーの有効化 (Reporting Services)](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)」を参照してください。  

**EnableReportDesignClientDownload**  
レポート ビルダーのインストール パッケージをレポート サーバーからダウンロードできるかどうかを指定します。 この設定をオフにすると、レポート ビルダーの URL が機能しません。 詳細については、「 [レポート ビルダーへのアクセスの構成](../../reporting-services/report-server/configure-report-builder-access.md)」を参照してください。  

**EditSessionCacheLimit**  
レポート編集セッションでアクティブにできるデータ キャッシュ エントリの数を指定します。 既定の数は 5 です。  

**EditSessionTimeout**  
レポート編集セッションがタイムアウトするまでの秒数を指定します。既定値は 7200 秒 (2 時間) です。  

**EnableCustomVisuals** ***(Power BI のレポート サーバーのみ)***  
PowerBI カスタム ビジュアルの表示を有効に PowerBI ReportServer ください。 値は、True を false の場合です。  既定値は True です。  

**EnablePowerBIReportExportData** ***(Power BI のレポート サーバーのみ)***  
Power Bi ビジュアルのデータのエクスポートを有効に PowerBI ReportServer ください。 値は、True を false の場合です。  既定値は True です。  

**EnableTestConnectionDetailedErrors**  
ユーザーがレポート サーバーを使用してデータ ソース接続をテストする際に、クライアント コンピューターに詳細なエラー メッセージが送信されるようにするかどうかを指定します。 既定値は **true**です。 このオプションを **false**に設定した場合は、一般的なエラー メッセージだけが送信されます。

**AccessControlAllowCredentials**  
'資格情報' フラグが設定されている場合に、クライアント要求に応答を公開することができるかどうかを示す true に設定します。 既定値は **false**です。

**AccessControlAllowHeaders**クライアント要求を行うときに、サーバーを許可するヘッダーのコンマ区切りリスト。 このプロパティは、空の文字列にすることができますを指定する * すべてのヘッダーを許可します。

**AccessControlAllowMethods**クライアント要求を行うときに、サーバーを許可する HTTP メソッドのコンマ区切りリスト。 既定値は、(GET、PUT、POST、PATCH、DELETE) を指定する * すべてのメソッドを許可します。

**AccessControlAllowOrigin**クライアント要求を行うときに、サーバーを許可するオリジンのコンマ区切りリスト。 既定値は空白を指定するすべての要求を防ぐことが * 資格情報が設定されていませんときに、すべてのオリジンを許可されます。オリジンの明示的なリストを指定する必要がありますの資格情報が指定した場合。

**AccessControlExposeHeaders**サーバーがクライアントに公開されるヘッダーのコンマ区切りリスト。 既定値は空白です。

**AccessControlMaxAge**プレフライト要求の結果をキャッシュする秒数を指定します。 既定値は 600 (10 分) です。

## <a name="see-also"></a>参照

[レポート サーバーのプロパティの設定 & #40 です。Management Studio &#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Management Studio でレポート サーバーに接続する](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services のプロパティ](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio のレポート サーバーの F1 ヘルプ](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[レポート サーバーのシステム プロパティ](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[配置タスクおよび管理タスクのスクリプト作成](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[個人用レポートの有効化と無効化](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

他に質問しますか。 [Reporting Services のフォーラムで質問してみてください。](http://go.microsoft.com/fwlink/?LinkId=620231)