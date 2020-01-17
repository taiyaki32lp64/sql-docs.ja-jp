---
title: SQL を埋め込む |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6a7fa2b3105aedee6cb054c5d5dfa76f3c430f35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915422"
---
# <a name="embedded-sql"></a>埋め込み SQL
DBMS に SQL ステートメントを送信するための最初の手法が埋め込まれた SQL です。 SQL は、変数とフロー制御ステートメントは使用しないので、多くの場合、C や COBOL などの従来のプログラミング言語で記述されたプログラムに追加できるデータベースのサブ言語として使用されます。 埋め込み SQL の中心になります。 ホスト プログラミング言語で記述されたプログラムで SQL ステートメントを配置することです。 簡単に、ホスト言語で SQL ステートメントを埋め込むには、次の手法が使用されます。  
  
-   組み込みの SQL ステートメントは、特別な SQL プリコンパイラを使用して処理されます。 すべての SQL ステートメントは、導入で始まる、終端記号は、SQL ステートメントに、プリコンパイル済みのフラグで終わります。 紹介子と終端記号は、ホスト言語によって異なります。 たとえば、"EXEC SQL"で C は、導入と"& SQL ("MUMPS で、終端記号は、セミコロン (;) と C および MUMPS に右かっこでします。  
  
-   ホストの変数と呼ばれる、アプリケーション プログラムからの変数は、定数が許可されている場所に、組み込みの SQL ステートメントで使用できます。 これらは、特定の状況と出力、クエリの結果を受信するには、SQL ステートメントを調整する入力で使用できます。  
  
-   1 行のデータを返すクエリは単一の SELECT ステートメントでは; で処理されます。このステートメントでは、クエリとデータを返すためのホスト変数の両方を指定します。  
  
-   複数行のデータを返すクエリは、カーソルで処理されます。 カーソルは、結果セット内の現在の行の追跡を保持します。 クエリを定義する DECLARE CURSOR ステートメント、OPEN ステートメントは、クエリ処理を開始します。、FETCH ステートメントは、データの連続する行を取得および CLOSE ステートメントは、クエリ処理を終了します。  
  
-   カーソルが開いているときに、位置指定更新と位置指定の delete ステートメントは、更新または削除、カーソルで現在選択されている行を使用できます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [埋め込み SQL の例](../../odbc/reference/embedded-sql-example.md)  
  
-   [埋め込み SQL プログラムのコンパイル](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [静的 SQL](../../odbc/reference/static-sql.md)  
  
-   [動的 SQL](../../odbc/reference/dynamic-sql.md)
