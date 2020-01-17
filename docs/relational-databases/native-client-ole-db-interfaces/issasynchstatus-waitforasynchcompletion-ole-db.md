---
title: 'ISSAsynchStatus:: WaitForAsynchCompletion (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
apitype: COM
helpviewer_keywords:
- WaitForAsynchCompletion method
ms.assetid: 9f65e9e7-eb93-47a1-bc42-acd4649fbd0e
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50751cdbb4a488913a9673d00195b4b6000f54ad
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73762622"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  非同期で実行している操作が完了するまで、またはタイムアウトが発生するまで待機します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT WaitForAsynchCompletion(   
        DWORD dwMillisecTimeOut);  
```  
  
## <a name="arguments"></a>引数  
 *dwMillisecTimeOut*[in]  
 ミリ秒単位のタイムアウト。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。  
  
 E_UNEXPECTED  
 **Itransaction:: Commit**または**Itransaction:: Abort**が呼び出されたか、初期化フェーズ中に行セットが取り消されたため、行セットが未使用の状態になっています。  
  
 DB_E_CANCELED  
 行セットの設定中またはデータ ソース オブジェクトの初期化中に、非同期処理が取り消されました。  
  
 DB_S_ASYNCHRONOUS  
 指定したタイムアウトに達しても、操作が完了していません。  
  
> [!NOTE]  
>  **ISSAsynchStatus::WaitForAsynchCompletion** メソッドでは、上記のリターン コード値以外に、主要な OLEDB **ICommand::Execute** メソッドや **IDBInitialize::Initialize** メソッドによって返されたリターン コード値もサポートします。  
  
## <a name="remarks"></a>Remarks  
 タイムアウト値 (ミリ秒) が経過するか、保留になっている操作が完了するまでは、**ISSAsynchStatus::WaitForAsynchCompletion** メソッドから制御が戻りません。 **Command**オブジェクトには、クエリがタイムアウトするまでに実行される秒数を制御する**CommandTimeout**プロパティがあります。**ISSAsynchStatus:: WaitForAsynchCompletion**メソッドと共に使用する場合、 **CommandTimeout**プロパティは無視されます。  
  
 非同期操作では、タイムアウト プロパティが無視されます。 **ISSAsynchStatus::WaitForAsynchCompletion** のタイムアウト パラメーターに、制御が呼び出し元に返されるまでに経過する最大時間を指定します。 タイムアウトが発生すると、DB_S_ASYNCHRONOUS が返されます。 タイムアウトによって非同期操作が取り消されることはありません。 タイムアウト期間内に完了しない非同期操作をアプリケーションで取り消す必要がある場合、タイムアウトを待機後、DB_S_ASYNCHRONOUS が返されたときに明示的に操作を取り消す必要があります。  
  
> [!NOTE]  
>  OLE DB サービス コンポーネントを使用していて、DB_S_ASYNCHRONOUS を待機しているときに S_OK が返されることがあります。そのため、S_OK または DB_S_ASYNCHRONOUS が返される場合は、[ISSAsynchStatus::GetStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) を呼び出して完了をチェックする必要があります。  
  
 *dwMillisecTimeOut* の値を INFINITE に設定すると、**ISSAsynchStatus::WaitForAsynchCompletion** メソッドは操作が完了するまでブロックされます。 *dwMillisecTimeOut* の値を 0 に設定すると、メソッドからすぐに制御が戻り、保留中の操作の状態が返されます。 操作が完了する前にタイムアウトが発生すると、DB_S_ASYNCHRONOUS が返されます。  
  
 タイムアウトが発生する前に操作が完了すると、返される HRESULT には操作から返された HRESULT が設定されます (返される HRESULT は、操作が同期的に実行された場合に返される HRESULT になります)。  
  
 また、DBPROPSET_SQLSERVERROWSET プロパティ セットに SSPROP_ISSAsynchStatus プロパティが追加されています。 [ISSAsynchStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md) インターフェイスをサポートするプロバイダーは、値 VARIANT_TRUE を指定してこのプロパティを実装する必要があります。  
  
## <a name="see-also"></a>参照  
 [非同期操作の実行](../../relational-databases/native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
