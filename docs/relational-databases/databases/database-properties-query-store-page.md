---
title: '[データベースのプロパティ] ([クエリ ストア] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 11/09/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.querystore.f1
ms.assetid: da47d75e-291a-4305-acef-4b0aaf5215da
author: stevestein
ms.author: sstein
ms.openlocfilehash: 592fa533d6c6d6c518f1dcaaa3e70da2808b93b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947024"
---
# <a name="database-properties-query-store-page"></a>データベースのプロパティ (クエリのストアのページ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このページにはプリンシパル データベースからアクセスし、これを使用してデータベースのクエリのストアのプロパティを構成および変更します。 これらのオプションは、 [ALTER DATABASE SET オプション](../../t-sql/statements/alter-database-transact-sql-set-options.md)を使用して構成することもできます。 クエリのストアの詳細については、「 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)」をご覧ください。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。|  
  
## <a name="options"></a>オプション  
 操作モード  
 有効な値は OFF、READ_ONLY、および READ_WRITE です。 OFF にすると、クエリのストアが無効になります。 READ_WRITE モードでは、クエリのストアでクエリ プランとランタイム実行の統計情報が収集および保持されます。 READ_ONLY モードでは、クエリのストアから情報を読み取ることができますが、新しい情報は追加されません。 クエリのストアの割り当て済み最大領域が不足すると、クエリのストアは操作モードを READ_ONLY にします。  
  
 操作モード (実際)  
 クエリのストアの実際の操作モードを取得します。  
  
 操作モード (要求)  
 クエリのストアの目的の操作モードを取得、および設定します。  
  
 データ フラッシュ間隔 (分)  
 クエリに書き込まれるデータ ストアが永続化する頻度を決定をディスクにします。 パフォーマンスを最適化するため、クエリ ストアで収集したデータは非同期的にディスクに書き込まれます。 この非同期転送が発生する頻度が構成されます。  
  
 統計情報の収集間隔  
 統計情報の収集間隔を取得、および設定します。  
  
 最大サイズ (MB)  
 クエリのストアに割り当てられた合計領域を取得、および設定します。  
  
 Query Store Capture Mode (クエリ ストアのキャプチャ モード)  
 -   [None] (なし) に設定すると、新しいクエリがキャプチャされません。  
  
-   [All] \(すべて) に設定すると、すべてのクエリがキャプチャされます。  
  
-   [Auto] (自動) に設定すると、リソースの消費量に基づいてクエリがキャプチャされます。  
  
 古いクエリのしきい値 (日)  
 古いクエリのしきい値を取得、および設定します。 STALE_QUERY_THRESHOLD_DAYS 引数を構成して、クエリのストア内にデータを保持する日数を指定します。  
  
 クエリ データの消去  
 クエリ ストアの内容を削除します。  
  
 円グラフ  
 左側のグラフには、ディスク上のデータベース ファイルの合計消費量、およびクエリのストアのデータを格納するファイルの部分が表示されます。  
  
 右側のグラフには、現在使用されているクエリのストアのクォータの部分が表示されます。 クォータは、左側のグラフには表示されないことにご注意ください。 クォータが、データベースの現在のサイズを超える場合があります。  
  
## <a name="remarks"></a>Remarks  
 クエリのストアの機能により、クエリ プランの選択やパフォーマンスに関する洞察が DBA に提供されます。 これにより、クエリ プランの変更によって生じるパフォーマンスの違いがすばやくわかるようになり、パフォーマンス上のトラブルシューティングを簡略化できます。 この機能により、クエリ、プラン、ランタイム統計情報の履歴が自動的にキャプチャされ、レビュー用に保持されます。 データは時間枠で区分されるため、データベースの使用パターンを表示して、サーバー上でクエリ プランが変わった時点を確認することができます。 クエリのストアは、クエリのストアのデータベース プロパティ ページを使用するか、 [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) オプションを使用して構成できます。 クエリのストアは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ダイアログ ボックスを使用して情報を表示します。 クエリのストアの詳細については、「 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [クエリ ストアのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
