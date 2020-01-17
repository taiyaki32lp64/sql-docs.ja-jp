---
title: '[塗りつぶし] ダイアログ ボックス (レポート ビルダーおよび SSRS) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportbody.fill.f1
- "10065"
- "10501"
- sql12.rtp.rptdesigner.shared.filldv.f1
- sql12.rtp.rptdesigner.rectangleproperties.fill.f1
- "10064"
- sql12.rtp.rptdesigner.textboxproperties.fill.f1
- "10124"
ms.assetid: 93a91d02-d558-4a0e-8d17-3fdf21e208d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86f54b00e530e70d1952461ce7b98b9238e4c3f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109156"
---
# <a name="fill-dialog-box-report-builder-and-ssrs"></a>[塗りつぶし] ダイアログ ボックス (レポート ビルダーおよび SSRS)
  **[塗りつぶし]** タブでは、データ領域やテキスト ボックスにある 1 つまたは複数のセルの背景色のオプションを指定できます。  
  
## <a name="options"></a>および  
 **塗りつぶしの色**  
 色のボタンをクリックして、四角形の塗りつぶしの色を選択します。 式を編集するには、 **[式]** _(fx)_ ボタンをクリックします。この式には、RGB 色を表す 16 進値、または **[式]** ダイアログ ボックスに用意されている定義済みの色の名前を使用できます。 定義済みの色の一覧を表示するには、 **[アイテム]** ペインの **[Web]** を選択します。 **[タイトル]** ペインに表示されている色の名前は、[式] ペインに入力できます。 色の名前を入力する場合は、等号 (=) または引用符 ("") を使用しないでください。  
  
 **画像ソースを選択します。**  
 レポートを表示する際にレポート プロセッサで表示できるように、画像が格納されている場所を指定します。  
  
-   **[外部]** レポート サーバーおよび Web サーバー上のファイルとして画像を残す場合にこのオプションを選択します。  
  
-   **[埋め込み]** レポートに画像を埋め込む場合にこのオプションを選択します。  
  
-   **[データベース]** レポートに含める画像を表すデータベース フィールド名を追加する場合にこのオプションを選択します。  
  
 **このイメージを使用します。**  
 このオプションは、 **[埋め込み]** または **[外部]** を選択した場合に表示されます。  
  
 画像を埋め込む場合は、レポートに追加する画像をドロップダウン リストから選択します。 ドロップダウン リストに画像を追加するには、 **[インポート]** をクリックします。 画像を **[データ]** ペインに追加した場合は、 **[埋め込み]** をクリックし、ドロップダウン リストから画像を選択すると、追加した画像を選択できます。  
  
 **[外部]** オプションを選択した場合は、画像の URL を入力します。 ネイティブ モード用に構成されたレポート サーバーにパブリッシュされたレポートの場合、完全なパスまたは相対パスを使用して、(たとえば、 http:// *\<servername >* /images/image1.jpg)。 SharePoint 統合モードで構成されているレポート サーバーにパブリッシュされたレポート、完全修飾 URL を使用して (http:// など *\<SharePointservername >/\<サイト >* ドキュメント/イメージ/image1.jpg)。  
  
 **[インポート]**  
 **[埋め込み]** を選択すると使用できます。 **[次の画像を使用]** ボックスの一覧に画像を追加する場合にクリックします。  
  
 **このフィールドを使用します。**  
 **[データベース]** を選択すると使用できます。 フィールド名を選択します。  
  
 **この MIME の種類を使用して、**  
 データベース内に含まれている画像の適切な形式を選択します (たとえば、.bmp、.jpeg、.gif、.png、.x-png など)。  
  
## <a name="see-also"></a>関連項目  
 [レポート アイテムの書式設定 (レポート ビルダーおよび SSRS)](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [テキストとプレースホルダーの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [画像 (レポート ビルダーおよび SSRS)](report-design/images-report-builder-and-ssrs.md)  
  
  
