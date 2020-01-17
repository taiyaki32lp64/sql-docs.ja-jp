---
title: ストアドプロシージャの呼び出し (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a960df20b7b07bffab900589ae4d520541d720c1
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688662"
---
# <a name="call-stored-procedures-odbc"></a>ストアド プロシージャの呼び出し (ODBC)
  SQL ステートメントで ODBC CALL エスケープ句を使用してストアドプロシージャを呼び出すと、Microsoft SQL Server ドライバーは、リモートストアドプロシージャコール (RPC) メカニズムを使用して SQL Server にプロシージャを送信します。 RPC 要求は、SQL Server でのステートメント解析やパラメーター処理の多くを省略するため、Transact-SQL の EXECUTE ステートメントを使用するよりも高速です。  
  
 この機能を示すサンプルアプリケーションについては、「[リターンコードと出力&#40;パラメーター&#41;の処理 ODBC](running-stored-procedures-process-return-codes-and-output-parameters.md)」を参照してください。  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>プロシージャを RPC として実行するには  
  
1.  ODBC CALL エスケープ シーケンスを使用する SQL ステートメントを作成します。 このステートメントでは、各入力、入出力、出力パラメーター、およびプロシージャの戻り値 (存在する場合) に対してパラメーター マーカーを使用します。  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  各入力、入出力、出力パラメーター、およびプロシージャの戻り値 (存在する場合) に対して[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)を呼び出します。  
  
3.  [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)を使用してステートメントを実行します。  
  
> [!NOTE]  
>  アプリケーションでプロシージャの送信に (ODBC CALL エスケープ シーケンスではなく) Transact-SQL の EXECUTE 構文を使用した場合、プロシージャ コールは、SQL Server ODBC ドライバーから SQL Server に、RPC ではなく SQL ステートメントとして渡されます。 また、Transact-SQL の EXECUTE ステートメントを使用した場合、出力パラメーターは返されません。  
  
## <a name="see-also"></a>参照  
 [ストアドプロシージャの実行方法に関する&#40;トピック&#41; ODBC](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [ストアドプロシージャ呼び出しのバッチ処理](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [ストアドプロシージャの実行](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [ストアドプロシージャ  の呼び出し](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
 [手順](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  
