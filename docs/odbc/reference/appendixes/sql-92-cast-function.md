---
title: Sql-92 CAST 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6682ae98f2da64f6936049bee96fe2fff2a84db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057061"
---
# <a name="sql-92-cast-function"></a>SQL-92 CAST 関数
**キャスト**、sql-92 で定義されている関数は、**変換**ODBC で定義された関数。 同等の関数の構文は次のとおりです。  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL 92**キャスト**関数でその他のデータ型に変換できるデータ型は必須です。 (詳細については、SQL 92 仕様を参照してください)。**キャスト**関数は、FIPS 過渡期のレベルでサポートされています。  
  
 アプリケーションのサポートを確認できます、**キャスト**関数の次のようにします。  
  
1.  呼び出す**SQLGetInfo** SQL_SQL_CONFORMANCE 情報の種類にします。 SQL_SC_FIPS127_2_TRANSITIONAL、SQL_SC_SQL92_INTERMEDIATE、または SQL_SC_SQL92_FULL、情報の種類の戻り値の場合、**キャスト**関数がサポートされています。  
  
2.  SQL_SQL_CONFORMANCE 情報の種類の戻り値が SQL_SC_ENTRY_LEVEL または 0 の場合は、呼び出す**SQLGetInfo** SQL_SQL92_VALUE_EXPRESSIONS 情報の種類にします。 SQL_SVE_CAST ビットが設定されている場合、**キャスト**関数がサポートされています。
