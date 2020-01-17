---
title: ローカルトランザクションのサポート |Microsoft Docs
description: OLE DB Driver for SQL Server でのローカル トランザクション
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c0cfc1ad6ff3439efe458f97394909c919b77075
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993962"
---
# <a name="supporting-local-transactions"></a>ローカル トランザクションのサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  セッションは、SQL Server ローカルトランザクションの OLE DB ドライバーのトランザクションスコープを区切ります。 コンシューマーの指示において、SQL Server の OLE DB ドライバーが接続されているインスタンス[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に要求を送信すると、要求は SQL Server の OLE DB ドライバーの作業単位になります。 ローカルトランザクションでは、常に1つ以上の作業単位が SQL Server セッションの1つの OLE DB ドライバーでラップされます。  
  
 OLE DB Driver for SQL Server の既定の自動コミット モードを使用すると、1 つの作業単位がローカル トランザクションのスコープとして扱われます。 ローカル トランザクションに参加するのは、1 単位のみです。 セッションが作成されると、SQL Server の OLE DB ドライバーによってセッションのトランザクションが開始されます。 作業単位の処理が正常に完了すると、その作業がコミットされます。 失敗すると、開始された作業がすべてロールバックされ、エラーがコンシューマーに報告されます。 いずれの場合も、OLE DB Driver for SQL Server は、同じセッションの新しいローカル トランザクションを開始し、すべての作業が 1 トランザクション内で実行されるようにします。  
  
 OLE DB Driver for SQL Server のコンシューマーは、**ITransactionLocal** インターフェイスを使用することで、より正確にローカル トランザクションのスコープを制御できます。 コンシューマーのセッションがトランザクションを開始すると、トランザクションの開始時点から、最終的に **Commit** または **Abort** メソッドが呼び出されるまでのセッションの作業単位すべてが、1 つのアトミックな単位として扱われます。 SQL Server の OLE DB ドライバーは、コンシューマーによって指示されたときにトランザクションを暗黙的に開始します。 コンシューマーがモードの保持を要求しないと、セッションは親のトランザクション レベルの動作 (通常は、自動コミット モード) に戻ります。  
  
 OLE DB Driver for SQL Server では、次のように**ITransactionLocal:: StartTransaction**パラメーターがサポートされています。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|*isoLevel*[in]|このトランザクションで使用する分離レベルを指定します。 ローカルトランザクションでは、SQL Server の OLE DB ドライバーは次の機能をサポートします。<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注: [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降では、データベースのバージョン管理が有効でも無効でも、ISOLATIONLEVEL_SNAPSHOT は *isoLevel* の引数として有効です。 ただし、ユーザーがステートメントを実行する際に、バージョン管理が有効か、データベースが読み取り専用の場合は、エラーが発生します。 また、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] より前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続している場合に、*isoLevel* に ISOLATIONLEVEL_SNAPSHOT を指定すると、XACT_E_ISOLATIONLEVEL エラーが発生します。|  
|*isoFlags*[in]|SQL Server の OLE DB ドライバーは、0以外の値に対してエラーを返します。|  
|*pOtherOptions*[in]|NULL 以外の場合、SQL Server の OLE DB ドライバーは、インターフェイスからオプションオブジェクトを要求します。 Options オブジェクトの*Ultimeout*メンバーが0でない場合、SQL Server の OLE DB ドライバーは XACT_E_NOTIMEOUT を返します。 SQL Server の OLE DB ドライバーは、 *Szdescription*メンバーの値を無視します。|  
|*pulTransactionLevel*[out]|NULL 以外の場合、SQL Server の OLE DB ドライバーは、トランザクションの入れ子になったレベルを返します。|  
  
 ローカルトランザクションの場合、SQL Server の OLE DB ドライバーは、次のように**ITransaction:: Abort**パラメーターを実装します。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|*pboidReason*[in]|設定しても無視されます。 NULL を指定しても問題ありません。|  
|*fRetaining*[in]|TRUE のときは、セッションの新しいトランザクションが暗黙的に開始されます。 このトランザクションは、コンシューマーがコミットまたは終了する必要があります。 FALSE の場合、SQL Server の OLE DB ドライバーは、セッションの自動コミットモードに戻ります。|  
|*fAsync*[in]|非同期中止は、SQL Server 用の OLE DB ドライバーではサポートされていません。 値が FALSE でない場合、SQL Server の OLE DB ドライバーは XACT_E_NOTSUPPORTED を返します。|  
  
 ローカルトランザクションの場合、SQL Server の OLE DB ドライバーは、次のように**ITransaction:: Commit**パラメーターを実装します。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|*fRetaining*[in]|TRUE のときは、セッションの新しいトランザクションが暗黙的に開始されます。 このトランザクションは、コンシューマーがコミットまたは終了する必要があります。 FALSE の場合、SQL Server の OLE DB ドライバーは、セッションの自動コミットモードに戻ります。|  
|*grfTC*[in]|非同期およびフェーズ1の戻り値は、SQL Server 用の OLE DB ドライバーではサポートされていません。 SQL Server の OLE DB ドライバーは、XACTTC_SYNC 以外の値に対して XACT_E_NOTSUPPORTED を返します。|  
|*grfRM*[in]|0 を指定する必要があります。|  
  
 セッションの OLE DB Driver for SQL Server の行セットは、行セット プロパティ DBPROP_ABORTPRESERVE と DBPROP_COMMITPRESERVE の値に基づいて、ローカル コミット操作時またはアボート操作時に保存されます。 既定では、これらのプロパティの値はどちらも VARIANT_FALSE で、セッションのすべての OLE DB Driver for SQL Server の行セットはすべて、アボート操作またはコミット操作が行われると失われます。  
  
 SQL Server の OLE DB ドライバーは、 **ITransactionObject**インターフェイスを実装していません。 このインターフェイスへの参照を取得しようとすると、コンシューマーは E_NOINTERFACE を返します。  
  
 次の例では、**ITransactionLocal** を使用します。  
  
```  
// Interfaces used in the example.  
IDBCreateSession*   pIDBCreateSession   = NULL;  
ITransaction*       pITransaction       = NULL;  
IDBCreateCommand*   pIDBCreateCommand   = NULL;  
IRowset*            pIRowset            = NULL;  
  
HRESULT             hr;  
  
// Get the command creation and local transaction interfaces for the  
// session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
if (FAILED(hr = pIDBCreateCommand->QueryInterface(IID_ITransactionLocal,  
    (void**) &pITransaction)))  
    {  
    // Process error. Release any references and return.  
    }  
  
// Start the local transaction.  
if (FAILED(hr = ((ITransactionLocal*) pITransaction)->StartTransaction(  
    ISOLATIONLEVEL_REPEATABLEREAD, 0, NULL, NULL)))  
    {  
    // Process error from StartTransaction. Release any references and  
    // return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then terminate.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, XACTTC_SYNC, 0)))  
        {  
        // Get error from failed commit.  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>参照  
 [トランザクション](../../oledb/ole-db-transactions/transactions.md)   
 [スナップショット分離を使用した作業](../../oledb/features/working-with-snapshot-isolation.md)  
  
  
