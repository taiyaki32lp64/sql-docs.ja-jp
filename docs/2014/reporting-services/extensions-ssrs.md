---
title: 拡張機能
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 2e1f0dadca7a7bdb98f828ce33e617a0cce0e8cf
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413125"
---
# <a name="extensions-for-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) の拡張機能

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のレポート サーバーでは、拡張機能を使用して、認証、データ処理、レポート表示、およびレポート配信で使用できる入力または出力の種類をモジュール化します。 これにより、既存の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] インストールで、業界の新しいソフトウェア標準 (新しい認証方法やカスタム データ ソースの種類など) を簡単に利用できます。 レポート サーバーは、カスタム認証拡張機能、データ処理拡張機能、レポート処理拡張機能、表示拡張機能、配信拡張機能、およびユーザーが RSReportServer.config 構成ファイルで構成できる拡張機能をサポートします。 たとえば、レポート ビューアーで使用できるエクスポート形式を制限できます。 レポート サーバーには、少なくとも 1 つの認証拡張機能、データ処理拡張機能、および表示拡張機能が必要です。 配信拡張機能とレポート処理拡張機能は省略可能ですが、レポートの配信またはカスタム コントロールをサポートする場合は必須です。  
  
 このトピックでは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]で簡単に使用できる拡張機能について説明します。  
  
## <a name="security-extensions"></a>セキュリティ拡張機能

 セキュリティ拡張機能は、レポート サーバーに対してユーザーおよびグループを認証および承認するために使用します。 既定のセキュリティ拡張機能は、Windows 認証に基づいています。 配置モデルで別の認証方法が必要な場合 (たとえば、インターネットまたはエクストラネット用にフォームベースの認証が必要な場合) は、カスタム セキュリティ拡張機能を作成し、既定のセキュリティを置き換えることができます。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の単一のインストールで使用できるセキュリティ拡張機能は 1 つだけです。 既定の Windows 認証セキュリティ拡張機能を置き換えることは可能ですが、カスタム セキュリティ拡張機能と併用することはできません。  
  
## <a name="data-processing-extensions"></a>データ処理拡張機能

 データ処理拡張機能は、データ ソースへのクエリを実行し、フラット化された行セットを返すために使用します。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 各種の拡張機能を使用して、さまざまな種類のデータ ソースと対話します。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]に含まれている拡張機能を使用することも、独自の拡張機能を開発することも可能です。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、Oracle、 [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)]、Hyperion Essbase、Teradata、OLE DB、ODBC の各データ ソース用のデータ処理拡張機能が用意されています。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] どのような [!INCLUDE[vstecado](../includes/vstecado-md.md)] データ プロバイダーも使用できます。 データ処理拡張機能は、次のタスクを実行することにより、レポート プロセッサ コンポーネントからのクエリ要求を処理します。  
  
- データ ソースへの接続を開きます。  
  
- クエリを分析し、フィールド名の一覧を返します。  
  
- データ ソースに対してクエリを実行し、行セットを返します。  
  
- 必要に応じて、クエリにパラメーターを渡します。  
  
- 行セットを反復処理し、データを取得します。  
  
一部の拡張機能は、次のタスクも実行できます。  
  
- クエリを分析し、クエリで使用したパラメーター名の一覧を返します。  
  
- クエリを分析し、グループ化に使用されたフィールドの一覧を返します。  
  
- クエリを分析し、並べ替えに使用されたフィールドの一覧を返します。  
  
- ユーザー名とパスワードを指定して、データ ソースに接続します。  
  
- 複数の値を持つパラメーターをクエリに渡します。  
  
- 行を反復処理し、補助メタデータを取得します。  
  
## <a name="rendering-extensions"></a>表示拡張機能

 表示拡張機能は、レポート プロセッサのデータとレイアウト情報をデバイス固有の形式に変換します。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] は、次の 7 種類の表示拡張機能を備えています:HTML、Excel、CSV、XML、Image、PDF、[!INCLUDE[msCoName](../includes/msconame-md.md)] Word。  
  
- **HTML 表示拡張機能** Web ブラウザーを使用してレポート サーバーのレポートを要求すると、レポート サーバーは HTML 表示拡張機能を使用してレポートを表示します。 HTML 表示拡張機能では、すべての HTML が UTF-8 エンコードを使用して生成されます。 詳細については、次を参照してください[HTML にレンダリング&#40;レポート ビルダーおよび SSRS&#41; ](report-builder/rendering-to-html-report-builder-and-ssrs.md)と[Reporting Services と Power View のブラウザー サポートの計画&#40;Reporting Services 2014&#41; ](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).  
  
- **Excel 表示拡張機能** Excel 表示拡張機能は、 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 97 以降のバージョンで表示および変更可能なレポートを表示します。 この表示拡張機能は、バイナリ交換ファイル形式 (BIFF) でファイルを作成します。 BIFF は、Excel データのネイティブなファイル形式です。 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] で表示されたレポートは、スプレッドシートで利用できる機能をすべてサポートします。 詳細については、「 [Microsoft Excel へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)で操作できます。  
  
