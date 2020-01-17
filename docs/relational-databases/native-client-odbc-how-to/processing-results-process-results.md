---
title: 結果の処理 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- processing results [ODBC]
ms.assetid: 4810fe3f-78ee-4f0d-8bcc-a4659fbcf46f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ebd41c30d72b86fe5344a15767648371a14f7a2f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73780910"
---
# <a name="processing-results---process-results"></a>結果の処理 - 処理結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

ODBC アプリケーションでの結果の処理では、最初に結果セットの特性を判断し、次に[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)または[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)のいずれかを使用してプログラム変数にデータを取得します。  
  
### <a name="to-process-results"></a>結果を処理するには  
  
1.  結果セットの情報を取得します。  
  
2.  バインドされた列が使用されている場合は、バインド先の列ごとに[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) を呼び出して、プログラム バッファーを列にバインドします。  
  
3.  結果セット内の各行に対して次の操作を行います。  
  
    -   [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) を呼び出して次の行を取得します。  
  
    -   バインドされた列が使用されている場合は、バインドされた列のバッファー内で現在使用可能なデータを使用します。  
  
    -   バインドされていない列が使用されている場合は、[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) を 1 回以上呼び出して、バインドされている最後の列の後に、バインドされていない列のデータを取得します。 **SQLGetData** の呼び出しは、列番号の昇順にする必要があります。  
  
    -   **SQLGetData** を複数回呼び出して、text または image 列からデータを取得します。  
  
4.  [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) が SQL_NO_DATA を返すことによって結果セットの終了を示したら、[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) を呼び出して、使用可能な結果セットが他にあるかどうかを確認します。  
  
    -   SQL_SUCCESS が返された場合は、別の結果セットを使用できます。  
  
    -   SQL_NO_DATA が返された場合は、他に使用できる結果セットはありません。  
  
    -   SQL_SUCCESS_WITH_INFO または SQL_ERROR が返された場合は、[SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) を呼び出して、PRINT ステートメントまたは RAISERROR ステートメントからの出力が使用可能かどうかを確認します。  
  
         バインドされたステートメントのパラメーターが出力パラメーターまたはストアド プロシージャの戻り値に使用されている場合は、バインドされたパラメーターのバッファーでデータを使用できるようになります。 バインドされたパラメーターが使用される場合は、[SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) または [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) への各呼び出しで、SQL ステートメントが *S* 回実行されます。*S* は、バインドされたパラメーターの配列内にある要素の数です。 つまり、処理する結果のセットが *S* 個あることを意味します。これらの結果の各セットには、結果セット、出力パラメーター、および通常 SQL ステートメントの 1 回の実行で返されるリターン コードがすべて含まれます。  
  
    > [!NOTE]  
    >  結果セットに計算行が含まれている場合、各計算行は個々の結果セットとして使用できるようになります。 これらの計算結果セットは標準行内に点在し、標準行は複数の結果セットに分割されます。  
  
5.  必要に応じて、SQL_UNBIND を使用して [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) を呼び出し、バインドされた列バッファーを解放します。  
  
6.  別の結果セットが使用できる場合は、手順 1 に戻ります。  

> [!NOTE]  
>  [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) によって SQL_NO_DATA が返される前に結果セットの処理を取り消すには、[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md) を呼び出します。  
  
## <a name="see-also"></a>参照  
[結果セットの情報&#40;の取得 ODBC&#41;](../../relational-databases/native-client-odbc-how-to/processing-results-retrieve-result-set-information.md)   
  
  
