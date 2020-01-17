---
title: SQLPrepare (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5835ddaf27d097dcfff608649f50c1f7f41a93df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996307"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:[完全]  
  
 ODBC API 準拠:コア レベル  
  
 最適化し、ステートメントを実行する方法を計画することにより、SQL ステートメントを準備します。 実行するため、SQL ステートメントがコンパイルされる[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)します。  
  
 テーブル、ビュー、またはフィールド名にスペースが含まれる場合の名前で囲みます背面に引用符 (') のマーク。 たとえば、データベースにマイ テーブルとフィールド My Field という名前のテーブルが含まれている場合を囲む識別子の各要素として次のように。  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 詳細については、次を参照してください。 [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)で、 *ODBC プログラマ リファレンス*します。
