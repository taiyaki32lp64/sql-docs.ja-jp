---
title: データ型の変換 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 590bd488ae87e8e871837c3055a3225794850d00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077013"
---
# <a name="data-type-conversions"></a>データ型変換
データに変換できる 1 つの型から別に 4 回のいずれか: 転送するときにデータが変数の 1 つのアプリケーションから別 (C に C)、ステートメントのパラメーター (C から SQL へ) をアプリケーション変数にデータが送信されるときに結果セット列のデータが返される場合アプリケーション変数 (SQL から C へ) と (SQL to SQL) 別に 1 つのデータ ソースの列からデータが転送されるときにします。  
  
 別の変数の 1 つのアプリケーションからデータを転送するときに発生するすべての変換は、このドキュメントの範囲外です。  
  
 アプリケーションが結果セットの列またはステートメントのパラメーターに変数をバインドするとき、アプリケーションはアプリケーション変数のデータ型の選択データ型の変換を暗黙的に指定します。 たとえば、列には、整数型のデータが含まれるとします。 アプリケーションでは、列に整数型の変数をバインドした場合は、ある変換が行われない。 を指定します。アプリケーションでは、列に文字変数をバインドした場合、データは、文字に整数から変換されることを指定します。  
  
 ODBC では、各 SQL と C# のデータ型の間でデータを変換する方法を定義します。 基本的には、ODBC では、整数および浮動小数点、整数の文字など、すべての適切な変換をサポートし、日付する浮動小数点数など、正しく定義されていない変換をサポートしていません。 ドライバーがサポートする各 SQL データ型のすべての変換をサポートするために必要です。 SQL と C# のデータ型間の変換の完全な一覧を参照してください[SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)と[C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)付録 d:。データ型。  
  
 ODBC では、1 つの SQL データ型からデータを変換するスカラー関数も定義します。 **変換**スカラー関数は、基になるスカラー関数またはデータ ソースの変換を実行する定義されている関数に、ドライバーによってマップされます。 この関数は DBMS 固有の関数にマップされている、ために、これらの変換のしくみや、どのような変換をサポートする必要がありますが ODBC に定義されていません。 アプリケーションの検出、特定のドライバーとデータ ソース内の SQL_CONVERT オプションによってどのような変換がサポートされている**SQLGetInfo**します。 詳細については、**変換**スカラー関数を参照してください[odbc エスケープ シーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)と[明示的なデータ型変換関数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)します。
