---
title: ローカル トランザクションのサポート |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: b75104940cca183005f8a465ea19d0a517247c25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213813"
---
# <a name="supporting-local-transactions"></a>ローカル トランザクションのサポート
  セッションのトランザクション スコープを取り出すため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのローカル トランザクション。 ときに、コンシューマーの方向にある、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのインスタンスに接続要求を送信する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、要求の作業単位の構成、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー。 ローカル トランザクションは常に 1 つ 1 つ以上の作業単位をラップ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダー セッション。  
  
 既定値を使用して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーの自動コミット モード、作業の 1 つの単位はローカル トランザクションのスコープとして扱われます。 ローカル トランザクションに参加するのは、1 単位のみです。 セッションが作成されたときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがセッションのトランザクションを開始します。 作業単位の処理が正常に完了すると、その作業がコミットされます。 失敗すると、開始された作業がすべてロールバックされ、エラーがコンシューマーに報告されます。 どちらの場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが、トランザクション内ですべての作業が実施されるように、セッションの新しいローカル トランザクションを開始します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーを使用してローカル トランザクションのスコープより細かく制御を転送することができます、 **ITransactionLocal**インターフェイス。 コンシューマーのセッションがトランザクションを開始すると、トランザクションの開始時点から、最終的に **Commit** または **Abort** メソッドが呼び出されるまでのセッションの作業単位すべてが、1 つのアトミックな単位として扱われます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、そのためには、コンシューマーによって指示された場合にトランザクションを暗黙的に開始します。 コンシューマーがモードの保持を要求しないと、セッションは親のトランザクション レベルの動作 (通常は、自動コミット モード) に戻ります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのサポート**itransactionlocal::starttransaction**パラメーターとして次のとおりです。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*isoLevel*[in]|このトランザクションで使用する分離レベルを指定します。 ローカル トランザクションの場合で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、次をサポートします。<br /><br /> -   ISOLATIONLEVEL_UNSPECIFIED<br />-   ISOLATIONLEVEL_CHAOS<br />-   ISOLATIONLEVEL_READUNCOMMITTED<br />-   ISOLATIONLEVEL_READCOMMITTED<br />-   ISOLATIONLEVEL_REPEATABLEREAD<br />-   ISOLATIONLEVEL_CURSORSTABILITY<br />-   ISOLATIONLEVEL_REPEATABLEREAD<br />-   ISOLATIONLEVEL_SERIALIZABLE<br />-   ISOLATIONLEVEL_ISOLATED<br />-ISOLATIONLEVEL_SNAPSHOT**に注意してください。** 以降で[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、ISOLATIONLEVEL_SNAPSHOT は有効で、 *isoLevel*引数は、データベースのバージョン管理が有効になっているかどうか。 ただし、ユーザーがステートメントを実行する際に、バージョン管理が有効か、データベースが読み取り専用の場合は、エラーが発生します。 また、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] より前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続している場合に、*isoLevel* に ISOLATIONLEVEL_SNAPSHOT を指定すると、XACT_E_ISOLATIONLEVEL エラーが発生します。|  
|*isoFlags*[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーには、0 以外の値のエラーが返されます。|  
|*pOtherOptions*[in]|NULL 以外の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーはインターフェイスからオプションのオブジェクトを要求します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]場合は、Native Client OLE DB プロバイダーは XACT_E_NOTIMEOUT を返しますのオプション オブジェクトの*ulTimeout*メンバーは 0 ではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの値は無視されます、 *szDescription*メンバー。|  
|*pulTransactionLevel*[out]|NULL 以外の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、トランザクションの入れ子のレベルを返します。|  
  
 ローカル トランザクションの場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの実装**itransaction::abort**パラメーターとして次のとおりです。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*pboidReason*[in]|設定しても無視されます。 NULL を指定しても問題ありません。|  
|*fRetaining*[in]|TRUE のときは、セッションの新しいトランザクションが暗黙的に開始されます。 このトランザクションは、コンシューマーがコミットまたは終了する必要があります。 FALSE の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがセッションの自動コミット モードに戻ります。|  
|*fAsync*[in]|非同期中止がでサポートされていない、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]値が FALSE でない場合、Native Client OLE DB プロバイダーは XACT_E_NOTSUPPORTED を返します。|  
  
 ローカル トランザクションの場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの実装**itransaction::commit**パラメーターとして次のとおりです。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*fRetaining*[in]|TRUE のときは、セッションの新しいトランザクションが暗黙的に開始されます。 このトランザクションは、コンシューマーがコミットまたは終了する必要があります。 FALSE の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがセッションの自動コミット モードに戻ります。|  
|*grfTC*[in]|非同期応答とフェーズのいずれかを返しますでサポートされていない、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは XACT_E_NOTSUPPORTED を XACTTC_SYN 以外の値を返します。|  
|*grfRM*[in]|0 を指定する必要があります。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セッション Native Client OLE DB プロバイダーの行セットのコミットをローカルに保存されますまたは行セット プロパティ DBPROP_ABORTPRESERVE と DBPROP_COMMITPRESERVE の値に基づいて操作を中止します。 これらのプロパティが VARIANT_FALSE とすべての両方には既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セッション Native Client OLE DB プロバイダーの行セットは次の中止またはコミット操作を失われます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが実装していない、 **ITransactionObject**インターフェイス。 このインターフェイスへの参照を取得しようとすると、コンシューマーは E_NOINTERFACE を返します。  
  
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
 [トランザクション](transactions.md)   
 [スナップショット分離を使用した作業](../native-client/features/working-with-snapshot-isolation.md)  
  
  
