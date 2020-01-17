---
title: リンク レポートを作成する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d0df6a3bdb6f542b02b62ccf4aa6614da290551f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102697"
---
# <a name="create-a-linked-report"></a>リンク レポートを作成する
  リンク レポートは、既存のレポートへのアクセス ポイントとなるレポート サーバー アイテムです。 概念的には、プログラムを実行したりファイルを開くのに使用する、プログラム ショートカットに似ています。  
  
 リンク レポートは、既存のレポートから派生し、元のレポート定義を保持しています。 リンク レポートは、常に、元のレポートのレポート レイアウトおよびデータ ソース プロパティを継承します。 セキュリティ、パラメーター、場所、サブスクリプション、スケジュールなど、その他のプロパティおよび設定はすべて、元のレポートとは異なる場合があります。  
  
 既存のレポートの追加バージョンを作成するときに、リンク レポートを作成することができます。 たとえば、単一の地域の売上レポートを使用し、すべての販売区域について、地域固有のレポートを作成することができます。  
  
 リンク レポートは通常はパラメーター化されたレポートに基づいていますが、パラメーター化されたレポートは必須ではありません。 リンク レポートは、異なる設定で既存のレポートを配置する場合にも作成できます。  
  
### <a name="to-create-a-linked-report"></a>リンク レポートを作成するには  
  
1.  レポート マネージャーで、リンク先のレポートのあるフォルダーに移動し、オプション メニューを開いて、 **[リンク レポートの作成]** をクリックします。  
  
2.  新規リンク レポートの名前を入力します。 必要に応じて、説明を入力します。  
  
3.  レポートを別のフォルダーに保存するには、 **[場所の変更]** をクリックします。 保存先のフォルダーをクリックするか、または **[場所]** ボックスにフォルダー名を入力します。 [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 別のフォルダーを指定しない場合、現在のフォルダー (リンク先のレポートが保存されているフォルダー) にリンク レポートが作成されます。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)] リンク レポートが表示されます。  
  
     リンク レポートのアイコンは、レポート サーバーによって管理されるその他のアイテムのアイコンとは異なります。 次のアイコンでリンク レポートを示します。  
  
     ![リンク レポート アイコン](../media/hlp-16linked.gif "リンク レポート アイコン")  
  
## <a name="see-also"></a>関連項目  
 [レポートを開閉する (レポート マネージャー)](../reports/open-and-close-a-report-report-manager.md)   
 [新しいリンク レポート ページ (レポート マネージャー)](../new-linked-report-page-report-manager.md)   
 [アイテムの場所の選択 ページ &#40;レポート マネージャー&#41;](../choose-item-location-page-report-manager.md)   
 [全般プロパティ ページ、レポート &#40;レポート マネージャー&#41;](../general-properties-page-reports-report-manager.md)   
 [Reporting Services の概念 &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)   
 [レポート マネージャー (SSRS ネイティブ モード)](../report-manager-ssrs-native-mode.md)  
  
  
