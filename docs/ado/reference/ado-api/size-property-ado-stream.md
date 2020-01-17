---
title: Size プロパティ (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e52d05cdbc0fe0ca397c3a7b417fec72703b8e1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916936"
---
# <a name="size-property-ado-stream"></a>Size プロパティ (ADO Stream)
バイト数のストリームのサイズを示します。  
  
## <a name="return-values"></a>戻り値  
 返します、**長い**ストリームのサイズをバイト数を指定する値。 既定値は、ストリームのサイズが不明である場合に、ストリーム、または-1 のサイズは。  
  
## <a name="remarks"></a>コメント  
 **サイズ**オープンでのみ使用できます[Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。  
  
> [!NOTE]
>  格納できる任意の数のビットを**Stream**オブジェクト、システム リソースによってのみ制限されます。 場合、 **Stream**がより多くのビットで表せる数よりも含まれています、**長い**値、**サイズ**は切り捨てられ、したがってを正確に表さない、の長さ**Stream**します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Size プロパティ (ADO Parameter)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
