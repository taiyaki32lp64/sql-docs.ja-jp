---
title: 自動チューニング |Microsoft Docs
description: SQL Server と Azure SQL Database で自動チューニングについて説明します
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ad185085c19d8286fa6a09e46742860a948849a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934556"
---
# <a name="automatic-tuning"></a>自動調整
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

自動チューニングは、潜在的なクエリ パフォーマンスの問題に関する洞察を提供し、解決策を推奨して、特定された問題を自動的に解決するデータベース機能です。

自動チューニング[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]潜在的なパフォーマンスの問題が検出され、修正措置を適用することができますが常に通知することもできます、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]自動的にパフォーマンスの問題を修正します。
自動チューニング[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]特定し、によるパフォーマンスの問題を修正することができます**クエリ実行プランの選択による後退**します。 自動チューニング[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]も必要なインデックスを作成し、未使用のインデックスを削除します。 クエリ実行プランの詳細については、次を参照してください。[実行プラン](../../relational-databases/performance/execution-plans.md)します。

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]モニター、データベースと自動的に実行されるクエリ ワークロードのパフォーマンスが向上します。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]組み込みのインテリジェンス メカニズムを自動的に調整して、ワークロードにデータベースを動的に適応することで、クエリのパフォーマンスを向上させることができます。 利用できる 2 つの自動チューニング機能があります。

 -  **自動プラン修正**問題のあるクエリ実行プランし、クエリの実行プランのパフォーマンスに関する問題の修正を識別します。 **適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
 -  **自動インデックス管理**を削除するインデックスと、データベースに追加するインデックスを識別します。 **適用対象**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

## <a name="why-automatic-tuning"></a>なぜ自動チューニングでしょうか。

特定の重要なワークロードを監視で従来のデータベース管理の主要なタスクのうち 3 つ[!INCLUDE[tsql_md](../../includes/tsql-md.md)]クエリ、インデックスをほとんど使用のパフォーマンスを向上させるために追加し、識別する必要があります。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]クエリと監視が必要なインデックスの詳細な洞察を提供します。 ただし、多数のデータベースを扱う場合は特に、ハード面倒なタスクがは常にデータベースを監視します。 膨大な数のデータベースを管理するは、効率的に実行することでない可能性があります。 監視と、データベースを手動でチューニング、代わりに委任する一部の監視とチューニング アクションを検討する可能性があります、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]自動チューニング機能を使用します。

### <a name="how-does-automatic-tuning-work"></a>どのように自動チューニング機能でしょうか。

自動チューニングと、継続的監視と分析プロセス、ワークロードの特性についての継続的に学習するには、潜在的な問題と改善点を識別します。

![自動チューニング プロセス](./media/tuning-process.png)

このプロセスにより、インデックスとプランのワークロードのパフォーマンスは向上し、ワークロードに影響するインデックスを検索して、ワークロードに動的に適応するデータベースです。 この調査結果に基づいてに自動チューニングを実行すると、ワークロードのパフォーマンスを向上させるチューニング アクションは適用されます。 さらに、データベースでは、継続的に、ワークロードのパフォーマンスが向上することを確実に自動チューニングによる変更後のパフォーマンスを監視します。 パフォーマンスを向上しなかったすべてのアクションは自動的に元に戻されます。 この検証プロセスは、自動チューニングによる変更が、ワークロードのパフォーマンスを低下しないようにする重要な機能です。

## <a name="automatic-plan-correction"></a>自動プラン修正

自動プラン修正は、自動チューニング機能を識別する**実行プランの選択の回帰**最後の既知の良好なプランを強制することで、問題を自動的に解決します。 詳細については、クエリ実行プランとクエリ オプティマイザーは、次を参照してください。、[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)します。

