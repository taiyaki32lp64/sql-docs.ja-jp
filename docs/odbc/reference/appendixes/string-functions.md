---
title: 文字列関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd4ec3e05acfd4faaafd38a79e48c67d03d86bd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070169"
---
# <a name="string-functions"></a>文字列関数
次の表には、文字列操作関数が一覧表示します。 文字列関数が呼び出すことによってドライバーによってサポートされているアプリケーションを調べる**SQLGetInfo**で、*情報の種類*SQL_STRING_FUNCTIONS の。  
  
## <a name="remarks"></a>コメント  
 として表される引数*string_exp* 、列の名前を指定できます、*文字文字列リテラル*、または SQL_CHAR、sql _ として基になるデータ型を表すことがもう 1 つのスカラー関数の結果Varchar 型、または SQL_LONGVARCHAR します。  
  
 として表される引数*character_exp*は可変長文字列。  
  
 として表される引数*開始*、*長さ*、または*カウント*できます、*数値リテラル*または別のスカラー関数の結果を基になるデータ型は、SQL_TINYINT、SQL_SMALLINT、または SQL_INTEGER として表すことができます。  
  
 次のとおり、文字列関数は 1 から始まります。これは、文字列の最初の文字では、1 文字があります。  
  
 BIT_LENGTH、CHAR_LENGTH、CHARACTER_LENGTH、OCTET_LENGTH、および位置の文字列のスカラー関数は、SQL 92 とを連携させる ODBC 3.0 で追加されました。  
  
