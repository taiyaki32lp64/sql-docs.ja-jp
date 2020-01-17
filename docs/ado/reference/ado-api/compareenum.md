---
title: CompareEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareEnum
helpviewer_keywords:
- CompareEnum enumeration [ADO]
ms.assetid: bc8f710d-0621-4673-8d8e-0361e44abed0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c109f90fc023b6fbfeda01c8b4404c42a822c40a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919557"
---
# <a name="compareenum"></a>CompareEnum
ブックマークによって表される 2 つのレコードの相対位置を指定します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adCompareEqual**|1|ブックマークが等しいことを示します。|  
|**adCompareGreaterThan**|2|2 つ目の後に最初のブックマークがあることを示します。|  
|**adCompareLessThan**|0|2 つ目の最初のブックマークがあることを示します。|  
|**adCompareNotComparable**|4|ブックマークを比較できないことを示します。|  
|**adCompareNotEqual**|3|ブックマークが異なっており、順位がないことを示します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.Compare.EQUAL|  
|AdoEnums.Compare.GREATERTHAN|  
|AdoEnums.Compare.LESSTHAN|  
|AdoEnums.Compare.NOTCOMPARABLE|  
|AdoEnums.Compare.NOTEQUAL|  
  
## <a name="applies-to"></a>適用対象  
 [CompareBookmarks メソッド (ADO)](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [CompareBookmarks メソッド (ADO)](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)
