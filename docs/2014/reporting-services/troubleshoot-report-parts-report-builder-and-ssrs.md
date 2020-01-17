---
title: レポート パーツ (レポート ビルダーおよび SSRS) のトラブルシューティング |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9fe1932-46e7-421b-a8a9-4c54d9576e94
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df37de909461ace62edbbf3cfe9e7b9dd8448b56
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099390"
---
# <a name="troubleshoot-report-parts-report-builder-and-ssrs"></a>レポート パーツのトラブルシューティング (レポート ビルダーおよび SSRS)
  レポート パーツを使用するために役立つヒントを以下に示します。  
  
## <a name="why-do-my-co-worker-and-i-see-different-instances-of-the-same-report-part-when-we-search-for-it"></a>同僚と同じレポート パーツを検索したのに、表示されるインスタンスが異なる  
 レポート サーバーまたはレポート サーバーに統合された SharePoint サイトには、1 つのレポート パーツに対して、すべて同じグローバル一意識別子 (GUID) を持つ複数のインスタンスが存在する場合があります。 検索結果には、最新のインスタンスのみが表示されます。 1 つのレポート パーツに複数のインスタンスがある場合は、それぞれの権限が異なる可能性があります。 サーバーに対する権限が同僚と異なる場合は、同じインスタンスが表示されません。 たとえば、すべて同じ GUID を持つレポート パーツの複数のコピーが SharePoint 統合モードのレポート サーバー上のそれぞれ異なるフォルダーに保存されているとします。 フォルダーの権限が異なる場合、これらのフォルダーのレポート パーツもそれぞれ異なる権限を持つことになります。  
  
 自分の権限と同僚の権限を確認するには、レポート サーバー管理者に問い合わせてください。  
  
## <a name="when-i-search-for-report-parts-that-i-uploaded-to-a-sharepoint-server-i-do-not-see-them-why-not"></a>SharePoint サーバーにアップロードしたレポート パーツを検索しても、 表示されない  
 レポート ビルダーを使用してパブリッシュする代わりに、SharePoint ドキュメント ライブラリに手動でアップロードしたレポート パーツは、レポート パーツ ギャラリーに表示されない場合があります。 ギャラリー検索に使用されるレポート サーバーは、SharePoint ドキュメント ライブラリのコンテンツと同期することが必要な場合があります。 詳細については、次を参照してください。 [SharePoint サーバーの全体管理でレポート サーバー ファイル同期機能をアクティブ化](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)で[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][オンライン ブックの「](https://go.microsoft.com/fwlink/?LinkId=154888) msdn.microsoft.com します。  
  
## <a name="why-cant-others-see-the-image-in-their-reports"></a>他の人のレポートに画像が表示されない  
 画像ファイルのリンクとなるレポート パーツをパブリッシュした場合、このレポート パーツは単なるリンクになります。 他の人がレポートに画像レポート パーツを作成したときに画像が表示されない場合は、リンク先の画像に対する権限を持っていないことが考えられます。  
  
 この解決方法として、次のいくつかの手段が挙げられます。  
  
-   画像ファイルへのリンクをレポート パーツとするのではなく、画像ファイルをレポート パーツにする。  
  
-   他の人が権限を持つ場所に画像ファイルを移動する。  
  
-   レポート サーバー管理者に権限を変更してもらう。  
  
## <a name="why-do-i-get-a-circular-reference-error-message-when-i-try-to-publish-my-report-part"></a>レポート パーツをパブリッシュしようとすると、"循環参照" エラー メッセージが表示される  
 レポート アイテムに循環参照が含まれている場合、そのアイテムをレポート パーツとしてパブリッシュすることはできません。 たとえば、レポート アイテムがデータセットを参照し、そのデータセットがパラメーターを参照するとします。 また、そのパラメーターはデータセットを参照します。 レポート パーツをパブリッシュするには、まずいずれかの参照を削除する必要があります。  
  
## <a name="see-also"></a>参照  
 [レポート パーツ &#40;レポート ビルダーおよび SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  
