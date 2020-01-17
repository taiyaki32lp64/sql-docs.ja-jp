---
title: パターン値の引数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 53c091fd0b7a6cfdf390997fb5163fbc9d98e18c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023341"
---
# <a name="pattern-value-arguments"></a>パターン値の引数
などのいくつかの引数で、カタログ関数、 *TableName*引数**SQLTables**、検索パターンをそのまま使用します。 これらの引数は、検索パターンをそのまま使用する sql_false になります SQL_ATTR_METADATA_ID ステートメントの属性が設定されている場合。この属性が SQL_TRUE に設定されている場合、検索パターンを受け入れない識別子引数です。  
  
 検索パターンの文字は次のとおりです。  
  
-   任意の 1 文字を表すスコア (_)。  
  
-   0 個以上の文字の任意のシーケンスを表すパーセント記号 (%)。  
  
-   ドライバー固有 % が、アンダー スコアを含めるために使用され、エスケープ文字とリテラルとエスケープ文字。 非特殊文字、エスケープ文字の前に場合、は、エスケープ文字に特別な意味がありません。 エスケープ文字に特殊文字が前にある場合は、特殊文字をエスケープします。 たとえば、"\a"、2 つの文字として取り扱われます"\\"および"a"が"\\%"特殊な非単一の文字「%」として取り扱われます。  
  
 エスケープ文字が SQL_SEARCH_PATTERN_ESCAPE オプションで取得した**SQLGetInfo**します。 任意のアンダー スコア、パーセント記号、またはエスケープ文字の前に引数を受け取るリテラルと文字を含む検索パターンにする必要があります。 次の表に例を示します。  
  
|検索パターン|説明|  
|--------------------|-----------------|  
|%、%|文字 A を含むすべての識別子|  
|ABC _|ABC で始まる 4 文字のすべての識別子|  
|ABC\\_|識別子のエスケープ文字と仮定した場合、abc _ は、円記号 (\\)|  
|\\\\%|円記号で始まるすべての識別子 (\\)、エスケープ文字が円記号|  
  
 検索パターンをそのまま使用する引数の検索パターンの文字をエスケープする特別な注意を実行する必要があります。 これは、アンダー スコア文字を識別子での一般的な使用に特に当てはまります。 アプリケーションでよくある間違いは、1 つのカタログ関数の値を取得し、別のカタログ関数の検索パターンの引数にその値を渡すには。 たとえば、アプリケーションの結果から MY_TABLE の設定、テーブル名を取得する**SQLTables**し、これを渡します**SQLColumns** MY_TABLE 内の列の一覧を取得します。 MY_TABLE の列を取得する代わりに、アプリケーションは MY_TABLE、MY1TABLE、MY2TABLE などの MY_TABLE 検索パターンに一致するすべてのテーブルの列を取得します。  
  
> [!NOTE]
>  ODBC 2。*x*ドライバー内の検索パターンをサポートしていません、 *CatalogName*引数**SQLTables**します。 ODBC 3 *.x* SQL_ATTR ODBC_VERSION 環境属性を SQL_OV_ODBC3 に設定されている場合、ドライバーが検索パターンでは、この引数を受け入れる; SQL_OV_ODBC2 に設定されている場合、この引数内の検索パターンは同意しません。  
  
 検索パターンの引数に null ポインターを渡すことはその引数の検索を制限しませんつまり、null ポインターと検索パターン % (任意の文字) では同等です。 長さ 0 の検索パターンの長さがゼロの文字列に有効なポインター - ただし、空の文字列のみと一致する場合 ("")。
