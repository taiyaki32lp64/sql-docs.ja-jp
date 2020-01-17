---
title: ObjectTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04c7b1d1cb5d07a300b82d13a7e80158498bbd5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965654"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
アクセス許可または所有権を設定する対象のデータベース オブジェクトの種類を指定します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|オブジェクトは、列です。|  
|**adPermObjDatabase**|3|オブジェクトは、データベースです。|  
|**adPermObjProcedure**|4|オブジェクトは、手順です。|  
|**adPermObjProviderSpecific**|-1|オブジェクトは、プロバイダーによって定義された型です。 場合、エラーが発生、 *ObjectType*パラメーターが**adPermObjProviderSpecific**と*ObjectTypeId*が指定されていません。|  
|**adPermObjTable**|1|オブジェクトは、テーブルです。|  
|**adPermObjView**|5|オブジェクトは、ビューです。|  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[GetObjectOwner メソッド (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions メソッド (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner メソッド](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions メソッド (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
