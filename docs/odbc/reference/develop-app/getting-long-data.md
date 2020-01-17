---
title: 長い形式のデータの取得 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 49f0023f726dd4bb290ffba1018ce2608800dd90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216366"
---
# <a name="getting-long-data"></a>長い形式のデータの取得
Dbms 定義*長いデータ*として任意の文字または 255 文字などの特定のサイズを超えるバイナリ データ。 このデータは、数千のいくつかの文字の部分の説明などの 1 つのバッファーに格納するのに十分な小さ可能性があります。 ただし、長いテキスト ドキュメントやビットマップなどのメモリに格納するには長すぎる場合があります。 使用して、パーツ内のドライバーから取得されるこのようなデータは、1 つのバッファーに格納されることはできません、ため**SQLGetData**行の他のデータがフェッチされた後にします。  
  
> [!NOTE]  
>  アプリケーションが任意の種類のデータを実際に取得**SQLGetData**部分の文字とバイナリ データだけを取得できますが、データを長いだけでなく。 ただし、データが 1 つのバッファーに合わせて大きさの場合は、理由はありません一般的に使用する**SQLGetData**します。 バッファーを列にバインドし、バッファー内のデータを返す、ドライバーで自動的にはるかに簡単になります。  
  
 アプリケーションの最初の呼び出しを長い形式のデータを列から取得する**SQLFetchScroll**または**SQLFetch**を行に移動し、データ バインドされた列をフェッチします。 その後、アプリケーションを呼び出す**SQLGetData**します。 **SQLGetData**として同じ引数を持つ**SQLBindCol**: ステートメント ハンドル; 列番号、アプリケーション変数; の C データ型、アドレス、およびバイト長と長さ/インジケーター バッファーのアドレス。 どちらの関数は、基本的に同じタスクを実行するために、同じ引数を指定します。ドライバーをアプリケーション変数について説明しますと、その変数に特定の列のデータを返すことを指定します。 主な違いが**SQLGetData**行がフェッチされた後に呼び出される (とも呼ば*遅延バインディング*この理由で) で、バインドが指定されていると**SQLGetData**は呼び出しの期間だけ継続します。  
  
 1 つの列に関する**SQLGetData**のように動作**SQLFetch**:列のデータを取得、アプリケーション変数の型に変換し、その変数に返します。 長さ/インジケーター バッファー内のデータのバイト長も返します。 方法の詳細について**SQLFetch**のデータを返しますを参照してください[行のデータのフェッチ](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)します。  
  
 **SQLGetData**異なります**SQLFetch** 1 つの重要な点でします。 呼び出された場合は複数回連続して、同じ列に、各呼び出しは、データの連続する部分を返します。 各呼び出しの最後の呼び出しを除く返しますから SQL_SUCCESS_WITH_INFO と SQLSTATE 01004 (文字列データの適切な切り捨てられました)。最後の呼び出しは関係なく SQL_SUCCESS を返します。 これは、どのように**SQLGetData**部分で長い形式のデータを取得するために使用します。 戻るには、データがある場合に**SQLGetData** sql_no_data が返されます。 アプリケーションは、長い形式のデータを編成するため、データの部分を連結することを意味する可能性があります。 各部分では、null で終わります。パーツを連結する場合、アプリケーションは、null 終了文字を削除する必要があります。 ブックマークを他の長い形式のデータの場合と同様に可変長の部分でのデータの取得を実行できます。 ドライバーを使用できるデータの量を見つけて、SQL_NO_TOTAL バイトの長さを返すことができないが一般的ですが、前の呼び出しで返されるバイト数で各呼び出しの長さ/インジケーター バッファーの増減に返される値。 以下に例を示します。  
  
```  
// Declare a binary buffer to retrieve 5000 bytes of data at a time.  
SQLCHAR       BinaryPtr[5000];  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd, BinaryLenOrInd, NumBytes;  
SQLRETURN     rc;   
SQLHSTMT      hstmt;  
  
// Create a result set containing the ID and picture of each part.  
SQLExecDirect(hstmt, "SELECT PartID, Picture FROM Pictures", SQL_NTS);  
  
// Bind PartID to the PartID column.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &PartID, 0, &PartIDInd);  
  
// Retrieve and display each row of data.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // Display the part ID and initialize the picture.  
   DisplayID(PartID, PartIDInd);  
   InitPicture();  
  
   // Retrieve the picture data in parts. Send each part and the number   
   // of bytes in each part to a function that displays it. The number   
   // of bytes is always 5000 if there were more than 5000 bytes   
   // available to return (cbBinaryBuffer > 5000). Code to check if   
   // rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLGetData(hstmt, 2, SQL_C_BINARY, BinaryPtr, sizeof(BinaryPtr),  
                           &BinaryLenOrInd)) != SQL_NO_DATA) {  
      NumBytes = (BinaryLenOrInd > 5000) || (BinaryLenOrInd == SQL_NO_TOTAL) ?  
                  5000 : BinaryLenOrInd;  
      DisplayNextPictPart(BinaryPtr, NumBytes);  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 使用していくつかの制限がある**SQLGetData**します。 一般に、列にアクセスで**SQLGetData**:  
  
-   列番号を昇順 (データ ソースから結果セットの列を読み取る方法) が原因でアクセスする必要があります。 呼び出すとエラーはたとえば、 **SQLGetData**列 5 の 4 列目にしを呼び出す。  
  
-   バインドすることはできません。  
  
-   最後のバインドされた列よりも高い列番号が必要です。 たとえば、最後のバインドされた列が列 3 の場合を呼び出すとエラー **SQLGetData**列 2 にします。 このため、アプリケーションが、選択リストの最後に、長い形式のデータ列を配置することを確認してください。  
  
-   場合に使用することはできません**SQLFetch**または**SQLFetchScroll**を 1 つ以上の行の取得が呼び出されました。 詳細については、次を参照してください。[ブロック カーソルを使用して](../../../odbc/reference/develop-app/using-block-cursors.md)します。  
  
 一部のドライバーでは、これらの制限は適用されません。 相互運用可能なアプリケーションには、存在か制限が呼び出すことによって適用されませんを決定するかを想定する必要があります**SQLGetInfo** SQL_GETDATA_EXTENSIONS オプションを使用します。  
  
 アプリケーションが文字またはバイナリ データ列のすべてのデータを不要な場合、ステートメントを実行する前に、SQL_ATTR_MAX_LENGTH ステートメント属性を設定 DBMS ベースのドライバーでのネットワーク トラフィックを削減できます。 これは、任意の文字またはバイナリ列に返されるデータのバイト数を制限します。 たとえば、列には、長いテキスト ドキュメントが含まれているとします。 この列を含むテーブルを参照するアプリケーションは、各ドキュメントの最初のページのみを表示する必要があります。 ドライバーでは、このステートメント属性をシミュレートできます、ですが、これを行う理由はありません。 具体的には、アプリケーションを文字またはバイナリ データを切り捨てる場合にする必要がありますバインド小さなバッファー列に**SQLBindCol**させて、ドライバー、データを切り捨てます。
