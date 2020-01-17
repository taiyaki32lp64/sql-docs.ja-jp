---
title: getMinutesOffset メソッド (DateTimeOffset) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6af552920698d4eb149f5edd5ee50128db0e1b61
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981804"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset (DateTimeOffset) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  この DateTimeOffset オブジェクトのオフセット (GMT からの分単位) を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>戻り値  
 分単位のオフセットです。  
  
## <a name="remarks"></a>Remarks  
 11:35:48-0800 2010 年3月8日を表す DateTimeOffset オブジェクトの場合、getMinutesOffset は値480を返します。  
  
## <a name="see-also"></a>参照  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset のメンバー](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
