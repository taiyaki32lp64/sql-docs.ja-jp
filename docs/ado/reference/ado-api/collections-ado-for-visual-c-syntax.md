---
title: コレクション (Visual C 構文用の ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f18884c7a1aabe138408cca7eb529f4f21120330
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919916"
---
# <a name="collections-ado-for-visual-c-syntax"></a>Collections (Visual C++ 構文用の ADO)
## <a name="parameters"></a>パラメーター  
  
### <a name="methods"></a>メソッド  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 詳細については、「  
  
-   [Append メソッド (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete メソッド (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh メソッド (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Properties  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 詳細については、「  
  
-   [Count プロパティ (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item プロパティ (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="fields"></a>フィールド  
  
### <a name="methods"></a>メソッド  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 詳細については、「  
  
-   [Append メソッド (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete メソッド (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh メソッド (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Properties  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 詳細については、「  
  
-   [Count プロパティ (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item プロパティ (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="errors"></a>エラー  
  
### <a name="methods"></a>メソッド  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 詳細については、「  
  
-   [Clear メソッド (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)  
  
-   [Refresh メソッド (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Properties  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 詳細については、「  
  
-   [Count プロパティ (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item プロパティ (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="properties"></a>Properties  
  
### <a name="methods"></a>メソッド  
  
```  
Refresh(void);  
```  
  
 詳細については、「  
  
-   [Refresh メソッド (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Properties  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 詳細については、「  
  
-   [Count プロパティ (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item プロパティ (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [エラーのコレクション (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [フィールド コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters コレクション (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
