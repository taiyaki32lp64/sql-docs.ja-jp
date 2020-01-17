---
title: SQLSetScrollOptions のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 06b6b0f982b5c8d864e5024c8544f1f8e9af75ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091704"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions のマッピング
アプリケーションを呼び出すと**SQLSetScrollOptions** ODBC を通じて*3.x*ドライバーとドライバーがサポートしない**SQLSetScrollOptions**への呼び出し  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 次のようになります。  
  
-   呼び出し  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     *情報の種類*引数の値に応じて、次の表に、値のいずれかに設定、*キーセット*引数**SQLSetScrollOptions**します。  
  
    |*キーセット引数*|*情報の種類の引数*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |大きい値、*複合カーソル*引数|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     場合の値、*キーセット*上記の表への呼び出しに引数一覧にない**SQLSetScrollOptions** SQLSTATE S1107 を返します (値が範囲外の行) されていて、次の手順のいずれも実行されます。  
  
     ドライバー マネージャーがで適切なビットを設定するかどうかを確認し、**InfoValuePtr*への呼び出しによって返される値**SQLGetInfo**の値に基づいて、 *同時実行*引数**SQLSetScrollOptions**します。  
  
    |*同時実行*引数|*情報の種類*設定|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     場合、*同時実行*引数は、前の表への呼び出しで値のいずれかではない**SQLSetScrollOptions** SQLSTATE S1108 を返します (同時実行オプションは範囲) は、次の手順のいずれも、実行されます。 (上記の表に示されます) として適切なビット設定されていない場合 **InfoValuePtr*に対応する値の 1 つ、*同時実行*引数への呼び出し**SQLSetScrollOptions** SQLSTATE S1C00 を返します (ドライバーに対応していない)、none、次の手順が実行されます。  
  
-   呼び出し  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     *\*ValuePtr*の値に基づいて、次の表の値のいずれかに設定、*キーセット*引数**SQLSetScrollOptions**します。  
  
    |*キーセット*引数|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |大きい値、*複合カーソル*引数|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   呼び出し  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     *\*ValuePtr*に設定、*同時実行*引数**SQLSetScrollOptions**します。  
  
-   場合、*キーセット*への呼び出しで引数**SQLSetScrollOptions**が正の値への呼び出し  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     *\*ValuePtr*に設定、*キーセット*引数**SQLSetScrollOptions**します。  
  
-   呼び出し  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     *\*ValuePtr*に設定、*複合カーソル*引数**SQLSetScrollOptions**します。  
  
    > [!NOTE]  
    >  ドライバー マネージャーがマップされます**SQLSetScrollOptions** ODBC を使用するアプリケーションの*3.x*がサポートされていないドライバー **SQLSetScrollOptions**、ドライバーマネージャーに SQL_ROWSET_SIZE ステートメントのオプション、not、SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性を設定、*複合カーソル*引数**SQLSetScrollOption**します。 その結果、 **SQLSetScrollOptions**への呼び出しで複数の行をフェッチするときに、アプリケーションでは使用できません**SQLFetch**または**SQLFetchScroll**します。 フェッチの複数の行への呼び出しで場合にのみ使用できます**SQLExtendedFetch**します。
