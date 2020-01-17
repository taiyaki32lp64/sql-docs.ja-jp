---
title: リンク レポートを作成する | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6dad85f35be1d7fb26f4c9eef6241e01baadb692
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492805"
---
# <a name="create-a-linked-report"></a>リンク レポートを作成する
  リンク レポートは、既存のレポートへのアクセス ポイントとなるレポート サーバー アイテムです。 概念的には、プログラムを実行したりファイルを開くのに使用する、プログラム ショートカットに似ています。  
  
 リンク レポートは、既存のレポートから派生し、元のレポート定義を保持しています。 リンク レポートは、常に、元のレポートのレポート レイアウトおよびデータ ソース プロパティを継承します。 セキュリティ、パラメーター、場所、サブスクリプション、スケジュールなど、その他のプロパティおよび設定はすべて、元のレポートとは異なる場合があります。  
  
 既存のレポートの追加バージョンを作成するときに、リンク レポートを作成することができます。 たとえば、単一の地域の売上レポートを使用し、すべての販売区域について、地域固有のレポートを作成することができます。  
  
 リンク レポートは通常はパラメーター化されたレポートに基づいていますが、パラメーター化されたレポートは必須ではありません。 リンク レポートは、異なる設定で既存のレポートを配置する場合にも作成できます。  
  
## <a name="to-create-a-linked-report"></a>リンク レポートを作成するには  
  
1. Web ポータルで、目的のレポートに移動します。 で、右クリックし、選択**管理**、ドロップ ダウン メニューから。

2. **管理<reportname>**  ] ページで、[**リンク レポートの作成**です。  
  
3. 新しいリンク レポートの名前を入力します。 必要に応じて説明を入力します。  
  
4. レポートの別のフォルダーを選択するには、右側にある省略記号ボタン (…) を選択します。***場所***します。  新しいフォルダーを選択してレポートに移動**選択**します。 別のフォルダーを選択しない場合は、リンク レポートが現在のフォルダーに作成されます。  
  
5. **[作成]** を選択します。 リンク レポートが作成されます。  

6. **詳細設定**、選択、さまざまな**レポートのタイムアウト**以外の場合、必要に応じて、値し、選択**適用**変更を保存します。
  
     リンク レポートのアイコンは、レポート サーバーによって管理されるその他のアイテムのアイコンとは異なります。 次のアイコンでリンク レポートを示します。  
  
     ![リンク レポート アイコン](../../reporting-services/report-server/media/hlp-16linked.gif "リンク レポート アイコン")  
  
## <a name="see-also"></a>参照  

 [Reporting Services の概念 &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)  
 [レポート サーバーの Web ポータル (SSRS ネイティブ モード)](../../reporting-services/web-portal-ssrs-native-mode.md)
  
