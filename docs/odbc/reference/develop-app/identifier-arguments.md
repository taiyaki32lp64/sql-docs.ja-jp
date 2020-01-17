---
title: 引数の識別子 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93cf744cf105762fb90a92049d6698e67a19d58c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138997"
---
# <a name="identifier-arguments"></a>識別子の引数
識別子の引数の文字列を引用符で囲まれた、ドライバーは先頭と末尾の空白を削除し、文字どおり引用符で囲まれた文字列が扱われます。 文字列が引用符で囲まれていない場合、ドライバーを削除末尾の空白およびフォールド文字列を大文字にします。 SQL_ERROR と SQLSTATE HY009 返します識別子の引数を null ポインターを設定 (null ポインターの無効な使用)、しない限り、引数がカタログ名とカタログがサポートされていません。  
  
 これらの引数は、SQL_ATTR_METADATA_ID ステートメントの属性が SQL_TRUE に設定されている場合、識別子の引数として扱われます。 この場合は、アンダー スコア (_)、パーセント記号 (%)検索パターンの文字としてではなく、実際の文字として扱うは。 これらの引数は、この属性は SQL_FALSE に設定されている場合、通常の引数または引数に応じての pattern 引数のいずれかとして扱われます。  
  
 特殊文字を含む識別子は、SQL ステートメントで引用符で囲む必要があります、ですが、する必要がありますいないは引用符で囲むカタログ関数の引数として渡されるときにカタログ関数に渡される引用符文字を解釈するため。 たとえば、識別子を引用符文字とします (特定のドライバーとを通じて返されることが**SQLGetInfo**) が二重引用符 (")。 最初の呼び出し**SQLTables**が 2 番目の呼び出しが意図した動作しない可能性がありますが、"Accounts Payable"テーブルに関する情報を返すときは、Accounts Payable のテーブルに関する情報を含む結果セットを返します。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 引用符で囲まれた識別子は、Oracle では、ROWID など、同じ名前の擬似列の場合は true。 列名を区別するために使用されます。 "ROWID"カタログ関数の引数を渡された場合関数は、ROWID の擬似列が存在する場合。 擬似列が存在しない場合、関数は"ROWID"列で機能します。 ROWID カタログ関数の引数を渡された場合、関数は ROWID 列で機能します。  
  
 引用符で囲まれた識別子の詳細については、次を参照してください。[引用符で囲まれた識別子](../../../odbc/reference/develop-app/quoted-identifiers.md)します。
