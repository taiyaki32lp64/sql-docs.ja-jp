---
title: '[サーバーのプロパティ] の [詳細設定] ページ - Reporting Services | Microsoft Docs'
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 11/05/2019
ms.openlocfilehash: defadad0d3a2545ba3d794d5d9c38c5734d3e9af
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73638027"
---
# <a name="server-properties-advanced-page---reporting-services"></a>[サーバーのプロパティ] の [詳細設定] ページ - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

このページを使用して、レポート サーバーのシステム プロパティを設定します。 システム プロパティを設定する方法はいくつかあります。 このツールにはグラフィカル ユーザー インターフェイスが用意されているので、コードを記述しなくてもプロパティを設定できます。

このページを開くには、SQL Server Management Studio を起動してレポート サーバー インスタンスに接続し、レポート サーバー名を右クリックして **[プロパティ]** をクリックします。 **[詳細設定]** を選択するとこのページが開きます。

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
> **0** の値を設定すると、実行ログからすべてのエントリが*削除*されます。 値が **-1** の場合、実行ログのエントリは保持され、それらは削除されません。

**RDLXReportTimetout** RDLX レポート *(SharePoint Server の Power View レポート)* レポート サーバーの名前空間で管理されるすべてのレポートに対する、処理タイムアウト値 (秒単位)。 この値はレポート レベルでオーバーライドできます。 このプロパティを設定すると、レポート サーバーは指定された時間が経過した後、レポートの処理を停止しようとします。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値に **-1**を設定すると、名前空間内のレポートが処理中にタイムアウトしません。 既定値は **1800**です。

**SessionTimeout** セッションがアクティブな状態になっている期間 (秒単位)。 既定値は **600**です。  

**SharePointIntegratedMode**  
この読み取り専用プロパティは、サーバー モードを示します。 この値が False の場合、レポート サーバーはネイティブ モードで実行されます。  

**SiteName**  
Web ポータルのページ タイトルに表示されるレポート サーバー サイトの名前。 既定値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]です。 このプロパティには空の文字列を指定できます。 最大長は 8,000 文字です。  

**StoredParametersLifetime** 格納されたパラメーターを保持できる最大日数を指定します。 有効値は **-1**、 **+1** ～ **2,147,483,647**です。 既定値は **180** 日です。  

**StoredParametersThreshold**  
レポート サーバーが保存できるパラメーター値の最大数を指定します。 有効値は **-1**、 **+1** ～ **2,147,483,647**です。 既定値は **1500**です。  

**UseSessionCookies**  
レポート サーバーがクライアント ブラウザーとの通信時にセッションクッキーを使用する必要があるかどうかを指定します。 既定値は **true**です。  

**ExternalImagesTimeout**  
この時間以内に外部画像ファイルを取得しないと接続がタイムアウトになる時間の長さを指定します。既定値は **600** 秒です。  

**SnapshotCompression** その時点のレポート サーバーのスナップショット。

**SnapshotCompression**  
スナップショットの圧縮方法を定義します。 既定値は **SQL**です。 有効な値は次のとおりです。

|値|[説明]|
|---------|---------|
|**SQL**|スナップショットは、レポート サーバー データベースへの格納時に圧縮されます。 この圧縮は現在の動作です。|
|**なし**|スナップショットは圧縮されません。|
|**すべて**|すべてのストレージ オプションのスナップショットが圧縮されます。このオプションには、レポート サーバー データベースやファイル システムが含まれます。|

**SystemReportTimeout**  
レポート サーバー名前空間で管理されているすべてのレポートの既定のレポート処理タイムアウト値 (秒単位)。 この値はレポート レベルでオーバーライドできます。 このプロパティを設定すると、レポート サーバーは指定された時間が経過した後、レポートの処理を停止しようとします。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値に **-1**を設定すると、名前空間内のレポートが処理中にタイムアウトしません。 既定値は **1800**です。  

**SystemSnapshotLimit**  
レポートに格納されるスナップショットの最大数。 有効値は **-1** ～ **2**、**147**、**483**、**647**です。 値が **-1**の場合、スナップショットに制限はありません。  

