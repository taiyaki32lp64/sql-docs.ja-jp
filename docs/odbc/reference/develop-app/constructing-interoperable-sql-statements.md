---
title: 相互運用可能な SQL ステートメントの構築 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87ad7b8b36c80d86e0c3ac0335dd6f348a30c7bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002241"
---
# <a name="constructing-interoperable-sql-statements"></a>相互運用可能な SQL ステートメントの構築
前のセクションで説明したように、相互運用可能なアプリケーションは、ODBC SQL 文法を使用しないでください。 ただし、この文法を使用して、外はさまざまな他の問題が相互運用可能なアプリケーションが直面しています。 たとえばと、アプリケーションはすべてのデータ ソースでサポートされていない機能、外部結合などを使用する必要がある場合  
  
 この時点では、いくつかの判断が必要な言語機能とオプションについてのことに、アプリケーションの作成者を使用する必要があります。 ほとんどの場合、特定のドライバーは、アプリケーションで必要な機能をサポートしていない場合、アプリケーションだけを拒否ドライバーを使用して実行します。 ただし、機能が省略可能な場合は、アプリケーションが、機能を回避することができます。 たとえば、により、機能を使用して、ユーザー インターフェイス部分を無効にする可能性がありますに。  
  
 サポートされている機能を確認するのにアプリケーションを呼び出すことによって開始**SQLGetInfo** SQL_SQL_CONFORMANCE オプションを使用します。 SQL への準拠レベルは、SQL はサポートされているさまざまなビューをアプリケーションに提供します。 このビューでは、アプリケーション呼び出しを絞り込む**SQLGetInfo**で多数の他のオプションのいずれか。 これらのオプションの完全な一覧を参照してください、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)関数の説明。 最後に、 **SQLGetTypeInfo**データ ソースでサポートされるデータ型に関する情報を返します。 次のセクションでは、さまざまなアプリケーションは、相互運用可能な SQL ステートメントを構築するときの注意しなければならない可能性の要因を一覧表示します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [カタログとスキーマの使用状況](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [カタログの位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [引用符で囲まれた識別子](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [識別子の大文字と小文字の区別](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [エスケープ シーケンス](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [リテラル プレフィックスおよびサフィックス](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [プロシージャ呼び出しのパラメーター マーカー](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL ステートメント](../../../odbc/reference/develop-app/ddl-statements.md)
