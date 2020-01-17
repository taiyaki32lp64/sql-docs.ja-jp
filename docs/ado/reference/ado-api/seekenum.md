---
title: SeekEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 886825b4d32354572a5162487add419b00ec35d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931065"
---
# <a name="seekenum"></a>SeekEnum
型を指定[シーク](../../../ado/reference/ado-api/seek-method.md)を実行します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|等しい最初のキーをシーク*KeyValues*します。|  
|**adSeekLastEQ**|2|最後のキーと等しいをシーク*KeyValues*します。|  
|**adSeekAfterEQ**|4|等しいか、キーをシーク*KeyValues*またはと一致するが、発生した後だけです。|  
|**adSeekAfter**|8|場所の直後に、キーをシークとの一致*KeyValues*発生します。|  
|**adSeekBeforeEQ**|16|等しいか、キーをシーク*KeyValues*かその直前まで一致するが発生した場所。|  
|**adSeekBefore**|32|キーの場所と一致する直前にシーク*KeyValues*発生します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>適用対象  
 [Seek メソッド](../../../ado/reference/ado-api/seek-method.md)
