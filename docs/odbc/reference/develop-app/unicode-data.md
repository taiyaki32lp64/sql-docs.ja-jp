---
title: Unicode データ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 899924b5c0847d5f42e383a9e04c33298bb368b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087756"
---
# <a name="unicode-data"></a>Unicode データ
SQL の Unicode データ型は、Unicode、DBMS にネイティブで存在するデータを記述する提供されます。 C の Unicode データ型は、Unicode バッファーにデータをバインドする、アプリケーションに提供されます。 ドライバー マネージャーは、Unicode C 型にするには、(SQL_C_WCHAR) からデータを変換できる関数は ANSI ドライバーを使用します。  
  
 ODBC 3.0 または 2 です。*x*アプリケーションは常に ANSI データ型にバインドします。 最適なパフォーマンスを得るには、ODBC 3.5 (またはそれ以降) アプリケーションは ANSI C のデータ型にバインドする必要がある場合 SQL 列の型は ANSI、および SQL 列の型が Unicode の場合、Unicode の C データ型にバインドする必要があります。  
  
 SQL Unicode 型を表すインジケーターは、SQL_WCHAR、SQL_WVARCHAR、SQL_WLONGVARCHAR です。 SQL_WCHAR データの固定文字列の長さ、SQL_WVARCHAR が宣言されている最大の可変長と SQL_WLONGVARCHAR がデータ ソースに依存している最大の可変長です。  
  
 C Unicode 型インジケーターは、SQL_C_WCHAR です。 これは、それぞれの SQL Unicode 型のインジケーターの既定値です。 すべての SQL 型は、SQL_C_WCHAR に変換できる SQL_C_WCHAR は、すべての SQL 型に変換することができます。 アプリケーションでは、3 つの方法のいずれかにデータを取得できます。  
  
-   SQL_C_CHAR としてデータを取得します。  
  
-   SQL_C_WCHAR としてデータを取得します。  
  
-   SQL_C_TCHAR としてデータを宣言します。 これは、アプリケーションが Unicode アプリケーションとしてコンパイルされるまたは ANSI アプリケーションとしてコンパイルされている場合は、SQL_C_CHAR を挿入する場合は、SQL_C_WCHAR を挿入するマクロです。  
  
 SQL_C_TCHAR に関数で、次のように宣言されます。  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Unicode アプリケーションとして、アプリケーションがコンパイルされるときに、 *ValueType* SQL_C_WCHAR に SQL_C_TCHAR から引数に変更します。 ANSI アプリケーションとして、アプリケーションがコンパイルされるときに、 *ValueType* SQL_C_CHAR に引数が変更されます。  
  
 Unicode ドライバーでは、SQL_CHAR をなど、ANSI データ型はサポートもする必要があります。 Unicode ドライバーで動作するアプリケーションは、SQL_CHAR にバインドした場合、ドライバー マネージャーは SQL_WCHAR を SQL_CHAR データをマップしません。 Unicode ドライバーには、SQL_CHAR データがそのまま使用する必要があります。  
  
 ドライバー マネージャーは、ドライバーと DSN 名を Unicode で格納し、必要に応じて ANSI にマッピングします。 文字を変換できませんでしたが、既定の文字の sup で表される場合は、Unicode 文字は、(ドライバーと DSN 名、コンピューターのネイティブ コード ページではないコード ページから文字を使用する場合に発生することができます)、ANSI 文字にマップすることはできません、システムによって plied します。
