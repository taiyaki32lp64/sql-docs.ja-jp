---
title: Append メソッド (ADOX Keys) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd66edb75bec4f4b7e35c53c9ebeabd9b3c75d83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967290"
---
# <a name="append-method-adox-keys"></a>Append メソッド (ADOX Keys)
新しく追加[キー](../../../ado/reference/adox-api/key-object-adox.md)オブジェクトを[キー](../../../ado/reference/adox-api/keys-collection-adox.md)コレクション。  
  
## <a name="syntax"></a>構文  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>パラメーター  
 *[キー]*  
 **キー**オブジェクトを追加するか、キーを作成し、追加の名前。  
  
 *KeyType*  
 任意。 A**長い**キーの種類を指定する値。 *キー*パラメーターに対応、[型](../../../ado/reference/adox-api/type-property-key-adox.md)のプロパティを**キー**オブジェクト。  
  
 *列*  
 任意。 A**文字列**インデックスを作成する列の名前を指定する値。 *列*パラメーターの値に対応、[名前](../../../ado/reference/adox-api/name-property-adox.md)のプロパティを[列](../../../ado/reference/adox-api/column-object-adox.md)オブジェクト。  
  
 *RelatedTable*  
 任意。 A**文字列**関連テーブルの名前を指定する値。 *RelatedTable*パラメーターの値に対応、**名前**のプロパティを[テーブル](../../../ado/reference/adox-api/table-object-adox.md)オブジェクト。  
  
 *RelatedColumn*  
 任意。 A**文字列**関連列の外部キーの名前を指定する値。 *RelatedColumn*パラメーターの値に対応、**名前**のプロパティを[列](../../../ado/reference/adox-api/column-object-adox.md)オブジェクト。  
  
## <a name="remarks"></a>コメント  
 *列*いずれかの列の名前または列名の配列パラメーターを取ることができます。  
  
## <a name="applies-to"></a>適用対象  
 [Keys コレクション (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>関連項目  
 [Keys Append メソッド、キーの種類、RelatedColumn、RelatedTable、UpdateRule プロパティの例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append メソッド (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append メソッド (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append メソッド (ADOX Indexes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append メソッド (ADOX Procedures)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append メソッド (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append メソッド (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
