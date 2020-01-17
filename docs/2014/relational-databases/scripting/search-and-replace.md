---
title: 検索と置換
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- match case [SQL Server]
- undo operations
- searches [SQL Server Management Studio]
- replacing text
- quick search and replaces [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], undo
- Query Editor [SQL Server Management Studio], searching
- regular expressions [SQL Server Management Studio]
- finding text [SQL Server Management Studio]
- text [SQL Server], search and replace operations
- finding [SQL Server Management Studio]
- locating text
- Query Editor [SQL Server Management Studio], replacing text
- Find and Replace dialog box
- wildcard options [SQL Server Management Studio]
- match whole word [SQL Server]
- searches [SQL Server Management Studio], replacing
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 631b6864529e903516857f68ea421365c144afef
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243299"
---
# <a name="search-and-replace"></a>検索と置換
  テキストの検索と置換にはいくつかの方法があります。 
  **[編集]** メニューの **[検索と置換]** には、 **[クイック検索]**、 **[クイック置換]**、 **[フォルダーを指定して検索]**、 **[フォルダーを指定して置換]** という 4 つのオプションが用意されています。 各オプションを選択すると、各バージョンの **[検索と置換]** ダイアログ ボックスが表示されます。 ダイアログ ボックスを使用しないで、インクリメンタル検索キーボード ショートカット キーによって検索することも可能です。 これらの方法によって、検索と置換の範囲を設定することや、検索一致項目や置換項目を確認する方法を選択することができます。  
  
 テキストの検索と置換に関する注意点は次のとおりです。  
  
-   
  **[検索と置換]** ダイアログ ボックスで設定したオプションは、すべての検索操作に影響します。 具体的には、 **[大文字と小文字を区別する]**、 **[単語単位]**、 **[上へ検索]**、 **[非表示のテキストを検索]**、 **[ワイルドカード]**、 **[正規表現]**、 **[検索対象: すべての開かれているドキュメント]**、 **[検索対象: 現在のプロジェクト]** の各オプションです。 すべてのバージョンの **[検索と置換]** ダイアログ ボックスですべてのオプションを使用できるわけではありません。  
  
-   [**元に戻す**] は、置換操作の後に開いたドキュメントに対してのみ使用できます。  
  
-   複数のファイルにまたがる**すべての置換**操作を**元に戻す**操作は、影響を受けるすべてのファイルに対して1つの一括操作と見なされます。 つまり、一部のファイルの変更を元に戻し、他のファイルの変更をそのまま残す、ということはできません。  
  
 一般に、グラフィカル ビューを持つ項目の検索はできません。  
  
## <a name="see-also"></a>参照  
 [アクティブドキュメントのインクリメンタル検索](search-an-active-document-incrementally.md)   
 [ドキュメントを対話形式で検索する](search-documents-interactively.md)   
 [結果一覧を使用してドキュメントを検索する](search-documents-using-results-lists.md)   
 [ワイルドカードを使用してテキストを検索する](search-text-with-wildcards.md)   
 [正規表現によるテキストの検索](search-text-with-regular-expressions.md)  
  
  
