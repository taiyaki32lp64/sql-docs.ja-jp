---
title: レコード セットのベース テーブル (ADO) にコントロールが変更された |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1b70920cd223223d5efb14925a6808168ca9cc16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911677"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>一意のテーブル、一意なスキーマに固有のカタログのプロパティ-動的 (ADO)
特定のベース テーブルに密接に変更をコントロールに有効にする、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)の複数のベース テーブルに対して結合操作をして形式がありません。  
  
-   **一意テーブル**更新、挿入、および削除を許可するとなるベース テーブルの名前を指定します。  
  
-   **一意のスキーマ**を指定します、*スキーマ*、またはテーブルの所有者の名前。  
  
-   **Unique Catalog**を指定します、*カタログ*、またはテーブルを含むデータベースの名前。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**文字列**テーブル、スキーマ、またはカタログの名前を指定する値。  
  
## <a name="remarks"></a>コメント  
 目的の基底のテーブルは、カタログ、スキーマ、およびテーブル名によって一意に識別されます。 ときに、**一意テーブル**プロパティが設定の値、**一意のスキーマ**または**Unique Catalog**ベース テーブルを検索するプロパティを使用します。 これは、必須ではありませんがそのいずれかまたは両方、**一意のスキーマ**と**固有のカタログ**プロパティを設定する前に、**一意テーブル**プロパティを設定します。  
  
 主キー、**一意テーブル**全体の主キーとして扱われる**レコード セット**します。 これは、主キーを必要とするすべてのメソッドで使用されるキーです。  
  
 中に**一意テーブル**が設定されている、[削除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)メソッドは、名前付きのテーブルのみに影響します。 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)、[再同期](../../../ado/reference/ado-api/resync-method.md)、 [Update](../../../ado/reference/ado-api/update-method.md)、および[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッド、の適切な基になるベーステーブルが影響**Recordset**します。  
  
 **一意テーブル**カスタムの再同期を実行する前に指定する必要があります。 場合**一意テーブル**が指定されていません、 [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)プロパティには効果はありません。  
  
 実行時エラーは、一意のベース テーブルが見つからない場合になります。  
  
 これらの動的プロパティはすべてに追加、 **Recordset**オブジェクト[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション時に、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティに設定されて**adUseClient**します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