### <a name="what-is-execution-plan-choice-regression"></a>実行プランの選択の回帰とは何ですか。

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)]さまざまな実行プランを使用して実行することがあります、[!INCLUDE[tsql_md](../../includes/tsql-md.md)]クエリ。 クエリ プランは、統計、インデックス、およびその他の要因に依存します。 いくつかを実行するために使用する必要があります、最適なプラン[!INCLUDE[tsql_md](../../includes/tsql-md.md)]クエリは、時間の経過と共に変更可能性があります。 場合によっては、新しいプランを先ほどよりも優れていますできない可能性があり、新しいプラン、パフォーマンスの低下が発生する可能性があります。

 ![クエリ実行プランの選択の回帰](media/plan-choice-regression.png "クエリ実行プランの選択の回帰") 

プラン選択の回帰のことを確認するたびに、以前正常なは、計画し、現在の 1 つ使用する代わりに強制的を検索する必要があります`sp_query_store_force_plan`プロシージャ。
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 機能低下したプランと是正措置をお勧めしますについての情報を提供します。
さらに、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]を使用すると、完全にこのプロセスを自動化し、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]プランの変更に関連するすべての問題を修正します。

### <a name="automatic-plan-choice-correction"></a>自動プラン選択修正

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] プランの選択の回帰が検出されるたびに、最後の既知の良好なプランに切り替える自動的にできます。

![クエリ実行プラン選択修正](media/force-last-good-plan.png "クエリ実行プラン選択修正") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 自動的に正しくないプランの代わりに使用する計画を含む、潜在的なプラン選択肢回帰を検出します。
ときに、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]適用の最後の既知の適切なプランを自動的に監視、適用されたプランのパフォーマンス。 新しいプランが強制されます、強制されたプランが機能低下したプランよりも適切でない場合、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]新しいプランをコンパイルします。 場合、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]強制されたプランが機能低下したプランよりも優れていますが、(たとえば、次の統計情報更新やスキーマの変更) 上に再コンパイルが行われるまで後退したプランよりも優れていますが、適用されたプランが保持されることを確認します。

> [!NOTE]
> 強制実行プランの自動任意は再起動の間は保持されません、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス。

### <a name="enabling-automatic-plan-choice-correction"></a>自動プラン選択修正を有効にします。