**AccessControlAllowCredentials**  
'credentials' フラグが true に設定されている場合に、クライアント要求への応答を公開できるかどうかを示します。 既定値は **false**です。

**AccessControlAllowHeaders** クライアントが要求したときに、サーバーが許可するヘッダーのコンマ区切りリスト。 このプロパティは、空の文字列にすることができます。* を指定すると、すべてのヘッダーが許可されます。

**AccessControlAllowMethods** クライアントが要求したときに、サーバーが許可する HTTP メソッドのコンマ区切りリスト。 既定値は GET、PUT、POST、PATCH、DELETE です。* を指定すると、すべてのメソッドが許可されます。

**AccessControlAllowOrigin** クライアントが要求したときに、サーバーが許可する要求元のコンマ区切りリスト。 既定値は空白で、すべての要求を防ぎます。* を指定すると、資格情報が設定されていない場合にすべての要求元が許可されます。資格情報が指定されている場合は、要求元の明示的なリストを指定する必要があります。

**AccessControlExposeHeaders** サーバーがクライアントに公開するヘッダーのコンマ区切りリスト。 既定値は空白です。

**AccessControlMaxAge** プリフライト要求の結果をキャッシュできる秒数を指定します。 既定値は 600 (10 分) です。

**AllowedResourceExtensionsForUpload** (Power BI Report Server および Reporting Services 2017 以降のみ) レポート サーバーにアップロードできるリソースの拡張子を設定します。 &ast;.rdl や &ast;.pbix のような組み込みのファイルの種類用の拡張子は含める必要はありません。 既定値は "&ast;、&ast;.xml、&ast;.xsd、&ast;.xsl、&ast;.png、&ast;.gif、&ast;.jpg、&ast;.tif、&ast;.jpeg、&ast;.tiff、&ast;.bmp、&ast;.pdf、&ast;.svg、&ast;.rtf、&ast;.txt、&ast;.doc、&ast;.docx、&ast;.pps、&ast;.ppt、&ast;.pptx" です。

**RestrictedResourceMimeTypeForUpload**ユーザーがコンテンツをアップロードすることが許可されていない mime の種類のセット。 制限付きの mime の種類で既に保存されているリソースは、ブラウザーによって開かれたり実行されたりするのではなく、アプリケーション/オクテットストリームとしてのみダウンロードできます。  既定では、この一覧には制限された項目はありませんが、セキュリティで保護されたエクスペリエンスを提供するために組織で設定することをお勧めします。

**EditSessionCacheLimit**  
レポート編集セッションでアクティブにできるデータ キャッシュ エントリの数を指定します。 既定の数は 5 です。  

**EditSessionTimeout**  
レポート編集セッションがタイムアウトするまでの秒数を指定します。既定値は 7,200 秒 (2 時間) です。  

**EnableIntegratedSecurity**  
Windows 統合セキュリティをレポート データ ソース接続でサポートするかどうかを決定します。 既定値は **True**です。 有効な値は次のとおりです。

|値|[説明]|
|---------|---------|
|**True**|Windows 統合セキュリティが有効になります。|
|**False**|Windows 統合セキュリティは無効になります。 Windows 統合セキュリティを使用するように構成されているレポート データ ソースは実行されません。|

**EnableLoadReportDefinition**  
ユーザーがレポート ビルダーのレポートから計画されていないレポートを実行できるかどうかを指定するには、このオプションを選択します。 このオプションをオンにすると、レポート サーバーの **EnableLoadReportDefinition** プロパティが設定されます。  

このオプションをオフにした場合は、このプロパティが False に設定されます。 データ ソースとしてレポート モデルを使用するレポートのクリックスルー レポートは、レポート サーバーによって生成されません。 LoadReportDefinition メソッドへの呼び出しはいずれもブロックされます。  

この機能を無効にすることで、悪意のあるユーザーが LoadReportDefinition 要求でレポート サーバーを過負荷にするサービス拒否攻撃の脅威を軽減することができます。  

