---
title: 'ISSAsynchStatus:: Abort (OLE DB) |Microsoft Docs'
description: ISSAsynchStatus::Abort (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4cb57bfac5af957bd9f2f539b025f32b5f481d66
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015428"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  非同期に実行されている操作を取り消します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>引数  
 *hChapter*[in]  
 操作を中止するチャプターのハンドル。 呼び出し中のオブジェクトが行セット オブジェクトではない場合、または操作がチャプターに適用されない場合は、呼び出し元では *hChapter* を DB_NULL_HCHAPTER に設定する必要があります。  
  
 *eOperation*[in]  
 中止する操作。 次の値を使用する必要があります。  
  
 DBASYNCHOP_OPEN。キャンセル要求が適用されるのは、行セットを非同期で開くか設定する場合、またはデータ ソース オブジェクトを非同期で初期化する場合です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 非同期操作を取り消す要求が処理されました。 その操作自体が取り消されたことが保証されるわけではありません。 実際に操作が取り消されたかどうかを判断するには、コンシューマーで [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) を呼び出し、DB_E_CANCELED が返されるかどうかを調べる必要があります。ただし、要求直後に呼び出しても、この値が返されないことがあります。  
  
 DB_E_CANTCANCEL  
 非同期操作をキャンセルできません。  
  
 DB_E_CANCELED  
 非同期操作を中止する要求は、通知中に取り消されました。 操作は引き続き非同期に実行されます。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。  
  
 E_INVALIDARG  
 *Hchapter*パラメーターが DB_NULL_HCHAPTER ではないか、 *EOPERATION*が DBASYNCH_OPEN ではありません。  
  
 E_UNEXPECTED  
 **IDBInitialize::Initialize** が呼び出されていないか、完了していないデータ ソース オブジェクトに対して **ISSAsynchStatus::Abort** が呼び出されました。  
  
 または、**IDBInitialize::Initialize** が呼び出されたものの、その後初期化前に取り消されたか、タイムアウトになったデータ ソース オブジェクトに対して **ISSAsynchStatus::Abort** が呼び出されました。データ ソース オブジェクトはまだ初期化されていません。  
  
 以前に **ITransaction::Commit** または **ITransaction::Abort** が呼び出された行セットに対して **ISSAsynchStatus::Abort** が呼び出された場合もこの値が返されます。この行セットはコミットまたはアボートの後に保持されず、ゾンビ状態になります。  
  
 初期化フェーズで非同期に取り消された行セットに対して **ISSAsynchStatus::Abort** が呼び出された場合も、この値が返されます。 行セットはゾンビ状態になります。  
  
## <a name="remarks"></a>Remarks  
 行セットまたはデータ ソース オブジェクトの初期化を中止すると、その行セットまたはデータ ソース オブジェクトはゾンビ状態になり、**IUnknown** メソッド以外のすべてのメソッドから E_UNEXPECTED が返されます。 この状態になると、コンシューマーはその行セットまたはデータ ソース オブジェクトの解放しか実行できません。  
  
 *eOperation* に DBASYNCHOP_OPEN 以外の値を渡して **ISSAsynchStatus::Abort** を呼び出すと、S_OK が返されます。 これは、操作が完了したか取り消されたことを示すわけではありません。  
  
## <a name="see-also"></a>参照  
 [非同期操作の実行](../../oledb/features/performing-asynchronous-operations.md)  
  
  
