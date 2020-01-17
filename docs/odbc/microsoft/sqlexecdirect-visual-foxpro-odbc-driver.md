---
title: SQLExecDirect (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e701340217a885fbf1e3372c33ed1a8cfdb21457
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053850"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:[完全]  
  
 ODBC API 準拠:コア レベル  
  
 新しい実行[準備可能な SQL ステートメント](../../odbc/microsoft/visual-foxpro-terminology.md)します。 Visual FoxPro ODBC ドライバーでは、任意のパラメーターは、ステートメントに存在しない場合、パラメーター マーカーの変数の現在の値が使用されます。  
  
 一度に 1 つ以上の SQL ステートメントを送信するバッチ コマンドを作成するには、セミコロン (;) を使用して、バッチ内の各 SQL ステートメントを区切ります。  
  
 テーブル、ビュー、またはフィールド名にスペースが含まれる場合の名前で囲みます引用符の背面にマークします。 たとえば、データベースにマイ テーブルとフィールド My Field という名前のテーブルが含まれている場合を囲む識別子の各要素として次のように。  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 詳細については、次を参照してください。 [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md)で、 *ODBC プログラマ リファレンス*します。
