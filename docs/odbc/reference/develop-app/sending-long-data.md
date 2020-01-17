---
title: 長い形式のデータの送信 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: acb4ff1637c1530527af88affaf437334596016b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094337"
---
# <a name="sending-long-data"></a>長い形式のデータの送信
Dbms 定義*長いデータ*として任意の文字または 254 文字などの特定のサイズを超えるバイナリ データ。 項目が、長いテキスト ドキュメントまたはビットマップを表す場合など、メモリ内の長い形式のデータ項目全体を格納できない可能性があります。 このようなデータは、1 つのバッファーに格納されることはできません、ため、データ ソース ドライバーに送信する、使用して、パーツで**SQLPutData**ステートメントが実行されるとします。 実行時にデータを送信するパラメーターと呼ばれる*実行時データ パラメーター*します。  
  
> [!NOTE]  
>  アプリケーションは実際に実行時にあらゆる種類のデータを送信**SQLPutData**部分の文字とバイナリ データのみを送信できます。 ただし、データが 1 つのバッファーに合わせて大きさの場合は、理由はありません一般的に使用する**SQLPutData**します。 バッファーをバインドし、バッファーからデータを取得、ドライバーで自動的にはるかに簡単になります。  
  
 アプリケーションを実行時にデータを送信するには、次の操作を実行します。  
  
1.  パラメーターを識別する 32 ビット値を渡す、 *ParameterValuePtr*引数**SQLBindParameter**バッファーのアドレスを渡すのではなく。 この値はドライバーによっては分析されません。 アプリケーションが意味する必要がありますので、後で、アプリケーションに返されるは。 たとえば、パラメーターの数またはデータを含むファイルのハンドルがあります。  
  
2.  長さ/インジケーター バッファーのアドレスを渡す、 *StrLen_or_IndPtr*の引数**SQLBindParameter**します。  
  
3.  SQL_DATA_AT_EXEC、SQL_LEN_DATA_AT_EXEC の結果を格納 (*長さ*) 長さ/インジケーター バッファー内のマクロ。 ドライバーに送信されるパラメーターのデータにこれらの値の両方を示す**SQLPutData**します。 SQL_LEN_DATA_AT_EXEC (*長さ*) を長い形式のデータのバイト数が送信されるため、領域を事前に知る必要があるデータ ソースを長い形式のデータを送信するときに使用します。 データ ソースは、この値を必要とする場合、アプリケーション呼び出しを確認する**SQLGetInfo** SQL_NEED_LONG_DATA_LEN オプションを使用します。 すべてのドライバーです。 このマクロをサポートする必要があります。データ ソースにバイトの長さを必要としない場合、ドライバーは無視できます。  
  
4.  呼び出し**SQLExecute**または**SQLExecDirect**します。 長さ/インジケーター バッファーには、SQL_DATA_AT_EXEC 値か、SQL_LEN_DATA_AT_EXEC の結果が含まれているドライバーを検出します (*長さ*) マクロと関数の戻り値として SQL_NEED_DATA を返します。  
  
5.  呼び出し**SQLParamData** SQL_NEED_DATA への応答値を返します。 長い形式のデータを送信する必要がある場合**SQLParamData** SQL_NEED_DATA を返します。 指すバッファーに、 *ValuePtrPtr*引数、ドライバーは、実行時データ パラメーターを識別する値を返します。 のデータを送信するのにパラメーターを決定するのに、アプリケーションがこの値を使用する必要があります 1 つ以上の実行時データ パラメーターがある場合ドライバーは、特定の順序で実行時データ パラメーターのデータを要求する必要はありません。  
  
6.  呼び出し**SQLPutData**ドライバーに、パラメーターのデータを送信します。 アプリケーションを呼び出す場合は、パラメーターのデータは、長い形式のデータの場合は、多くの場合とに 1 つのバッファーに収まらない、 **SQLPutData** ; の部分で、データを送信するには、繰り返しのデータを再構成するためのドライバーとデータ ソースの責任です。 アプリケーションが null で終わる文字列データを渡す場合、ドライバーまたはデータ ソースは、再構築プロセスの一環として null 終了文字を削除する必要があります。  
  
7.  呼び出し**SQLParamData**をすべてのパラメーターのデータ、送信されたことを示すためにもう一度です。 ドライバーが SQL_NEED_DATA と次のパラメーターを識別する値を返すデータが送信されていないすべての実行時データ パラメーターがある場合アプリケーションは、手順 6 を返します。 すべての実行時データ パラメーターのデータを送信すると、ステートメントが実行されます。 **SQLParamData**返します SQL_SUCCESS、SQL_SUCCESS_WITH_INFO やことができますを返す任意の戻り値または診断を**SQLExecute**または**SQLExecDirect**返すことができます。  
  
 後**SQLExecute**または**SQLExecDirect** SQL_NEED_DATA を返します、ステートメントが必要なデータの状態が最後の実行時データ パラメーターのデータが完全に送信されて、前にします。 ステートメントは、データの必要がある状態では、アプリケーションはのみ呼び出すことができます**SQLPutData**、 **SQLParamData**、 **SQLCancel**、 **SQLGetDiagField**、または**SQLGetDiagRec**; その他のすべての関数は、SQLSTATE HY010 を返す (関数のシーケンス エラーです)。 呼び出す**SQLCancel**ステートメントの実行をキャンセルし、前の状態に戻ります。 詳細については、次を参照してください[付録 b:。ODBC の状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)します。  
  
 実行時にデータを送信することの例は、次を参照してください。、 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)関数の説明。
