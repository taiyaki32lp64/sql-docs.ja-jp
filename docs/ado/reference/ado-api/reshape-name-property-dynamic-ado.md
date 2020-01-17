---
title: Reshape Name プロパティ-動的 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec72b2b1908f967caee4610e27315acaab787ac9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917173"
---
# <a name="reshape-name-property-dynamic-ado"></a>Reshape Name プロパティ - 動的 (ADO)
名前を指定します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
## <a name="return-values"></a>戻り値  
 返します、**文字列**値の名前、 **Recordset**します。  
  
## <a name="remarks"></a>コメント  
 まで、または接続の間、名前を保持、 **Recordset**が閉じられました。  
  
 **Reshape Name**プロパティは、再整形の機能で使用する主な対象は、 [Microsoft Data Shaping Service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)サービス プロバイダー。 名前は、再整形に参加するで一意である必要があります。  
  
 このプロパティは読み取り専用設定することがない直接ときに、 **Recordset**が作成されます。 などの場合、句の Shape コマンドが作成されます。 を**レコード セット**を使用して、エイリアス名を割り当てます、 **AS**エイリアスが割り当てられているキーワード、、 **Reshape Name**プロパティ。 エイリアスが宣言されていない場合、 **Reshape Name**プロパティには、データのシェイプ サービスによって生成された一意の名前が割り当てられます。 エイリアス名は、既存の名前と同じ場合**レコード セット**、 **Recordset**うち 1 つが解放されるまでに形状変更できます。 一意の名前を設定して、既定の動作を変更することができます、 [Reshape Name](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)プロパティを ADO 接続を**True**します。 データのシェイプの一意性を確保するために必要な場合は、割り当てられているユーザーの名前を変更するサービスのアクセス許可は、このプロパティを設定します。 形状を変更の詳細については、次を参照してください。 [OLE DB (ADO サービス プロバイダー) の Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)します。  
  
 使用して、 **Reshape Name**プロパティを参照するときに、**レコード セット**図形コマンドで、または Data Shaping Service によって作成されたため、名前を判断できない場合。 その場合は、コマンドによって返される文字列を連結することによって SHAPE コマンドを生成する可能性があります、 **Reshape Name**プロパティ。  
  
 **名前を変形**動的プロパティに追加、**レコード セット**オブジェクトの[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクションと、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) に設定されて**adUseClient**します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Microsoft のデータ シェイプの OLE DB (ADO サービス プロバイダー) のサービス](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [一般的な shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
