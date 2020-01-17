---
title: 長い形式のデータ、SQLSetPos および SQLBulkOperations |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 578c85331a65c15cb25b5d9b75b7156ab509e910
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036411"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>長い形式のデータ、SQLSetPos および SQLBulkOperations
行の更新時に長いデータを送信できるように SQL ステートメントのパラメーターを持つ場合は、 **SQLBulkOperations**または**SQLSetPos**を持つ行を挿入するときに、または**SQLBulkOperations**. 複数回呼び出すと、パーツ内のデータが送信される**SQLPutData**します。 実行時にデータを送信する列と呼ばれる*実行時データ列*します。  
  
> [!NOTE]  
>  アプリケーションには実行時にあらゆる種類のデータを送信することが実際にできます。 **SQLPutData**、部分の文字とバイナリ データのみを送信できます。 ただし、データが 1 つのバッファーに合わせて大きさの場合は、理由はありません一般的に使用する**SQLPutData**します。 バッファーをバインドし、バッファーからデータを取得、ドライバーで自動的にはるかに簡単になります。  
  
 アプリケーションが呼び出す前に列をバインドする必要がありますので、通常の長いデータ列はバインドされていない、 **SQLBulkOperations**または**SQLSetPos**呼び出した後、これをアンバインドし、 **SQLBulkOperations**または**SQLSetPos**します。 に、列をバインドする必要があります**SQLBulkOperations**または**SQLSetPos**バインドされた列に対してのみ動作し、バインドされている必要がありますように**SQLGetData**データを取得するために使用できます列。  
  
 実行時にデータを送信するには、アプリケーションは、次を行います。  
  
1.  データ値ではなく、行セットのバッファーには、32 ビット値を配置します。 アプリケーションを使用すると、列の数やデータを含むファイルのハンドルなどの意味のある値に設定する必要がありますので、後で、アプリケーションにこの値が返されます。  
  
2.  SQL_LEN_DATA_AT_EXEC の結果に長さ/インジケーター バッファーの値を設定 (*長さ*) マクロです。 この値はドライバーに送信されるパラメーターのデータを示します。 **SQLPutData**します。 *長さ*長い形式のデータを長い形式のデータのバイト数が送信されるため、領域が事前に割り当てることを確認する必要があるデータ ソースに送信するときに値が使用されます。 データ ソースにこの値は、アプリケーション呼び出しが必要かどうかを判断する**SQLGetInfo** SQL_NEED_LONG_DATA_LEN オプションを使用します。 すべてのドライバーです。 このマクロをサポートする必要があります。データ ソースにバイトの長さを必要としない場合、ドライバーは無視できます。  
  
3.  呼び出し**SQLBulkOperations**または**SQLSetPos**します。 長さ/インジケーター バッファーが、SQL_LEN_DATA_AT_EXEC の結果が含まれているドライバーを検出します (*長さ*) マクロと関数の戻り値として SQL_NEED_DATA を返します。  
  
4.  呼び出し**SQLParamData** SQL_NEED_DATA への応答値を返します。 長い形式のデータを送信する必要がある場合**SQLParamData** SQL_NEED_DATA を返します。 指すバッファーに、 *ValuePtrPtr*引数、ドライバーは、行セットのバッファーに、アプリケーションが配置されて一意の値を返します。 アプリケーションが; のデータを送信する列を決定する値を使用して 1 つ以上の実行時データ列がある場合ドライバーは、特定の順序で実行時データ列のデータを要求する必要はありません。  
  
5.  呼び出し**SQLPutData**ドライバーに列のデータを送信します。 アプリケーションを呼び出す場合は、列のデータは、長い形式のデータの場合は、多くの場合とに 1 つのバッファーに収まらない、 **SQLPutData** ; の部分で、データを送信するには、繰り返しのデータを再構成するためのドライバーとデータ ソースの責任です。 アプリケーションが null で終わる文字列データを渡す場合、ドライバーまたはデータ ソースは、再構築プロセスの一環として null 終了文字を削除する必要があります。  
  
6.  呼び出し**SQLParamData**をすべての列のデータ、送信されたことを示すためにもう一度です。 ドライバーが SQL_NEED_DATA と、次の実行時データ列の一意の値を返しますのデータが送信されていないすべての実行時データ列がある場合アプリケーションは、手順 5 を返します。 すべての実行時データ列のデータが送信された場合は、行のデータがデータ ソースに送信されます。 **SQLParamData** SQL_SUCCESS、SQL_SUCCESS_WITH_INFO やことができますを返します。 返す任意の SQLSTATE を**SQLBulkOperations**または**SQLSetPos**返すことができます。  
  
 後**SQLBulkOperations**または**SQLSetPos** SQL_NEED_DATA を返しますと、データが最後の実行時データ列を完全に送信される前にステートメントが必要なデータの状態。 この状態で、アプリケーションはのみ呼び出すことができます**SQLPutData**、 **SQLParamData**、 **SQLCancel**、 **SQLGetDiagField**、または**SQLGetDiagRec**; その他のすべての関数は、SQLSTATE HY010 を返す (関数のシーケンス エラーです)。 呼び出す**SQLCancel**ステートメントの実行をキャンセルし、前の状態に戻ります。 詳細については、次を参照してください[付録 b:。ODBC の状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)します。
