---
title: 画像のプロパティ ダイアログ ボックス、一般的な (レポート ビルダーおよび SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10051"
- sql12.rtp.rptdesigner.pictureproperties.general.f1
ms.assetid: c2218b93-f7fe-46ef-995f-d7dadf9752ec
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a66c424bfe5bd4a2587140a0f5238f46833a061
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109029"
---
# <a name="image-properties-dialog-box-general-report-builder-and-ssrs"></a>[全般] ([画像のプロパティ] ダイアログ ボックス) (レポート ビルダーおよび SSRS)
  **[画像のプロパティ]** ダイアログ ボックスの **[全般]** を選択すると、画像の追加、画像の既定の名前の変更、およびツールヒントのテキストの追加を実行できます。  
  
## <a name="options"></a>および  
 **名前**  
 アイテムの名前を入力します。 名前はレポート内で一意である必要があります。 既定では、Image1 や Image2 などの一般的な名前が割り当てられます。  
  
 **ツール ヒント**  
 テキスト、または結果がツールヒントになる式を入力します。 式を編集するには、式 ( *[fx]* ) ボタンをクリックします。 **[ツールヒント]** は、ユーザーが HTML レポートのアイテムの上にポインターを置いたときに表示されます。  
  
 **画像ソースを選択します。**  
 レポートを表示する際にレポート プロセッサで画像の取得元が認識されるように、画像が格納されている場所を指定します。  
  
-   **[外部]** レポート サーバーおよび Web サーバー上のファイルとして画像を残す場合にこのオプションを選択します。  
  
-   **[埋め込み]** レポートに画像を埋め込む場合にこのオプションを選択します。  
  
-   **[データベース]** レポートに含める画像を表すデータベース フィールド名を追加する場合にこのオプションを選択します。  
  
 **このイメージを使用します。**  
 このオプションは、 **[埋め込み]** または **[外部]** を選択した場合に表示されます。  
  
 画像を埋め込む場合は、レポートに追加する画像をドロップダウン リストから選択します。 ドロップダウン リストに画像を追加するには、 **[インポート]** ボタンをクリックします。  
  
 **[外部]** オプションを選択した場合は、画像の URL を入力します。 ネイティブ モード用に構成されているレポート サーバーにレポートをパブリッシュする場合は、完全パスまたは相対パスを指定します。 たとえば、 http://\<servername >/images/image1.jpg します。 SharePoint 統合モードで構成されているレポート サーバーにレポートをパブリッシュする場合は、完全修飾 URL を指定します。 たとえば、 http://\<*SharePointservername*>/\<*サイト*>/Documents/images/image1.jpg します。  
  
 **[インポート]**  
 **[次の画像を使用]** ボックスの一覧に画像を追加する場合にクリックします。  
  
 **このフィールドを使用します。**  
 このオプションは、 **[データベース]** オプションを選択した場合に表示されます。 フィールド名を選択します。  
  
 **この MIME の種類を使用して、**  
 データベース内に含まれている画像の適切な形式を選択します (.bmp、.jpeg、.gif、.png、.x-png など)。  
  
## <a name="see-also"></a>関連項目  
 [式の例 (レポート ビルダーおよび SSRS)](report-design/expression-examples-report-builder-and-ssrs.md)   
 [画像 &#40;レポート ビルダーおよび SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [レポート ビルダーのダイアログ ボックス、ペイン、およびウィザードに関するヘルプ](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
