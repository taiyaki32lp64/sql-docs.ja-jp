---
title: 結果データのフェッチ |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLFetchScroll function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], fetching
- SQLBindCol function
- result sets [ODBC], fetching
- fetching [ODBC]
- ODBC data types, fetching
- SQLFetch function
- SQL Server Native Client ODBC driver, data types
- SQLGetData function
ms.assetid: b289c7fb-5017-4d7e-a2d3-19401e9fc4cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b803ca3742f9cb831e51105aab9d0ed75ad78e16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200083"
---
# <a name="fetching-result-data"></a>結果データのフェッチ
  ODBC アプリケーションでは、結果データのフェッチを 3 つの方法で実行できます。  
  
 最初のオプションがに基づいて[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)します。 アプリケーションを使用して、結果のフェッチを設定する前に**SQLBindCol**プログラム変数に結果セットの各列にバインドします。 変数に現在の行のデータが結果セット列にバインドされているドライバーの転送時間アプリケーション呼び出しの後、列がバインドされたら、 **SQLFetch**または[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)します。 結果セット列のデータ型とプログラム変数のデータ型が異なる場合、ドライバーによってデータ変換が処理されます。 呼び出すたびに入力されるすべての変数の配列に結果の列をバインドできるアプリケーションに SQL_ATTR_ROW_ARRAY_SIZE に 1 より大きい設定がある場合は、 **SQLFetchScroll**します。  
  
 2 番目のオプションがに基づいて[SQLGetData](../native-client-odbc-api/sqlgetdata.md)します。 アプリケーションが使用しない**SQLBindCol**結果をバインドする列をプログラム変数に設定します。 呼び出すたび**SQLFetch**、アプリケーション呼び出し**SQLGetData** 1 回、結果の各列に対して設定します。 **SQLGetData**特定のプログラム変数に特定の結果セット列からデータを転送するドライバーに指示し、列と変数のデータ型を指定します。 そのため、結果列のデータ型とプログラム変数のデータ型が異なる場合は、ドライバーでデータを変換できます。 **テキスト**、 **ntext**、および**イメージ**列はプログラム変数よりも大きく、通常を使用して取得できます**SQLGetData**します。 場合、**テキスト**、 **ntext**、または**イメージ**結果列のデータが、プログラム変数よりも大きい**SQLGetData** SQL_SUCCESS_ を返しますWITH_INFO と SQLSTATE 01004 (文字列データの右側が切り捨てられました)。 連続して呼び出す**SQLGetData**の連続したチャンクを返す、**テキスト**または**イメージ**データ。 データの末尾に達すると、 **SQLGetData** SQL_SUCCESS を返します。 SQL_ATTR_ROW_ARRAY_SIZE に 1 よりも大きい値を指定すると、フェッチのたびに行セットが返されます。 使用する前に**SQLGetData**、最初に使用する必要があります**SQLSetPos**を現在の行として行セット内の特定の行を指定します。  
  
 3 番目のオプションは、の組み合わせを使用する**SQLBindCol**と**SQLGetData**します。 アプリケーションは、でしたし、たとえば、結果セットの最初の 10 個の列をバインドし、フェッチのたびに呼び出す**SQLGetData** 3 回の 3 つのバインドされていない列からデータを取得します。 これは通常、使用、結果セットには、1 つまたは複数が含まれている場合**テキスト**または**イメージ**列。  
  
 カーソル オプションに応じて、結果セットの設定、アプリケーション オプションも使用できます、スクロールの**SQLFetchScroll**結果セットをスクロールします。  
  
 使用、余分な**SQLBindCol**セットの列をプログラム変数には、高価な結果をバインドするため、 **SQLBindCol**によりメモリの割り当てに ODBC ドライバー。 いずれかが呼び出されるまでそのバインドが有効になります変数に結果列をバインドするときに[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)を呼び出し、ステートメント ハンドルを解放する[SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md)で*fOption*を SQL_UNBIND に設定します。 バインドは、ステートメントが完了しても自動的には元に戻りません。  
  
 このロジックにより、異なるパラメーターを指定して同じ SELECT ステートメントを何度も実行することで、効率を上げることができます。 結果セットは、同じ構造を保持するため、結果セットのバインドを 1 回、すべての SELECT ステートメントを処理し、呼び出す**SQLFreeStmt**で*fOption*前回の実行後、SQL_UNBIND に設定します。 呼び出す必要はありません**SQLBindCol**結果セットを最初に呼び出さずに、列をバインドする**SQLFreeStmt**で*fOption* SQL_UNBIND に設定すると、それまでのバインドを解放します。  
  
 使用する場合**SQLBindCol**、行方向または列方向のバインドも実行できます。 行方向のバインドの方が、列方向のバインドよりも処理がやや高速になります。  
  
 使用することができます**SQLGetData**結果のバインドではなく列単位ごとにデータを取得する設定を使用して列**SQLBindCol**します。 結果セットに数行のみが含まれている場合を使用して**SQLGetData**の代わりに**SQLBindCol**が高速。 それ以外**SQLBindCol**最適なパフォーマンスが得られます。 常にデータを変数の同じセットに配置はない場合は使用**SQLGetData**常に再バインドの代わりにします。 のみ使用できます**SQLGetData**列ですべての列をバインドした後、選択リスト内を**SQLBindCol**します。 列は既に使用したすべての列の後に表示する必要がありますも**SQLGetData**します。  
  
 ODBC 関数のデータの移動、プログラム変数の内外になどを処理する**SQLGetData**、 **SQLBindCol**、および[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)、暗黙的なデータ型のサポート変換を行います。 たとえば、整数列を文字列プログラム変数にバインドするアプリケーションでは、プログラム変数にデータを格納する前に、ドライバーが自動的にそのデータを整数から文字に変換します。  
  
 アプリケーションでのデータ変換は最小限に抑える必要があります。 列やパラメーターは、アプリケーションでの処理にデータ変換が必要な場合を除き、同じデータ型のプログラム変数にバインドする必要があります。 ただし、あるデータ型から別のデータ型に変換する必要がある場合は、アプリケーションでのデータ変換よりもドライバーによるデータ変換の方が効率的です。 通常、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、ネットワーク バッファーからアプリケーションの変数にデータを直接転送します。 データ変換を行うようにドライバーに要求すると、ドライバーはデータをバッファーに格納し、CPU サイクルを使用してデータを変換します。  
  
 プログラム変数を除く、列から転送されたデータを保持するのに十分な大きさにする必要があります**テキスト**、 **ntext**、および**イメージ**データ。 結果セットのデータを取得してそのデータを変数に格納するときに、その変数が小さすぎてデータを保持できない場合、ドライバーは警告を生成します。 その結果、ドライバーでは警告メッセージ用のメモリを割り当て、ドライバーとアプリケーションの両方で、警告メッセージの処理やエラーの処理に CPU サイクルが必要になります。 アプリケーションでは、取得するデータを保持するのに十分なサイズの変数を割り当てるか、選択リストで SUBSTRING 関数を使用して結果セット内の列のサイズを小さくする必要があります。  
  
 SQL_C_DEFAULT を使用して C 変数のデータ型を指定する場合は注意が必要です。 SQL_C_DEFAULT は、C 変数のデータ型と、列やパラメーターの SQL データ型を一致させることを指定します。 SQL_C_DEFAULT が指定されている場合、 **ntext**、 **nchar**、または**nvarchar**列で、Unicode データは、アプリケーションに返されます。 そのため、アプリケーションが Unicode データを処理するようにコーディングされていないと、さまざまな問題が発生する可能性があります。 同じ種類の問題が発生する、 **uniqueidentifier** (SQL_GUID) データ型。  
  
 **テキスト**、 **ntext**、および**イメージ**データが大きすぎて、単一のプログラム変数に通常と処理は通常**SQLGetData**の代わりに**SQLBindCol**します。 サーバー カーソルを使用する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーにバインドされていないため、データを転送しないように最適化された**テキスト**、 **ntext**、または**イメージ**列で、行をフェッチした時刻。 **テキスト**、 **ntext**、または**イメージ**データは実際には取得されません、サーバーからアプリケーションの問題まで**SQLGetData**用、列です。  
  
 この最適化は、アプリケーションに適用できるようにありません**テキスト**、 **ntext**、または**イメージ**ユーザーがカーソルを上下にスクロール中にデータが表示されます。 アプリケーションを呼び出して、ユーザーが行を選択後**SQLGetData**を取得する、**テキスト**、 **ntext**、または**イメージ**データ。 転送、**テキスト**、 **ntext**、または**イメージ**のどの行のデータ、ユーザーは選択を解除して、非常に大量のデータの送信を節約できます。  
  
## <a name="see-also"></a>参照  
 [結果の処理&#40;ODBC&#41;](processing-results-odbc.md)  
  
  
