---
title: SQLSTATE マッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3987085d7d04bf248bcc728c3bcd1ee5503d9af1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107362"
---
# <a name="sqlstate-mappings"></a>SQLSTATE マッピング
このトピックでは、ODBC の SQLSTATE 値を説明*2.x*および ODBC *3.x*します。 ODBC の詳細については*3.x* SQLSTATE の値を参照してください[付録 a:ODBC エラー コード](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)します。  
  
 ODBC で*3.x*HYxxx SQLSTATEs が S1xxx、代わりに返される、S00XX ではなく 42Sxx SQLSTATEs が返されます。 これは、Open Group および ISO 標準に合わせて行われました。 多くの場合、標準がいくつかについての解釈を再定義があるため、マッピングは 1 対 1 ありません。  
  
 ときに、ODBC *2.x*を ODBC アプリケーションはアップグレード*3.x* ODBC の期待に変更するアプリケーション、アプリケーションが*3.x* ODBCではなくSQLSTATEs*2.x* SQLSTATEs します。 次の表は、ODBC *3.x* SQLSTATEs を各 ODBC *2.x* SQLSTATE にマップされます。  
  
 ODBC ドライバーの投稿 SQL_OV_ODBC2 を SQL_ATTR_ODBC_VERSION 環境属性を設定すると、 *2.x* ODBC ではなく SQLSTATEs *3.x* SQLSTATEs とき**SQLGetDiagField**または**SQLGetDiagRec**が呼び出されます。 特定のマッピングは、ODBC に注意して決定できます*2.x* ODBC に対応する次の表の 1 列目の SQLSTATE *3.x*列 2 の SQLSTATE。  
  
|ODBC *2.x* SQLSTATE|ODBC *3.x* SQLSTATE|コメント|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018||  
|S0001|42S01||  
|S0002|42S02||  
|S0011|42S11||  
|S0012|42S12||  
|S0021|42S21||  
|S0022|42S22||  
|S0023|42S23||  
|S1000|HY000||  
|S1001|HY001||  
|S1002|07009|ODBC *2.x* odbc SQLSTATE S1002 がマップされている*3.x* SQLSTATE 07009 場合は、基になる関数**SQLBindCol**、 **SQLColAttribute**、**SQLExtendedFetch**、 **SQLFetch**、 **SQLFetchScroll**、または**SQLGetData**します。|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Null ポインターで使用するが返されます。|  
|S1009|HY024|無効な属性値に対して返されます。|  
|S1009|HY092|更新、またはデータの削除の呼び出しによって返される**SQLSetPos**、または追加、更新、またはへの呼び出しでデータを削除する**SQLBulkOperations**、同時実行性が読み取り専用です。|  
|S1010|HY007 HY010|SQLSTATE S1010 が SQLSTATE HY007 にマップされているときに**SQLDescribeCol**呼び出す前に呼び出されますが**SQLPrepare**、 **SQLExecDirect**、または、のカタログ関数*StatementHandle*します。 それ以外の場合、SQLSTATE S1010 は SQLSTATE HY010 にマップされます。|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC *3.x* odbc SQLSTATE 07009 がマップされている*2.x*関数を基になる場合は、SQLSTATE S1093 **SQLBindParameter**または**SQLDescribeParam**.|  
|S1096|HY096||  
|S1097|HY097||  
|S1098|HY098||  
|S1099|HY099||  
|S1100|HY100||  
|S1101|HY101||  
|S1103|HY103||  
|S1104|HY104||  
|S1105|HY105||  
|S1106|HY106||  
|S1107|HY107||  
|S1108|HY108||  
|S1109|HY109||  
|S1110|HY110||  
|S1111|HY111||  
|S1C00|HYC00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC *3.x* odbc SQLSTATE 07008 がマップされている*2.x* SQLSTATE S1000 します。
