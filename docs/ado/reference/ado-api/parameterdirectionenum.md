---
title: 値の |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 68aaa0bfb8aa72c9e94a8b5db65768fe85895f0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917741"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
指定するかどうか、[パラメーター](../../../ado/reference/ado-api/parameter-object.md)表します入力パラメーター、出力パラメーター、両方の入力と出力パラメーター、またはストアド プロシージャからの戻り値。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|既定値です。 パラメーターが入力パラメーターを表すことを示します。|  
|**adParamInputOutput**|3|パラメーターが入力と出力の両方のパラメーターを表すことを示します。|  
|**adParamOutput**|2|パラメーターが出力パラメーターを表すことを示します。|  
|**adParamReturnValue**|4|パラメーターが戻り値を表すことを示します。|  
|**adParamUnknown**|0|パラメーターの方向が既知であることを示します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.ParameterDirection.INPUT|  
|AdoEnums.ParameterDirection.INPUTOUTPUT|  
|AdoEnums.ParameterDirection.OUTPUT|  
|AdoEnums.ParameterDirection.RETURNVALUE|  
|AdoEnums.ParameterDirection.UNKNOWN|  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[CreateParameter メソッド (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|[Direction プロパティ](../../../ado/reference/ado-api/direction-property.md)|
