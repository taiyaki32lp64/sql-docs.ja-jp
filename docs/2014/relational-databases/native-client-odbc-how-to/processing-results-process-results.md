---
title: 計算 (ODBC) の処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- processing results [ODBC]
ms.assetid: 4810fe3f-78ee-4f0d-8bcc-a4659fbcf46f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21474aed83aac1fe86e2242b1238affa11ae64a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200318"
---
# <a name="process-results-odbc"></a>結果の処理 (ODBC)
    
### <a name="to-process-results"></a>結果を処理するには  
  
1.  結果セットの情報を取得します。  
  
2.  バインドされた列が使用されている場合は、バインド先の列ごとに[SQLBindCol](../native-client-odbc-api/sqlbindcol.md) を呼び出して、プログラム バッファーを列にバインドします。  
  
3.  結果セット内の各行に対して次の操作を行います。  
  
    -   [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) を呼び出して次の行を取得します。  
  
    -   バインドされた列が使用されている場合は、バインドされた列のバッファー内で現在使用可能なデータを使用します。  
  
    -   バインドされていない列が使用されている場合は、[SQLGetData](../native-client-odbc-api/sqlgetdata.md) を 1 回以上呼び出して、バインドされている最後の列の後に、バインドされていない列のデータを取得します。 呼び出す`SQLGetData`列番号の昇順である必要があります。  
  
    -   `SQLGetData` を複数回呼び出して、text または image 列からデータを取得します。  
  
4.  [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) が SQL_NO_DATA を返すことによって結果セットの終了を示したら、[SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) を呼び出して、使用可能な結果セットが他にあるかどうかを確認します。  
  
    -   SQL_SUCCESS が返された場合は、別の結果セットを使用できます。  
  
    -   SQL_NO_DATA が返された場合は、他に使用できる結果セットはありません。  
  
    -   SQL_SUCCESS_WITH_INFO または SQL_ERROR が返された場合は、[SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) を呼び出して、PRINT ステートメントまたは RAISERROR ステートメントからの出力が使用可能かどうかを確認します。  
  
         バインドされたステートメントのパラメーターが出力パラメーターまたはストアド プロシージャの戻り値に使用されている場合は、バインドされたパラメーターのバッファーでデータを使用できるようになります。 バインドされたパラメーターが使用される場合は、[SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) または [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) への各呼び出しで、SQL ステートメントが *S* 回実行されます。*S* は、バインドされたパラメーターの配列内にある要素の数です。 つまり、処理する結果のセットが *S* 個あることを意味します。これらの結果の各セットには、結果セット、出力パラメーター、および通常 SQL ステートメントの 1 回の実行で返されるリターン コードがすべて含まれます。  
  
    > [!NOTE]  
    >  結果セットに計算行が含まれている場合、各計算行は個々の結果セットとして使用できるようになります。 これらの計算結果セットは標準行内に点在し、標準行は複数の結果セットに分割されます。  
  
5.  必要に応じて、SQL_UNBIND を使用して [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) を呼び出し、バインドされた列バッファーを解放します。  
  
6.  別の結果セットが使用できる場合は、手順 1 に戻ります。  
  
> [!NOTE]  
>  [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) によって SQL_NO_DATA が返される前に結果セットの処理を取り消すには、[SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md) を呼び出します。  
  
## <a name="see-also"></a>参照  
 [結果の操作方法に関するトピックを処理&#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  
