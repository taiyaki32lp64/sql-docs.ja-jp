---
title: Microsoft Word へのエクスポート (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 12/06/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
description: Word 表示拡張機能は、改ページ調整されたレポートを  [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 形式 (.docx) で表示します。 形式は、Office Open XML です。
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 0cd8ae26-4682-4473-8f15-af084951defd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9efad50aeb778c4cae01145fb39dd10a71c42ca0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66413567"
---
# <a name="exporting-to-microsoft-word-report-builder-and-ssrs"></a>Exporting to Microsoft Word (Report Builder and SSRS)

  Word 表示拡張機能は、改ページ調整されたレポートを Microsoft Word 形式 (.docx) で表示します。 形式は、Office Open XML です。  
  
 このレンダラーによって生成されるファイルのコンテンツ タイプは **application/vnd.openxmlformats-officedocument.wordprocessingml.document** で、ファイル拡張子は .docx です。  
  
 Word へのエクスポート方法については、「[レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)」を参照してください。  
  
 レポートを Word 文書にエクスポートした後は、レポートの内容を変更したり、宛名ラベル、発注書、手紙など、文書形式のレポートをデザインしたりできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItemsWord"></a> Word のレポート アイテム  
 Word にエクスポートされたレポートは、そのレポート本文を表す、入れ子の表として表示されます。 Tablix データ領域は、レポート内のデータ領域の構造を反映した、入れ子の表としてレンダリングされます。 テキスト ボックスおよび四角形は、表内のセルとしてレンダリングされます。 テキスト ボックスの値はセル内部に表示されます。  
  
 画像、グラフ、データ バー、スパークライン、マップ、インジケーター、およびゲージは、それぞれ表のセル内に静的な画像としてレンダリングされます。 これらのレポート アイテムでは、設定されているハイパーリンクやドリルスルー リンクがレンダリングされます。 グラフ内のクリック可能なマップや領域はサポートされません。  
  
 ニュースレター形式のカラム レポートは、Word ではレンダリングされません。 レポート本文およびページ背景の画像およびカラーはレンダリングされません。  
  
##  <a name="Pagination"></a> ページ割り付け  
 レポートを Word で開くと、レポート全体の改ページ位置が、ページ サイズに基づいて自動的に修正されます。 改ページ位置の修正によって、想定しない場所に改ページが挿入されることがあります。場合によっては、エクスポートされたレポートに連続して 2 つの改ページが挿入されたり、空白のページが追加されたりすることもあります。 Word の改ページは、ページ余白を調整することによって変更できます。  
  
 このレンダラーでは、論理的な改ページのみがサポートされます。  
  
### <a name="page-sizing"></a>ページのサイズ設定  
 Word でレポートをレンダリングするときのページの高さと幅は、各種の RDL プロパティ (用紙サイズの高さと幅、左右のページ余白、および上下のページ余白) によって設定されます。  
  
### <a name="page-width"></a>ページの幅  
 Word では、最大 22 インチのページ幅がサポートされます。 レポートの幅が 22 インチを超えたとしても、レポートのレンダリングは続行されます。ただし、Word の印刷レイアウト表示または閲覧レイアウト表示では、レポートの内容が表示されません。 データを表示するには、下書き表示モードまたは Web レイアウト表示に切り替えてください。 この場合、Word によって、空白のサイズが縮小されるため、より多くのレポート コンテンツを表示できるようになります。  
  
 レンダリング時には、コンテンツを表示できるように、必要に応じてレポートの幅が最大 22 インチまで拡大されます。 レポートの最小幅は、[プロパティ] ペインの RDL の Width プロパティに基づきます。  
  
##  <a name="DocumentProperties"></a> ドキュメント プロパティ  
 Word レンダラーでは、次のメタデータが DOCX ファイルに書き込まれます。  
  
|レポート要素のプロパティ|Description|  
|-------------------------------|-----------------|  
|Report Title (レポート タイトル)|[タイトル]|  
|Report.Author|Author|  
|Report.Description|コメント|  
  
##  <a name="ReportHeadersFooters"></a> ページ ヘッダーとページ フッター  
 ページのヘッダーとフッターは、Word のヘッダー領域およびフッター領域としてレンダリングされます。 ページ ヘッダーまたはページ フッターに、レポートの合計ページ数を表すページ番号 (または式) が表示される場合、これらは、レンダリング後のレポートに正確なページ番号が表示されるように、Word のフィールドに変換されます。 レポートで設定されたヘッダーまたはフッターの高さは、Word では反映されません。 状況によっては、PrintOnFirstPage プロパティを使用して、ページ ヘッダーとページ フッターのテキストをレポートの最初のページに印刷するかどうかを指定できます。 表示レポートに複数のページがあり、ページごとに 1 つのセクションのみが含まれる場合は、PrintOnFirstPage を False に設定でき、最初のページのテキストは非表示になります。それ以外の場合は、PrintOnFirstPage プロパティの値に関係なく、テキストが印刷されます。  
  
 Word レンダラーでは、レポートが Word にエクスポートされるときに、ページのヘッダーとフッター内にあるすべての式の解析が試行されます。 式の多くの形式では、解析が完了すると、すべてのレポート ページのページ フッターとページ ヘッダーに予期された値が表示されます。  
  
 ただし、ページ フッターまたはページ ヘッダーに複合式が含まれており、この複合式がレポートのページごとに異なる値として評価される場合は、すべてのレポート ページに同じ値が表示されることがあります。 次の 2 つの式では、ページ番号がエクスポートされたレポートで増加しません。 ページ番号はすべてのレポート ページで同じ値になります。  
  
-   `="Page: " + Globals!PageNumber.ToString + " of " + Globals!TotalPages.ToString`  
  
-   `=Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
 この問題は、Word レンダラーがレポートの **PageNumber** や **TotalPages** などの改ページに関連するフィールドを解析して単純な参照のみを処理し、関数の呼び出しが行われないために生じます。 この場合、式は **ToString** 関数を呼び出します。 次の 2 つの式は同等であり、レポート ビルダーやレポート デザイナーでレポートをプレビューするか、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータルや SharePoint ライブラリでパブリッシュされたレポートを表示した場合は、両方とも正しく表示されます。 ただし、Word レンダラーでは 2 番目の式のみが正しく解析され、正しいページ番号が表示されます。  
  
-   **複合式:**  式は以下のとおりです: `="Average Sales " & Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
-   **テキスト ランを使用した式:** テキスト、 **Average Sales**、および式、  `=Avg(Fields!YTDPurchase.Value, "Sales)`、およびテキスト、 **ページ番号**、および式 `=Globals!PageNumber`  
  
 この問題を回避するには、フッターおよびヘッダーで式を使用するときに 1 つの複合式ではなく複数のテキスト ランを使用します。 次の 2 つの式は等価です。 最初の式は複合式で、2 番目の式はテキスト ランを使用しています。 Word レンダラーでは、2 番目の式のみが正しく解析されます。  
  
##  <a name="Interactivity"></a> 対話性  
 Word では、いくつかの対話型要素がサポートされています。 具体的な動作について説明します。  
  
### <a name="show-and-hide"></a>表示/非表示  
 Word レンダラーでは、レンダリング時の状態に基づいてレポート アイテムがレンダリングされます。 レポート アイテムの状態が非表示であった場合、そのレポート アイテムは Word 文書にレンダリングされません。 レポート アイテムが表示状態であった場合、そのレポート アイテムは Word 文書にレンダリングされます。 Word で表示と非表示を切り替えることはできません。  
  
### <a name="document-map"></a>ドキュメント マップ  
 レポートに存在するドキュメント マップ ラベルは、レポートの各アイテムやグループに対する Word の目次 (TOC) ラベルとしてレンダリングされます。 ドキュメント マップ ラベルは、TOC ラベルのラベル テキストとして使用されます。 ターゲット リンクは、ラベルが設定されたアイテム付近に配置されます。 Word 文書に TOC が自動的に作成されるわけではありませんが、レポートにレンダリングされるドキュメント マップ ラベルを使って、独自に TOC を作成することはできます。  
  
### <a name="hyperlink-and-drillthrough-links"></a>ハイパーリンクとドリルスルー リンク  
 テキスト ボックスや画像のレポート アイテムに設定されているハイパーリンクおよびドリルスルー リンクは、Word 文書ではハイパーリンクとしてレンダリングされます。 ハイパーリンクをクリックすると、既定の Web ブラウザーが開いて、対応する URL に移動します。 ドリルスルー ハイパーリンクをクリックした場合は、生成元のレポート サーバーがアクセスされます。  
  
### <a name="interactive-sorting"></a>対話的な並べ替え  
 レポート コンテンツは、現在の並べ替え状態に基づいて、レポート データ領域内にレンダリングされます。 Word では、対話的な並べ替えがサポートされません。 レポートのレンダリング後は、Word の表の並べ替え機能を使用してください。  
  
### <a name="bookmarks"></a>ブックマーク  
 レポート内のブックマークは、Word のブックマークとしてレンダリングされます。 ブックマーク リンクは、文書内のブックマーク ラベルに接続するハイパーリンクとしてレンダリングされます。 ブックマーク ラベルは 40 文字未満にする必要があります。 ブックマーク ラベルに使用できる特殊文字はアンダースコア (_) だけです。 サポート外の特殊文字はブックマーク ラベルの名前から削除されます。また、40 文字を超えた場合、名前が切り詰められます。 レポートに重複するブックマーク名が存在した場合、それらのブックマークは、Word ではレンダリングされません。  
  
##  <a name="WordStyleRendering"></a> Word スタイルのレンダリング  
 以降、Word におけるスタイルのレンダリングについて簡単に説明します。  
  
### <a name="color-palette"></a>色パレット  
 レポートにレンダリングされた色は、Word 文書にレンダリングされます。  
  
### <a name="border"></a>罫線  
 ページ罫線を除く、レポート アイテムの罫線は、Word の表のセル罫線としてレンダリングされます。  
  
##  <a name="SquigglyLines"></a> エクスポートされたレポートの波線  
 レポート データまたは定数をエクスポートして Word で表示すると、その部分の下に赤または緑の波線が表示される場合があります。 赤い波線はスペル ミスを示します。 緑の波線は文法エラーを示します。 これは、Word で指定された編集言語の校正 (スペルおよび文法) 規則に適合しない単語がレポートに含まれている場合に生じます。 たとえば、レポートの列タイトルが英語である場合に、このレポートをスペイン語版の Word でレンダリングすると、列タイトルに赤い波線の下線が表示される可能性があります。 レポートには完全な文や段落ではなく短いテキストのみが含まれていることが多いため、レポートでは文法エラーとして認識されるエラーよりスペル ミスとして認識されるエラーの方がより一般的です。  
  
 レポート内に波線が存在する場合、そのレポートにエラーがある可能性を示していますが、実際のエラーではないことが少なくありません。 このような波線は、レポートの校正言語を変更することで除去できます。 校正言語を変更するには、レポートのコンテンツを選択し、そのコンテンツの適切な言語を指定します。 コンテンツをすべて選択することも、部分的に選択することもできます。 Word の言語オプションである **[校正言語の設定]** は、 **[校閲]** タブの **[言語]** にあります。コンテンツを更新した後は、再度ドキュメントを保存する必要があります。  
  
 Office プログラムの言語バージョンによって、選択した言語の校正ツール (辞書など) がプログラムに含まれている場合と、購入した [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 言語パックで提供されている場合があります。  
  
 以下のトピックでは、Office および Word のオプションについて詳しく説明します。  
  
-   Word の **[Microsoft Office 言語設定]** または **[Word のオプション]** ダイアログ ボックスで編集言語を変更する方法。 詳細については、「 [編集言語、表示言語、またはヘルプ言語を設定する](https://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1)」を参照してください。  
  
-   Office 言語パックを追加して編集言語を変更する方法。 詳細については、「 [編集言語、表示言語、またはヘルプ言語を設定する](https://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1) 」および「 [Office の言語オプション](https://office.microsoft.com/language/)」を参照してください。  
  
> [!NOTE]  
>  Word の **[Microsoft Office 言語設定]** または **[Word のオプション]** ダイアログ ボックスで編集言語を変更すると、その変更がすべての Office プログラムに適用されます。  
  
##  <a name="WordLimitations"></a> Word の制限  
 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]では、次の制限事項が適用されます。  
  
-   Word の表でサポートされる列数は、最大 63 です。 列数が 63 を超えるレポートをレンダリングしようとすると、Word によって表が分割されます。 追加列は 63 列目と隣接するように、レポート本文に配置されます。 そのため、レポートの列位置にずれが生じる場合があります。  
  
-   Word でサポートされるページの幅と高さの最大値は、22 インチ × 22 インチです。 コンテンツのサイズが 22 インチを超えた場合、印刷レイアウト表示で一部のデータが表示されない場合があります。  
  
-   Word では、ページ ヘッダーとページ フッターに適用されている高さの設定が無視されます。  
  
-   レポートのエクスポート後、Word によって改ページ位置の自動修正が再度実行されます。 これにより、レンダリングされたレポートに余分な改ページが追加される場合があります。  
  
-   Tablix (テーブル、マトリックス、または一覧) の静的なヘッダー行の RepeatOnNewPage プロパティを **True**に設定しても、Word では、2 ページ目以降にヘッダー行が表示されません。 新しいページにヘッダー行を表示するには、レポートで明示的な改ページを定義することができます。 ただし、Word では、独自の改ページ位置の自動修正が、Word にエクスポートされた表示レポートに適用されるため、結果は異なる可能性があり、ヘッダー行が予測どおりに表示されない場合があります。 静的なヘッダー行とは、列見出しを含む行のことです。  
  
-   改行をしないスペースが含まれている場合、テキスト ボックスが大きくなります。  
  
-   テキストを Word にエクスポートした際に、一部のフォントについては、フォント装飾付きテキストによって、レンダリング後のレポートに予期しないグリフや存在しないグリフが生成される場合があります。  
  
##  <a name="WordBenefits"></a> Word レンダラーを使用する利点  
 エクスポートされたレポートで [!INCLUDE[ofprword](../../includes/ofprword-md.md)] .docx ファイルの新機能が利用できるようになる点に加え、エクスポートされたレポートの *.docx ファイルのサイズが小さくなる傾向があります。 Word レンダラーを使用してエクスポートされたレポートは通常、Word 2003 レンダラーを使用してエクスポートされた同じレポートよりもサイズがかなり小さくなります。  
  
## <a name="backward-compatibility-of-exported-reports"></a>エクスポートされたレポートの下位互換性  
 Word 互換性モードを選択し、互換性オプションを設定できます。 Word レンダラーでは互換性モードをオンにしてドキュメントが作成されます。 互換性モードをオフにしてドキュメントを再度保存すると、ドキュメントのレイアウトに影響する場合があります。  
  
 互換性モードをオフにしてレポートを再度保存すると、レポートのレイアウトが予期しない方法で変更される場合があります。  
  
##  <a name="AvailabilityWord"></a> Word 2003 レンダラー  
  
> [!IMPORTANT]  
>  [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 (.doc) 表示拡張機能の使用は非推奨とされます。 詳細については、「 [SQL Server 2016 における SQL Server Reporting Services の非推奨の機能](~/reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)」を参照してください。  
  
 Word レンダラーはインストールされている Word/Excel/PowerPoint 用 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] Office 互換機能パックにより、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 2003 との互換性が維持されます。 詳細については、「 [Word、Excel、および PowerPoint 2007 用ファイル形式互換機能パック](https://www.microsoft.com/download/details.aspx?id=12439)」を参照してください。  
  
 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 と互換性のある Word 表示拡張機能の以前のバージョンは、名前が Word 2003 に変更されます。 既定では、Word 表示拡張機能のみを使用できます。 Word 2003 表示拡張機能を使用できるようにするには、Reporting Services の構成ファイルを更新する必要があります。 Word 2003 レンダラーで生成されるファイルのコンテンツ タイプは **application/vnd.ms-word** で、ファイル名拡張子は .doc です。  
  
 SQL Server Reporting Services の既定の Word レンダラーは、[!INCLUDE[ofprword](../../includes/ofprword-md.md)] 形式 (.docx) を表示するバージョンです。 これは、 **Web ポータルおよび SharePoint リストの** [エクスポート] **メニューに用意されている** [Word] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] オプションです。 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 のみと互換性のある以前のバージョンは、Word 2003 という名前になり、この名前がメニューに表示されます。 **[Word 2003]** メニュー オプションは、既定では表示されません。このメニュー オプションを表示するには、管理者が RSReportServer 構成ファイルを更新する必要があります。 Word 2003 レンダラーを使用して [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] からレポートをエクスポートするには、RSReportDesigner 構成ファイルを更新します。 ただし、Word 2003 レンダラーを表示するように設定しても、Word 2003 レンダラーがすべてのシナリオで使用できるわけではありません。 RSReportServer 構成ファイルはレポート サーバー上に存在しているため、レポートをエクスポートするツールまたは製品が構成ファイルを読み取るためにレポート サーバーに接続されている必要があります。 ツールまたは製品を切断モードまたはローカル モードで使用している場合、Word 2003 レンダラーを表示する設定は効果がありません。 **[Word 2003]** メニュー オプションは使用可能になりません。 RSReportDesigner 構成ファイルで Word 2003 レンダラーを表示するように設定した場合、 **のレポート プレビューで** [Word 2003] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] メニュー オプションが常に使用可能になります。  
  
 **[Word 2003]** メニュー オプションは、次の状況では表示されません。  
  
-   レポート ビルダーが切断モードのときにレポート ビルダーでレポートをプレビューした場合。  
  
-   レポート ビューアー Web パーツがローカル モードで、SharePoint ファームが [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーと統合されていない場合。 詳細については、「[レポート ビューアーでのローカル モードと接続モードのレポート &#40;Reporting Services の SharePoint モード&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
 **[Word 2003]** レンダラーが表示されるように構成されている場合は、 **Word** と **Word 2003** の両方のメニュー オプションが次の状況で使用可能になります。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータル (Reporting Services がネイティブ モードでインストールされている場合)。  
  
-   SharePoint サイト (Reporting Services が SharePoint 統合モードでインストールされている場合)。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] でレポートをプレビューする場合。  
  
-   レポート ビルダーがレポート サーバーに接続されている場合。  
  
-   リモート モードのレポート ビューアー Web パーツ。  
  
 次の XML は、RSReportServer 構成ファイルと RSReportDesigner 構成ファイルの 2 つの Word 表示拡張機能の要素を示します。  
  
 `<Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>`  
  
 `<Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>`  
  
 WORDOPENXML 拡張機能は [!INCLUDE[ofprword](../../includes/ofprword-md.md)] .docx ファイル用の Word レンダラーを定義します。 WORD 拡張機能は、 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 バージョンを定義します。 `Visible = "false"` は、Word 2003 レンダラーが非表示であることを示します。 詳細については、「 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 」および「 [RSReportDesigner 構成ファイル](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)」を参照してください。  
  
### <a name="differences-between-the-word-and-word-2003-renderers"></a>Word レンダラーと Word 2003 レンダラーの違い  
 Word レンダラーまたは Word 2003 レンダラーを使用して表示されたレポートは、見た目では区別できない傾向にあります。 ただし、Word または Word 2003 の 2 つの形式の間で若干の違いが見つかる場合があります。  
  
##  <a name="DeviceInfo"></a> デバイス情報設定  
 このレンダラーでは、デバイス情報設定を変更することによって、一部の既定の設定を変更できます。たとえば、ハイパーリンクやドリルスルー リンクを省略することも、展開表示と縮小表示の切り替えが可能な項目について、レンダリング時の状態に関係なく、すべての項目を展開することもできます。 詳しくは、「 [Word Device Information Settings](../../reporting-services/word-device-information-settings.md)」をご覧ください。  

## <a name="next-steps"></a>次の手順

[Reporting Services の改ページ](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
[レンダリングの動作](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
[さまざまなレポート表示拡張機能の対話機能](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
[レポート アイテムのレンダリング](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
[テーブル、マトリックス、および一覧](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
