---
title: データ マイニング スキーマ行セットのクエリ (Analysis Services - データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- data mining [Analysis Services], queries
- mining model content
- data mining [Analysis Services], schema rowsets
- schema rowsets [Analysis Services], retrieving
- data mining [Analysis Services], troubleshooting
ms.assetid: 442d8c29-07c7-45de-9a15-d556059f68d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30a4a503b16693a3774aa7f68771fb0f9dd70810
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084908"
---
# <a name="querying-the-data-mining-schema-rowsets-analysis-services---data-mining"></a>データ マイニング スキーマ行セットのクエリ (Analysis Services - データ マイニング)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、既存の OLE DB データ マイニング スキーマ行セットの多くが、データ マイニング拡張機能 (DMX) ステートメントを使用して照会できるシステム テーブルのセットとして公開されます。 データ マイニング スキーマ行セットに対するクエリを作成することによって、利用可能なサービスの特定、モデルおよび構造の状態の更新、モデル コンテンツまたはパラメーターに関する詳細の確認を行うことができます。 データ マイニング スキーマ行セットの説明については、「 [データ マイニング スキーマ行セット](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)」を参照してください。  
  
> [!NOTE]  
>  データ マイニング スキーマ行セットに対するクエリは、XMLA を使用して実行することもできます。 これを SQL Server Management Studio で実行する方法については、「 [XMLA を使用したデータ マイニング クエリの作成](create-a-data-mining-query-by-using-xmla.md)」を参照してください。  
  
## <a name="list-of-data-mining-schema-rowsets"></a>データ マイニング スキーマ行セットの一覧  
 次の表に、クエリおよび監視に役立つデータ マイニング スキーマ行セットの一覧を示します。  
  
|行セット名|説明|  
|-----------------|-----------------|  
|DMSCHEMA_MINING_MODELS|現在のコンテキスト内のすべてのマイニング モデルの一覧が表示されます。<br /><br /> 作成日、モデルの作成に使用されたパラメーター、トレーニング セットのサイズなどの情報が含まれます。|  
|DMSCHEMA_MINING_COLUMNS|現在のコンテキスト内のマイニング モデルで使用されるすべての列の一覧が表示されます。<br /><br /> マイニング構造ソース列へのマッピング、データ型、有効桁数、列で使用できる予測関数などの情報が含まれます。|  
|DMSCHEMA_MINING_STRUCTURES|現在のコンテキスト内のすべてのマイニング構造の一覧が表示されます。<br /><br /> 構造にデータが設定されているかどうか、構造が最後に処理された日付、構造の予約データ セットの定義などの情報が含まれます。|  
|DMSCHEMA_MINING_STRUCTURE_COLUMNS|現在のコンテキスト内のマイニング構造で使用されるすべての列の一覧が表示されます。<br /><br /> コンテンツの種類、データ型、NULL 値の許容属性、入れ子になったテーブル データが列に格納されるかどうかなどの情報が含まれます。|  
|DMSCHEMA_MINING_SERVICES|指定されたサーバーで利用可能なすべてのマイニング サービスまたはアルゴリズムの一覧を表示します。<br /><br /> サポートされているモデリング フラグ、入力の種類、サポートされているデータ ソースの種類などの情報が含まれます。|  
|DMSCHEMA_MINING_SERVICE_PARAMETERS|現在のインスタンス上で利用可能なマイニング サービスのすべてのパラメーターの一覧を表示します。<br /><br /> 各パラメーターのデータ型、既定値、上限値と下限値などの情報が含まれます。|  
|DMSCHEMA_MODEL_CONTENT|モデルが処理された場合、モデルの内容を返します。<br /><br /> 詳細については、「[マイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-analysis-services-data-mining.md)」を参照してください。|  
|DBSCHEMA_CATALOGS|Analysis Services の現在のインスタンス内のすべてのデータベース (カタログ) の一覧が表示されます。|  
|MDSCHEMA_INPUT_DATASOURCES|Analysis Services の現在のインスタンス内のすべてのデータ ソースの一覧が表示されます。|  
  
> [!NOTE]  
>  表で示した内容がすべてではありません。トラブルシューティングに特に必要と思われる行セットのみを示しています。  
  
## <a name="examples"></a>使用例  
 次のセクションで、データ マイニング スキーマ行セットに対するクエリの例をいくつか示します。  
  
### <a name="example-1-list-data-mining-services"></a>例 1 : リストのデータ マイニング サービス  
 次のクエリでは、現在のサーバーで使用できるマイニング サービス、すなわち有効なアルゴリズムの一覧が返されます。 各マイニング サービスに対して指定される列には、各アルゴリズムで使用できるモデリング フラグとコンテンツの種類、各サービスの GUID、および各サービスに対して追加されている予測の制限が含まれます。  
  
```  
SELECT *  
FROM $system.DMSCHEMA_MINING_SERVICES  
```  
  
### <a name="example-2-list-mining-model-parameters"></a>例 2:マイニング モデル パラメーターの一覧  
 次の例では、特定のマイニング モデルの作成に使用されたパラメーターを返します。  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
### <a name="example-3-list-all-rowsets"></a>例 3: すべての行セットを一覧表示します。  
 次のクエリでは、現在のサーバーで使用できる行セットの詳細な一覧が返されます。  
  
```  
SELECT *   
FROM $system.DBSCHEMA_TABLES  
```  
  
## <a name="see-also"></a>参照  
 [トラブルシューティングの概念 (Analysis Services - データ マイニング)](https://msdn.microsoft.com/library/cc645881.aspx)  
  
  
