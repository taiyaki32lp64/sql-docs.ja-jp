---
title: HTML での表示 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: cf559b0a-499a-4d74-b520-b382b87e0b17
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: de76ab165f201500399ff6c0585a49122d6b9cc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580652"
---
# <a name="rendering-to-html-report-builder-and-ssrs"></a>HTML での表示 (レポート ビルダーおよび SSRS)
  XML 表示拡張機能では、ページ分割されたレポートが XML 形式で返されます。 また、完全な HTML ページを生成することも、他の HTML ページに埋め込むための HTML の一部分を生成することもできます。 すべての HTML は、UTF-8 エンコードで生成されます。  

 HTML 表示拡張機能は、 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] Web ポータルで実行する場合など、ブラウザーで表示されるレポートの既定の表示拡張機能です。 HTML 表示拡張機能を使用すると、HTML を部分的に表示することも、完全な HTML ドキュメントとして表示することもできます。 HTML がフラグメントの場合、HTML ドキュメントの **HEAD**タグ、 **HTML**タグ、および **BODY** タグが削除されています。 表示されるのは、 **BODY** タグの内容のみです。 これは、他のアプリケーションで作成した HTML に HTML を埋め込む場合に便利です。  
  
 状況によっては、レポート パラメーターを使用して、レポートが HTML で表示される際にスクリプト インジェクション攻撃を開始することも可能であることを意味します。 レポートのセキュリティ保護の詳細については、「 [レポートとリソースの保護](../../reporting-services/security/secure-reports-and-resources.md)」を参照してください。  
  
 ブラウザーの詳細については、「 [Reporting Services と Power View のブラウザー サポート](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RenderingMHTML"></a> MHTML での表示  
 HTML 表示拡張機能を使用すると、MHTML (MIME Encapsulation of Aggregate HTML Documents) でレポートを表示することもできます。 MHTML は、HTML を拡張して、画像などのエンコードされているオブジェクトを HTML ドキュメントに埋め込むことができるようにしたものです。 MHTML 表示拡張機能を使用すると、画像、ドキュメント、その他のバイナリ ファイルなどのリソースを、レポート HTML 内部の MIME 構造として単一のファイルに埋め込むことができます。 また、MHTML レポートは、すべてのリソースがレポートの中に含まれるので、電子メール メッセージに埋め込むのにも役立ちます。 実際に MHTML を表示するのは HTML 表示拡張機能ですが、この機能を MHTML 表示拡張機能と呼ぶこともあります。  
  
  
##  <a name="BrowserSupport"></a> ブラウザー サポート  
 この表示拡張機能では、次のブラウザー バージョンをサポートしています。  
  
-   Internet Explorer 5.5 以降  
  
-   Firefox 1.5 以降  
  
-   Safari 3.0 以降  
  
 各ブラウザーで適切に処理されるようにするため、表示されるレポートはブラウザーによって多少異なる場合があります。 たとえば、テキスト ボックスには WritingMode というプロパティが表示されます。 このプロパティは Firefox でサポートされていません。  
  
  
##  <a name="HTMLSpecificRenderingRules"></a> HTML 固有の表示規則  
 表示する際は、次の HTML 固有の規則が適用されます。  
  
-   各 **ReportItems** コレクション内にアイテムが複数存在する場合は、レンダラーによって、すべてのアイテムを格納するための HTML テーブル構造が構築されます。  
  
-   テーブル構造内の各アイテムは 1 つのセルを占有します。  
  
-   空のセルをできる限りまとめて HTML のサイズを小さくします。  
  
-   ブラウザーでテーブルを表示する速度を上げるために、上端に空のセルの行が追加され、左端に 1 列が追加されます。  
  
-   テーブルのアイテムが格納されていない行や列、つまりアイテムの間隔は、幅と高さが固定されています。  
  
-   その他すべての行と列は、各レポート アイテムのサイズに応じて拡張できます。  
  
-   すべての座標とレポート アイテム サイズはミリメートルに変換されます。 スタイル プロパティなどの他のすべてのサイズは、元の単位のままになります。 0\.2 mm に満たないサイズや位置の差は 0 mm として扱われます。  
  
  
##  <a name="Interactivity"></a> 対話性  
 HTML では、いくつかの対話型要素がサポートされています。 具体的な動作について説明します。  
  
### <a name="show-and-hide"></a>表示/非表示  
 表示の切り替えが可能なレポート アイテムは、切り替えイメージの展開 (+) と折りたたみ (-) と共に表示され、クリック可能です。 アイテムをクリックすると、変更後の表示/非表示状態で出力を再表示するために、サーバーへのコールバックが行われます。  
  
### <a name="document-map"></a>ドキュメント マップ  
 ドキュメント マップ ラベルが表示されると、ビューアー コントロールのドキュメント マップを使用することでそのラベルに移動できます。 データ領域のヘッダーが省略される場合、ラベルは最初の子セルに表示されます。 子セルが存在しない場合、ラベルはその前にある子に表示されます。  
  
### <a name="bookmarks"></a>ブックマーク  
 ブックマーク リンクは、ハイパーリンクとして表示されます。 ブックマーク対象が表示されると、ブックマーク リンクをクリックすることでその対象に移動できます。 ブックマーク リンクをクリックすると、レポート内で最初に出現する対象のブックマーク ラベルに移動します。さらに、可能な場合は、ブックマーク リンクがウィンドウの上部に表示されるようにブラウザーがスクロールされます。 HTML アンカー (\<a>) タグは、ブックマーク対象にマークを付けるために使用されます。  
  
### <a name="interactive-sorting"></a>対話的な並べ替え  
 テキスト ボックスでユーザーによる並べ替えが定義されている場合、HTML 表示拡張機能により、テキスト ボックス内で各項目の右側に並べ替えアイコンが表示されます。 ユーザーによる並べ替えが定義されているテキスト ボックスがレポートに含まれている場合は、JavaScript が表示されます。このスクリプトにより、並べ替えイメージをクリックしたときにサーバーへのポストバックが行われます。  
  
### <a name="hyperlinks-and-drillthrough"></a>ハイパーリンクとドリルスルー  
 ハイパーリンクとドリルスルー リンクは、これらのリンクが定義されているアイテムを HTML アンカー (\<a>) タグで囲むことにより、レポート アイテムのハイパーリンクとして表示されます。  
  
### <a name="search"></a>検索  
 検索機能を使用すると、ユーザーは、レポート内で文字列を検索することができます。  
  
 追加の検索機能は、ReportViewer Web フォーム コントロールによって提供されます。  
  
  
##  <a name="DeviceInfo"></a> デバイス情報設定  
 デバイス情報設定を変更することによって、このレンダラーに関する既定の設定の一部 (表示モードなど) を変更することができます。 詳細については、「 [HTML デバイス情報設定](../../reporting-services/html-device-information-settings.md)」を参照してください。  
  
  
## <a name="see-also"></a>参照  
 [Reporting Services の改ページ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [さまざまなレポート表示拡張機能の対話機能 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [レポート アイテムのレンダリング &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
