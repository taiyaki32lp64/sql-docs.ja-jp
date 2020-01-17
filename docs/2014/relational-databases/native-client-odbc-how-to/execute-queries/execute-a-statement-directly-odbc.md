---
title: ステートメントの直接 (ODBC) の実行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statement execution
ms.assetid: b690f9de-66e1-4ee5-ab6a-121346fb5f85
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0597054914dcbce7e7b1fb1475beb29bab7b8a57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200401"
---
# <a name="execute-a-statement-directly-odbc"></a>ステートメントの直接実行 (ODBC)
    
### <a name="to-execute-a-statement-directly-and-one-time-only"></a>ステートメントを直接一度だけ実行するには  
  
1.  使用して、ステートメントにパラメーター マーカーがある場合は、 [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md)各パラメーターをプログラム変数にバインドします。 プログラム変数にデータ値を入力してから、実行時データ パラメーターをセットアップします。  
  
2.  呼び出す[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)ステートメントを実行します。  
  
3.  実行時データ入力パラメーターを使用している場合[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) SQL_NEED_DATA を返します。 使用して、データをチャンク単位で送信[SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405)と[SQLPutData](../../native-client-odbc-api/sqlputdata.md)します。  
  
### <a name="to-execute-a-statement-multiple-times-by-using-column-wise-parameter-binding"></a>列方向のパラメーターのバインドを使用してステートメントを複数回実行するには  
  
1.  呼び出す[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)次の属性を設定します。  
  
     SQL_ATTR_PARAMSET_SIZE に、パラメーターのセット数 (S) を設定します。  
  
     SQL_ATTR_PARAM_BIND_TYPE を SQL_PARAMETER_BIND_BY_COLUMN に設定します。  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR 属性を、処理されたパラメーターの数を格納する SQLUINTEGER 変数を指すように設定します。  
  
     Sql_attr_params_status_ptr をパラメーターの状態インジケーターを格納する SQLUSSMALLINT 変数の配列 [S] を指すように設定します。  
  
2.  各パラメーター マーカーについて、次の操作を行います。  
  
     データ値を格納する S パラメーター バッファーの配列を割り当てます。  
  
     データの長さを格納する S パラメーター バッファーの配列を割り当てます。  
  
     呼び出す[SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md)パラメーター データの値とデータ長の配列をステートメント パラメーターにバインドします。  
  
     実行時データ テキストまたはイメージ パラメーターをセットアップします。  
  
     S データ値および S データの長さを、バインドされたパラメーター配列に置きます。  
  
3.  呼び出す[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)ステートメントを実行します。 ドライバーによって、S 回 (パラメーターのセットごとに 1 回) ステートメントが効率よく実行されます。  
  
4.  実行時データ入力パラメーターを使用している場合[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) SQL_NEED_DATA を返します。 使用して、データをチャンク単位で送信[SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405)と[SQLPutData](../../native-client-odbc-api/sqlputdata.md)します。  
  
### <a name="to-execute-a-statement-multiple-times-by-using-row-wise-parameter-binding"></a>行方向のパラメーターのバインドを使用してステートメントを複数回実行するには  
  
1.  構造体の配列[S] を割り当てます。この S は行パラメーターのセット数です。 構造体には各パラメーターについて 1 つの要素があり、各要素は次の 2 つの部分で構成されています。  
  
     最初の部分は、パラメーター データを格納する適切なデータ型の変数です。  
  
     2 つ目の部分は、状態インジケーターを格納する SQLINTEGER 変数です。  
  
2.  呼び出す[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)次の属性を設定します。  
  
     SQL_ATTR_PARAMSET_SIZE に、パラメーターのセット数 (S) を設定します。  
  
     SQL_ATTR_PARAM_BIND_TYPE を、手順 1. で割り当てた構造体のサイズに設定します。  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR 属性を、処理されたパラメーターの数を格納する SQLUINTEGER 変数を指すように設定します。  
  
     Sql_attr_params_status_ptr をパラメーターの状態インジケーターを格納する SQLUSSMALLINT 変数の配列 [S] を指すように設定します。  
  
3.  各パラメーター マーカーを呼び出して[SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md)に手順 1. で割り当てた構造体の配列の最初の要素では、その変数をパラメーターのデータ値とデータ長のポインターをポイントします。 パラメーターが実行時データ パラメーターである場合は、そのパラメーターをセットアップします。  
  
4.  バインドされたパラメーターのバッファー配列にデータ値を入力します。  
  
5.  呼び出す[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)ステートメントを実行します。 ドライバーによって、S 回 (パラメーターのセットごとに 1 回) ステートメントが効率よく実行されます。  
  
6.  実行時データ入力パラメーターを使用している場合[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) SQL_NEED_DATA を返します。 使用して、データをチャンク単位で送信[SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405)と[SQLPutData](../../native-client-odbc-api/sqlputdata.md)します。  
  
 **注**と共に多くの使用は列方向と行方向のバインド[SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)と[SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400)よりで[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399).  
  
## <a name="see-also"></a>参照  
 [クエリを実行方法に関するトピック&#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
