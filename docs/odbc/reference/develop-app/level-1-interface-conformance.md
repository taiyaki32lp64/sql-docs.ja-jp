---
title: レベル 1 インターフェイスの適合性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05cf381ccbb8c0747db88259acfb4ba218d3e0ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135011"
---
# <a name="level-1-interface-conformance"></a>レベル 1 インターフェイスの適合性
レベル 1 インターフェイスの適合性レベルには、コア インターフェイスへの準拠レベルの機能に加えて、OLTP のリレーショナル DBMS で通常利用できるトランザクションなどの追加機能が含まれています。 レベル 1 インターフェイスに準拠のドライバーにより、アプリケーションは、コア インターフェイスの適合性レベルで機能に加え、次の操作します。  
  
|||  
|-|-|  
|101|データベースのスキーマのテーブルし、ビュー (2 つの部分が名前付けを使用) を指定します。 (詳細については、3 つの部分の命名で 201 の機能を参照してください[レベル 2 インターフェイスの適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md))。|  
|102|ODBC 関数、ODBC 関数を適用できますが、すべて同期または特定の接続で非同期の場合は true。 の非同期実行を呼び出します。|  
|103|スクロール可能なカーソルを使用し、それによってによって結果セットのメソッドで順方向専用、以外の呼び出しへのアクセスを実現**SQLFetchScroll**で、 *FetchOrientation* SQL_FETCH_NEXT 以外の引数。 (、SQL_FETCH_BOOKMARK *FetchOrientation*で feature 204[レベル 2 インターフェイスの適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md))。|  
|104|呼び出すことによって、テーブルの主キーを取得**SQLPrimaryKeys**します。|  
|105|プロシージャ呼び出しについて、ODBC エスケープ シーケンスの実行中のストアド プロシージャを使用して、ストアド プロシージャに関するデータのディクショナリを呼び出すことによってクエリ**SQLProcedureColumns**と**SQLProcedures**します。 (プロシージャの作成し、データ ソースに格納されているプロセスは、このドキュメントの範囲外です)。|  
|106|対話形式で呼び出すことによって、使用可能なサーバーを参照してデータ ソースに接続する**SQLBrowseConnect**します。|  
|107|特定のデータベース操作を実行するのに SQL ステートメントの代わりに ODBC 関数を使用します。**SQLSetPos** SQL_POSITION SQL_REFRESH とします。|  
|108|呼び出すことによって、バッチおよびストアド プロシージャは、によって生成される複数の結果セットの内容にアクセスできる**SQLMoreResults**します。|  
|109|True の原子性と SQL_ROLLBACK を指定する機能でいくつかの ODBC 関数にまたがるトランザクションを区切る**SQLEndTran**します。|