- **CSV 表示拡張機能** コンマ区切り (CSV) 表示拡張機能は、書式を持たないコンマ区切りのプレーン テキスト形式のファイルでレポートを表示します。 ユーザーは、 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]などのスプレッドシート アプリケーション、またはテキスト ファイルを読み取る他のプログラムで、これらのファイルを開くことができます。 詳細については、「 [CSV ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)で操作できます。  
  
- **XML 表示拡張機能** XML 表示拡張機能は、XML ファイル形式でレポートを表示します。 これらの XML ファイルは、他のプログラムで保存したり読み込んだりすることができます。 XSLT 変換を使用してレポートを別の XML スキーマに変換し、別のアプリケーションで使用できるようにすることも可能です。 XML 表示拡張機能によって生成された XML は、UTF-8 でエンコードされます。 詳細については、「 [XML へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](report-builder/exporting-to-xml-report-builder-and-ssrs.md)で操作できます。  
  
-   **画像表示拡張機能** 画像表示拡張機能は、レポートをビットマップまたはメタファイルとして表示します。 拡張機能は、次の形式でレポートを表示できます。BMP、EMF、GIF、JPEG、PNG、TIFF、および WMF。 既定では、画像は TIFF 形式で表示されます。TIFF 形式は、使用するオペレーティング システムの既定のイメージ ビューアー (たとえば、Windows 画像と FAX ビューアー) で表示できます。 ビューアーからプリンターに画像を送ることができます。 画像表示拡張機能を使用してレポートを表示することにより、すべてのクライアントで同じレポートが表示されます (ユーザーが HTML 形式でレポートを表示する場合、ユーザーが使用するブラウザー、ブラウザーの設定、および使用できるフォントによって、レポートの外観が異なります)。画像表示拡張機能はレポートをサーバー上で表示します。そのため、すべてのユーザーが同じ画像を見ることができます。 レポートはサーバー上で表示されるため、レポートで使用されるすべてのフォントがサーバーにインストールされている必要があります。 詳細については、「 [画像ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)で操作できます。  
  
- **PDF 表示拡張機能** PDF 表示拡張機能は、Adobe Acrobat 6.0 以降のバージョンで開いたり表示したりすることができる PDF ファイル形式でレポートを表示します。 詳細については、「 [PDF ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)で操作できます。  
  
- **Word 表示拡張機能** [!INCLUDE[msCoName](../includes/msconame-md.md)] Word 表示拡張機能は、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Word 2000 以降と互換性のある Word 文書としてレポートを表示します。 詳細については、「 [Microsoft Word へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)で操作できます。  
  
## <a name="report-processing-extensions"></a>レポート処理拡張機能

 レポート処理拡張機能を追加すると、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]に含まれていないレポート アイテム用のカスタム レポート処理を提供できます。 既定では、レポート サーバーはテーブル、グラフ、マトリックス、一覧、テキスト ボックス、画像、およびその他すべてのレポート アイテムを処理できます。 レポートの実行中にカスタム処理を必要とする特別な機能をレポートに追加する場合 (たとえば、 [!INCLUDE[msCoName](../includes/msconame-md.md)] MapPoint の地図を埋め込む場合)、その処理を実行するレポート処理拡張機能を作成できます。  
  
## <a name="delivery-extensions"></a>配信拡張機能

 バックグラウンド処理アプリケーションは、配信拡張機能を使用して、さまざまな場所にレポートを配信します。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 電子メールの配信拡張機能とファイル共有の配信拡張機能があります。 電子メール配信拡張機能は、簡易メール転送プロトコル (SMTP) を使用して、レポートそのものまたはレポートへの URL リンクのいずれかを含む電子メール メッセージを送信できます。 URL リンクやレポートを含まない短い通知を、ポケットベル、電話、またはその他のデバイスに送信することもできます。 ファイル共有配信拡張機能は、ネットワークの共有フォルダーにレポートを保存します。 作成したファイルには、場所、表示形式、ファイル名、および上書きオプションを指定できます。 表示したレポートをアーカイブしたり、非常に大きいレポートを扱うための方法の一部として、ファイル共有配信を使用できます。 配信拡張機能はサブスクリプションと共に機能します。 ユーザーはサブスクリプションを作成するときに、利用可能な配信拡張機能のいずれかを選択して、レポートの配信方法を決定します。