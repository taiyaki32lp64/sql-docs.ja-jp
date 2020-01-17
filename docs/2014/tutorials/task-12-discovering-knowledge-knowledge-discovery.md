---
title: タスク 12:(ナレッジ検出) のナレッジを検出する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6dd54475ee63b2f6ef5e1b56b94c11aafd5996ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484683"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>タスク 12:ナレッジを検出する (ナレッジ検出)
  このタスクで実行して、**ナレッジ検出**でアクティビティ**Supplier ID**と**Supplier Name**ドメイン。 このシナリオでは、ナレッジ検出プロセスにより主にこれら 2 つのドメインの値をインポートします。  
  
 このチュートリアルでは、ナレッジ ベースを最初から作成しました。 さらに、ナレッジ検出アクティビティを実行してナレッジ ベースを作成することができます。 クリックすると**ナレッジ ベースを作成**をページにする DQS クライアントは、のメイン ページで、**ドメイン管理**活動の選択したアクティビティ。 変更することができます、**アクティビティ**に**ナレッジ検出**とし、次のページでドメインを作成できます、ナレッジ検出プロセスの一部として。 参照してください[Perform Knowledge Discovery](https://msdn.microsoft.com/library/hh510398.aspx)の詳細。  
  
1.  DQS クライアントのメイン ページでの**最近使用したナレッジ ベース**セクションで、**右矢印**横に、 **Suppliers**ナレッジ ベースをクリックします**ナレッジ探索**します。 また、クリックすることができます**ナレッジ ベースを開く**を選択します**Suppliers**から、**ナレッジ ベースの一覧**、**ナレッジ検出**として**アクティビティ**クリック**次**します。  
  
     ![ナレッジ検出 メニューのメイン ページ](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "ナレッジ検出 メニューのメイン ページ")  
  
2.  選択**Excel ファイル**の**データソース**します。  
  
3.  をクリックして**参照**移動して、選択**Suppliers.xls**、 をクリック**オープン**します。  
  
4.  選択**Suppliers for Discovery**の**ワークシート**します。  
  
5.  **マッピング**セクションで、マップ**SupplierID**列から、 **Excel**ファイルを**Supplier ID**ドメインと**Supplier Name**列を**Supplier Name**を使用してドメイン**ドロップ ダウン リスト**します。 Excel ファイルがサンプル データを**Supplier ID**と**Supplier Name**ドメイン。 検出プロセスでは、値を検出するドメインを選択できます。 このページでドメインを作成し、これらのドメインにソース列をマップできます。 ドメイン管理アクティビティ中にドメインを作成する代わりに、ナレッジ検出アクティビティ中にドメインを作成することは一般的でありません。  
  
     ![検出プロセスのページ マップ](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "検出プロセスのページのマップ")  
  
6.  をクリックして**次**に切り替える、 **Discover**ページ。  
  
7.  **Discover** ] ページで [**開始**検出プロセスを開始します。 探索が実行される、列で**SupplierID**と**Supplier Name**で、 **Suppliers.xls**ファイル。 **Supplier ID**と**Supplier Name**検出から取得されたナレッジ ドメインを設定する必要があります。  
  
     ![検出プロセスのページを検出](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "検出プロセスのページを検出")  
  
8.  分析が完了すると、確認、**のソース統計情報**で、 **Profiler タブ**ページの下部にあります。 10 個の新しいレコードが 20 個の値を合計ことに注意してください (**SupplierID**と**Supplier Name**値から、 **Excel ワークシート**) 検出されました。 さらに、これらの値のうちいくつが、新しい値、一意の値、新しい一意の値、および有効な値であるかがわかります。 右側のリスト ボックスには、検出プロセスに使用された各ドメインの詳細が表示されます。 [完全] 列のステータス バーにマウス ポインターを合わせると、ソースの列に不足値があるかどうかを表示できます。  
  
     ![ナレッジ検出結果](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "ナレッジ検出の結果")  
  
9. クリックして**次**に切り替える、**ドメイン値の管理**ページ。  
  
10. **ドメイン値の管理**] ページで [ **Supplier Name**ドメインの一覧からドメイン。  
  
11. 右側のウィンドウで右クリック**Lazy Country Storex** (最後には通知 'x') を選択および**Lazy Country Store**します。 DQS により、ドメインに対するスペル チェッカーの実行後、この変更内容が提案されます。 既定では、作成するドメインに対するスペル チェックが有効になっています。  
  
     ![仕入先名 - Lazy Country Store の修正](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "仕入先名 - Lazy Country Store を修正")  
  
12. ドメイン値の一覧のことを確認します値**Lazy Country Storex**エラーとして設定されます (赤い**X**マーク) を**Lazy Country Store**修正しても、として**Lazy Country Store**有効な値としても追加されます。  
  
     ![ドメイン値し、次の値に修正](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "ドメイン値し、次の値に修正")  
  
13. **[完了]** をクリックします。  
  
14. **SQL Server Data Quality Services**ダイアログ ボックスで、をクリックして**発行**します。  
  
15. をクリックして**OK** [成功] メッセージ ボックス。  
  
     これで、チュートリアルの最初のレッスンを完了しました。  
  
## <a name="next-step"></a>次の手順  
 [レッスン 2:Suppliers ナレッジ ベースを使用して仕入先データのクレンジング](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
