---
title: Cellset オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9524e9801f284d3dff3125b850cdd1fd32a361a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928644"
---
# <a name="cellset-object-ado-md"></a>CellSet オブジェクト (ADO MD)
多次元クエリの結果を表します。 これは、キューブまたはその他のセルセットから選択したセルのコレクションです。  
  
## <a name="remarks"></a>コメント  
 内のデータを**セルセット**、直接の配列に似たアクセスを使用して取得されます。 そのメンバーに関するデータを取得する特定のメンバーをドリルダウンすることができます。 たとえば、次のコード キャプションを返します最初のメンバーの最初の位置でセルセットという名前の最初の軸で`cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>コメント  
 セル セット内の現在のセルの概念はありません。 代わりに、[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)プロパティ取得[セル](../../../ado/reference/ado-md-api/cell-object-ado-md.md)セルセットからオブジェクト。 引数、**項目**プロパティを決定するセルを取得します。 セルの序数に基づく一意の値を指定することができます。 セルはセル セットの各軸の位置番号を使用して取得することもできます。 セルを取得する方法についての詳細については、次を参照してください。、[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)プロパティ。  
  
 コレクション、メソッド、およびプロパティの使用、**セルセット**オブジェクトを次を行うことができます。  
  
-   開いている接続を関連付ける、**セルセット**オブジェクトを設定してその[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)プロパティ。  
  
-   実行し、多次元クエリの結果を取得、[オープン](../../../ado/reference/ado-md-api/open-method-ado-md.md)メソッド。  
  
-   取得、**セル**から、**セルセット**で、[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)プロパティ。  
  
-   返す、[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)を定義するオブジェクト、**セルセット**で、[軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)コレクション。  
  
-   データをフィルター処理に使用されるディメンションに関する情報を取得、**セルセット**で、 [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md)プロパティ。  
  
-   返すかを定義するためのクエリを指定、**セルセット**で、[ソース](../../../ado/reference/ado-md-api/source-property-ado-md.md)プロパティ。  
  
-   現在の状態を返す、**セルセット**(オープン、クローズを実行する、または接続する) で、[状態](../../../ado/reference/ado-md-api/state-property-ado-md.md)プロパティ。  
  
-   閉じる、開く**セルセット**で、[閉じる](../../../ado/reference/ado-md-api/close-method-ado-md.md)メソッド。  
  
-   プロバイダー固有の情報の取得、**セルセット**標準の ADO を使用した[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [プロパティ、メソッド、およびイベント](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [セルセットの例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Axes コレクション (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Cell オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
