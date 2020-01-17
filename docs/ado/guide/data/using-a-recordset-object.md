---
title: レコード セット オブジェクトを使用して |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dda89464598ddc4ecfee0078b36aadd01b4486f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923637"
---
# <a name="using-a-recordset-object"></a>レコードセット オブジェクトを使用する
また、使用することができます**Recordset.Open**を暗黙的に接続を確立し、1 回の操作では、その接続経由でコマンドを発行します。 たとえばでは Visual Basic の場合。  
  
```  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.CursorLocation = adUseClient  
oRs.Open sSQL, sConn, adOpenStatic, _  
               adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
oRs.Close          
Set oRs = Nothing  
```  
  
 注意**oRs.Open**は接続文字列を受け取り (*sConn*) の代わりに、**接続**オブジェクト (*oConn*)、そのの値として**ActiveConnection**パラメーター。 設定によって、クライアント側カーソルの種類を適用することも、 **CursorLocation**プロパティを**Recordset**オブジェクト。 ここでも、これと対照的に、 **HelloData**例。
