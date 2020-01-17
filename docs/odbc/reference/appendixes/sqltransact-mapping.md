---
title: SQLTransact のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2082a97b24284afcc879048bb08e86a7b2bb3ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070109"
---
# <a name="sqltransact-mapping"></a>SQLTransact のマッピング
**SQLTransact**置き換わっています**SQLEndTran**します。 2 つの関数の主な違いは**SQLEndTran**引数が含まれています*HandleType*、実行する作業のスコープを指定します。 *HandleType*引数は、環境または接続ハンドルを指定できます。 次の呼び出しに**SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 をマップされます。  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 場合*ConnectionHandle* SQL_NULL_HDBC と等しくないです。 *ConnectionHandle*引数の値に設定されて*hdbc*します。  
  
 **SQL_Transact**にマップされます  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 場合*ConnectionHandle* SQL_NULL_HDBC を等しきます。 *EnvironmentHandle*引数の値に設定されて*henv*します。  
  
 前のケースの両方で、 *CompletionType*引数と同じ値に設定されて*fType*します。
