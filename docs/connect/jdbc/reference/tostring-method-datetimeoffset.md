---
title: toString メソッド (DateTimeOffset) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3acffe6a922084fd63e38a8e212b5cf86d6b278
ms.sourcegitcommit: c0fd28306a3b42895c2ab673734fbae2b56f9291
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2019
ms.locfileid: "71096903"
---
# <a name="tostring-method-datetimeoffset"></a>toString (DateTimeOffset) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **DateTimeOffset**オブジェクトの文字列表現を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>戻り値  
 **DateTimeOffset**オブジェクトの文字列表現。  
  
## <a name="remarks"></a>Remarks  
 この文字列の形式は `YYYY-MM-DD HH:mm:ss[.fffffff] [+|-]HH:mm` になります。  
  
 返される文字列の小数部では、宣言されている有効桁数になるまでゼロが埋め込まれます。 たとえば、値が "2010-03-10 12:34: 56.78-08:00" の**datetimeoffset (6)** は、datetimeoffset によって "2010-03-10 12:34: 56.780000-08:00" として書式設定されます。  
  
## <a name="see-also"></a>参照  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset のメンバー](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