|関数|説明|  
|--------------|-----------------|  
|**ASCII (** _string_exp_ **)** (ODBC 1.0)|左端の文字の ASCII コード値を返します*string_exp*を整数として。|  
|**BIT_LENGTH (** _string_exp_ **)** (ODBC 3.0)|文字列式の長さ (ビット単位) を返します。<br /><br /> 文字列データ型に対してのみは機能は、変換は暗黙的にない*string_exp*文字列の代わりには、どのようなデータ型の (内部) のサイズを返します。|  
|**CHAR (** _コード_ **)** (ODBC 1.0)|持つ、ASCII 文字コードによって指定された値を返します。*コード*します。 値*コード*0 ~ 255 の範囲にする必要があります。 それ以外の場合、戻り値は、データ ソースに依存します。|  
|**CHAR_LENGTH (** _string_exp_ **)** (ODBC 3.0)|文字列式が文字データ型以外の場合は、文字列式の文字の長さを返しますそれ以外の場合、文字列式の (最小の整数 8 で割った値のビット数より小さくない) バイトの長さを返します。 (この関数は CHARACTER_LENGTH 関数と同じ) です。|  
|**CHARACTER_LENGTH(** _string_exp_ **)**  (ODBC 3.0)|文字列式が文字データ型以外の場合は、文字列式の文字の長さを返しますそれ以外の場合、文字列式の (最小の整数 8 で割った値のビット数より小さくない) バイトの長さを返します。 (この関数は CHAR_LENGTH 関数と同じ) です。|  
|**CONCAT(** _string_exp1_,_string_exp2_ **)**  (ODBC 1.0)|連結の結果である文字列を返します*string_exp2*に*string_exp1*します。 結果の文字列は DBMS に依存します。 たとえば、によって表される列*string_exp1*は NULL が SQL Server の戻り値は文字列を返す、NULL 以外、NULL 値を DB2 に含まれます。|  
|**相違点 (** _string_exp1_、_string_exp2_ **)** (ODBC 2.0)|SOUNDEX 関数によって返される値の差を示す整数値を返します*string_exp1*と*string_exp2*します。|  
|**挿入 (** _string_exp1_、*開始*、*長さ*、 _string_exp2_ **)** (ODBC 1.0)|場所を文字列で文字を返します*長さ*から削除された文字*string_exp1*で始まる、*開始*、場所と*string_exp2*が挿入されて*string_exp、* から始まる*開始*します。|  
|**LCASE (** _string_exp_ **)** (ODBC 1.0)|文字列を返します*string_exp*、すべて大文字の文字を小文字に変換します。|  
|**左 (** _string_exp_、_カウント_ **)** (ODBC 1.0)|返します、左端*カウント*の文字*string_exp*します。|  
|**長さ (** _string_exp_ **)** (ODBC 1.0)|内の文字の数を返します*string_exp、* 末尾の空白を除外します。<br /><br /> **長さ**のみの文字列を受け入れます。 このため変換は暗黙的に*string_exp*文字列、および戻り値 (データ型のサイズ内部ではなく) この文字列の長さにします。|  
|**LOCATE(** _string_exp1_, *string_exp2*[, *start*] **)** (ODBC 1.0)|最初に見つかった位置の開始位置を返します*string_exp1*内*string_exp2*します。 最初に出現する位置検索*string_exp1*内の最初の文字位置から始まります*string_exp2*しない限り、オプションの引数*開始*を指定します。 場合*開始*を指定すると、検索の値で指定された文字位置から始まります*開始*します。 最初の文字の位置で*string_exp2*は値 1 で示されます。 場合*string_exp1*内に見つからなかった*string_exp2*値 0 が返されます。<br /><br /> アプリケーションが使用して、検索スカラー関数を呼び出すことができるかどうか、 *string_exp1*、 *string_exp2*と*開始*ドライバーは、引数を返します SQL_FN_STR_LOCATE とき**SQLGetInfo**を呼び出すと、*オプション*SQL_STRING_FUNCTIONS の。 アプリケーションでのみ使用して、検索スカラー関数を呼び出すことができる場合、 *string_exp1*と*string_exp2*引数、ドライバーは SQL_FN_STR_LOCATE_2 を返しますと**SQLGetInfo**を呼び出すと、*オプション*SQL_STRING_FUNCTIONS の。 2 つまたは 3 つの引数を使用して、検索関数を呼び出すことをサポートするドライバーは、SQL_FN_STR_LOCATE と SQL_FN_STR_LOCATE_2 の両方を返します。|  
|**LTRIM (** _string_exp_ **)** (ODBC 1.0)|文字を返します*string_exp*に先行する空白を削除します。|  
|**OCTET_LENGTH (** _string_exp_ **)** (ODBC 3.0)|文字列式の長さ (バイト単位) を返します。 結果は、ビット数を 8 で割った値以上の最小の整数になります。<br /><br /> 文字列データ型に対してのみは機能は、変換は暗黙的にない*string_exp*文字列の代わりには、どのようなデータ型の (内部) のサイズを返します。|  
|**位置 (** _character_exp_ **IN** _character_exp_ **)** (ODBC 3.0)|2 番目の文字式には、最初の文字式の位置を返します。 結果は、実装定義の有効桁数と小数点以下を含みませんの正確な数値です。|  
|**繰り返し (** _string_exp、_ _カウント_ **)** (ODBC 1.0)|構成される文字列を返します*string_exp*繰り返し*カウント*時間。|  
|**REPLACE(** _string_exp1_, *string_exp2*, _string_exp3_ **)** (ODBC 1.0)|検索*string_exp1*の foroccurrences *string_exp2*、置き換えます*string_exp3*します。|  
|**右 (** _string_exp_、_カウント_ **)** (ODBC 1.0)|返します、右端*カウント*の文字*string_exp*します。|  
|**RTRIM (** _string_exp_ **)** (ODBC 1.0)|文字を返します*string_exp*の末尾に空白を削除します。|  
|**SOUNDEX (** _string_exp_ **)** (ODBC 2.0)|内の単語の発音を表すデータ ソースに依存する文字の文字列を返します*string_exp*します。 たとえば、SQL Server には 4 桁の SOUNDEX コード; が返されますOracle では、各単語の音声表現を返します。|  
|**容量 (** _カウント_ **)** (ODBC 2.0)|構成される文字列を返します*カウント*スペース。|  
|**部分文字列 (** _string_exp_、*開始*、長さ **)** (ODBC 1.0)|派生した文字列を返します*string_exp*を開始位置で指定した文字位置*開始*の*長さ*文字。|  
|**UCASE (** _string_exp_ **)** (ODBC 1.0)|文字列を返します*string_exp*、すべて小文字の文字を大文字に変換します。|
