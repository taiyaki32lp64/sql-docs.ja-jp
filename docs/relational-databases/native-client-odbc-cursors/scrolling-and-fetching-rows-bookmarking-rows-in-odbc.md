---
title: ODBC での行のブックマーク |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc90fd2a24e8850922e45d17fb331ce412dde482
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784087"
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>行のスクロールとフェッチ - ODBC での行のブックマーク
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ブックマークは、データ行の識別に使われる値です。 ブックマーク値の意味を解釈できるのは、ドライバーまたはデータ ソースのみです。 たとえば、ブックマークは、行番号のような単純な値の場合も、ディスク アドレスのような複雑な値の場合もあります。 ODBC では、アプリケーションが特定の行のブックマークを要求し、これを保存し、カーソルに戻して行に返します。  
  
 [Sqlfetchscroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)を使用して行をフェッチする場合、アプリケーションでは開始行を選択するための基礎としてブックマークを使用できます。 これは、現在のカーソルの位置に依存しないので、絶対アドレスの形式になります。 ブックマークが付けられた行までスクロールするには、アプリケーションは SQL_FETCH_BOOKMARK の*Fetchorientation*を使用して**sqlfetchscroll**を呼び出します。 この操作では、SQL_ATTR_FETCH_BOOKMARK_PTR オプション属性によって示されるブックマークを使用します。 結果として、そのブックマークによって識別される行で始まる行セットが返されます。 アプリケーションでは、 **Sqlfetchscroll**の呼び出しの*fetchoffset*引数でこの操作のオフセットを指定できます。 オフセットを指定すると、結果の行セットの最初の行は、ブックマークで識別される行番号に FetchOffset 引数の数を加算した結果によって決まります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、静的カーソルとキーセット カーソルに対してのみブックマークがサポートされます。 ブックマークが設定されている場合に動的カーソルが要求されると、代わりにキーセット カーソルが開かれます。  
  
 ブックマークを**Sqlbulkoperations**関数と共に使用して、ブックマークで始まる一連の行に対して操作を実行することもできます。  
  
## <a name="see-also"></a>参照  
 [行のスクロールとフェッチ](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  
