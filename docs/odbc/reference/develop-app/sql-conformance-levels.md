---
title: SQL の適合性レベル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7862b2e3a86c6d98a51c73ecb470d59bcfe29dc9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107523"
---
# <a name="sql-conformance-levels"></a>SQL の適合性レベル
ドライバーによってサポートされている SQL 92 文法のレベルがへの呼び出しによって返される値によって示される**SQLGetInfo** SQL_SQL_CONFORMANCE 情報の種類にします。 これは、ドライバーが、sql-92 で定義されたエントリ、FIPS Transitional、中間、または完全なレベルに準拠しているかどうかを示します。  
  
 すべての ODBC ドライバーで説明されている最小 SQL 文法をサポートする必要があります[SQL の文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)付録 c:SQL 文法。 この文法には、SQL 92 のエントリ レベルのサブセットです。 ドライバーは、その他の SQL をサポートし、SQL 92 エントリ、中間、または完全レベル、または、FIPS に準拠する 127-2 の移行レベルである可能性があります。 特定のレベルの SQL 92 または FIPS 127-2 に準拠しているドライバーより高いレベルのいずれかの追加機能をサポートまだ完全に準拠するレベルにはできません。 機能がサポートされているかどうかを判断するアプリケーションを呼び出す必要があります**SQLGetInfo**で適切な情報の種類。 SQL の機能の準拠レベルは、対応する情報の種類の説明です。 (を参照してください、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)関数の説明です)。
