---
title: データ バッファーの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 615625ca396e5f2ae094962457cc9e746730ddcf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067414"
---
# <a name="data-buffer-type"></a>データ バッファーの種類
バッファーの C データ型は、アプリケーションによって指定されます。 1 つの変数には、アプリケーションは、変数を割り当てるときに発生します。 汎用的なメモリの使用は、void - 型のポインターで指し示されるメモリ場合、アプリケーションが特定の種類にメモリをキャストです。 ドライバーは、2 つの方法でこの型を検出します。  
  
-   **データ バッファーの型引数です。** バッファーを使用してバインドなどのパラメーター値と結果セットのデータを転送するために使用するバッファー *TargetValuePtr*で**SQLBindCol**、通常などの関連付けられている型の引数がある、 *TargetType*引数**SQLBindCol**します。 この引数では、アプリケーションは、バッファーの型に対応する C 型識別子を渡します。 呼び出す次の場合など**SQLBindCol**、SQL_C_TYPE_DATE 値の通知、ドライバー、*日付*バッファーが、SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     型識別子の詳細については、次を参照してください。、 [ODBC のデータ型](../../../odbc/reference/develop-app/data-types-in-odbc.md)セクションで、このセクションで後述します。  
  
-   **定義済みの型。** によって示されるバッファーを送信し、オプションや、バッファーなどの属性を取得するために使用、 *InfoValuePtr*引数**SQLGetInfo**、指定されたオプションに依存する型は固定であります。 ドライバーは、この型のデータ バッファーを前提としています。この型のバッファーを割り当て、アプリケーションの役目です。 たとえば、以下でを呼び出す**SQLGetInfo**ドライバーでは、バッファーは 32 ビット整数 SQL_STRING_FUNCTIONS オプションが必要とこれが前提としています。  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 ドライバーは、バッファー内のデータを解釈するのに C データ型を使用します。