データベースごとに自動調整を有効にし、プラン変更の機能低下が検出されたときは最後の正常なプランを適用することを指定できます。 自動調整は、次のコマンドを使って有効にします。

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```

このオプションを有効にすると、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]は自動的に推定される CPU ゲインが 10 秒を超えるまたは推奨されるプランでは、新しいプランでのエラーの数がエラーの数よりも高い位置には、任意の推奨インデックスを強制し、いることを確認します強制されたプランは現在よりも優れています。

### <a name="alternative---manual-plan-choice-correction"></a>代替 - 手動プラン選択修正

自動調整しないときは、ユーザーが定期的にシステムを監視し、機能低下したクエリを検索する必要があります。 以前正常なは、計画し、現在の 1 つ使用する代わりに強制的にユーザーが見つける場合は、プランが機能低下した、`sp_query_store_force_plan`プロシージャ。 ベスト プラクティスは、古いプランが統計またはインデックスの変更のために有効な可能性があるために、最後の既知の良好なプランを強制することです。 最後の既知の良好なプランを強制的のユーザーは、強制されたプランを使用して実行されるクエリのパフォーマンスを監視し、その強制されたプランが期待どおりに動作することを確認する必要があります。 監視と分析の結果に応じてプランを適用する必要があります。 またはユーザーがクエリの最適化を他の何らかの方法を見つける必要があります。
手動で強制適用されたプランはならない、永久にため、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]最適なプランを適用できる必要があります。 ユーザーまたは DBA が最終的に強制プランを使用して、`sp_query_store_unforce_plan`され、let、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]最適なプランを検索します。 

> [!TIP]
> Alternativelly、使用、**強制プランとクエリ**クエリ ストア ビューを検索して、プランを強制します。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] すべての必要なビューとパフォーマンスを監視し、クエリ ストアで問題を修正するために必要な手順を説明します。

[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]、クエリ ストアのシステム ビューを使用したプランの選択による後退を見つけることができます。 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]を検出し、潜在的なプランの選択による後退とに適用される推奨される操作を示しています、 [sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)ビュー。 問題、機能低下したプランの ID、比較については、ベースラインとして使用されていたプランの ID は、識別されたクエリなどの詳細と、問題の重要性に関する情報を表示、[!INCLUDE[tsql_md](../../includes/tsql-md.md)]ステートメントを修正するために実行できますが、問題があります。

| type | description | DATETIME | score | 詳細情報 | [...] |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | CPU 時間が 4 ミリ秒から 14 ミリ秒に変更されました | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | 37 ms から 84 ミリ秒に変更された CPU 時間 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

このビューから一部の列は、次の一覧について説明します。
 - -推奨されるアクションの種類 `FORCE_LAST_GOOD_PLAN`
 - なぜ情報を含む説明[!INCLUDE[ssde_md](../../includes/ssde_md.md)]このプランの変更に、潜在的なパフォーマンスの低下があると思われる
 - 潜在的な低下が検出された日時
 - この推奨事項のスコア
 - 検出されたプランを強制的に、問題を解決するプランの ID、後退したプランの ID の ID などの問題の詳細について[!INCLUDE[tsql_md](../../includes/tsql-md.md)]スクリプトなどの問題を修正するために適用可能性があります。詳細が格納されている[JSON の形式](../../relational-databases/json/index.md)

使用して、問題と、推定に関する追加情報を修正するスクリプトを入手する次のクエリが得られます。

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressedPlanId int '$.regressedPlanId',
            recommendedPlanId int '$.recommendedPlanId',
            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,
            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float
          ) AS planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | スクリプト (script) | query\_id | 現在のプラン\_id | プランをお勧めします\_id | 推定\_を得る | エラー\_発生しやすい
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CPU 時間が 3 ミリ秒から 46 ミリ秒に変更されました | 36 | EXEC sp\_クエリ\_格納\_強制\_プラン 12、17 です。 | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` 現在のプランではなく実行される、推奨される計画が保存されます秒の推定数を表します。 ゲインが 10 秒より大きい場合は、現在のプランではなくをお勧めのプランを強制する必要があります。 推奨される現在のプランよりも多くのエラー (たとえば、タイムアウトまたは中止された実行) がある場合の計画、列`error_prone`値に設定が`YES`します。 エラーが発生しやすいプランは、推奨されるプランを適用して、現在ではなく理由別の理由です。

[!INCLUDE[ssde_md](../../includes/ssde_md.md)]プラン選択の回帰は継続的な監視とパフォーマンスの問題の修正を識別するために必要なすべての情報には、面倒な可能性がありますを提供します。 自動チューニングと、このプロセスがはるかに簡単になります。

> [!NOTE]
> Sys.dm_db_tuning_recommendations DMV 内のデータは、再起動の間は保持されません、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス。

## <a name="automatic-index-management"></a>インデックスの自動管理

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]、インデックスの管理が容易なため、[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]はワークロードについて学習し、データが常に最適な状態でインデックス付けされることを確認します。 適切なインデックスの設計は、ワークロードの最適なパフォーマンスにとって非常に重要とインデックスの自動管理では、インデックスを最適化するのに役立ちます。 インデックスの自動管理いずれかが正しくないインデックス付きデータベースのパフォーマンスの問題を修正またはを維持でき、既存のデータベース スキーマのインデックスを強化できます。 自動チューニング[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]は、次の操作を実行します。

 - パフォーマンスを向上させることがインデックスを識別、[!INCLUDE[tsql_md](../../includes/tsql-md.md)]テーブルからデータを読み取るクエリ。
 - 冗長なインデックスを削除できませんでした時間の長い期間使用されていないインデックスを識別します。 不要なインデックスを削除するには、テーブル内のデータを更新するクエリのパフォーマンスが向上します。

### <a name="why-do-you-need-index-management"></a>インデックスの管理が必要な理由

インデックスでは、テーブルからデータを読み取るクエリの一部を高速化します。ただし、データを更新するクエリ速度が低下することができます。 インデックスを作成するときに、どのような列を慎重に分析する必要がある、インデックスに含める必要があります。 一部のインデックスは、しばらく必要はありません。 そのため、定期的に識別して、すべての特典を表示しないインデックスを削除する必要があります。 未使用のインデックスを無視すると、データを読み取るクエリの利点が得せずデータを更新するクエリのパフォーマンスが低下するは。 未使用のインデックスでは、追加の更新プログラムが不要なログを必要とするため、システム全体のパフォーマンスも影響します。

