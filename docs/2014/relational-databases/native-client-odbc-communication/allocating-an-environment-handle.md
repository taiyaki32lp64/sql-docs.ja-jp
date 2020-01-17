---
title: 環境ハンドルの割り当て |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66afa14ccb1953265f526f8c8861237638f569fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199035"
---
# <a name="allocating-an-environment-handle"></a>環境ハンドルの割り当て
  どの ODBC 関数をアプリケーションから呼び出す場合でも、呼び出す前に ODBC 環境を初期化して環境ハンドルを割り当てる必要があります。 環境ハンドルはグローバルなコンテキスト ハンドルで、ODBC の他のハンドルのプレースホルダーです。 呼び出すことによって、これを行う**SQLAllocHandle**で、 *HandleType*パラメーターを sql_handle_env として設定し、 *InputHandle* SQL_NULL_HANDLE に設定します。  
  
 環境ハンドルを割り当てたら、使用する ODBC 関数呼び出しのバージョンを指定する環境属性を設定する必要があります。 ODBC 3 を使用します。*x*関数を呼び出す[SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)で、*属性*パラメーターを SQL_ATTR_ODBC_VERSION に設定し、 *ValuePtr* SQL_OV_ に設定ODBC3 します。  
  
## <a name="see-also"></a>参照  
 [SQL Server と通信する&#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
