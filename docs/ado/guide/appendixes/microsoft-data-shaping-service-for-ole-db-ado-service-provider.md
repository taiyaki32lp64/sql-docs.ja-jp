---
title: Microsoft のデータ シェイプの OLE DB (ADO サービス プロバイダー) のサービス |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ddef2feab633627c9549b73787faa1d104d69c5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926818"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft のデータ シェイプの Service for OLE DB の概要
> [!IMPORTANT]
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、アプリケーションでは、XML を使用する必要があります。

 サービス プロバイダーの OLE DB 用の Microsoft Data Shaping Service は、階層の構築をサポートしています (形)[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)データ プロバイダーからのオブジェクト。

## <a name="provider-keyword"></a>プロバイダーのキーワード
 OLE db Data Shaping Service を呼び出すには、接続文字列で、次のキーワードと値を指定します。

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>動的プロパティ
 このサービス プロバイダーが呼び出されたときに、次の動的なプロパティに追加されます、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)のコレクション、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。

|動的なプロパティ名|説明|
|---------------------------|-----------------|
|**Reshape の一意の名前**|示すかどうか**レコード セット**に対して重複する値を持つオブジェクト、 **Reshape Name**プロパティは使用できます。 この動的プロパティは、する場合**True**され、新しい**レコード セット**は既存のと同じ reshape のユーザーが指定した名前で作成**レコード セット**、し、新しい**レコード セット**オブジェクトのパス名が一意になるように変更します。 このプロパティは、する場合**False**され、新しい**レコード セット**は既存のと同じ reshape のユーザーが指定した名前で作成**レコード セット**の両方を**レコード セット**オブジェクトが同じ reshape 名前が与えられます。 そのため、どちらも**Recordset**両方のレコード セットが存在する限り、形状変更できます。<br /><br /> プロパティの既定値は**False**します。|
|**データ プロバイダー**|形状になる行を提供するプロバイダーの名前を示します。 行を指定するプロバイダーは使用しない場合は、この値は [なし] で指定できます。|

 接続文字列のキーワードとしてその名前を指定することで、書き込み可能な動的プロパティを設定することもできます。 たとえば、Microsoft Visual Basic では、設定、**データ プロバイダー** "MSDASQL"を指定することでの動的なプロパティ。

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 設定またはのインデックスとしてその名前を指定することで動的プロパティを取得することも、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)プロパティ。 たとえば、次のコード例は取得しの現在の値を出力、**データ プロバイダー**動的プロパティは新しい値を場合に設定し、cn。DataProvider は、"MSDataShape"に設定されています (直接または間接的に接続文字列を使用)、接続が開かれていないと。

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  動的なプロパティ、**データ プロバイダー**、開かれていないでのみ設定できる**接続**オブジェクト。 接続が開いたら、**データ プロバイダー**プロパティは読み取り専用になります。

 データ シェイプの詳細については、次を参照してください。[データ シェイプ](../../../ado/guide/data/data-shaping-overview.md)します。

## <a name="see-also"></a>関連項目
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
