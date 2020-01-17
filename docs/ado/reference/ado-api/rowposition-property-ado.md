---
title: RowPosition プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords:
- RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a333a2be2728f3c0b412246b0a793dae64096ae5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931227"
---
# <a name="rowposition-property-ado"></a>RowPosition プロパティ (ADO)
OLE DB の設定を取得または**RowPosition**オブジェクトとの間で、 **ADORecordsetConstruction**オブジェクト。 使用すると**put_RowPosition**を設定する、 **RowPosition**オブジェクト、その結果、**レコード セット**オブジェクトで使用、 **RowPosition**オブジェクトを現在の行を決定します。  
  
 読み取りと書き込みが可能です。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>パラメーター  
 *ppRowPos*  
 OLE DB へのポインター **RowPosition**オブジェクト。  
  
 *PRowPos*  
 OLE DB **RowPosition**オブジェクト。  
  
## <a name="return-values"></a>戻り値  
 このプロパティのメソッドでは、S_OK および E_FAIL を含む、標準の HRESULT 値を返します。  
  
## <a name="remarks"></a>コメント  
 このプロパティ設定されている場合場合、**行セット**上のオブジェクト、 **RowPosition**オブジェクトは異なる、**行セット**上のオブジェクト、 **Recordset**オブジェクト、後者の場合、前者をオーバーライドします。 現在でも同じ動作に**章**の**RowPosition**もします。  
  
## <a name="applies-to"></a>適用対象  
 [ADORecordsetConstruction インターフェイス](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
