---
title: StringFormatEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85bef64902f014e7b5269d6df328128bc8fe8d6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937883"
---
# <a name="stringformatenum"></a>StringFormatEnum
取得するときに、形式を指定します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)を文字列として。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adClipString**|2|行を区切ります*RowDelimiter*、列、 *ColumnDelimiter*、および null 値によって*NullExpr*します。 これら 3 つのパラメーターの[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)メソッドはでのみ有効ですが、 *StringFormat*の**adClipString**します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>適用対象  
 [GetString メソッド (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
