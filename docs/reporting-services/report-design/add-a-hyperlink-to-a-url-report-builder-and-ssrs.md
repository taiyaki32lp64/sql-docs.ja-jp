---
title: URL へのハイパーリンクの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 09/07/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 84f7ebd295cb64ca4d6f77427a727c1d0182b142
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574827"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>URL へのハイパーリンクの追加 (レポート ビルダーおよび SSRS)
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  のページ分割されたレポートでテキスト ボックス、画像、グラフ、ゲージにハイパーリンク アクションを追加する方法について説明します。 リンクで他のレポート、レポート内のブックマーク、静的または動的な URL に移動できます。 

 ハイパーリンク アクションは、グラフ内のテキスト ボックス、画像、計算系列などの **Action** プロパティがあるアイテムに追加できます。 ユーザーがそのレポート アイテムをクリックすると、定義されたアクションが実行されます。  
  
*   指定した **URL でブラウザーを開くハイパーリンクを追加** できます。 ハイパーリンクには、静的な URL または URL を評価する式を使用できます。 URL を保持しているデータベースのフィールドがある場合は、式にそのフィールドを指定し、レポートにハイパーリンクの動的な一覧を渡すことができます。 URL を指定する場合、レポートを読む人がその URL にアクセスできることを確認します。  
   
*  自分やユーザーに URL 要求を利用して表示する許可が与えられているレポート サーバー上であれば、そこにあるレポートへの **ドリルスルーを URL を指定して作成** できます。 たとえば、レポートを指定して、レポートがユーザーに最初に表示されたときにドキュメント マップを非表示にすることができます。 詳細については、「[URL アクセス &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md)」と「[外部アイテムへのパスの指定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)」を参照してください。
 
 *  また、同じレポートの **特定の場所にブックマークを追加** できます。 
  
「[チュートリアル: テキストの書式設定 &#40;レポート ビルダー&#41;](../../reporting-services/tutorial-format-text-report-builder.md)」で、サンプル データを利用し、ハイパーリンクの追加をお試しください。  
  
> [!NOTE]  
>  データセット フィールドにバインドされているリンクは、悪意的な改ざんに対して脆弱である可能性があります。 詳細については、「 [レポートとリソースの保護](../../reporting-services/security/secure-reports-and-resources.md)」を参照してください。  
  
## <a name="to-add-a-hyperlink-and"></a>ハイパーリンクを追加するには   
  
1.  レポート デザイン ビューで、リンクを追加するテキスト ボックス、画像、またはグラフを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  [プロパティ] ダイアログ ボックスで、 **[アクション]** タブをクリックします。オプションの詳細については、読み進めてください。  

## <a name="-add-drillthrough-to-another-report"></a>別のレポートにドリルスルーを追加するには

1. **[アクション]** タブで、 **[レポートに移動する]** を選択します。 

2. ターゲット レポートと使用するパラメーターを指定します。 パラメーター名は、対象のレポートで定義されているパラメーターと一致する必要があります。 

3. パラメーターを追加または削除するには **[追加]** ボタンまたは **[削除]** ボタンを使用し、パラメーターの一覧の順序を設定するには上矢印および下矢印を使用します。

4.  詳細レポート内の名前付きパラメーターに渡す **値** を入力または選択します。 式を編集するには、[式]\(fx) ボタンをクリックします。

5. **[省略]** を選択すると、パラメーターの実行が回避されます。 既定では、このチェック ボックスはオフになっており、アクティブではありません。 このチェック ボックスをオンにするには、式 ([fx]) ボタンをクリックし、「True」と入力するか式を作成します。 このチェック ボックスは、[式] ダイアログ ボックスで **[OK]** をクリックするとオンになります。
  
   詳細については、「 [レポートへのドリルスルー アクションの追加](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) 」を参照してください。 
   
6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
   
## <a name="-add-a-bookmark"></a>ブックマークを追加するには

現在のレポート内のある場所へのブックマークにリンクできます。 ブックマークにリンクするには、まずレポート アイテムの **Bookmark** プロパティを設定する必要があります。 **Bookmark** プロパティを設定するには、レポート アイテムを選択し、プロパティ ペインでブックマーク ID の値または式 (SalesChart、5TopSales など) を入力します。

1. **[アクション]** タブで、 **[ブックマークに移動する]** を選択します。 

2. レポートのブックマーク ID を入力または選択し、そのブックマークに移動するようにします。 式を変更するには、式 ([fx]) ボタンをクリックします。 

   ブックマーク ID には、静的 ID、または結果がブックマーク ID になる式のいずれかを指定できます。 式には、ブックマーク ID を含むフィールドを含めることができます。
   
   詳細については、「 [レポートへのブックマークの追加](../../reporting-services/report-design/add-a-bookmark-to-a-report-report-builder-and-ssrs.md) 」を参照してください。
   
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="-add-a-hyperlink"></a>ハイパーリンクを追加するには 
  
1. **[アクション]** タブで、 **[URL に移動する]** を選択します。 このオプションのダイアログ ボックスに追加のセクションが表示されます。  
  
4.  **[Select URL]** ボックスで、URL または URL に評価される式を入力または選択するか、下矢印をクリックして URL が格納されているフィールドの名前をクリックします。 

    ネイティブ モード用に構成されているレポート サーバーにアイテムをパブリッシュする場合は、完全パスまたは相対パスを指定します。 たとえば、 `https://<servername>/images/image1.jpg`のようにします。 
    
    SharePoint 統合モードで構成されているレポート サーバーにアイテムをパブリッシュする場合は、完全修飾 URL を指定します。 たとえば、 `https://<SharePointservername>/<site>/Documents/images/image1.jpg`のようにします。
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="after-you-add-a-hyperlink"></a>ハイパーリンクの追加後
  
1.  (省略可) テキストがリンクとして自動的に書式設定されることはありません。 テキストでは、テキストの色と効果を変更してそのテキストがリンクであることを示すと便利です。 たとえば、リボンの [ホーム] タブの **[フォント]** セクションで、色を青に変更し、効果を下線に変更します。  
  
7.  リンクをテストするには、 **[実行]** をクリックしてレポートをプレビューし、リンクを設定したレポート アイテムをクリックします。  
  
## <a name="see-also"></a>参照  
 [対話的な並べ替え、ドキュメント マップ、およびリンク &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [ドキュメント マップの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-a-document-map-report-builder-and-ssrs.md)  
  
  
