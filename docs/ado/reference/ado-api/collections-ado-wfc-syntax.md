---
title: コレクション (ADO - WFC 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- syntax indexes [ADO], ADO/WFC
- collections [ADO], ADO/WFC syntax
- ADO/WFC syntax index [ADO]
ms.assetid: 073f9a0e-c755-42dd-9f71-4647d68e331a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b26c78f514ef6786f642c534b2621d0c81c71e51
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919904"
---
# <a name="collections-ado---wfc-syntax"></a>Collections (ADO - WFC 構文)
**package com.ms.wfc.data**  
  
## <a name="parameters"></a>パラメーター  
  
### <a name="methods"></a>メソッド  
  
```  
public void append(com.ms.wfc.data.Parameter param)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public Parameter getItem(int n)  
public Parameter getItem(String s)  
```  
  
### <a name="properties"></a>Properties  
  
```  
public int getCount()  
```  
  
## <a name="fields"></a>フィールド  
  
### <a name="methods"></a>メソッド  
  
```  
public void append(String name, int type)  
public void append(String name, int type, int definedSize)  
public void append(String name, int type, int definedSize, int attrib)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public com.ms.wfc.data.Field getItem(int n)  
public com.ms.wfc.data.Field getItem(String s)  
```  
  
### <a name="properties"></a>Properties  
  
```  
public int getCount()  
```  
  
## <a name="errors"></a>エラー  
  
### <a name="methods"></a>メソッド  
  
```  
public void clear()  
public void refresh()  
public com.ms.wfc.data.Error getItem(int n)  
public com.ms.wfc.data.Error getItem(String s)  
```  
  
### <a name="properties"></a>Properties  
  
```  
public int getCount()  
```  
  
## <a name="see-also"></a>関連項目  
 [エラーのコレクション (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [フィールド コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters コレクション (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
