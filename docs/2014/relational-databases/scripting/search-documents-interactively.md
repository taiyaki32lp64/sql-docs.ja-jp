---
title: ドキュメントの対話形式の検索
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- interactive searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], interactive
- Query Editor [SQL Server Management Studio], interactive search
ms.assetid: dae65ac5-67af-45c6-a6e0-952fea26d680
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac2a15bae8fde50315ab6c7c41f2e3e57973061f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243288"
---
# <a name="search-documents-interactively"></a>ドキュメントの対話形式の検索
  [**検索と置換**] ダイアログボックスを使用すると、1つ以上の開いているファイルまたはウィンドウを検索し、検索結果を1つずつ検索できます。 この方法では、検索結果の各文字列をその前後のテキストのコンテキストで個別に確認できます。 さらに、 **[検索と置換]** ダイアログ ボックスには、一括検索操作を実行し、結果をレポート形式で確認するオプションも用意されています。  
  
### <a name="to-search-all-open-documents"></a>開いているドキュメントをすべて検索するには  
  
1.  検索する項目を開きます。  
  
2.  
  **[編集]** メニューの **[検索と置換]** をポイントし、 **[クイック検索]** をクリックします。  
  
3.  
  **[検索と置換]** ボックスに、検索するテキストを入力します。  
  
4.  
  **[検索対象]** ボックスの一覧の **[すべての開かれているドキュメント]** をクリックします。  
  
    > [!NOTE]  
    >  
  **[すべての開かれているドキュメント]** を選択しても、開いている特定のファイルは検索されないことがあります。 検索の対象になるのは、コード ビューなどのテキスト ビューで現在開いているファイルだけです。 デザイナー ビューのファイルは、検索対象に含まれません。  
  
5.  さらに検索精度を高めるには、検索オプションを選択します。  
  
6.  
  **[次を検索]** をクリックして検索を開始します。最後のファイルの検索が完了するまで **[次を検索]** のクリックを続けます。  
  
 検索がドキュメントの先頭または末尾に達すると、ステータス バーにメッセージが表示されます。 検索の開始位置に達すると、メッセージ ボックスが表示されます。  
  
#### <a name="to-replace-in-all-active-files-interactively"></a>すべてのアクティブ ファイル内で対話的に置換を行うには  
  
1.  
  **[編集]** メニューの **[検索と置換]** をポイントし、 **[クイック置換]** をクリックします。  
  
2.  
  **[検索する文字列]** ボックスに、検索するテキストを入力します。  
  
3.  
  **[置換後の文字列]** ボックスに置換後のテキストを入力します。  
  
4.  
  **[検索対象]** ボックスの一覧の **[すべての開かれているドキュメント]** をクリックします。  
  
5.  
  **[置換]** をクリックし、最後のファイル内で最後に見つかった検索結果の置換が完了するまで **[置換]** のクリックを続けます。 検索結果を置換しないでスキップする場合は、 **[次を検索]** をクリックします。  
  
     または  
  
     
  **[すべて置換]** をクリックしてすべての検索結果を置換します。 置換の総数を示すメッセージ ボックスが表示されます。  
  
 
  **[すべて置換]** をクリックすると、 **[次を検索]** によってスキップした検索結果も含め、すべての検索結果が置換されます。 
  **[すべて置換]** を取り消すには、ファイルを閉じる前に **[編集]** メニューの **[元に戻す]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [アクティブドキュメントのインクリメンタル検索](search-an-active-document-incrementally.md)   
 [検索と置換](search-and-replace.md)   
 [結果一覧を使用してドキュメントを検索する](search-documents-using-results-lists.md)   
 [ワイルドカードを使用してテキストを検索する](search-text-with-wildcards.md)   
 [正規表現によるテキストの検索](search-text-with-regular-expressions.md)  
  
  
