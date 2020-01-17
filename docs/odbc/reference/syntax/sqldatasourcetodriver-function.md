---
title: SQLDataSourceToDriver 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSourceToDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSourceToDriver
helpviewer_keywords:
- SQLDataSourceToDriver function [ODBC]
ms.assetid: 0d87fcac-30a0-4303-ad8f-a5b53f4b428d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba5019b15fdbb8bce06f04d5109813b88c40647d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104844"
---
# <a name="sqldatasourcetodriver-function"></a>SQLDataSourceToDriver 関数
**SQLDataSourceToDriver** supportstranslations ODBC ドライバー。 ODBC 対応のアプリケーションではこの関数は呼び出されませんアプリケーション要求経由で翻訳**SQLSetConnectAttr**します。 関連付けられているドライバー、 *ConnectionHandle*で指定されている**SQLSetConnectAttr**ドライバーにデータ ソースから送られて、すべてのデータの翻訳を実行する指定された DLL を呼び出します。 ODBC 初期化ファイルには、既定のトランスレーター DLL を指定できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLDataSourceToDriver(  
     UDWORD     fOption,  
     SWORD      fSqlType,  
     PTR        rgbValueIn,  
     SDWORD     cbValueIn,  
     PTR        rgbValueOut,  
     SDWORD     cbValueOutMax,  
     SDWORD *   pcbValueOut,  
     UCHAR *    szErrorMsg,  
     SWORD      cbErrorMsgMax,  
     SWORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>引数  
 *fOption*  
 [入力]オプションの値。  
  
 *fSqlType*  
 [入力]SQL データ型です。 この引数に変換する方法をドライバーに指示*rgbValueIn*アプリケーションで許容される形式にします。 有効な SQL データ型の一覧は、次を参照してください、 [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)付録 d: セクション。データ型。  
  
 *rgbValueIn*  
 [入力]変換する値。  
  
 *cbValueIn*  
 [入力]長さ*rgbValueIn*します。  
  
 *rgbValueOut*  
 [出力]変換の結果。  
  
> [!NOTE]  
>  トランスレーター DLL は、この値を終了-null はしません。  
  
 *cbValueOutMax*  
 [入力]長さ*rgbValueOut*します。  
  
 *pcbValueOut*  
 [出力]\(Null 終了バイトを除く) バイトの合計数で返される使用可能な*rgbValueOut*です。  
  
 文字またはバイナリ データより大きいまたは等しい場合は*cbValueOutMax*、内のデータ*rgbValueOut*に切り捨てられます*cbValueOutMax*バイト。  
  
 他のすべてのデータ型の値の*cbValueOutMax*は無視されることが前提と翻訳の DLL とのサイズ*rgbValueOut* で指定したSQLデータ型の既定のCデータ型のサイズです*fSqlType*します。  
  
 *PcbValueOut*引数が null ポインターを指定できます。  
  
 *szErrorMsg*  
 [出力]エラー メッセージの記憶域へのポインター。 これは、変換が失敗しない限り、空の文字列です。  
  
 *cbErrorMsgMax*  
 [入力]長さ*後*します。  
  
 *pcbErrorMsg*  
 [出力]\(Null 終了バイトを除く) バイトの総数へのポインターで返される使用可能な*後*です。 大きいまたは等しい場合は*cbErrorMsg*、内のデータ*後*に切り捨てられます*cbErrorMsgMax*マイナス、null 終了文字。 *PcbErrorMsg*引数が null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 変換が成功した場合、false の場合、変換に失敗した場合は TRUE。  
  
## <a name="comments"></a>コメント  
 ドライバー呼び出し**SQLDataSourceToDriver** alldata (結果セットのデータ、テーブル名、行数、エラー メッセージ、およびなど) を変換するデータから渡すことは、ドライバー ソースします。 トランスレーター DLL ではデータの型と翻訳の DLL の目的に応じて、一部のデータが変換されない可能性があります。たとえば、1 つのコード ページから別の文字データを変換する DLL は、すべての数値とバイナリ データを無視します。  
  
 値*fOption*の値に設定されている*vParam*を呼び出して指定**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 属性を持つ。 特定の翻訳の DLL の特定の意味を持つ 32 ビット値です。 たとえば、特定の文字セットの変換を指定します。  
  
 同じバッファーが指定されて場合*rgbValueIn*と*rgbValueOut*バッファー内のデータの変換の場所で実行されます。  
  
 *CbValueIn*、 *cbValueOutMax*、および*pcbValueOut*の種類が、SDWORD **SQLDataSourceToDriver**必要はありません膨大なポインターをサポートします。  
  
 場合**SQLDataSourceToDriver**変換中にデータの切り捨てが発生したは、FALSE を返します。 場合*pcbValueOut* (出力バッファーに返される使用可能なバイト数) がより大きい*cbValueOutMax* (出力バッファーの長さ)、切り捨てが発生しました。 ドライバーは、切り捨てが許容されるかどうかを判断する必要があります。 切り捨てが発生しなかった場合、 **SQLDataSourceToDriver**別のエラーにより FALSE が返されます。 いずれの場合も、特定のエラー メッセージが返される*後*します。  
  
 データの翻訳の詳細については、次を参照してください。[翻訳の Dll](../../../odbc/reference/develop-app/translation-dlls.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|データ ソースに送信されるデータを変換します。|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|接続属性の設定を返す|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
