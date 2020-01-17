---
title: セッション |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 3a980816-675c-4fba-acc9-429297d85bbd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f594ace96fc34a77adca244e79c55551f0ddb8d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228973"
---
# <a name="sessions"></a>セッション
  A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー セッションのインスタンスへの接続を 1 つを表す[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、セッションがデータ ソースのトランザクション領域を区切ることが必要です。 特定のセッション オブジェクトから作成されたすべてのコマンド オブジェクトは、そのセッション オブジェクトのローカル トランザクションまたは分散トランザクションに関係します。  
  
 初期化されたデータ ソースで最初に作成されるセッション オブジェクトが、初期化時に確立された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続を受け取ります。 そのセッション オブジェクトのインターフェイスのすべての参照が解放されると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの接続で、データ ソースで作成される別のセッション オブジェクトを使用できるようになります。  
  
 データ ソースで新たに作成されるセッション オブジェクトは、データ ソースでの指定に従って、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの独自の接続を確立します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの接続は、そのセッションを作成したオブジェクトに対するすべての参照がアプリケーションによって解放された時点で削除されます。  
  
 次の例では、使用する方法、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーに接続するため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
```  
int main()  
{  
    // Interfaces used in the example.  
    IDBInitialize*      pIDBInitialize      = NULL;  
    IDBCreateSession*   pIDBCreateSession   = NULL;  
    IDBCreateCommand*   pICreateCmd1        = NULL;  
    IDBCreateCommand*   pICreateCmd2        = NULL;  
    IDBCreateCommand*   pICreateCmd3        = NULL;  
  
    // Initialize COM.  
    if (FAILED(CoInitialize(NULL)))  
    {  
        // Display error from CoInitialize.  
        return (-1);  
    }  
  
    // Get the memory allocator for this task.  
    if (FAILED(CoGetMalloc(MEMCTX_TASK, &g_pIMalloc)))  
    {  
        // Display error from CoGetMalloc.  
        goto EXIT;  
    }  
  
    // Create an instance of the data source object.  
    if (FAILED(CoCreateInstance(CLSID_SQLNCLI10, NULL,  
        CLSCTX_INPROC_SERVER, IID_IDBInitialize, (void**)  
        &pIDBInitialize)))  
    {  
        // Display error from CoCreateInstance.  
        goto EXIT;  
    }  
  
    // The InitFromPersistedDS function   
    // performs IDBInitialize->Initialize() establishing  
    // the first application connection to the instance of SQL Server.  
    if (FAILED(InitFromPersistedDS(pIDBInitialize, L"MyDataSource",  
        NULL, NULL)))  
    {  
        goto EXIT;  
    }  
  
    // The IDBCreateSession interface is implemented on the data source  
    // object. Maintaining the reference received maintains the   
    // connection of the data source to the instance of SQL Server.  
    if (FAILED(pIDBInitialize->QueryInterface(IID_IDBCreateSession,  
        (void**) &pIDBCreateSession)))  
    {  
        // Display error from pIDBInitialize.  
        goto EXIT;  
    }  
  
    // Releasing this has no effect on the SQL Server connection  
    // of the data source object because of the reference maintained by  
    // pIDBCreateSession.  
    pIDBInitialize->Release();  
    pIDBInitialize = NULL;  
  
    // The session created next receives the SQL Server connection of  
    // the data source object. No new connection is established.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd1)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // A new connection to the instance of SQL Server is established to support the  
    // next session object created. On successful completion, the  
    // application has two active connections on the SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd2)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // pICreateCmd1 has the data source connection. Because the  
    // reference on the IDBCreateSession interface of the data source  
    // has not been released, releasing the reference on the session  
    // object does not terminate a connection to the instance of SQL Server.  
    // However, the connection of the data source object is now   
    // available to another session object. After a successful call to   
    // Release, the application still has two active connections to the   
    // instance of SQL Server.  
    pICreateCmd1->Release();  
    pICreateCmd1 = NULL;  
  
    // The next session created gets the SQL Server connection  
    // of the data source object. The application has two active  
    // connections to the instance of SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd3)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
EXIT:  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd1 has the connection of the data source   
    // object.  
    if (pICreateCmd1 != NULL)  
        pICreateCmd1->Release();  
  
    // Releasing the reference on pICreateCmd2 terminates the SQL  
    // Server connection supporting the session object. The application  
    // now has only a single active connection on the instance of SQL Server.  
    if (pICreateCmd2 != NULL)  
        pICreateCmd2->Release();  
  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd3 has the connection of the   
    // data source object.  
    if (pICreateCmd3 != NULL)  
        pICreateCmd3->Release();  
  
    // On release of the last reference on a data source interface, the  
    // connection of the data source object to the instance of SQL Server is broken.  
    // The example application now has no SQL Server connections active.  
    if (pIDBCreateSession != NULL)  
        pIDBCreateSession->Release();  
  
    // Called only if an error occurred while attempting to get a   
    // reference on the IDBCreateSession interface of the data source.  
    // If so, the call to IDBInitialize::Uninitialize terminates the   
    // connection of the data source object to the instance of SQL Server.  
    if (pIDBInitialize != NULL)  
    {  
        if (FAILED(pIDBInitialize->Uninitialize()))  
        {  
            // Uninitialize is not required, but it fails if an  
            // interface has not been released. Use it for  
            // debugging.  
        }  
        pIDBInitialize->Release();  
    }  
  
    if (g_pIMalloc != NULL)  
        g_pIMalloc->Release();  
  
    CoUninitialize();  
  
    return (0);  
}  
```  
  
 接続[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーのセッション オブジェクトのインスタンスに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]継続的に作成し、セッション オブジェクトをリリースするアプリケーションのかなりのオーバーヘッドを生成することができます。 管理することによって、オーバーヘッドを最小化できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダー セッション オブジェクトを効率的にします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー アプリケーションを保つことができます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクトの少なくとも 1 つのインターフェイスの参照を保持することによってアクティブなセッション オブジェクトの接続。  
  
 たとえば、コマンド作成オブジェクト参照のプールを保持することで、プール内にあるセッション オブジェクトのアクティブな接続が維持されます。 セッション オブジェクトが必要になると、プールを保持するコードは、セッションを必要とするアプリケーション メソッドに対して、有効な **IDBCreateCommand** インターフェイス ポインターを渡します。 アプリケーション メソッドでセッションが不要になると、このメソッドは、プールを保持するコードにインターフェイス ポインターを返します。ただし、コマンド作成オブジェクトへのアプリケーションの参照は解放されません。  
  
> [!NOTE]  
>  上記の例で **IDBCreateCommand** インターフェイスを使用したのは、**ICommand** インターフェイスに **GetDBSession** メソッドが実装されているためです。このメソッドは、オブジェクトが作成されたセッションを特定できる、コマンドまたは行セットのスコープ内にある唯一のメソッドです。 したがって、コマンド オブジェクトを使用すると、追加のセッションを作成できるデータ ソース オブジェクト ポインターをアプリケーションで取得できます。  
  
## <a name="see-also"></a>参照  
 [データ ソース オブジェクト&#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
