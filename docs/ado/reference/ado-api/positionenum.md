---
title: PositionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d5f7ca47177a953313ff983bb25f9178b73b4930
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917602"
---
# <a name="positionenum"></a>PositionEnum
内のレコード ポインターの現在位置を示す、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|BOF に現在のレコード ポインターがあることを示します (つまり、 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)プロパティは**True**)。|  
|**adPosEOF**|-3|EOF に現在のレコード ポインターがあることを示します (つまり、 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)プロパティは**True**)。|  
|**adPosUnknown**|-1|示します、 **Recordset**が空で、現在の位置が不明、またはプロバイダーがサポートしていない、 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)または[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)プロパティ。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[AbsolutePage プロパティ (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[AbsolutePosition プロパティ (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
