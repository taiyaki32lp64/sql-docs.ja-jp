---
title: ローカルトランザクションのサポート |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- SQL Server Native Client OLE DB provider, transactions
- local transactions [OLE DB]
ms.assetid: 78f2e5fc-b6fb-4eda-9f71-991a4d6c4902
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 76e14df87e8dca104fc0b9da44836288dc56ea69
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761553"
---
# <a name="supporting-local-transactions"></a>ローカル トランザクションのサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  セッションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーローカルトランザクションのトランザクションスコープを区切ります。 コンシューマーの方向で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の接続されたインスタンスに要求を送信すると、要求は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの作業単位になります。 ローカルトランザクションでは、1つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーセッションで、1つまたは複数の作業単位が常にラップされます。  
  
 既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの自動コミットモードを使用すると、1つの作業単位がローカルトランザクションのスコープとして扱われます。 ローカル トランザクションに参加するのは、1 単位のみです。 セッションが作成されると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、セッションのトランザクションを開始します。 作業単位の処理が正常に完了すると、その作業がコミットされます。 失敗すると、開始された作業がすべてロールバックされ、エラーがコンシューマーに報告されます。 どちらの場合も、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、すべての作業がトランザクション内で実行されるように、セッションの新しいローカルトランザクションを開始します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーコンシューマーは、 **ITransactionLocal**インターフェイスを使用して、ローカルトランザクションのスコープをより細かく制御できます。 コンシューマーのセッションがトランザクションを開始すると、トランザクションの開始時点から、最終的に **Commit** または **Abort** メソッドが呼び出されるまでのセッションの作業単位すべてが、1 つのアトミックな単位として扱われます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、コンシューマーによって指示されたときにトランザクションを暗黙的に開始します。 コンシューマーがモードの保持を要求しないと、セッションは親のトランザクション レベルの動作 (通常は、自動コミット モード) に戻ります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、次のように**ITransactionLocal:: StartTransaction**パラメーターがサポートされています。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|*isoLevel*[in]|このトランザクションで使用する分離レベルを指定します。 ローカルトランザクションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは次の機能をサポートします。<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注: [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降では、データベースのバージョン管理が有効でも無効でも、ISOLATIONLEVEL_SNAPSHOT は *isoLevel* の引数として有効です。 ただし、ユーザーがステートメントを実行する際に、バージョン管理が有効か、データベースが読み取り専用の場合は、エラーが発生します。 また、*より前のバージョンの* に接続している場合に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]isoLevel[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] に ISOLATIONLEVEL_SNAPSHOT を指定すると、XACT_E_ISOLATIONLEVEL エラーが発生します。|  
|*isoFlags*[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、0以外の値に対してエラーを返します。|  
|*pOtherOptions*[in]|NULL でない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、インターフェイスから options オブジェクトを要求します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、options オブジェクトの*Ultimeout*メンバーが0でない場合に XACT_E_NOTIMEOUT を返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 *Szdescription*メンバーの値を無視します。|  
|*pulTransactionLevel*[out]|NULL 以外の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、トランザクションの入れ子になったレベルを返します。|  
  
 ローカルトランザクションの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、次のように**ITransaction:: Abort**パラメーターを実装します。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|*pboidReason*[in]|設定しても無視されます。 NULL を指定しても問題ありません。|  
|*fRetaining*[in]|TRUE のときは、セッションの新しいトランザクションが暗黙的に開始されます。 このトランザクションは、コンシューマーがコミットまたは終了する必要があります。 FALSE の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、セッションの自動コミットモードに戻ります。|  
|*fAsync*[in]|非同期中止は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーではサポートされていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、値が FALSE でない場合に XACT_E_NOTSUPPORTED を返します。|  
  
 ローカルトランザクションの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、次のように**ITransaction:: Commit**パラメーターを実装します。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|*fRetaining*[in]|TRUE のときは、セッションの新しいトランザクションが暗黙的に開始されます。 このトランザクションは、コンシューマーがコミットまたは終了する必要があります。 FALSE の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、セッションの自動コミットモードに戻ります。|  
|*grfTC*[in]|非同期およびフェーズ1の戻り値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーではサポートされていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、XACTTC_SYNC 以外の値に対して XACT_E_NOTSUPPORTED を返します。|  
|*grfRM*[in]|0 を指定する必要があります。|  
  
 セッションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの行セットは、行セットのプロパティ DBPROP_ABORTPRESERVE および DBPROP_COMMITPRESERVE の値に基づいて、ローカルのコミットまたは中止操作で保持されます。 既定では、これらのプロパティは両方とも VARIANT_FALSE ます。また、セッションのすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー行セットは、中止またはコミット操作後に失われます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 **ITransactionObject**インターフェイスを実装していません。 このインターフェイスへの参照を取得しようとすると、コンシューマーは E_NOINTERFACE を返します。  
  
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
 [トランザクション](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [スナップショット分離を使用した作業](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
  
  
