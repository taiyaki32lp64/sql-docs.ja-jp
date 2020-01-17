---
title: AbsolutePosition プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b9795f962d0ead59a8d4f993e799a0ae4e2b750
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921692"
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition プロパティ (ADO)
序数位置を示す、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトの現在のレコード。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 32 ビット コードでは、設定または取得を**長い**内のレコードの数に 1 の値、**レコード セット**オブジェクト ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)) のいずれかを返しますまたは、 [PositionEnum](../../../ado/reference/ado-api/positionenum.md)値。  
  
 64 ビット コードでは、64 ビット値のストレージを提供するデータ型を使用します。 たとえば、時間の長いまたは別のいずれかを使用可能性があります DBORDINAL などの 64 ビット長の値します。 使用しない**PositionEnum**値を 32 ビットの長さに制限されているためです。  
  
## <a name="remarks"></a>コメント  
 設定するには、 **AbsolutePosition**を使用する OLE DB プロバイダーを実装する必要がありますプロパティ、ADO、 [IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx)インターフェイス。  
  
 アクセス、 **AbsolutePosition**のプロパティを**レコード セット**順方向専用で開かれるされているか、動的カーソルは、エラーを発生させます**adErrFeatureNotAvailable**します。 OLE DB プロバイダーでサポートされていれば別のカーソルの種類では、正しい位置が返される、 **IRowsetScroll:IRowsetLocate**インターフェイス。 プロバイダーがサポートされていない場合、 **IRowsetScroll**インターフェイス、プロパティに設定が**adPosUnknown**します。 サポートするかどうかを確認するには、プロバイダーのドキュメントを参照して**IRowsetScroll**します。  
  
 使用して、 **AbsolutePosition**内の序数位置に基づいて、レコードに移動するプロパティ、**レコード セット**オブジェクト、または現在のレコードの序数位置を決定します。 プロバイダーは、このプロパティを使用するための適切な機能をサポートする必要があります。  
  
 ように、 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)プロパティ、 **AbsolutePosition**は 1 に基づいており、現在のレコードが最初のレコードは 1 に等しい、 **Recordset**します。 内のレコードの合計数を取得することができます、 **Recordset**オブジェクトから、 [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)プロパティ。  
  
 設定すると、 **AbsolutePosition**プロパティ、現在のキャッシュ内のレコードになった場合でも ADO キャッシュに再読み込みを指定したレコードとレコードの新しいグループにします。 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)プロパティは、このグループのサイズを決定します。  
  
> [!NOTE]
>  使用しないようにする、 **AbsolutePosition**プロパティ レコード番号の代わりにします。 前のレコードを削除すると、特定のレコードの位置を変更します。 またの特定のレコードと同じことが保証はありません**AbsolutePosition**場合、**レコード セット**オブジェクトのクエリを再実行または再度開きます。 ブックマークが保持して、指定した位置に戻るをお勧めはあらゆる種類の配置の唯一の方法であり**Recordset**オブジェクト。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [AbsolutePosition および CursorLocation プロパティの例 (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition および CursorLocation プロパティの例 (vc++)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage プロパティ (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [RecordCount プロパティ (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
