---
title: 行セットのバインドの使用 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 542834d73cdea5a985ea6926d011f1db4711f3e5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73781514"
---
# <a name="use-rowset-binding-odbc"></a>行セットのバインドの使用 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-use-column-wise-binding"></a>列方向のバインドを使用するには  
  
1.  バインドされた各列で、次の操作を行います。  
  
    -   データ値を格納するための R 個以上の列バッファーの配列を割り当てます。R は行セット内の行の数です。  
  
    -   必要に応じて、データ長を格納するための R 個以上の列バッファーの配列を割り当てます。  
  
    -   [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md)を呼び出して、列のデータ値とデータ長の配列を行セットの列にバインドします。  
  
2.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を呼び出して、次の属性を設定します。  
  
    -   SQL_ATTR_ROW_ARRAY_SIZE を、行セットの行の数 (R) に設定します。  
  
    -   SQL_ATTR_ROW_BIND_TYPE を SQL_BIND_BY_COLUMN に設定します。  
  
    -   SQL_ATTR_ROWS FETCHED_PTR 属性を、フェッチされた行の数を格納する SQLUINTEGER 変数を指すように設定します。  
  
    -   SQL_ATTR_ROW_STATUS_PTR を、行状態インジケーターを格納する SQLUSSMALLINT 変数の配列 [R] を指すように設定します。  
  
3.  ステートメントを実行します。  
  
4.  [Sqlfetch](https://go.microsoft.com/fwlink/?LinkId=58401)または[sqlfetchscroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)を呼び出すたびに R 行が取得され、データがバインドされた列に転送されます。  

### <a name="to-use-row-wise-binding"></a>行方向のバインドを使用するには  
  
1.  構造体の配列 [R] を割り当てます。この R は行セット内の行数です。 構造体には各列について 1 つの要素があり、各要素は 2 つの部分で構成されています。  
  
    -   最初の部分は、列データを格納する適切なデータ型の変数です。  
  
    -   2 つ目の部分は、列状態インジケーターを格納する SQLINTEGER 変数です。  
  
2.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を呼び出して、次の属性を設定します。  
  
    -   SQL_ATTR_ROW_ARRAY_SIZE を、行セットの行の数 (R) に設定します。  
  
    -   SQL_ATTR_ROW_BIND_TYPE を、手順 1. で割り当てた構造体のサイズに設定します。  
  
    -   SQL_ATTR_ROWS_FETCHED_PTR 属性を、フェッチされた行の数を格納する SQLUINTEGER 変数を指すように設定します。  
  
    -   SQL_ATTR_PARAMS_STATUS_PTR を、行状態インジケーターを格納する SQLUSSMALLINT 変数の配列 [R] を指すように設定します。  
  
3.  結果セットの各列に対して、 [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md)を呼び出して、列のデータ値とデータ長のポインターが、手順 1. で割り当てられた構造体の配列の最初の要素にある変数を指すようにします。  
  
4.  ステートメントを実行します。  
  
5.  [Sqlfetch](https://go.microsoft.com/fwlink/?LinkId=58401)または[sqlfetchscroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)を呼び出すたびに R 行が取得され、データがバインドされた列に転送されます。  
  
## <a name="see-also"></a>参照  
 [カーソルの使用方法に関する&#40;トピック&#41; ODBC](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)   
 [カーソルの実装方法](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [カーソル&#40;を使用する ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/use-cursors-odbc.md)  
  
  
