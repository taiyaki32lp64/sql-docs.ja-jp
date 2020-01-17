---
title: Append メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 17fa0ff30e8dcdbf7ea67080f17c3e066bba8605
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920670"
---
# <a name="append-method-ado"></a>Append メソッド (ADO)
コレクションにオブジェクトを追加します。 コレクションが場合[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)、新しい[フィールド](../../../ado/reference/ado-api/field-object.md)それをコレクションに追加する前に、オブジェクトを作成できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>パラメーター  
 *collection*  
 コレクション オブジェクトです。  
  
 *fields*  
 A**フィールド**コレクション。  
  
 *object*  
 オブジェクト変数を追加するオブジェクトを表します。  
  
 *名前*  
 A**文字列**の新しい名前を含む値**フィールド**オブジェクトし、同じ名前であり、他のオブジェクトを指定できません必要があります*フィールド*します。  
  
 *型*  
 A[格納](../../../ado/reference/ado-api/datatypeenum.md)値、既定値は**adEmpty**、新しいフィールドのデータ型を指定します。 ADO では、次のデータ型はサポートされていないとする必要がありますいないときに使用を追加する新しいフィールドを[レコード セット オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md):**追加**、**しようとする**、 **adVariant**します。  
  
 *DefinedSize*  
 任意。 A**長い**文字または新しいフィールドのバイト単位で定義されたサイズを表す値です。 このパラメーターの既定値がから派生した*型*します。 フィールドを持つ、 *DefinedSize*可変長列として扱われます 255 バイトより大きい。 既定の*DefinedSize*が指定されていません。  
  
 *Attrib*  
 任意。 A [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)値、既定値は**adFldDefault**、新しいフィールドの属性を指定します。 この値が指定されていない場合、フィールドがから派生した属性に格納*型*します。  
  
 *FieldValue*  
 任意。 A**バリアント**新しいフィールドの値を表します。 指定されていない場合は、null 値を持つフィールドが追加されます。  
  
## <a name="remarks"></a>コメント  
  
## <a name="parameters-collection"></a>Parameters コレクション  
 設定する必要があります、[型](../../../ado/reference/ado-api/type-property-ado.md)のプロパティを[パラメーター](../../../ado/reference/ado-api/parameter-object.md)オブジェクトに追加する前に、[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクション。 設定する必要がある可変長データ型を選択した場合、[サイズ](../../../ado/reference/ado-api/size-property-ado-parameter.md)プロパティを 0 より大きい値にします。  
  
 パラメーターの記述では、プロバイダーへの呼び出しを最小化し、ストアド プロシージャまたはパラメーター化クエリを使用すると、そのためパフォーマンスが向上します。 ただし、ストアド プロシージャに関連付けられたまたは呼び出そうとクエリをパラメーター化されたパラメーターのプロパティを把握する必要があります。  
  
 使用して、 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)メソッドを作成する**パラメーター**オブジェクトを使用して適切なプロパティの設定、 **Append**メソッドに追加する、 [パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクション。 これにより設定およびパラメーターについては、プロバイダーに連絡しなくてもパラメーターの値を取得できます。 このメソッドを使用して、手動で設定する必要がありますパラメーター情報を提供しないプロバイダーを作成する場合、**パラメーター**パラメーターを使用するためにコレクション。  
  
## <a name="fields-collection"></a>Fields コレクション  
 *FieldValue*パラメーターは、追加する場合にのみ有効です、**フィールド**オブジェクトを[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクトでなく、**レコード セット**オブジェクト。 **レコード**オブジェクト、フィールドを追加し、同時に値を提供できます。 **レコード セット**オブジェクトの中にフィールドを作成する必要があります、**レコード セット**が閉じて、おり、開き、**レコード セット**フィールドに値を割り当てます。  
  
> [!NOTE]
>  新しい**フィールド**に追加されたオブジェクト、**フィールド**のコレクションを**レコード**オブジェクト、[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティを設定する必要がありますその他の前に**フィールド**プロパティを指定できます。 最初に、特定の値を**値**プロパティが割り当てられている必要がありますと[Update](../../../ado/reference/ado-api/update-method.md)上、**フィールド**という名前のコレクション。 その他のプロパティなど、[型](../../../ado/reference/ado-api/type-property-ado.md)または[属性](../../../ado/reference/ado-api/attributes-property-ado.md)アクセスできます。 **フィールド**次のデータ型のオブジェクト (**格納**) に追加することはできません、**フィールド**コレクションが発生するエラーが発生し、: **adArray**、**adChapter**、 **adEmpty**、 **adPropVariant**、および**adUserDefined**します。 また、次のデータ型は、ADO でサポートされていない:**追加**、**しようとする**、および**エラー**します。 これらの種類を追加するときにエラーが発生しないが、使用量がメモリ リークを含む、予期しない結果を生成できます。  
  
## <a name="recordset"></a>レコードセット  
 設定しない場合、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを呼び出す前に、 **Append**メソッド、 **CursorLocation**に設定されます**adUseClient** ([CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)値) 時に自動的に、[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)のメソッド、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトが呼び出されます。  
  
 実行時エラーが発生、 **Append**メソッドが、**フィールド**、オープンのコレクション**レコード セット**、または、**レコード セット**場所、 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)プロパティが設定されています。 フィールドを追加することができますのみ、**レコード セット**が開いていないと、データ ソースに接続されていません。 これは通常、ときに、**レコード セット**でオブジェクトが用意、 [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)メソッドまたはオブジェクト変数に割り当てられます。  
  
## <a name="record"></a>レコード  
 場合、実行時エラーが発生しない、 **Append**でメソッドが呼び出される、**フィールド**、オープンのコレクション**レコード**します。 新しいフィールドを追加は、**フィールド**のコレクション、**レコード**オブジェクト。 場合、**レコード**から派生した、**レコード セット**に新しいフィールドは表示されません、**フィールド**のコレクション、 **Recordset**オブジェクト。  
  
 存在しないフィールドを作成してに追加できる、**フィールド**フィールド オブジェクトをコレクションに既に存在していた場合、値を割り当てることでコレクション。 割り当てを自動作成を追加することのトリガー、**フィールド**オブジェクト、し、割り当てが完了します。  
  
 追加した後、**フィールド**を**フィールド**のコレクションを**レコード**オブジェクトを呼び出す、**更新**のメソッド、**フィールド**コレクションの変更を保存します。  
  
## <a name="applies-to"></a>適用対象  
  
- [Fields コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Parameters コレクション (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Append および CreateParameter メソッドの例 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append および CreateParameter メソッドの例 (vc++)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter メソッド (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete メソッド (ADO Fields コレクション)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete メソッド (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete メソッド (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update メソッド](../../../ado/reference/ado-api/update-method.md)
