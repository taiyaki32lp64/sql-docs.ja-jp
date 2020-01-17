---
title: 複数の結果 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f8679bea49b63ffd5dc7164942b42ac9eed7e9ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086362"
---
# <a name="multiple-results"></a>複数の結果
A*結果*何かによって返されるデータ ソース、ステートメントが実行された後にします。 ODBC には 2 つの種類の結果: 結果セットと、行の数。 *行数*は、更新によって影響を受ける行の数は、削除、またはステートメントを挿入します。 説明されているバッチ、 [SQL ステートメントのバッチ](../../../odbc/reference/develop-app/batches-of-sql-statements.md)、複数の結果を生成することができます。  
  
 次の表、 **SQLGetInfo**オプションのアプリケーションを使用してデータ ソースがバッチの種類ごとの複数の結果を返すかどうかを判断します。 具体的には、データ ソースは、ステートメントのバッチ全体の 1 つの行の数を返すことができます。 またはバッチ内の各ステートメントの個々 の行をカウントします。 結果セットを生成するステートメントを実行するパラメーターの配列との場合、データ ソースが単一の結果セットのすべてのパラメーターのセットを返すことができます。 または個々 の結果がパラメーターのセットごとに設定します。  
  
|バッチの種類|行の数|結果セット|  
|----------------|----------------|-----------------|  
|明示的なバッチ|[A] SQL_BATCH_ROW_COUNT|-[b]。|  
|手順|[A] SQL_BATCH_ROW_COUNT|-[b]。|  
|パラメーターの配列|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 行のバッチ内の数を生成するステートメントはサポートされている可能性があります、まだ行カウントの戻り値はサポートされません。 SQL_BATCH_SUPPORT オプション**SQLGetInfo**を示すかどうかの行の数を生成するステートメントがバッチで許可されている; SQL_BATCH_ROW_COUNTS オプションでは、これらの行カウントがアプリケーションに返されるかどうかを示します。  
  
 [b] 明示的なバッチおよびプロシージャ、複数の結果セットを生成するステートメントが含まれている、複数の結果セットを常に返します。  
  
> [!NOTE]  
>  ODBC 1.0 で導入された SQL_MULT_RESULT_SETS オプションでは、複数の結果セットが返されるかどうかの一般的なのみについて説明します。 具体的には、SQL_BS_SELECT_EXPLICIT、SQL_BS_SELECT_PROC または bits が SQL_BATCH_SUPPORT に対して返される場合、または SQL_PARAM_ARRAYS_SELECT SQL_PAS_BATCH が返されます場合"Y"に設定されます。  
  
 複数の結果を処理するアプリケーションを呼び出す**SQLMoreResults**します。 この関数は、現在の結果を破棄し、次の結果を使用できるようにします。 これ以外の結果が使用できる場合は、sql_no_data が返さを返します。 たとえば、次のステートメントがバッチとして実行されます。  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 アプリケーションによって作成された結果セットから行をフェッチするこれらのステートメントが実行された後、**選択**ステートメント。 呼び出すことにより、行のフェッチが完了したら、 **SQLMoreResults** repriced された部分の数を使用できるようにします。 必要に応じて、 **SQLMoreResults**取り出されていない行を破棄し、カーソルを閉じます。 その後、アプリケーションを呼び出す**SQLRowCount**を判断する方法の多くの部分は、によって repriced された、 **UPDATE**ステートメント。  
  
 これは、すべての結果ができるようになりますにバッチ全体のステートメントを実行するかどうかドライバー固有です。 このケースでは、これは一部の実装呼び出す他のユーザーで**SQLMoreResults**バッチの次のステートメントの実行をトリガーします。  
  
 バッチ内のステートメントのいずれかが失敗した場合、 **SQLMoreResults** SQL_ERROR または SQL_SUCCESS_WITH_INFO が返されます。 ステートメントが失敗しました、失敗したステートメントがバッチ内の最後のステートメントまたはバッチが中止された場合**SQLMoreResults** SQL_ERROR が返されます。 ステートメントが失敗しました、失敗したステートメントは、バッチの最後のステートメントでした。 ときに、バッチが中断されていない場合**SQLMoreResults** sql_success_with_info が返されます。 SQL_SUCCESS_WITH_INFO は、少なくとも 1 つの結果セットまたは数が生成されたことと、バッチが中断されていないことを示します。
