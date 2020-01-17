---
title: 'ISSAsynchStatus:: Abort (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7250c27e2ce35abbd15fc334f4f0ac07e94e985b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789521"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  非同期に実行されている操作を取り消します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>引数  
 *hChapter*[in]  
 操作を中止するチャプターのハンドル。 呼び出されるオブジェクトが行セットオブジェクトではない場合、または操作がチャプターに適用されない場合、呼び出し元は*Hchapter*を DB_NULL_HCHAPTER に設定する必要があります。  
  
 *eOperation*[in]  
 中止する操作。 この引数には、  
  
 DBASYNCHOP_OPEN。キャンセル要求が適用されるのは、行セットを非同期で開くか設定する場合、またはデータ ソース オブジェクトを非同期で初期化する場合です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 非同期操作を取り消す要求が処理されました。 ただし、その操作自体が取り消されることが保証されるわけではありません。 実際に操作が取り消されたかどうかを判断するには、コンシューマーで [ISSAsynchStatus::GetStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) を呼び出し、DB_E_CANCELED が返されるかどうかを調べる必要があります。ただし、要求直後に呼び出しても、この値が返されないことがあります。  
  
 DB_E_CANTCANCEL  
 非同期操作をキャンセルできません。  
  
 DB_E_CANCELED  
 非同期操作を中止する要求は、通知中に取り消されました。 操作は引き続き非同期に実行されます。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。  
  
 E_INVALIDARG  
 *Hchapter*パラメーターが DB_NULL_HCHAPTER ないか、または*eoperation*が DBASYNCH_OPEN ではありません。  
  
 E_UNEXPECTED  
 **IDBInitialize:: Initialize**が呼び出されていないか、または完了していないデータソースオブジェクトに対して**ISSAsynchStatus:: Abort**が呼び出されました。  
  
 **IDBInitialize:: Initialize**が呼び出されたが、その後初期化前にキャンセルされたか、またはタイムアウトしたデータソースオブジェクトに対して**ISSAsynchStatus:: Abort**が呼び出されました。データソースオブジェクトはまだ初期化されていません。  
  
 **Itransaction:: commit**または**Itransaction:: Abort**が以前に呼び出された行セットで**ISSAsynchStatus:: abort**が呼び出されましたが、行セットがコミットまたは中止になっておらず、ゾンビ状態になっています。  
  
 初期化フェーズで非同期に取り消された行セットに対して **ISSAsynchStatus::Abort** が呼び出された場合も、この値が返されます。 行セットはゾンビ状態になります。  
  
## <a name="remarks"></a>解説  
 行セットまたはデータ ソース オブジェクトの初期化を中止すると、その行セットまたはデータ ソース オブジェクトはゾンビ状態になり、**IUnknown** メソッド以外のすべてのメソッドから E_UNEXPECTED が返されます。 この状態になると、コンシューマーはその行セットまたはデータ ソース オブジェクトの解放しか実行できません。  
  
 **eOperation** に DBASYNCHOP_OPEN 以外の値を渡して *ISSAsynchStatus::Abort* を呼び出すと、S_OK が返されます。 これは、操作が完了したか取り消されたことを示すわけではありません。  
  
## <a name="see-also"></a>参照  
 [非同期操作の実行](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
