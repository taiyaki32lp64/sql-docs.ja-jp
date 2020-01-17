---
title: StreamOpenOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 562e79590a2a5f1f5e9bb609b9a0ad0ea8b2bfd9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928689"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
開くのためのオプションを指定します、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。 値は、OR 演算と組み合わせることができます。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|開く、 **Stream**非同期モードでのオブジェクト。|  
|**adOpenStreamFromRecord**|4|内容を識別、*ソース*パラメーターは既に開いている[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクト。 既定の動作を扱う方法が*ソース*ツリー構造内のノードを直接指す URL として。 そのノードに関連付けられている既定のストリームが開かれます。|  
|**adOpenStreamUnspecified**|-1|既定値です。 開始を指定します、 **Stream**既定オプションを含むオブジェクト。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 これらの定数には、ADO と WFC 対応はありません。  
  
## <a name="applies-to"></a>適用対象  
 [Open メソッド (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)
