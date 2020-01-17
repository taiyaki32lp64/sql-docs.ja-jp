---
title: SQLGetInfo (Excel ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Excel Driver
ms.assetid: fed4aea2-6d3d-4199-a5db-3d033eb63927
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba2e23bf4b3c464c5483897c0a9dd3e6c9dea626
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003278"
---
# <a name="sqlgetinfo-excel-driver"></a>SQLGetInfo (Excel ドライバー)
> [!NOTE]  
>  このトピックでは、Excel ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 **SQLGetInfo** SQL_FILE_USAGE 情報の種類をサポートしています。 返される値は、ドライバーが直接データ ソース内のファイルを処理する方法を示す 16 ビット整数を示します。  
  
-   SQL_FILE_NOT_SUPPORTED - ドライバーは、1 階層のドライバーではありません。  
  
-   SQL_FILE_TABLE - 1 階層のドライバーは、テーブルとしてデータ ソース内のファイルを扱います。  
  
-   SQL_FILE_QUALIFIER - 1 階層のドライバーは、修飾子としてデータ ソース内のファイルを扱います。  
  
 ODBC ドライバーは、各ファイルは、テーブルでは、マイクロソフト Exceldriver の SQL_FILE_TABLE を返します。  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|バージョン|バージョン番号の形式|  
|----------|-------------|-------------------------------|  
|Microsoft Excel|3.0|03.00.0000|  
||4.0|04.00.0000|  
||5.0/7.0|05.00.0000|  
||97/2000|08.00.0000|  
  
## <a name="sqlfileusage"></a>SQL_FILE_USAGE  
 SQL_FILE_TABLE (Excel 3.0 または 4.0)  
  
 SQL_FILE_CATALOG (Excel 5.0 または 7.0)  
  
## <a name="sqlmaxcharliterallen"></a>SQL_MAX_CHAR_LITERAL_LEN  
 255 (Excel 3.0/4.0/5.0/7.0)  
  
 65535 (Excel 97)  
  
## <a name="sqlmaxcolumnnamelen"></a>SQL_MAX_COLUMN_NAME_LEN  
 30 (Excel 3.0 または 4.0)  
  
 64 (Excel 5.0/7.0/97)  
  
## <a name="sqlmaxtablenamelen"></a>SQL_MAX_TABLE_NAME_LEN  
 12 (Excel 3.0 または 4.0)  
  
 31 (Excel 5.0/7.0/97)  
  
## <a name="sqlcatalognameseparator"></a>SQL_CATALOG_NAME_SEPARATOR  
 "\\"(Excel 3.0 または 4.0)  
  
 "."(Excel 5.0/7.0/97)  
  
## <a name="sqlcatalogterm"></a>SQL_CATALOG_TERM  
 "Directory"(Excel 3.0 または 4.0)  
  
 「ブック」(Excel 5.0/7.0/97)  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; です。 SQL_FN_TD_CURTIME &#124; です。 SQL_FN_TD_DAYOFMONTH &#124;です。 SQL_FN_TD_DAYOFWEEK &#124; です。SQL_FN_TD_DAYOFYEAR &#124; です。 SQL_FN_TD_HOUR &#124; です。SQL_FN_TD_MINUTE &#124;です。SQL_FN_TD_MONTH &#124;です。 SQL_FN_TD_NOW &#124; です。SQL_FN_TD_SECOND&#124;です。SQL_FN_TD_WEEK&#124;です。SQL_FN_TD_YEAR
