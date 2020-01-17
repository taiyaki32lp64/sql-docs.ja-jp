---
title: SQLStatistics (Excel ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Excel Driver
ms.assetid: 02506664-8dcc-4bd0-a8bb-d49fcbdd5722
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1c36d68f42b9b7f76310c453d704c6815ee6de22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132474"
---
# <a name="sqlstatistics-excel-driver"></a>SQLStatistics (Excel ドライバー)
> [!NOTE]  
>  このトピックでは、Excel ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
|[列]|コメント|  
|------------|--------------|  
|TABLE_QUALIFIER|ディレクトリへのパス。<br /><br /> パターン マッチングはではサポートされていません、 *szTableQualifier*引数。|  
|TABLE_OWNER|所有者名がサポートされていないために、この列で NULL が返されます。|  
|TABLE_NAME|区切りのないテーブルの名前。<br /><br /> パターン マッチングはではサポートされていません、 *szTableName*引数。|  
|INDEX_QUALIFIER|NULL は常に返されます。|  
|INDEX_NAME|インデックスに依存します。|  
|TYPE|型の SQL_TABLE_STAT または SQL_INDEX_OTHER のみが返されます。|  
|SEQ_IN_INDEX|インデックスに依存します。|  
|COLUMN_NAME|インデックスに依存します。|  
|COLLATION|インデックスに依存します。|  
|PAGES|NULL は常に返されます。|  
  
 一意性に基づくフィルター処理は、(、 *fUnique*引数)。 *FAccuracy*パラメーターは無視されます。
