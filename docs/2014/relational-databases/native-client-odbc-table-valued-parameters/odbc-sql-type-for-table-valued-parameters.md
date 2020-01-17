---
title: テーブル値パラメーター用の ODBC SQL 型 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90857b24fb467df0292beeb88fb9751e68204d12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199982"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>テーブル値パラメーター用の ODBC SQL 型
  テーブル値パラメーターは、新しい ODBC SQL 型である SQL_SS_TABLE でサポートされます。  
  
## <a name="remarks"></a>コメント  
 SQL_SS_TABLE は、他の ODBC データ型または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型に変換できません。  
  
 SQL_SS_TABLE が C のデータ型として使用されるかどうか、 *ValueType* SQL_DESC_TYPE を SQL_SS_TABLE にアプリケーション パラメーター記述子 (APD) レコードで設定するされる SQLBindParameter、または試行のパラメーターと、SQL_ERROR が返されると、診断レコードが生成されます SQLSTATE = HY003、「無効なアプリケーション バッファーの種類」。  
  
 IPD レコードで SQL_DESC_TYPE を SQL_SS_TABLE に設定し、対応するアプリケーション パラメーター記述子レコードが SQL_C_DEFAULT ではない場合、SQL_ERROR が返され、"アプリケーションのバッファー型が無効です" というメッセージで SQLSTATE=HY003 の診断レコードが生成されます。 これに該当、 *ParameterType* SQLSetDescField、SQLSetDescRec SQLBindParameter の。  
  
 場合、 *TargetType* SQLGetData を呼び出すときに、パラメーターが SQL_SS_TABLE、SQL_ERROR が返され、sqlstate 診断レコードが生成された = HY003、「無効なアプリケーション バッファーの種類」です。  
  
 テーブル値パラメーターの列は、SQL_SS_TABLE 型としてバインドできません。 場合`SQLBindParameter`を使用して呼び出した*ParameterType*を SQL_SS_TABLE に設定すると、SQL_ERROR が返され、sqlstate 診断レコードが生成された = HY004、「無効な SQL データ型」です。 SQLSetDescField および SQLSetDescRec これにも該当します。  
  
 テーブル値パラメーターの列の値には、パラメーターおよび結果列と同じデータ変換オプションが設定されています。  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降では、テーブル値パラメーターは入力パラメーターのみに使用できます。 = HY105 とメッセージ"無効なパラメーターの SQL_DESC_PARAMETER_TYPE を SQLBindParameter または SQLSetDescField SQL_PARAM_INPUT 以外の値に設定しようとしましたが、SQL_ERROR が返され、診断レコードが sqlstate ステートメントに追加する場合"を入力します。  
  
 テーブル値パラメーター列に SQL_DEFAULT_PARAM を使用できない*StrLen_or_IndPtr*テーブル値パラメーターの行ごとの既定値はサポートされていません。 代わりに、アプリケーションで列の属性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE を 1 に設定できます。 つまり、この列にすべての行の既定値が含まれます。 場合*StrLen_or_IndPtr*設定を SQL_DEFAULT_PARAM SQLExecute、SQLExecDirect または SQL_ERROR を返し、診断レコードは、sqlstate ステートメントに追加されます = HY090 と"無効な文字列長またはバッファー長"のメッセージ。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
