---
title: 'Issasynchstatus: (OLE DB) |マイクロソフトのドキュメント'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAsynchStatus::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b61f5e3e44f9584fc3f93efb521585e3173b6c1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638724"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
  非同期に実行されている操作を取り消します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT Abort(  
  HCHAPTER hChapter,  
  DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>引数  
 *hChapter*[in]  
 操作を中止するチャプターのハンドル。 呼び出されるオブジェクトは、行セット オブジェクトではない場合、または、操作がチャプターに適用されません、呼び出し元を設定する必要があります*hChapter* DB_NULL_HCHAPTER にします。  
  
 *eOperation*[in]  
 中止する操作。 この引数には、  
  
 DBASYNCHOP_OPEN、要求をキャンセルするには、行セットの作成、非同期の開始にまたはデータ ソース オブジェクトの非同期初期化が適用されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 非同期操作を取り消す要求が処理されました。 ただし、その操作自体が取り消されることが保証されるわけではありません。 実際に操作が取り消されたかどうかを判断するには、コンシューマーで [ISSAsynchStatus::GetStatus](issasynchstatus-getstatus-ole-db.md) を呼び出し、DB_E_CANCELED が返されるかどうかを調べる必要があります。ただし、要求直後に呼び出しても、この値が返されないことがあります。  
  
 DB_E_CANTCANCEL  
 非同期操作をキャンセルできません。  
  
 DB_E_CANCELED  
 非同期操作を中止する要求は、通知中に取り消されました。 操作は引き続き非同期に実行されます。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。  
  
 E_INVALIDARG  
 *HChapter*パラメーターがない DB_NULL_HCHAPTER または*eOperation* DBASYNCH_OPEN ではありません。  
  
 E_UNEXPECTED  
 **Issasynchstatus:** をデータ ソース オブジェクトで呼び出された**idbinitialize::initialize**が呼び出されていない、またはが完了していません。  
  
 または、**IDBInitialize::Initialize** が呼び出されたものの、その後初期化前に取り消されたか、タイムアウトになったデータ ソース オブジェクトに対して **ISSAsynchStatus::Abort** が呼び出されました。データ ソース オブジェクトがまだ初期化されていません。  
  
 **Issasynchstatus:** を行セットに対して呼び出された**itransaction::commit**または**itransaction::abort** 、以前に呼び出された行セットのコミット後も存続または中止していないと、ゾンビ状態。  
  
 初期化フェーズで非同期に取り消された行セットに対して **ISSAsynchStatus::Abort** が呼び出された場合も、この値が返されます。 行セットはゾンビ状態になります。  
  
## <a name="remarks"></a>コメント  
 行セットまたはデータ ソース オブジェクトの初期化を中止すると、その行セットまたはデータ ソース オブジェクトはゾンビ状態になり、**IUnknown** メソッド以外のすべてのメソッドから E_UNEXPECTED が返されます。 この状態になると、コンシューマーはその行セットまたはデータ ソース オブジェクトの解放しか実行できません。  
  
 *eOperation* に DBASYNCHOP_OPEN 以外の値を渡して **ISSAsynchStatus::Abort** を呼び出すと、S_OK が返されます。 これは、操作が完了したか取り消されたことを示すわけではありません。  
  
## <a name="see-also"></a>参照  
 [非同期操作の実行](../native-client/features/performing-asynchronous-operations.md)  
  
  
