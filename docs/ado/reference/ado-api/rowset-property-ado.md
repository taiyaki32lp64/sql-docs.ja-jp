---
title: 行セット プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::PutRowset
- ADORecordsetConstruction::GetRowset
- ADORecordsetConstruction::Rowset
- ADORecordsetConstruction::put_Rowset
- ADORecordsetConstruction::get_Rowset
helpviewer_keywords:
- Rowset property [ADO]
ms.assetid: 7d359294-4ff2-47e0-8111-0c221b24d80e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 922f6690679d86bdb6cdafb721e3a5ed6bb674ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917120"
---
# <a name="rowset-property-ado"></a>Rowset プロパティ (ADO)
OLE DB の設定を取得または**行セット**オブジェクトとの間で、 **ADORecordsetConstruction**オブジェクト。 行セットは ADO を変える put_Rowset を使用して、 **Recordset**オブジェクト。  
  
 読み取りと書き込みが可能です。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>パラメーター  
 *ppRowset*  
 OLE DB へのポインター**行セット**オブジェクト。  
  
 *PRowset*  
 OLE DB**行セット**オブジェクト。  
  
## <a name="return-values"></a>戻り値  
 このプロパティのメソッドでは、S_OK および E_FAIL を含む、標準の HRESULT 値を返します。  
  
## <a name="applies-to"></a>適用対象  
 [ADORecordsetConstruction インターフェイス](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
