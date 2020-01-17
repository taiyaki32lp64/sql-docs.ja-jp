---
title: ステートメントを直接実行する (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statement execution
ms.assetid: b690f9de-66e1-4ee5-ab6a-121346fb5f85
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a5ece0a8b0e0844e8c33779796b0217ebf744050
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73781420"
---
# <a name="execute-a-statement-directly-odbc"></a>ステートメントの直接実行 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-execute-a-statement-directly-and-one-time-only"></a>ステートメントを直接一度だけ実行するには  
  
1.  ステートメントにパラメーターマーカーがある場合は、 [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)を使用して、各パラメーターをプログラム変数にバインドします。 プログラム変数にデータ値を入力してから、実行時データ パラメーターをセットアップします。  
  
2.  [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)を呼び出して、ステートメントを実行します。  
  
3.  実行時データ入力パラメーターが使用されている場合、 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)は SQL_NEED_DATA を返します。 [Sqlparamdata](https://go.microsoft.com/fwlink/?LinkId=58405)と[sqlparamdata](../../../relational-databases/native-client-odbc-api/sqlputdata.md)を使用して、データをチャンク単位で送信します。  

### <a name="to-execute-a-statement-multiple-times-by-using-column-wise-parameter-binding"></a>列方向のパラメーターのバインドを使用してステートメントを複数回実行するには  
  
1.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を呼び出して、次の属性を設定します。  
  
     SQL_ATTR_PARAMSET_SIZE に、パラメーターのセット数 (S) を設定します。  
  
     SQL_ATTR_PARAM_BIND_TYPE を SQL_PARAMETER_BIND_BY_COLUMN に設定します。  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR 属性を、処理されたパラメーターの数を格納する SQLUINTEGER 変数を指すように設定します。  
  
     パラメーターの状態インジケーターを保持する SQLUSSMALLINT 変数の配列 [S] をポイントするように SQL_ATTR_PARAMS_STATUS_PTR を設定します。  
  
2.  各パラメーター マーカーについて、次の操作を行います。  
  
     データ値を格納する S パラメーター バッファーの配列を割り当てます。  
  
     データの長さを格納する S パラメーター バッファーの配列を割り当てます。  
  
     [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)を呼び出して、パラメーターのデータ値とデータ長の配列をステートメントパラメーターにバインドします。  
  
     実行時データ テキストまたはイメージ パラメーターをセットアップします。  
  
     S データ値および S データの長さを、バインドされたパラメーター配列に置きます。  
  
3.  [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)を呼び出して、ステートメントを実行します。 ドライバーによって、S 回 (パラメーターのセットごとに 1 回) ステートメントが効率よく実行されます。  
  
4.  実行時データ入力パラメーターが使用されている場合、 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)は SQL_NEED_DATA を返します。 [Sqlparamdata](https://go.microsoft.com/fwlink/?LinkId=58405)と[sqlparamdata](../../../relational-databases/native-client-odbc-api/sqlputdata.md)を使用して、データをチャンク単位で送信します。  
  
### <a name="to-execute-a-statement-multiple-times-by-using-row-wise-parameter-binding"></a>行方向のパラメーターのバインドを使用してステートメントを複数回実行するには  
  
1.  構造体の配列[S] を割り当てます。この S は行パラメーターのセット数です。 構造体には各パラメーターについて 1 つの要素があり、各要素は次の 2 つの部分で構成されています。  
  
     最初の部分は、パラメーター データを格納する適切なデータ型の変数です。  
  
     2 つ目の部分は、状態インジケーターを格納する SQLINTEGER 変数です。  
  
2.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を呼び出して、次の属性を設定します。  
  
     SQL_ATTR_PARAMSET_SIZE に、パラメーターのセット数 (S) を設定します。  
  
     SQL_ATTR_PARAM_BIND_TYPE を、手順 1. で割り当てた構造体のサイズに設定します。  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR 属性を、処理されたパラメーターの数を格納する SQLUINTEGER 変数を指すように設定します。  
  
     パラメーターの状態インジケーターを保持する SQLUSSMALLINT 変数の配列 [S] をポイントするように SQL_ATTR_PARAMS_STATUS_PTR を設定します。  
  
3.  パラメーターマーカーごとに、 [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)を呼び出して、パラメーターのデータ値とデータ長のポインターが、手順 1. で割り当てた構造体の配列の最初の要素にある変数を指すようにします。 パラメーターが実行時データ パラメーターである場合は、そのパラメーターをセットアップします。  
  
4.  バインドされたパラメーターのバッファー配列にデータ値を入力します。  
  
5.  [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)を呼び出して、ステートメントを実行します。 ドライバーによって、S 回 (パラメーターのセットごとに 1 回) ステートメントが効率よく実行されます。  
  
6.  実行時データ入力パラメーターが使用されている場合、 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)は SQL_NEED_DATA を返します。 [Sqlparamdata](https://go.microsoft.com/fwlink/?LinkId=58405)と[sqlparamdata](../../../relational-databases/native-client-odbc-api/sqlputdata.md)を使用して、データをチャンク単位で送信します。  
  
 **メモ**列方向と行方向のバインドは、通常、 [SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)と[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)ではなく[sqlexecute](https://go.microsoft.com/fwlink/?LinkId=58400)と組み合わせて使用されます。  
  
## <a name="see-also"></a>参照  
 [クエリの実行方法に関する&#40;トピック ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
