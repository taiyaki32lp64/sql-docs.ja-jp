---
title: SQLGetStmtOption (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5521fb11cad064cf487d38562f4146fd32587993
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898785"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:[完全]  
  
 ODBC API 準拠:1 つのレベル  
  
 ステートメント オプションの現在の設定を返します。  
  
|*fOption*|戻り値|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|現在のレコード数のブックマークは、32 ビット整数値|  
|SQL_ROW_NUMBER|結果内の現在の行の位置を指定する 32 ビット整数の設定|  
|SQL_TRANSLATE_DLL|エラー:"Driver できません。"|  
  
 Visual FoxPro ODBC ドライバーには、翻訳の Dll がありません。  
  
 詳細については、次を参照してください。 [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md)で、 *ODBC プログラマ リファレンス*します。
