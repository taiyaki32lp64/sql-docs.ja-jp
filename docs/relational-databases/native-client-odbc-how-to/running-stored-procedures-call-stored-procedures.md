---
title: ストアドプロシージャの呼び出し (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2d9d3dd9955f8b7f5cf6b02934f34af0d420dae8
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73780648"
---
# <a name="running-stored-procedures---call-stored-procedures"></a>ストアド プロシージャの実行 - ストアド プロシージャの呼び出し
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC ドライバーは、リモート ストアド プロシージャとしてのストアド プロシージャの実行をサポートします。 ストアド プロシージャをリモート ストアド プロシージャとして実行すると、ドライバーとサーバーでプロシージャ実行のパフォーマンスが最適化されます。  
  
  SQL ステートメントで ODBC CALL エスケープ句を使用してストアド プロシージャを呼び出すと、Microsoft® SQL Server™ ドライバーは、リモート ストアド プロシージャ コール (RPC) メカニズムを使用して、プロシージャを SQL Server に送信します。 RPC 要求は、SQL Server でのステートメント解析やパラメーター処理の多くを省略するため、Transact-SQL の EXECUTE ステートメントを使用するよりも高速です。  
  
 この機能を示すサンプルアプリケーションについては、「[リターンコードと出力&#40;パラメーター&#41;の処理 ODBC](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md)」を参照してください。  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>プロシージャを RPC として実行するには  
  
1.  ODBC CALL エスケープ シーケンスを使用する SQL ステートメントを作成します。 このステートメントでは、各入力、入出力、出力パラメーター、およびプロシージャの戻り値 (存在する場合) に対してパラメーター マーカーを使用します。  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  各入力、入出力、出力パラメーター、およびプロシージャの戻り値 (存在する場合) に対して[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)を呼び出します。  
  
3.  [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)を使用してステートメントを実行します。  
  
> [!NOTE]  
>  アプリケーションでプロシージャの送信に (ODBC CALL エスケープ シーケンスではなく) Transact-SQL の EXECUTE 構文を使用した場合、プロシージャ コールは、SQL Server ODBC ドライバーから SQL Server に、RPC ではなく SQL ステートメントとして渡されます。 また、Transact-SQL の EXECUTE ステートメントを使用した場合、出力パラメーターは返されません。  
  
## <a name="see-also"></a>参照  
  [ストアドプロシージャ呼び出しのバッチ処理](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [ストアドプロシージャの実行](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [ストアドプロシージャ  の呼び出し](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
 [手順](../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
  
