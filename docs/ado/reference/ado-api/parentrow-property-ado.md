---
title: ParentRow プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords:
- ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a81eb6ee58d942547a159728b9c3edf9a30f1ece
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917670"
---
# <a name="parentrow-property-ado"></a>ParentRow プロパティ (ADO)
OLE DB のコンテナーを設定します**行**上のオブジェクト、 **ADORecordConstruction**オブジェクト、行の親が ADO に変換されるよう**レコード**オブジェクト。  
  
 書き込み専用です。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>パラメーター  
 *pParent*  
 行のコンテナーです。  
  
## <a name="return-values"></a>戻り値  
 このプロパティのメソッドでは、S_OK および E_FAIL を含む、標準の HRESULT 値を返します。  
  
## <a name="applies-to"></a>適用対象  
 [ADORecordConstruction インターフェイス](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
