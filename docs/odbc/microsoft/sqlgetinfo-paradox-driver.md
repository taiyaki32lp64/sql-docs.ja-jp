---
title: SQLGetInfo (Paradox ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Paradox Driver
ms.assetid: 43aab762-68f4-4128-b8f5-8878ea5f1258
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a35f3bdbd68b674736ac22f447a8be45c1342682
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003247"
---
# <a name="sqlgetinfo-paradox-driver"></a>SQLGetInfo (Paradox ドライバー)
> [!NOTE]  
>  このトピックでは、Paradox ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 **SQLGetInfo** SQL_FILE_USAGE 情報の種類をサポートしています。 返される値は、ドライバーが直接データ ソース内のファイルを処理する方法を示す 16 ビット整数を示します。  
  
-   SQL_FILE_NOT_SUPPORTED - ドライバーは、1 階層のドライバーではありません。  
  
-   SQL_FILE_TABLE - 1 階層のドライバーは、テーブルとしてデータ ソース内のファイルを扱います。  
  
-   SQL_FILE_QUALIFIER - 1 階層のドライバーは、修飾子としてデータ ソース内のファイルを扱います。  
  
 ODBC ドライバーは、各ファイルがテーブルであるために、SQL_FILE_TABLE を返します。  
  
## <a name="sqlaltertable"></a>SQL_ALTER_TABLE  
 SQL_AT_ADD_COLUMN &#124; SQL_AT_DROP_COLUMN  
  
## <a name="sqlddlindex"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|バージョン|バージョン番号の形式|  
|----------|-------------|-------------------------------|  
|Paradox|3.x|03.00.0000|  
||4.x|04.00.0000|  
||5.x|05.00.0000|  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION &#124; SQL_QU_INDEX_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