**EnableRemoteErrors**  
リモート コンピューターからレポートを要求したユーザーに返されるエラー メッセージに、外部エラー情報 (レポート データ ソースに関するエラー情報など) を含めます。 有効値は **true** および **false**です。 既定値は **false**です。 詳細については、「[リモート エラーの有効化 (Reporting Services)](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)」を参照してください。  

**EnableCustomVisuals** ***(Power BI Report Server のみ)*** Power BI カスタム ビジュアルの表示を有効にします。 値は True と False です。 *既定値は True です。*  

**ExecutionLogLevel** 実行ログのレベルを設定します。 *既定値は Normal です。*

**InterProcessTimeoutMinutes** プロセスのタイムアウトを分単位で設定します。 *既定値は 30 です。*

**MaxFileSizeMb** レポートの最大ファイル サイズを MB 単位で設定します。 *既定値は 1000 です。最大値は 2000 です。*

**ModelCleanupCycleminutes** モデルのクリーンアップ サイクルを分単位で設定します。 *既定値は 15 です。*

**OfficeAccessTokenExpirationSeconds** ***(Power BI Report Server のみ)*** Office Access トークンの有効期限を秒単位で設定します。 *既定値は 60 です。*

**OfficeOnlineDiscoveryURL** ***(Power BI Report Server のみ)*** Excel ブックを表示するための Office Online Server インスタンスのアドレスを設定します。

**RequireIntune** Intune は、Power BI モバイル アプリ経由で組織のレポートにアクセスする必要があります。 *既定値は False です。*

**ScheduleRefreshTimeoutMinutes** ***(Power BI Report Server のみ)*** スケジュールされた更新がタイムアウトになるまでの時間を設定します。*既定値は 120 です。*

**ShowDownloadMenu** クライアント ツールのダウンロード メニューを有効にします。 *既定値は true です。*

**SupportedHyperlinkSchemes** ***(Power BI Report Server のみ)*** 表示できるハイパーリンク アクションで定義できる URI スキームのコンマ区切りの一覧を設定するか、"&ast;" を設定してすべてのハイパーリンク スキームを有効にします。 たとえば、"http,https" を設定すると、"https://www. contoso.com" へのハイパーリンクは許可されますが、"mailto:bill@contoso.com" や "javascript:window.open(‘www.contoso.com’, ‘_blank’)" へのハイパーリンクは削除されます。 既定値は "&ast;" です。

**TimeInitialDelaySeconds** 初期時間を遅延させる時間を秒単位で設定します。 *既定値は 60 です。*

**TrustedFileFormat** Reporting Services ポータル サイトにおいてブラウザーで開くすべての外部ファイルの形式を設定します。 外部ファイルの形式が一覧に含まれない場合は、オプションのダウンロードを求めるメッセージがブラウザーに表示されます。 既定値は、jpg、jpeg、jpe、wav、bmp、pdf、img、gif、json、mp4、web、png です。

**EnablePowerBIReportExportData** ***(Power BI Report Server のみ)***  
Power BI ビジュアルからの Power BI Report Server のデータ エクスポートを有効にします。 値は True、False です。  既定値は True です。  

**ScheduleRefreshTimeoutMinutes** ***(Power BI Report Server のみ)***  
AS モデルが埋め込まれた Power BI レポートでのスケジュールされた更新用のデータ更新のタイムアウト (分)。 既定値は 120 分です。

**EnableTestConnectionDetailedErrors**  
ユーザーがレポート サーバーを使用してデータ ソース接続をテストする際に、クライアント コンピューターに詳細なエラー メッセージを送信するかどうかを指定します。 既定値は **true**です。 このオプションを **false**に設定した場合は、一般的なエラー メッセージだけが送信されます。

## <a name="see-also"></a>参照

[レポート サーバーのプロパティを設定する (Management Studio)](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Management Studio でレポート サーバーに接続する](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services のプロパティ](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio のレポート サーバーの F1 ヘルプ](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[レポート サーバーのシステム プロパティ](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[配置タスクおよび管理タスクのスクリプト作成](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[個人用レポートの有効化と無効化](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
