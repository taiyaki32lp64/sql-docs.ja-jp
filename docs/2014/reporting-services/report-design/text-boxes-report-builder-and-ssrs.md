---
title: テキスト ボックス (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10134"
- sql12.rtp.rptdesigner.textproperties.general.f1
- "10120"
- sql12.rtp.rptdesigner.textboxproperties.general.f1
ms.assetid: df49e4e3-f279-4c63-a03b-b70c095f4ba2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fb96831c54a67a6ea74ca984cb346dcaaf50a335
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104629"
---
# <a name="text-boxes-report-builder-and-ssrs"></a>テキスト ボックス (レポート ビルダーおよび SSRS)
  テキスト ボックスといえば、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office PowerPoint のように領域にテキストを含むスタンド アロンのボックスを思い浮かべると思います。 レポート ビルダーでは、同じように、タイトル、説明、およびラベルのリテラル テキスト、または式に基づく動的なテキストを表示できます。 ただし、テーブルまたはマトリックス (Tablix データ領域) の各セルにはテキスト ボックスがあり、レポート内のスタンドアロン テキスト ボックスと同じ方法で書式設定することもできます。  
  
> [!NOTE]  
>  レポート デザイン画面またはレポート デザイン画面上のテキスト ボックスに、レポート データセットのフィールド値を直接ドラッグすると、レポートを実行する際に、結果セットの最初の値のみが表示されます。 フィールドのすべての値を表示するには、テーブルまたはマトリックスのセルにフィールドをドラッグする必要があります。 この状態でレポートを実行すると、そのフィールドにすべての値が表示されます。  
  
 自由形式レイアウトでテキストを繰り返し表示するには、一覧データ領域にテキスト ボックスを配置します。 複数値に対し形式を繰り返す場合は、一覧を使用します。たとえば、各顧客につき 1 回繰り返される請求書フォームなどです。 詳細については、次を参照してください。[一覧&#40;レポート ビルダーおよび SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)します。  
  
 テキスト ボックス レイアウト、および最後のテキスト ボックスの下の空白を制御するには、四角形のコンテナーを使用します。 詳細については、「[四角形と線 &#40;レポート ビルダーおよび SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md)」を参照してください。  
  
 テキスト ボックス内で式を使用して、リテラル テキストを保持したり、データベースのフィールドを指定したり、データを計算したりできます。 すべての式はプレースホルダー テキストとして表示され、番号、色、および他の外観のプロパティを書式設定できます。 同じテキスト ボックス内でプレースホルダーをリテラル テキストと組み合わせることもできます。  
  
 複数のフォント、色、スタイル、およびアクションを使用して、1 つのテキスト ボックスでテキストを書式設定できます。 詳細については、「 [テキストとプレースホルダーの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="GrowShrinkTextBox"></a> テキスト ボックスの拡張と圧縮  
 既定では、テキスト ボックスのサイズは固定されています。 テキスト ボックスをその内容に応じて縦に縮小または拡張されるようにすることができます。 詳細については、「 [テキスト ボックスの拡大または縮小 &#40;レポート ビルダーおよび SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="orienting-a-text-box"></a>テキスト ボックスの向きの調整  
 テキスト ボックスの向きを調整することによって、より読みやすいレポートを作成したり、ロケール特有のテキストの向きに対応したり、ページ サイズが固定された印刷レポートに合うようにより多くの列を調整したり、視覚的により優れたレポートを作成したりできます。 テキスト ボックスは、水平方向、垂直方向、または 270 度回転させて向きを調整できます。 垂直オプションは、上から下に字を書く東アジアの言語で最も一般的に使用されます。 大部分のレンダラーで、垂直オプションは、テキストが上から下に配置されるように (文字は横向きにならない) グリフの回転プロパティを処理します。 その他の言語の場合、垂直オプションおよび 270 度回転オプションではテキストは横向きに配置されます。  
  
 リテラル テキスト、レポート データセットからのフィールド、または計算されたデータを含むテキスト ボックスに向きを適用できます。 テキスト ボックスは、レポート本文、テーブルまたはマトリックス、レポート ヘッダーとフッターでスタンドアロンになることができます。  
  
 次の図は、月ごとにデータをグループ化するテーブル レポートの 3 つのバージョンを示しています。 月の値を含むテキスト ボックスでは、異なるテキスト ボックスの向きが使用されます。  
  
 ![rs_TextBoxOrientation](../media/rs-textboxorientation.gif "rs_TextBoxOrientation")  
  
 方向はテキスト ボックスに対して設定されるため、そのテキスト ボックス内のすべてのテキストにその方向が適用されます。 テキスト ボックスの一部のみに異なる方向を指定することはできません。  
  
 すばやくテキストの向きの変更を開始するには、テキストの回転に関するセクションを参照、[チュートリアル。テキストの書式設定 &#40;レポート ビルダー&#41;](../tutorial-format-text-report-builder.md)」をご覧ください。 詳細については、次を参照してください。[設定のテキスト ボックスの方向&#40;レポート ビルダーおよび SSRS&#41;](set-text-box-orientation-report-builder-and-ssrs.md)します。  
  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 [テキスト ボックスの追加、移動、または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-move-or-delete-a-text-box-report-builder-and-ssrs.md)  
  
 [テキスト ボックス内のテキストの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
 [テキスト ボックスの方向の設定 &#40;レポート ビルダーおよび SSRS&#41;](set-text-box-orientation-report-builder-and-ssrs.md)  
  
 [テキスト ボックスの拡大または縮小 &#40;レポート ビルダーおよび SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>参照  
 [テキストとプレースホルダーの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [数値と日付の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)  
  
  
