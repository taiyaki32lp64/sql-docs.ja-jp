---
title: Refresh メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a676bf5eb3d8d98f1b2eb9367aa8ad56f0da209d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931253"
---
# <a name="refresh-method-ado"></a>Refresh メソッド (ADO)
プロバイダーをコレクションから、使用可能なオブジェクトを反映するように、特定のオブジェクトを更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>コメント  
 **更新**メソッドが呼び出し元となるコレクションに応じてさまざまなタスクを実行します。  
  
### <a name="parameters"></a>パラメーター  
 使用して、**更新**メソッドを[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)のコレクションを[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトは、ストアド プロシージャのプロバイダー側のパラメーター情報を取得しますまたは。指定されたパラメーター化されたクエリ、**コマンド**オブジェクト。 コレクションは、ストアド プロシージャの呼び出しまたはパラメーター化クエリをサポートしないプロバイダーを空になります。  
  
 設定する必要があります、 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)のプロパティ、**コマンド**を有効なオブジェクト[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト、 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)プロパティ有効なコマンドを[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)プロパティを**adCmdStoredProc**呼び出す前に、**更新**メソッド。  
  
 アクセスする場合、**パラメーター**コレクションを呼び出す前に、**更新**メソッド、ADO は自動的にメソッドを呼び出すし、コレクションを設定します。  
  
> [!NOTE]
>  使用する場合、**更新**プロバイダーからパラメーター情報を取得するメソッドが 1 つまたは複数の可変長データ型を返します[パラメーター](../../../ado/reference/ado-api/parameter-object.md)オブジェクトの場合、ADO が基づくパラメーターのメモリを割り当てることができます潜在的なサイズの最大の実行中にエラーが発生するされます。 明示的に設定する必要があります、[サイズ](../../../ado/reference/ado-api/size-property-ado-parameter.md)呼び出す前にこれらのパラメーターのプロパティ、 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)エラーを防ぐためのメソッド。  
  
### <a name="fields"></a>フィールド  
 使用して、**更新**メソッドを[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクションが表示される影響を与えません。 基になるデータベース構造からの変更を取得する、いずれかを使用する必要があります、 [Requery](../../../ado/reference/ado-api/requery-method.md)メソッドや、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトは、ブックマークをサポートしていません、 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)メソッド。  
  
### <a name="properties"></a>Properties  
 使用して、**更新**メソッドを**プロパティ**一部のオブジェクトのコレクションが、プロバイダーを公開する動的プロパティのコレクションを設定します。 これらのプロパティは、ADO がサポートする組み込みのプロパティを超える、プロバイダーに固有の機能に関する情報を提供します。  
  
## <a name="applies-to"></a>適用対象  
  
||||  
|-|-|-|  
|[Axes コレクション](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[列のコレクション](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs コレクション](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Dimensions コレクション](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[エラーのコレクション](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields コレクション](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[グループのコレクション](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies コレクション](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[インデックスのコレクション](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[キーのコレクション](../../../ado/reference/adox-api/keys-collection-adox.md)|[Levels コレクション](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[メンバーのコレクション](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Parameters コレクション](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Positions コレクション](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Procedures コレクション](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[プロパティのコレクション](../../../ado/reference/ado-api/properties-collection-ado.md)|[Tables コレクション](../../../ado/reference/adox-api/tables-collection-adox.md)|[ユーザー コレクション](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Views コレクション](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>関連項目  
 [Refresh メソッドの例 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh メソッドの例 (vc++)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Count プロパティ (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Refresh メソッド (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
