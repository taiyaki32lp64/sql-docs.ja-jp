---
title: メソッドの SkipLine |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0e96900fdac55e97e3481ba5198e0f51d659877
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713760"
---
# <a name="skipline-method"></a>SkipLine メソッド
テキストを読み取るときに、1 つの行全体をスキップ[Stream](../../../ado/reference/ado-api/stream-object-ado.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>コメント  
 次の行区切り記号を含むすべての文字はスキップされます。 既定で、 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)は**adCRLF**します。 スキップしようとした場合[EOS](../../../ado/reference/ado-api/eos-property.md)、現在の位置は、引き続き**EOS**します。  
  
 **SkipLine**メソッドは、テキスト ストリームの使用 ([型](../../../ado/reference/ado-api/type-property-ado-stream.md)は**adTypeText**)。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
