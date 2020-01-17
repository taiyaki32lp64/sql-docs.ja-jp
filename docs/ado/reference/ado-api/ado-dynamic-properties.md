---
title: ADO の動的プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71396a071a42d7dd40a6537a2834541aab2b6bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921092"
---
# <a name="ado-dynamic-properties"></a>ADO の動的プロパティ
動的プロパティに追加できる、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)のコレクション、[接続](../../../ado/reference/ado-api/connection-object-ado.md)、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)、または[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 これらのプロパティのソースは、いずれかのデータ プロバイダーをなどが、 [OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)、またはサービス プロバイダーの場合など、 [OLE DB 用の Microsoft カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)します。 適切なデータ プロバイダーまたは特定の動的プロパティの詳細についてはサービス プロバイダーのマニュアルを参照してください。  
  
 [ADO Dynamic プロパティ インデックス](../../../ado/reference/ado-api/ado-dynamic-property-index.md)各標準 OLE DB プロバイダー動的プロパティ用の ADO および OLE DB 名の間の相互参照を提供します。  
  
 次の動的プロパティは、特に興味深いものし、上記のソースにも記載されています。 ADO の特別な機能は、次の一覧で、ADO のヘルプ トピックに記載されています。  
  
|||  
|-|-|  
|[最適化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|このフィールドにインデックスを作成する必要があるかどうかを指定します。|  
|[プロンプト](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|OLE DB プロバイダーが初期化情報をユーザーのメッセージを表示するかどうかを指定します。|  
|[名前を変更します。](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|名前を指定します、 **Recordset**オブジェクト。|  
|[再同期コマンド](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|文字列をユーザーが指定したコマンドを指定します、**再同期**でという名前のテーブルにデータを更新するメソッドの問題、**一意テーブル**動的プロパティ。|  
|[Unique Table、Unique Schema、Unique Catalog](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**一意テーブル**更新、挿入、および削除を許可するとなるベース テーブルの名前を指定します。<br /><br /> **一意のスキーマ**スキーマ、またはテーブルの所有者の名前を指定します。<br /><br /> **Unique Catalog**カタログ、またはテーブルを含むデータベースの名前を指定します。|  
|[更新プログラムの再同期](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|指定するかどうか、 **UpdateBatch**メソッドの後に、暗黙的な**再同期**メソッドの操作であれば、その操作のスコープ。|  
  
## <a name="see-also"></a>関連項目  
 [ADO の API リファレンス](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO のコレクション](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO の列挙定数](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [付録 B: ADO エラー](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベント](../../../ado/reference/ado-api/ado-events.md)   
 [ADO メソッド](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO オブジェクト モデル](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO オブジェクトとインターフェイス](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO のプロパティ](../../../ado/reference/ado-api/ado-properties.md)
