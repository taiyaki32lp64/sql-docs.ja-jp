---
title: ワイルドカードを使用したテキスト検索
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vswildcardsbuilder
helpviewer_keywords:
- searches [SQL Server Management Studio], wildcards
- Query Editor [SQL Server Management Studio], wildcard searches
- wildcard options [SQL Server Management Studio]
ms.assetid: 449600f8-cc87-4b3f-878a-59c158a88a40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caeda52d612f4df6672f686e06834de6fef0cc67
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243275"
---
# <a name="search-text-with-wildcards"></a>ワイルドカードを使用したテキスト検索
  次の式では、[ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **検索と置換**] ダイアログボックスの [**検索**する文字列] フィールドの文字または数字を置き換えることができます。  
  
#### <a name="to-search-using-wildcards"></a>ワイルドカードを使用して検索を行うには  
  
1.  [クイック検索]、 **[フォルダーを指定して検索]** 、 **[クイック置換]**、 **[フォルダーを指定して置換]** の各操作に関して、 **[検索する文字列]** フィールドでのワイルドカードの使用を有効にするには、 **[検索オプション]** の下の **[条件]** をオンにして、 **[ワイルドカード]** をオンにします。  
  
2.  
  **[検索する文字列]** フィールドの横にある三角形の **参照一覧** ボタンが使用可能になります。 このボタンをクリックすると、使用可能なワイルドカードの一覧が表示されます。 
  **参照一覧**から項目を選択すると、その項目が **[検索する文字列]** の文字列に挿入されます。  
  
 
  **参照一覧**から使用できるワイルドカードを以下にまとめます。  
  
|［式］|構文|説明|  
|----------------|------------|-----------------|  
|任意の 1 文字|?|任意の 1 文字に相当します。|  
|任意の 1 つの数字|#|任意の 1 つの数字に相当します。 一例として、7# は 7 とその後の 1 つの数字に相当します (たとえば、71 は一致項目ですが、17 は違います)。|  
|セット内以外の文字|[! ]|セット内に指定されていない任意の 1 文字に相当します。|  
|1 つ以上の文字|*|任意の 1 つ以上の文字に相当します。 一例として、new* は「new」を含む任意のテキスト (newfile.txt など) に相当します。|  
|文字のセット|[ ]|セット内に指定されている任意の 1 文字に相当します。|  
  
## <a name="see-also"></a>参照  
 [検索と置換](search-and-replace.md)   
 [正規表現によるテキストの検索](search-text-with-regular-expressions.md)  
