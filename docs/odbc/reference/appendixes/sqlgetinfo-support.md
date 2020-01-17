---
title: SQLGetInfo のサポート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f40299dccc0313f662aeadfcb26b71326cdc6d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073903"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo のサポート
ODBC 2 時にします。*x*アプリケーション呼び出し**SQLGetInfo** 、ODBC 3 *.x*ドライバー、*情報の種類*次の表の引数をサポートする必要があります。  
  
|*情報の種類*|戻り値|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0)**に注意してください。** この情報の種類は非推奨ではないです。右側の列で、各ビットマスクが非推奨とされます。|内の句を列挙する SQLINTEGER ビットマスク、 **ALTER TABLE**ステートメント、データ ソースでサポートされています。<br /><br /> 次のビットマスクを使用して、どの句がサポートされているを調べます。<br /><br /> SQL_AT_DROP_COLUMN = 列を削除する機能がサポートされています。 結果が cascade これ、または動作を制限するかどうかは、ドライバーの定義です。 (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = 単一の ALTER TABLE ステートメントで複数の列のサポートを追加する機能。 このビットは、他の SQL_AT_ADD_COLUMN_XXX bits または SQL_AT_CONSTRAINT_XXX bits と組み合わせるはできません。 (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> 情報の種類が ODBC 1.0; で導入されました。各ビットマスクが導入されたバージョンが付いています。|サポートされるフェッチ方向オプションを列挙する SQLINTEGER ビットマスク。<br /><br /> 以下のビットマスクは、どのオプションがサポートされているかを判断するとフラグの組み合わせで使用されます。<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) (ODBC 1.0) SQL_FD_FETCH_FIRST SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) (ODBC 1.0)、SQL_FD_FETCH_RELATIVE SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|サポートされているロックを列挙する SQLINTEGER ビットマスク型、*群れ*引数**SQLSetPos**します。<br /><br /> 次のビットマスクは、どのロックの種類がサポートされているかを判断するとフラグの組み合わせで使用されます。<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|ODBC 準拠のレベルを示す SQLSMALLINT 値。<br /><br /> SQL_OAC_NONE = なし<br /><br /> SQL_OAC_LEVEL1 = レベル 1 のサポート<br /><br /> SQL_OAC_LEVEL2 = レベル 2 のサポート|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|ドライバーによってサポートされている SQL 文法を示す SQLSMALLINT 値。 参照してください[付録 c:SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)SQL の適合性レベルの定義についてはします。<br /><br /> SQL_OSC_MINIMUM = サポートされている最低限の文法<br /><br /> SQL_OSC_CORE = サポートされているコアの文法<br /><br /> SQL_OSC_EXTENDED = サポートされている文法の拡張|  
|SQL_POS_OPERATIONS (ODBC 2.0)|サポートされる操作を列挙する SQLINTEGER ビットマスク**SQLSetPos**します。<br /><br /> 以下のビットマスクは、どのオプションがサポートされているかを判断するフラグと組み合わせてでに使用されます。<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH   (ODBC 2.0) SQL_POS_UPDATE     (ODBC 2.0) SQL_POS_DELETE     (ODBC 2.0) SQL_POS_ADD          (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|サポートされている列挙、SQLINTEGER ビットマスクは、SQL ステートメントを配置します。<br /><br /> 次のビットマスクを使用して、どのステートメントがサポートされているを調べます。<br /><br /> SQL_PS_POSITIONED_DELETE、SQL_PS_POSITIONED_UPDATE、SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|カーソルのサポートされている同時実行制御オプションを列挙する SQLINTEGER ビットマスク。<br /><br /> 次のビットマスクを使用して、どのオプションがサポートされているを調べます。<br /><br /> SQL_SCCO_READ_ONLY = カーソルは読み取り専用です。 更新は許可されません。<br /><br /> SQL_SCCO_LOCK、行を更新することを確認するための十分なロックの最下位レベルのカーソルの使用を = です。<br /><br /> SQL_SCCO_OPT_ROWVER SQLBase ROWID または Sybase タイムスタンプなどの行のバージョンを比較する、カーソルはオプティミスティック同時実行制御を = です。<br /><br /> SQL_SCCO_OPT_VALUES 値を比較する、カーソルはオプティミスティック同時実行制御を = です。|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|アプリケーションで静的であるか、キーセット ドリブン カーソルを使用して変更するかどうか、SQLINTEGER ビットマスクを列挙する**SQLSetPos**または位置指定の update または delete ステートメントは、そのアプリケーションによって検出できます。<br /><br /> SQL_SS_ADDITIONS = 追加された行がカーソルに表示されます。これらの行にカーソルがスクロールできます。 カーソルをこれらの行が追加されると、ドライバーによって異なります。<br /><br /> SQL_SS_DELETIONS = 削除された行は、カーソルを使用できなくと; 結果セットに「穴」せず削除された行から、カーソルがスクロールした後は、その行を返すことはできません。<br /><br /> SQL_SS_UPDATES = 行の更新がカーソルに表示されます。カーソルからスクロールし、更新行へ返すと、カーソルによって返されるデータが元のデータではなく、更新されたデータ。 このオプションには、キーセット ドリブン カーソル、キーを更新しないにのみに静的カーソルや更新プログラムが適用されます。 このオプションは、動的カーソルまたは混合カーソル内のキーが変更された場合に適用されません。<br /><br /> アプリケーションが、同じアプリケーション内の他のカーソルを含む、他のユーザーごとに結果セットに加えられた変更を検出するかどうかは、カーソルの種類によって異なります。|  
  
 ODBC 3 *.x* 、ODBC 3 の操作アプリケーション *.x*ドライバーは呼び出さないでください**SQLGetInfo**で、*情報の種類*で説明されている引数上記のテーブルが、ODBC 3 を使用する必要があります *.x* *情報の種類*引数は、次の段落に一覧表示します。 一対一の対応関係がない*情報の種類*ODBC 2 で使用される引数 *。x* ODBC 3 で使用されるものと *.x*します。 ODBC 3 *.x* ODBC 2 を使用するアプリケーション *。x*ドライバー、その一方で、使用する必要があります、*情報の種類*引数が以前に説明します。  
  
 カーソルの属性情報の種類を優先して、前の表の情報の種類の一部は非推奨します。 これらは、情報の種類は SQL_FETCH_DIRECTION、SQL_LOCK_TYPES、SQL_POS_OPERATIONS、SQL_POSITIONED_STATEMENTS、SQL_SCROLL_CONCURRENCY、および SQL_STATIC_SENSITIVITY が非推奨とされます。 新しい種類のカーソルの属性は、DYNAMIC、FORWARD_ONLY、KEYSET_DRIVEN、静的または XXX と等しい、SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2 です。 新しい型のそれぞれには、ドライバーの機能は、1 つのカーソルの種類のことを示します。 これらのオプションの詳細については、次を参照してください。、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)関数の説明。
