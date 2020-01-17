---
title: SQL 文法の選択 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f7bf7e77f892f10de17402b59e732523d58fbc6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036553"
---
# <a name="choosing-an-sql-grammar"></a>SQL 文法の選択
使用するには、どの文法は、SQL ステートメントを構築するときに最初に決定します。 Open Group、ANSI、および ISO など、さまざまな標準化団体から使用可能な文法だけでなくは、ほぼすべての DBMS ベンダーは、標準と若干異なりますそれぞれの独自の文法を定義します。  
  
 [付録 C: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)、すべての ODBC ドライバーのサポートが必要な SQL 文法について説明します。 この文法には、SQL 92 のエントリ レベルのサブセットです。 ドライバーは、中間、Full、または、sql-92 での FIPS 127-2 過渡期のレベルの定義に準拠するその他の文法をサポート可能性があります。 詳細については、次を参照してください[SQL 最小文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)付録 c:。SQL の文法と sql-92 します。  
  
 付録 C も定義*エスケープ シーケンス*外部結合などの一般的な言語機能の標準的な文法を格納しているをでカバーされていない SQL 92 文法。 詳細については、次を参照してください[ODBC エスケープ シーケンス](../../../odbc/reference/appendixes/odbc-escape-sequences.md)付録 c:。SQL の文法と[エスケープ シーケンス](../../../odbc/reference/develop-app/escape-sequences.md)、このセクションで後述します。  
  
 選択されている文法では、ドライバーが、ステートメントを処理する方法に影響します。 ドライバーは、SQL 92 SQL と DBMS に固有の sql の ODBC で定義されたエスケープ シーケンスを変更する必要があります。 SQL 文法のほとんどは、1 つまたは複数のさまざまな標準に基づいているために、ほとんどのドライバーは、この要件を満たすためにほとんどまたはまったくの操作を行います。 多くの場合、定義されているエスケープ シーケンスの検索ののみで構成されます ODBC と DBMS に固有の文法に置き換えることができます。 ドライバーには、文法が認識しないが検出されると、文法は DBMS 固有であり実行のデータ ソースを変更しなくても、SQL ステートメントを渡すと仮定します。  
  
 したがってが本当に使用する文法の 2 つの選択肢: SQL 92 文法 (および ODBC のエスケープ シーケンス) と DBMS に固有の文法。 相互運用可能なすべてのアプリケーションで使用する必要があります、2 つの相互運用性は、SQL 92 文法のみ。 相互運用可能なれていないアプリケーションには、SQL 92 文法または DBMS 固有の文法を使用できます。 DBMS に固有の文法では、2 つの利点があります。Sql-92 に含まれないすべての機能を利用することができ、若干速く、ドライバーがそれらを変更する必要はありませんので。 後者の機能は、ドライバーの検索と置換のエスケープ シーケンスを停止する、SQL_ATTR_NOSCAN ステートメント属性を設定して、部分的に適用できます。  
  
 どのように呼び出すことによって、ドライバーによって変更されて、アプリケーションを検出できます SQL 92 文法を使用する場合**SQLNativeSql**します。 これは、アプリケーションのデバッグ時に多くの場合に便利です。 **SQLNativeSql** SQL ステートメントを受け取り、ドライバーが変更された後、それを返します。 この関数は、コア インターフェイスの適合性レベルにあるため、すべてのドライバーでサポートされています。