テーブルからデータを読み取り、更新プログラムの最小限の影響を与えるクエリのパフォーマンスを向上させるインデックスの最適なセットを見つけると、継続的で複雑な分析が必要があります。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 使用して組み込みのインテリジェンスと分析、クエリでは、高度なルールは、現在のワークロードに対して最適なインデックスを識別して、インデックスを削除する可能性があります。 Azure SQL Database の場合は、インデックスを他のクエリに対する影響を最小化されたデータを読み取るクエリの最適化のために必要な最低限に維持します。

### <a name="automatic-index-management"></a>インデックスの自動管理

検出、に加えて[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]特定された推奨事項を自動的に適用できます。 組み込みの規則が、データベースのパフォーマンスを向上させる場合は、することができます[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]インデックスを自動的に管理します。

自動チューニングを有効にする[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]完全ワークロードの管理を参照してください、自動チューニング機能と[Azure portal を使用して Azure SQL Database での自動チューニングを有効にする](/azure/sql-database/sql-database-automatic-tuning-enable)します。

ときに、 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] CREATE INDEX や DROP INDEX の推奨事項の適用、インデックスの影響を受けるクエリのパフォーマンスを自動的に監視します。 影響を受けるクエリのパフォーマンスが向上する場合にのみ、新しいインデックスが保持されます。 インデックスがないのために実行速度が低下するいくつかのクエリがある場合、ドロップされたインデックスは自動的に再作成されます。

### <a name="automatic-index-management-considerations"></a>自動インデックス管理の考慮事項

必要なインデックスの作成に必要なアクション[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]リソースを消費し、一時的にワークロードのパフォーマンスに影響する可能性があります。 ワークロードのパフォーマンスのインデックス作成の影響を最小限に抑える[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]インデックス管理操作の適切な時間枠を検索します。 データベース ワークロードを実行するリソースを必要とする場合の延期し、データベースには十分なときに開始チューニング アクションは、メンテナンス タスクで使用できる未使用のリソース。 自動インデックス管理の 1 つの重要な機能は、アクションの検証です。 ときに[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]作成または削除、インデックス監視プロセスは、アクションが、パフォーマンスを向上することを確認するワークロードのパフォーマンスを分析します。 -が大幅に向上を提供していない場合、アクションはすぐに戻されます。 これにより、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]する自動アクション悪い影響を与えない、ワークロードのパフォーマンスをによりします。 自動チューニングによって作成されたインデックスは、基になるスキーマでのメンテナンス操作に対して透過的です。 削除するか、列名の変更などのスキーマ変更は自動的に作成されたインデックスの存在によってブロックされません。 によって自動的に作成されるインデックス[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]とすぐに削除がテーブルまたは列の削除に関連します。

### <a name="alternative---manual-index-management"></a>代替 - 手動のインデックスの管理

ユーザーは手動でクエリを実行する必要があります、自動インデックス管理[sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)でパフォーマンス ダッシュ ボード レポートを表示または[!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]が検索インデックスにパフォーマンスを向上させる、このビューで詳細情報を使用してインデックスを作成し、手動でクエリのパフォーマンスを監視します。 削除するインデックスを検索するには、するには、ユーザーはあまり使われない検索インデックスにインデックスの運用上の使用状況の統計を監視する必要があります。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] このプロセスを簡略化します。 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] ワークロードを分析し、新しいインデックスでは、高速実行するクエリが識別されます未使用または重複するインデックスを識別します。 変更する必要があるインデックスの識別に関する詳細情報[Azure portal でのインデックスの推奨事項を見つける](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal)します。

## <a name="see-also"></a>参照  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 関数](../../relational-databases/json/index.md)    
 [実行プラン](../../relational-databases/performance/execution-plans.md)    
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [パフォーマンス監視およびチューニング ツール](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [クエリのチューニング アシスタント](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)
