---
title: 行のプロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::PutRow
- ADORecordConstruction::GetRow
- ADORecordConstruction::get_Row
- ADORecordConstruction::Row
- ADORecordConstruction::put_Row
helpviewer_keywords:
- Row property [ADO]
ms.assetid: 21019d89-2dd1-4a26-ac6f-384b81d66949
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 134f5fe05f89d6c8662a68f9f782f460c4b5f0aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917112"
---
# <a name="row-property-ado"></a>Row プロパティ (ADO)
OLE DB の設定を取得または**行**オブジェクトから、または 、 [ADORecordConstruction インターフェイス](../../../ado/reference/ado-api/adorecordconstruction-interface.md)オブジェクト。 使用すると**put_Row**を設定する、**行**オブジェクト、行は、ADO に変換されます**レコード**オブジェクト。  
  
## <a name="readwritesyntax"></a>読み取り/書き込みです。構文  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>パラメーター  
 *ppRow*  
 OLE DB へのポインター**行**オブジェクト。  
  
 *pRow*  
 OLE DB**行**オブジェクト。  
  
## <a name="return-values"></a>戻り値  
 このプロパティのメソッドでは、S_OK および E_FAIL を含む、標準の HRESULT 値を返します。  
  
## <a name="applies-to"></a>適用対象  
 [ADORecordConstruction インターフェイス](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
