---
title: SQLGetTypeInfo (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f29be5e03a6cc9c1c91809db2b8ec7c686e90f11
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898628"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:[完全]  
  
 ODBC API 準拠:レベル 1  
  
 データ ソースでサポートされるデータ型に関する情報を返します。 ドライバーは、SQL 結果セット内の情報を返します。 次の表は、ODBC データ型と対応する Visual FoxPro データ型を示します。  
  
|ODBC の種類|Visual FoxPro 型|  
|---------------|------------------------|  
|SQL_BIGINT|サポートされていません。 64 ビット Visual FoxPro の型はありません。|  
|SQL_BIT|論理|  
|SQL_CHAR|文字|  
|SQL_DATE|date|  
|SQL_DECIMAL|数値|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|メモ (バイナリ)|  
|SQL_LONGVARCHAR|メモ|  
|SQL_NUMERIC|数値 *、通貨、Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|サポートされていません。 Visual FoxPro のない*時間*型。|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|メモ (バイナリ) *、一般的な|  
|SQL_VARCHAR|文字|  
  
 \* 既定の種類  
  
 Visual FoxPro データの種類の詳細については、次を参照してください。 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)します。 この関数の詳細については、次を参照してください。 [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)で、 *ODBC プログラマ リファレンス*します。
