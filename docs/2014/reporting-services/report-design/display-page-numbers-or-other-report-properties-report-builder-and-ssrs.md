---
title: ページ番号またはその他のレポート プロパティの表示 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c7d95245-4709-4d04-acb4-59bf71e60d97
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8a8b6cc94bf769be46bf3a2fc101731ba28d2021
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321874"
---
# <a name="display-page-numbers-or-other-report-properties-report-builder-and-ssrs"></a>ページ番号またはその他のレポート プロパティの表示 (レポート ビルダーおよび SSRS)
  レポートのページ ヘッダーまたはページ フッターにページ番号、レポート タイトル、ファイル名、およびその他のレポート プロパティを簡単に追加できます。 これらのプロパティは、レポート データ ペインの [組み込みフィールド] フォルダーのフィールドとして保存されます。  
  
-   [実行時間]  
  
-   [ページ番号]  
  
-   [レポート フォルダー]  
  
-   [レポート名]  
  
-   [レポート サーバー URL]  
  
-   [総ページ数]  
  
-   [ユーザー ID]  
  
-   言語  
  
 ページ番号については、番号の前に "ページ" という語を追加したり、 総ページ数を表示したりすることもできます。  
  
> [!NOTE]  
>  フッターに総ページ数を追加すると、レポートの実行時やプレビュー時にパフォーマンスが低下することがあります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-number-or-other-report-properties"></a>ページ番号またはその他のレポート プロパティを追加するには  
  
1.  レポート データ ペインで [組み込みフィールド] フォルダーを展開します。  
  
    > [!NOTE]  
    >  [レポート データ] ペインが表示されていない場合は、[表示] タブの **[レポート データ]** をオンにします。  
  
2.  **[ページ番号]** フィールドを、[レポート データ] ペインからレポート ヘッダーまたはレポート フッターにドラッグします。  
  
    > [!NOTE]  
    >  ページ フッターはレポートに自動的に追加されます。 ページ ヘッダーを追加するには、 **[挿入]** タブで、 **[ヘッダー]** をクリックして **[ヘッダーの追加]** をクリックします。  
    >   
    >  [&PageNumber] という単純な式が含まれているテキスト ボックスが追加されます。  
  
### <a name="to-add-the-word-page-before-the-page-number"></a>ページ番号の前に "ページ" という語を追加するには  
  
1.  [&PageNumber] が含まれているテキスト ボックスを右クリックし、**[式]** をクリックします。  
  
     **[式の設定: 値]** テキスト ボックスに、=Globals!PageNumber という式が含まれています。  
  
2.  種類と = 記号の後にカーソルを置き`"Page " &`します。  
  
     式は、="ページ "&Globals!PageNumber となります。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-total-number-of-pages-after-the-page-number"></a>ページ番号の後ろに総ページ数を追加するには  
  
1.  式が含まれているテキスト ボックスを右クリックし、 **[式]** をクリックします。  
  
2.  式の末尾に「**&"/"&**」と入力します。  
  
3.  [カテゴリ] ペインで、 **[組み込みフィールド]** を展開し、 **[TotalPages]** をダブルクリックします。  
  
     式は、="ページ "&Globals!PageNumber &"/"&Globals!TotalPages となります。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [ページ ヘッダーとページ フッター&#40;レポート ビルダーおよび SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)   
 [テキスト ボックス内のテキストを書式設定&#40;レポート ビルダーおよび SSRS&#41;](format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
  