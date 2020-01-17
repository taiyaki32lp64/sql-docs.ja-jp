---
title: (レポート ビルダーおよび SSRS) レポートのエクスポート |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d8b4fe6e791f84f0949b0657b890c79db99dfbf9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107945"
---
# <a name="exporting-reports-report-builder-and-ssrs"></a>レポートのエクスポート (レポート ビルダーおよび SSRS)
  レポートを実行した後は、Excel や PDF など、別の形式にレポートをエクスポートできます。また、レポートから利用できる Atom 準拠のデータ フィードを一覧表示する Atom サービス ドキュメントを生成してエクスポートすることもできます。  
  
 レポートは、次の目的のためにエクスポートします。  
  
-   レポート データを別のアプリケーションで操作する。 たとえば、レポートを Excel にエクスポートした後で、引き続きそのデータを Excel で編集できます。  
  
-   レポートを異なる形式で印刷する。 たとえば、レポートを PDF ファイル形式にエクスポートして、印刷できます。  
  
-   レポートのコピーを別の種類のファイルとして保存する。 たとえば、レポートを Word にエクスポートして保存することで、レポートのコピーを作成できます。  
  
-   レポート データをデータ フィードとしてアプリケーションで使用する。 たとえば、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] クライアントで使用できる Atom 準拠のデータ フィードを生成してから、そのデータを [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]で操作できます。  
  
 エクスポート オプションには、レポート マネージャーのレポート ビューアー ツール バーからアクセスできます。このツール バーは、レポート サーバーでレポートを表示したときに、すべてのレポートの最上部に表示され、レポートをプレビューしたときは、レポート ビルダーのリボンに表示されます。 データ フィード オプションは、レポート マネージャーでのみ使用できます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、さまざまな表示拡張機能が用意されており、一般的なファイル形式へのレポートのエクスポートがサポートされます。 これらの表示拡張機能では、ソフト改ページを含むファイル形式 (Word や Excel など)、ハード改ページを含むファイル形式 (PDF や TIFF など)、またデータのみのファイル形式 (CSV や Atom 準拠の XML など) がサポートされます。  
  
 すぐにするレポートのエクスポートとレポートから Atom 準拠のデータ フィードを生成すると、次を参照してください[別のファイルの種類としてレポートをエクスポート&#40;レポート ビルダーおよび SSRS&#41; ](../export-a-report-as-another-file-type-report-builder-and-ssrs.md)と[からのデータ フィードを生成します。レポート&#40;レポート ビルダーおよび SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md)します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RendererTypes"></a> 表示拡張機能の種類  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の表示拡張機能には、次の 3 種類があります。  
  
-   **データ表示拡張機能** データ表示拡張機能では、すべての書式設定とレイアウト情報がレポートから取り除かれ、データのみが表示されます。 生成されたファイルを使用して、生のレポート データを別のファイル形式 (Excel、他のデータベース、XML データ メッセージ、カスタム アプリケーションなど) にインポートできます。 データ表示拡張機能では、改ページはサポートされません。  
  
     次のデータ表示拡張機能がサポートされます。CSV、XML、Atom。  
  
-   **ソフト改ページ表示拡張機能** ソフト改ページ表示拡張機能では、レポートのレイアウトと書式設定が維持されます。 生成されたファイルは、Web ページや **ReportViewer** コントロールなど、画面上での閲覧や配信に最適化されます。  
  
     次のソフト改ページ表示拡張機能がサポートされます。[!INCLUDE[msCoName](../../includes/msconame-md.md)]Excel、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word、Web アーカイブ (MHTML)。  
  
-   **ハード改ページ表示拡張機能** ハード改ページ表示拡張機能では、レポートのレイアウトと書式設定が維持されます。 生成されたファイルは、一貫した印刷結果を提供すること、または、レポートを印刷物のような形でオンライン配信する際の見やすさを優先して最適化されます。  
  
     次のハード改ページ表示拡張機能がサポートされます。TIFF と PDF。  
  
##  <a name="ExportFormats"></a> エクスポート形式  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、さまざまな形式でレポートを表示する表示拡張機能が用意されています。 この機能を使用する予定がある場合は、選択したファイル形式に合わせてレポート デザインを最適化する必要があります。 表示拡張機能に関するトピックでは、レポートがその形式にレンダリングされるしくみについて詳しく説明します。  
  
 次の表に、使用できる形式を示します。  
  
|形式|表示拡張機能の種類|説明|  
|------------|------------------------------|-----------------|  
|CSV|データ|CSV (コンマ区切り) 表示拡張機能では、レポートのデータを平面的に表して、標準化されたプレーンテキスト形式でレポートを表示します。プレーンテキスト形式のレポートは、多くのアプリケーションで簡単に読み取ったり変換したりすることができます。<br /><br /> 詳細については、「 [CSV ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md)で操作できます。|  
|[エクスポート]|ソフト改ページ|Excel 表示拡張機能では、インストールされている Word/Excel/PowerPoint 用 Microsoft Office 互換機能パックによって、レポートが [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007-2010 および [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 と互換性のある Excel 文書として表示されます。 レポートを Excel ワークシートにエクスポートすると、一部のレイアウトと元のデザイン要素が除去されます。レポートおよびレポート内のグループのプロパティを設定して、Excel へのエクスポート時にワークシート タブの名前を指定できます。 このレンダラーで生成されるファイル名の拡張子は xlsx です。<br /><br /> 詳細については、「 [Microsoft Excel へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md)で操作できます。<br /><br /> 注:レポートを [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 のネイティブ形式で表示する Excel 2003 表示拡張機能は、一部のレポート シナリオで使用できます。|  
|Word|ソフト改ページ|Word 表示拡張機能では、インストールされている Word/Excel/PowerPoint 用 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] Office 互換機能パックによって、レポートが [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010 および [!INCLUDE[msCoName](../../includes/msconame-md.md)] 2003 と互換性のある Word 文書として表示されます。 レポートを Word 文書にエクスポートした後は、レポートの内容を変更したり、宛名ラベル、発注書、手紙など、文書形式のレポートをデザインしたりできます。 このレンダラーによって生成されるファイルの拡張子は docx です。<br /><br /> 詳細については、「 [Microsoft Word へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md)で操作できます。<br /><br /> 注:レポートを [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 のネイティブ形式で表示する Word 2003 表示拡張機能は、一部のレポート シナリオで使用できます。|  
|Web アーカイブ|ソフト改ページ|HTML 表示拡張機能では、HTML 形式でレポートを表示します。 また、完全な HTML ページを生成することも、他の HTML ページに埋め込むための HTML の一部分を生成することもできます。 すべての HTML は、UTF-8 エンコードで生成されます。<br /><br /> HTML 表示拡張機能は、レポート マネージャーで実行する場合など、レポート ビルダーでプレビューされ、ブラウザーで表示されるレポートの既定の表示拡張機能です。<br /><br /> 詳細については、「 [HTML での表示 &#40;レポート ビルダーおよび SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md)で操作できます。|  
|Acrobat (PDF) ファイル|ハード改ページ|PDF 表示拡張機能を使用すると、Adobe Acrobat および PDF 1.3 をサポートするその他のサードパーティ製 PDF ビューアーで開くことのできるファイルとしてレポートが表示されます。 PDF 1.3 は Adobe Acrobat 4 以降のバージョンと互換性がありますが、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では Adobe Acrobat 6 以降がサポートされています。 この表示拡張機能では、レポートの表示処理に Adobe 製のソフトウェアは必要ありません。 ただし、レポートを PDF 形式で表示または印刷するには、Adobe Acrobat などの PDF ビューアーが必要です。<br /><br /> 詳細については、「 [PDF ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md)で操作できます。|  
|TIFF ファイル|ハード改ページ|画像表示拡張機能では、レポートがビットマップまたはメタファイルとして表示されます。 画像表示拡張機能では、既定でレポートの TIFF ファイルが生成されます。このファイルは、複数のページに表示することもできます。 クライアントは、受信した画像をイメージ ビューアーで表示したり、印刷したりできます。<br /><br /> 画像表示拡張機能は、[!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)] でサポートされている次のいずれの形式でもファイルを生成できます:BMP、EMF、EMFPlus、GIF、JPEG、PNG、TIFF。<br /><br /> 詳細については、「 [画像ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md)で操作できます。|  
|XML|データ|XML 表示拡張機能では、レポートが XML 形式で返されます。 レポート XML のスキーマは、レポート固有のものであり、データのみを含んでいます。 XML 表示拡張機能では、レイアウト情報はレンダリングされません。また、改ページ位置も維持されません。 この拡張機能で生成された XML は、データベースにインポートしたり、XML データ メッセージとして使用したり、カスタム アプリケーションに送信することができます。<br /><br /> 詳細については、「 [XML へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md)で操作できます。|  
|Atom|データ|Atom 表示拡張機能では、Atom 準拠のデータ フィードがレポートから生成されます。 データ フィードは、Atom 準拠のデータ フィードを使用するアプリケーション ( [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] クライアントなど) で読み取りと交換が可能です。<br /><br /> 出力は、レポートで使用可能なデータ フィードを一覧表示する Atom サービス ドキュメントです。 レポート内の各データ領域について、少なくとも 1 つのデータ フィードが作成されます。 データ領域の種類およびデータ領域に表示されるデータによっては、複数のデータ フィードが生成される場合があります。<br /><br /> 詳細については、「 [複数のレポートからのデータ フィードの生成 &#40;レポート ビルダーおよび SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)で操作できます。|  
  
##  <a name="ExportingReport"></a> レポートをエクスポートします。  
 レポートをエクスポートするには、レポート マネージャーまたはレポート ビルダーでレポートを実行した後、[エクスポート] ドロップダウン リストから形式を選択します。 ファイルを保存するか、開くかを選択するメッセージが表示されます。 **[開く]** を選択すると、選択した表示形式に関連付けられているアプリケーションでレポートが開きます。 たとえば、 **[Excel]** を選択した場合は、レポートが Excel で開きます。 **[保存]** を選択すると、レポートが保存されます。 たとえば、Excel にエクスポートする場合は、.xls ファイルとしてレポートが保存されます。 ローカル コンピューターで定義されているファイルの関連付けにより、特定の表示形式に使用されるアプリケーションが決まります。 詳細については、次を参照してください。[別のファイルの種類としてレポートをエクスポート&#40;レポート ビルダーおよび SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md)します。  
  
 レポート サーバーでは、現在のユーザー セッションに存在するレポートがエクスポートされます。 レポートが開いている間、またはレポートに表示されているデータが変更されている間に、更新されたバージョンがパブリッシュされても、エクスポート後のレポートは更新されません。  
  
 異なる形式でレポートをエクスポートすると、レポートのページ割り当てに影響する場合があります。 レポートをプレビューすると、HTML 表示拡張機能により、ソフト改ページ規則に従ってレポートが表示されます。 レポートを、Adobe Acrobat (PDF) などの別のファイル形式にエクスポートする場合、改ページは、ハード改ページ規則に従う物理ページ サイズに基づきます。 また、レポートに追加した論理的な改ページによってページを区切ることもできますが、実際のページの長さは、使用するレンダラーの種類によって異なります。 レポートの改ページを変更するには、選択した表示拡張機能の改ページの動作を理解する必要があります。 この表示拡張機能に合わせてレポート レイアウトのデザインの調整が必要になる場合があります。 詳細については、「[ページ レイアウトとレンダリング &#40;レポート ビルダーおよび SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md)」を参照してください。  
  
##  <a name="GeneratingDataFeedsFromReport"></a> レポートからのデータ フィードの生成  
 レポートからデータ フィードを生成するには、レポート マネージャーでレポートを実行した後、[レポート マネージャー] ツール バーの **[データ フィードの生成]** アイコンをクリックします。 ファイルを保存するか、開くかを選択するメッセージが表示されます。 **[開く]** を選択すると、.atomsvc ファイル拡張子に関連付けられているアプリケーションで Atom サービス ドキュメントが開きます。 **[保存]** を選択すると、ドキュメントが .atomsvc ファイルとして保存されます。 既定では、ファイルの名前はレポートの名前です。 この名前は、わかりやすい名前に変更できます。  
  
 Atom サービス ドキュメントは自分のコンピューターに保存されます。 後でレポート サーバーまたは別のサーバーにレポートをアップロードして、他のユーザーがレポートを使用できるようにすることができます。 詳細については、「[複数のレポートからのデータ フィードの生成 &#40;レポート ビルダーおよび SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)」および「[1 つのレポートからのデータ フィードの生成 &#40;レポート ビルダーおよび SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md)」を参照してください。  
  
##  <a name="Troubleshooting"></a> エクスポートされたレポートのトラブルシューティング  
 レポートを別の形式にエクスポートした場合、表示が変わったり、思いどおりに動作しなかったりすることがあります。 これは、特定の規則や制限がレンダラーに適用されることがあるためです。 多くの制限には、レポートの作成時に考慮することにより対処可能です。 場合によっては、レポートで若干異なるレイアウトを使用する、レポート内へのアイテムの配置を工夫する、レポートのフッターを 1 行のテキストに制限するなどの作業が必要になります。  
  
 レポートにアラビア数字の Unicode テキストが含まれている場合やアラビア語の日付が含まれている場合、レポートを次のいずれかの形式でエクスポートしたりレポートを印刷したりすると、日付と数字が正しく表示されません。  
  
-   PDF  
  
-   Word  
  
-   [エクスポート]  
  
-   Image/TIFF  
  
 レポートを HTML にエクスポートした場合、日付と数字は正しく表示されます。  
  
 特定のレンダラーについてのトピックで、レポート アイテムとデータ領域がどのように表示されるかと、レンダラーごとの制限とソリューションについて説明します。  
  
-   [CSV ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [Microsoft Excel へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [Microsoft Word へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [HTML での表示 &#40;レポート ビルダーおよび SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md)  
  
-   [PDF ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [画像ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [XML へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [複数のレポートからのデータ フィードの生成 &#40;レポート ビルダーおよび SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、他の形式でも適切に動作するレポートを作成できるように、次の追加機能が用意されています。 Tablix データ領域 (テーブル、マトリックス、一覧) の改ページ、グループ、四角形により、レポートのページ割り当てをより適切に制御できます。 改ページで区切られたレポートのページに、さまざまなページ名を付け、ページ番号をリセットできます。 式を使用すると、レポートの実行時にページ名とページ番号を動的に更新できます。 詳細については、「[Reporting Services の改ページ &#40;レポート ビルダーおよび SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)」を参照してください。  
  
 また、組み込みの RenderFormat グローバルを使用することにより、条件に応じてレンダラーごとに異なるレポート レイアウトを適用することもできます。 詳細については、「[組み込み Globals および Users 参照 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)」をご覧ください。  
  
##  <a name="OtherWaysExportingReports"></a> レポートをエクスポートするその他の方法  
 レポートのエクスポートは、レポート マネージャーまたはレポート ビルダーでレポートを開くときに必要に応じて実行するタスクです。 エクスポート操作を自動化する場合は (レポートを、定期的なスケジュールで特定のファイルの種類として共有フォルダーにエクスポートする場合など)、レポートを共有フォルダーに配信するサブスクリプションを作成します。 詳細については、「 [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md)」を参照してください。  
  
 レポート ツールでプレビューしたレポート、またはレポート マネージャーなどのブラウザー アプリケーションで開いたレポートは常に、まず HTML でレンダリングされます。 表示の既定として別の表示拡張機能を指定することはできません。 ただし、後から電子メールの受信ボックスや共有フォルダーに配信する際に必要な表示形式でレポートを生成するサブスクリプションを作成できます。 詳細については、次を参照してください。 [Create, Modify, and 標準サブスクリプションの削除&#40;Reporting Services ネイティブ モードの&#41;](../subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)と[作成、変更、およびデータ ドリブン サブスクリプションを削除](../subscriptions/data-driven-subscriptions.md)します。  
  
 また、URL パラメーターとして表示拡張機能を指定する URL を使用してレポートにアクセスし、最初に HTML でレポートをレンダリングすることなく、指定した形式に直接レンダリングすることもできます。 次の例は、Excel 形式でレポートを表示します。  
  
```  
http://<Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 詳細については、「 [URL アクセスを使用してレポートをエクスポート](../export-a-report-using-url-access.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [改ページ、見出し、列、および行の制御 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [レポートの検索、表示、管理 &#40;レポート ビルダーおよび SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [レポートの印刷 &#40;レポート ビルダーおよび SSRS&#41;](print-reports-report-builder-and-ssrs.md)   
 [レポートの保存 &#40;レポート ビルダー&#41;](saving-reports-report-builder.md)  
  
  
