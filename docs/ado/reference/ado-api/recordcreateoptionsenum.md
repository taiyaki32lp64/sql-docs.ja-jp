---
title: RecordCreateOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65fe33b73cf77a27fcd69743ffb09cb05e197797
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917343"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
指定します、既存かどうか**レコード**開かれているか、新しい**レコード**用に作成された、[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクト[オープン](../../../ado/reference/ado-api/open-method-ado-record.md)メソッド。 値は、AND 演算子と組み合わせることができます。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|新たに作成**レコード**によって指定されたノードで*ソース*既存を開く代わりに、パラメーター**レコード**します。 ソースを指している場合、既存のノードでは、実行時エラーが発生し、しない限り、 **adCreateCollection**を組み合わせて**adOpenIfExists**または**adCreateOverwrite**します。|  
|**adCreateNonCollection**|0|新たに作成**レコード**型の[adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md)します。|  
|**adCreateOverwrite**|0x4000000|作成フラグを変更します。 **adCreateCollection**、 **adCreateNonCollection**、および**adCreateStructDoc**します。 ときにソース URL は、既存のノードを指している場合にこの値は、作成フラグの値のいずれかで使用またはまたは**レコード**、既存の**レコード**が上書きされ、新しい場所を作成します。 この値はと共に使用することはできません**adOpenIfExists**します。|  
|**adCreateStructDoc**|0x80000000|新たに作成**レコード**型の[adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md)、既存を開く代わりに**レコード**します。|  
|**adFailIfNotExists**|-1|既定値です。 場合、実行時エラーが発生*ソース*存在しないノードを指します。|  
|**adOpenIfExists**|0x2000000|作成フラグを変更します。 **adCreateCollection**、 **adCreateNonCollection**、および**adCreateStructDoc**します。 ときにソース URL は、既存のノードを指している場合にこの値は、作成フラグの値のいずれかで使用またはまたは**レコード**オブジェクト プロバイダーは、既存を開く必要があります**レコード**新しいを作成するのではなく1 つです。 この値はと共に使用することはできません**adCreateOverwrite**します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 これらの定数には、ADO と WFC 対応はありません。  
  
## <a name="applies-to"></a>適用対象  
 [Open メソッド (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)
