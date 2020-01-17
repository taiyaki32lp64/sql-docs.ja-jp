---
title: 'コレクション (Visual C 構文のインデックスで #import) |Microsoft Docs'
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
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77a45203c50555168d2cd163c8b97406b8377694
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919896"
---
# <a name="collections-visual-c-syntax-index-with-import"></a>コレクション (Visual C 構文のインデックスで #import)
コレクションが特定の一般的なメソッドとプロパティを継承するかを把握すると便利です。  
  
 すべてのコレクションの継承、**カウント**プロパティと**更新**メソッド、およびすべてのコレクションを追加、**項目**プロパティ。 **エラー**コレクションを追加、**クリア**メソッド。 **パラメーター**コレクションの継承、 **Append**と**削除**メソッド、中に、**フィールド**コレクションに追加、 **Append**、**削除**、および**Update**メソッド。  
  
## <a name="properties-collection"></a>プロパティのコレクション  
  
### <a name="methods"></a>メソッド  
  
```  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Properties  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="errors-collection"></a>エラーのコレクション  
  
### <a name="methods"></a>メソッド  
  
```  
HRESULT Clear( );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Properties  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="parameters-collection"></a>Parameters コレクション  
  
### <a name="methods"></a>メソッド  
  
```  
HRESULT Append( IDispatch * Object );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Properties  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="fields-collection"></a>Fields コレクション  
  
### <a name="methods"></a>メソッド  
  
```  
HRESULT Append( _bstr_t Name, enum DataTypeEnum Type, long DefinedSize, enum FieldAttributeEnum Attrib, const _variant_t & FieldValue = vtMissing );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
HRESULT Update( );  
```  
  
### <a name="properties"></a>Properties  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="see-also"></a>関連項目  
 [エラーのコレクション (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [フィールド コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters コレクション (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
