---
title: SQLGetConnectOption のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d0533a0ee616d4097793eca46c7d45a269142737
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086405"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption のマッピング
アプリケーションを呼び出すと**SQLGetConnectOption** ODBC を通じて*3.x*ドライバーへの呼び出し  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 次のようにマップされます。  
  
-   場合*fOption*ドライバー マネージャーの呼び出し、文字列を返す ODBC で定義された接続オプションを示します  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   場合*fOption*ドライバー マネージャーの呼び出し、32 ビット整数値を返す ODBC で定義された接続オプションを示します  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   場合*fOption*ドライバー定義ステートメントのオプション、ドライバー マネージャーの呼び出しを示します  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 上記の 3 つのケース、 *ConnectionHandle*引数の値に設定されて*hdbc*、*属性*引数の値に設定されて*fOption*、および*ValuePtr*引数と同じ値に設定されて*pvParam*します。  
  
 ODBC で定義された文字列の接続オプションは、ドライバー マネージャーの設定、 *BufferLength*への呼び出しで引数**SQLGetConnectAttr**定義済みの最大長 (SQL_MAX_OPTION_STRING_LENGTH)。文字列以外の接続オプション、 *BufferLength*は 0 に設定します。  
  
 ODBC の*3.x*ドライバー、ドライバー マネージャーは不要になったかどうかを確認します*オプション*SQL_CONN_OPT_MIN と SQL_CONN_OPT_MAX、間、または SQL_CONNECT_OPT_DRVR_START よりも大きい。 ドライバーは、オプションの値の有効性を確認する必要があります。
