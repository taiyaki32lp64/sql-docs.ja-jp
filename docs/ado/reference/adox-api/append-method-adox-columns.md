---
title: Append メソッド (ADOX Columns) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6493157c00e5a71c7c2f085191231bb33bb5279a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967328"
---
# <a name="append-method-adox-columns"></a>Append メソッド (ADOX Columns)
新しく追加[列](../../../ado/reference/adox-api/column-object-adox.md)オブジェクトを[列](../../../ado/reference/adox-api/columns-collection-adox.md)コレクション。  
  
## <a name="syntax"></a>構文  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>パラメーター  
 *列*  
 **列**オブジェクトを追加するかを作成し、付加列の名前。  
  
 *型*  
 任意。 A**長い**列のデータ型を指定する値。 *型*パラメーターに対応、[型](../../../ado/reference/adox-api/type-property-column-adox.md)のプロパティを**列**オブジェクト。  
  
 *DefinedSize*  
 任意。 A**長い**列のサイズを指定する値。 *DefinedSize*パラメーターに対応、 [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md)のプロパティを**列**オブジェクト。  
  
> [!NOTE]
>  追加するときにエラーが発生する**列**を**列**のコレクション、[インデックス](../../../ado/reference/adox-api/index-object-adox.md)場合、**列**に存在しません[テーブル](../../../ado/reference/adox-api/table-object-adox.md)に既に追加されて、[テーブル](../../../ado/reference/adox-api/tables-collection-adox.md)コレクション。  
  
## <a name="applies-to"></a>適用対象  
 [Columns コレクション (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>関連項目  
 [Columns および Tables Append メソッド、Name プロパティの例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys Append メソッド、キーの種類、RelatedColumn、RelatedTable、UpdateRule プロパティの例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append メソッド (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append メソッド (ADOX Indexes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append メソッド (ADOX Keys)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append メソッド (ADOX Procedures)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append メソッド (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append メソッド (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
