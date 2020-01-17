---
title: フルテキスト カタログのプロパティ (テーブルとビュー ページ) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.tablesviews.f1
ms.assetid: 2d45fcd2-0f0f-4167-9027-316d6696c106
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 78d7dc111bc0b6eb10e80f32785beeda710e52bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779193"
---
# <a name="full-text-catalog-properties-tables-and-views-page"></a>[フルテキスト カタログのプロパティ] ([テーブルとビュー] ページ)
  このダイアログ ページを使用すると、フルテキスト カタログに割り当てられたテーブルおよびビューを表示したり、変更したりできます。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **このデータベース内のすべての対象となるテーブル/ビュー オブジェクト**  
 一意のインデックスが定義されていて、まだフルテキスト カタログに割り当てられていないテーブルおよびビューを一覧表示します。 テーブルまたはビューを選択して、カタログに割り当てる、リスト ボックス項目を選択および"-> ボタンを押します。  
  
 **カタログに割り当てられたテーブル/ビュー オブジェクト**  
 現在フル テキスト カタログに割り当てられているテーブルおよびビューを一覧表示します。  
  
## <a name="selected-object-properties"></a>[選択したオブジェクトのプロパティ]  
 **選択したオブジェクトのプロパティ**  
 カタログに割り当てられたオブジェクトのリスト ボックスで選択したオブジェクトのプロパティを表示します。  
  
 **一意のインデックス**  
 テーブルまたはビューの利用可能な一意インデックスを一覧表示します。  
  
 **テーブルは、フルテキストが有効になっています。**  
 テーブルのフルテキスト インデックスを有効にする場合は、このチェック ボックスをオンにします。 フルテキスト インデックスを無効にする場合は、チェック ボックスをオフにします。  
  
## <a name="eligible-columns-grid"></a>[対象になる列] グリッド  
  
|||  
|-|-|  
|**使用可能な列**|フルテキスト インデックス付きの列をすべて表示します。 フルテキスト インデックスに列を追加する場合は、このチェック ボックスをオンにします。|  
|**ワード ブレーカーの言語**|ワード ブレーカーの言語を表示します。|  
|**データ型の列**|列のドキュメントの種類を保持するテーブル内の列の名前を一覧表示**使用可能な列**、列がある場合、`varbinary(max)`または`image`列。|  
|**[統計的セマンティクス]**|選択されている列に対するセマンティック インデックスを有効にするかどうかを選択します。 詳細については、「[セマンティック検索 &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md)」を参照してください。<br /><br /> **[統計的セマンティクス]** を選択する前に **[言語]** を選択した場合、選択した言語にセマンティック言語モデルが関連付けられていなければ、 **[統計的セマンティクス]** チェック ボックスは無効になります。 **[言語]** を選択する前に **[統計的セマンティクス]** を選択した場合、ドロップダウン コンボ ボックスで使用できる言語は、セマンティック言語モデルでサポートされているものだけに制限されます。|  
  
## <a name="track-changes"></a>[変更の追跡]  
  
|||  
|-|-|  
|**自動**|基になるテーブル内のデータが変更、追加、または削除されると、フルテキスト インデックスは自動的に更新されます。|  
|**手動**|インデックス付きデータのデータが変更、追加、または削除されると、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は変更を追跡します。 **[手動]** による変更の追跡が選択されている場合、インデックスはこれらの変更によって自動的に更新されません。 代わりに、管理者は変更を手動で適用を使用して、 [ALTER FULLTEXT INDEX.START UPDATE POPULATION](/sql/t-sql/statements/alter-fulltext-index-transact-sql)ステートメント。|  
|**変更を追跡しません。**|このオプションが有効になっていると、カタログ内のインデックス付きデータへの変更は記録されません。 管理者は、FULL POPULATION または INCREMENTAL POPULATION のいずれかで ALTER FULLTEXT INDEX を使用してインデックスを構築する必要があります。|  
  
## <a name="see-also"></a>参照  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)   
 [フルテキスト インデックスの作成](../relational-databases/indexes/indexes.md)  
  
  
