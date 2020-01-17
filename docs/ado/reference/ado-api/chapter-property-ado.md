---
title: Chapter プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2791bc1a89f8cec1362ab1f00c3be739f7d56b96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920106"
---
# <a name="chapter-property-ado"></a>Chapter プロパティ (ADO)
OLE DB の設定を取得または**章**オブジェクトとの間で、 [ADORecordsetConstruction インターフェイス](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)オブジェクト。 使用すると**put_Chapter**を設定する、**章**オブジェクト、ADO に行のサブセットになって[Recordset オブジェクト](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 これにより、設定の現在の章、**行セット**オブジェクト。 このプロパティは読み取り/書き込み可能です。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>パラメーター  
 *plChapter*  
 チャプターのハンドルへのポインター。  
  
 *LChapter*  
 チャプターのハンドル。  
  
## <a name="return-values"></a>戻り値  
 このプロパティのメソッドでは、S_OK および E_FAIL を含む、標準の HRESULT 値を返します。  
  
## <a name="applies-to"></a>適用対象  
 [ADORecordsetConstruction インターフェイス](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
