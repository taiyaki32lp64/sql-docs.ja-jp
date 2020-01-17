---
title: 拡張イベントを使用した T-SQL の監視
description: 拡張イベントを使用して、SQL Server Machine Learning Services で PREDICT T-SQL ステートメントを監視およびトラブルシューティングする方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9e891ee16ce664e12f12b16c9deda957d0fa2263
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727726"
---
# <a name="monitor-predict-t-sql-statements-with-extended-events-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services の拡張イベントで PREDICT T-SQL ステートメントを監視する

拡張イベントを使用して、SQL Server Machine Learning Services で [PREDICT](../../t-sql/queries/predict-transact-sql.md) T-SQL ステートメントを監視およびトラブルシューティングする方法について説明します。

## <a name="table-of-extended-events"></a>拡張イベントの表

次の拡張イベントは、[PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) T-SQL ステートメントをサポートするすべてのバージョンの SQL Server で使用できます。 

|NAME |object_type|description| 
|----|----|----|
|predict_function_completed |イベント  |組み込み実行時間のブレークダウン|
|predict_model_cache_hit |イベント|モデルが PREDICT 関数モデル キャッシュから取得されるときに発生します。 PREDICT 関数モデル キャッシュが原因で発生した問題についてトラブルシューティングを行うには、このイベントを他の predict_model_cache_* イベントと共に使用します。|
|predict_model_cache_insert |イベント  |   モデルが PREDICT 関数モデル キャッシュに挿入されるときに発生します。 PREDICT 関数モデル キャッシュが原因で発生した問題についてトラブルシューティングを行うには、このイベントを他の predict_model_cache_* イベントと共に使用します。    |
|predict_model_cache_miss   |イベント|モデルが PREDICT 関数モデル キャッシュで見つからないときに発生します。 このイベントが頻繁に発生する場合、SQL Server がより多くのメモリを必要としていることを示している可能性があります。 PREDICT 関数モデル キャッシュが原因で発生した問題についてトラブルシューティングを行うには、このイベントを他の predict_model_cache_* イベントと共に使用します。|
|predict_model_cache_remove |イベント| モデルが PREDICT 関数のモデル キャッシュから削除されるときに発生します。 PREDICT 関数モデル キャッシュが原因で発生した問題についてトラブルシューティングを行うには、このイベントを他の predict_model_cache_* イベントと共に使用します。|

## <a name="query-for-related-events"></a>関連イベントをクエリします。

これらのイベントに対して返されたすべての列の一覧を表示するには、SQL Server Management Studio で次のクエリを実行します。

```sql
SELECT * 
FROM sys.dm_xe_object_columns 
WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>使用例

PREDICT を使用してスコアリング セッションのパフォーマンスに関する情報を取得するには次の手順を実行します。

1. Management Studio またはサポートされている別の[ツール](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)を使用して、新しい拡張イベント セッションを作成します。
2. イベント `predict_function_completed` と `predict_model_cache_hit` をセッションに追加します。
3. 拡張イベント セッションを開始します。
4. PREDICT を使用するクエリを実行します。

結果で次の列を確認します。

+ `predict_function_completed` の値は、モデルの読み込みとスコアリングのためにクエリが費やした時間を示します。
+ `predict_model_cache_hit` のブール値は、クエリがキャッシュされたモデルを使用したかどうかを示します。 

### <a name="native-scoring-model-cache"></a>ネイティブ スコアリング モデル キャッシュ

PREDICT 固有のイベントに加えて、次のクエリを使用して、キャッシュされたモデルとキャッシュの使用に関する詳細情報を取得できます。

ネイティブ スコアリング モデル キャッシュの表示:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

モデル キャッシュ内のオブジェクトの表示:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

## <a name="next-steps"></a>次の手順

拡張イベント (XEvent と呼ばれることもあります) の詳細と、セッションのイベントを追跡する方法の詳細については、次の記事を参照してください。

+ [SQL Server Machine Learning Services の拡張イベントで Python および R のスクリプトを監視する](extended-events.md)
+ [拡張イベントの概念とアーキテクチャ](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [SSMS でのイベント キャプチャの設定](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [SQL Server オブジェクト エクスプローラーでのイベント セッションの管理](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)
