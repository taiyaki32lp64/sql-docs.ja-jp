---
title: 高速順方向専用カーソル (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc07980dfe78bb22c6281b19d8684d846f8a8db1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902437"
---
# <a name="fast-forward-only-cursors-odbc"></a>高速順方向専用カーソル (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  インスタンスに接続されているときに[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、順方向専用かつ読み取り専用のカーソルのパフォーマンスの最適化をサポートしています。 高速順方向専用カーソルは、既定の結果セットに類似した方法で、ドライバーとサーバーによって内部的に実装されます。 高速順方向専用カーソルには、パフォーマンスが高いこと以外にも、次のような特性があります。  
  
-   [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)はサポートされていません。 結果セットの列を、プログラム変数にバインドする必要があります。  
  
-   サーバーはカーソルの最後に達したことを検出すると、そのカーソルを自動的に閉じます。 アプリケーションを呼び出す必要がありますも[SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)または[SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE) ドライバーがサーバーにクローズ要求を送信する必要はありませんが。 この動作により、ネットワーク経由でのサーバーとのやり取りが抑えられます。  
  
 アプリケーションでは、ドライバー固有のステートメント属性 SQL_SOPT_SS_CURSOR_OPTIONS を使用して高速順方向専用カーソルを要求します。 SQL_SOPT_SS_CURSOR_OPTIONS 属性に SQL_CO_FFO を設定すると、高速順方向専用カーソルが有効になりますが、autofetch オプションは有効になりません。 SQL_CO_FFO_AF を設定すると、autofetch オプションも有効になります。 Autofetch オプションの詳細については、次を参照してください。 [Autofetch と ODBC カーソル](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md)します。  
  
 autofetch オプションを有効にした高速順方向専用カーソルは、サーバーとのやり取りを 1 度だけ行って小さい結果セットを取得する場合に使用できます。 次の手順で*n*返される行の数です。  
  
1.  SQL_SOPT_SS_CURSOR_OPTIONS を SQL_CO_FFO_AF に設定します。  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE を設定*n* + 1 です。  
  
3.  配列に結果列をバインド*n* + 1 の要素 (安全場合*n* + 1 行が実際にフェッチされた)。  
  
4.  いずれかにカーソルをオープン**SQLExecDirect**または**SQLExecute**します。  
  
5.  戻り値の状態が SQL_SUCCESS の場合は、呼び出して**SQLFreeStmt**または**SQLCloseCursor**カーソルを閉じます。 行のすべてのデータが、バインドされたプログラム変数に格納されます。  
  
 これらの手順により、 **SQLExecDirect**または**SQLExecute** autofetch オプションを有効にして、カーソルを開く要求を送信します。 クライアントからこの要求を 1 つ受け取ると、サーバーでは次の手順が実行されます。  
  
-   カーソルを開きます。  
  
-   結果セットを作成してクライアントに行を送信します。  
  
-   行セットのサイズを結果セットの行数よりも 1 だけ多いサイズに設定したので、サーバーでカーソルが最後まで達したことが検出され、そのカーソルが閉じられます。  
  
## <a name="see-also"></a>参照  
 [カーソル プログラミングの詳細&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
