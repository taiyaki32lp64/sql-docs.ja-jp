---
title: SearchDirectionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f8926e932317096cb3891cc8c480164268751cea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916998"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
内のレコードの検索の方向を指定します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|先頭で停止する旧バージョンと、検索、 **Recordset**します。 一致が見つからない場合、レコード ポインターは[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)します。|  
|**adSearchForward**|1|検索が転送の最後に停止する、 **Recordset**します。 一致が見つからない場合、レコード ポインターは[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>適用対象  
 [Find メソッド (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
