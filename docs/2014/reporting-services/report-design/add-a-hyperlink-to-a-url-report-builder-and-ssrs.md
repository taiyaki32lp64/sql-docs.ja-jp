---
title: URL へのハイパーリンクの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6fa7b0d32a62e5e2d729e05c88b892ccaffc0fc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106816"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>URL へのハイパーリンクの追加 (レポート ビルダーおよび SSRS)
  ユーザーがレポート内のリンクをクリックするとブラウザーが開かれ、指定した URL にアクセスできるようにするために、レポート アイテムへのハイパーリンクを追加できます。 ハイパーリンクには、静的な URL または URL を評価する式を使用できます。 URL を保持しているデータベースのフィールドがある場合は、式にそのフィールドを指定し、レポートにハイパーリンクの動的な一覧を渡すことができます。 ハイパーリンクは、テキスト ボックス、画像、グラフ、およびゲージに追加できます。 ただし、ユーザーがその URL にアクセスできることを確認する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 表示アクセス権のあるレポート サーバーへの URL 要求を使用して、レポート サーバー上のレポートへの URL を指定することもできます。 たとえば、レポートを指定して、レポートがユーザーに最初に表示されたときにドキュメント マップを非表示にすることができます。 詳細については、[Reporting Services のドキュメント](https://go.microsoft.com/fwlink/?linkid=121312) ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブック) の「[URL アクセス &#40;SSRS&#41;](../url-access-ssrs.md)」を参照してください。  
  
 URL へのハイパーリンクは、グラフ内のテキスト ボックス、画像、計算系列などの **Action** プロパティがあるアイテムに追加できます。 ユーザーがそのレポート アイテムをクリックすると、定義されたアクションが実行されます。 詳細については、「[[アクション プロパティ] ダイアログ ボックス &#40;レポート ビルダーおよび SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md)」と「[外部アイテムへのパスの指定 &#40;レポート ビルダーおよび SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)」を参照してください。  
  
 すぐに使用するには、「[チュートリアル:テキストの書式設定 &#40;レポート ビルダー&#41;](../tutorial-format-text-report-builder.md)」をご覧ください。  
  
> [!NOTE]  
>  データセット フィールドにバインドされているリンクは、悪意的な改ざんに対して脆弱である可能性があります。 詳細については、msdn.microsoft.com で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?LinkId=154888)の「[レポートとリソースの保護](../security/secure-reports-and-resources.md)」を参照してください。  
  
### <a name="to-add-a-hyperlink"></a>ハイパーリンクを追加するには  
  
1.  レポート デザイン ビューで、リンクを追加するテキスト ボックス、画像、またはグラフを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  [プロパティ] ダイアログ ボックスで **[アクション]** をクリックします。  
  
3.  **[URL に移動する]** を選択します。 このオプションのダイアログ ボックスに追加のセクションが表示されます。  
  
4.  **[Select URL]** ボックスで、URL または URL に評価される式を入力または選択するか、下矢印をクリックして URL が格納されているフィールドの名前をクリックします。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (省略可) テキストがリンクとして自動的に書式設定されることはありません。 テキストでは、テキストの色と効果を変更してそのテキストがリンクであることを示すと便利です。 たとえば、リボンの [ホーム] タブの **[フォント]** セクションで、色を青に変更し、効果を下線に変更します。  
  
7.  リンクをテストするには、 **[実行]** をクリックしてレポートをプレビューし、リンクを設定したレポート アイテムをクリックします。  
  
## <a name="see-also"></a>参照  
 [対話的な並べ替え、ドキュメント マップ、およびリンク &#40;レポート ビルダーおよび SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [ドキュメント マップの作成 &#40;レポート ビルダーおよび SSRS&#41;](create-a-document-map-report-builder-and-ssrs.md)  
  
  
