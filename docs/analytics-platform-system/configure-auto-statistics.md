---
title: 自動統計
description: Analytics Platform System AU7 で導入された自動統計機能について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 7071c9cb46bde6e2d353293cec9f01451c0b4f67
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401283"
---
# <a name="configure-auto-statistics"></a>自動統計の構成

自動統計を使用して統計を自動的に作成および更新するように並列データウェアハウスを構成する方法について説明します。  この機能を使用すると、クエリプランが向上し、クエリのパフォーマンスが向上します。

**適用対象:** APS (2016 から開始) (AU7)

## <a name="what-are-statistics"></a>統計とは何ですか。
クエリ最適化の統計情報は、テーブルの1つまたは複数の列の値の分布に関する統計情報を含むオブジェクトです。 クエリ オプティマイザーでは、これらの統計を使用してクエリ結果のカーディナリティ、つまり行数を推定します。 これらのカーディナリティの推定に基づいて、クエリ オプティマイザーでは高品質なクエリ プランを作成できます。 たとえば、APS では、MPP クエリオプティマイザーはカーディナリティの推定を使用して、join 句で使用される2つのテーブルのうち小さい方のテーブルをシャッフルまたはレプリケートすることを選択します。これにより、クエリのパフォーマンスが向上します。  詳細については、「[統計](../relational-databases/statistics/statistics.md)と[DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) 」を参照してください。

## <a name="what-are-auto-statistics"></a>自動統計とは何ですか。
自動統計とは、クエリオプティマイザーによって自動的に作成および更新され、クエリプランを改善するための統計です。 読み込み、挿入、更新、削除の各操作の後、統計が古くなる可能性があります。 自動統計を使用しない場合は、統計が必要な列と統計を更新する必要があるかを理解するために、独自の分析を行う必要があります。

自動統計には、次の3つの設定が含まれます。 

### <a name="auto_create_statistics"></a>AUTO_CREATE_STATISTICS
統計の自動作成オプション AUTO_CREATE_STATISTICS が ON の場合、クエリ プランのカーディナリティの推定を向上させるために、クエリ オプティマイザーによってクエリ述語内の個々の列に関する統計が必要に応じて作成されます。 これらの 1 列ずつの統計は、既存の統計オブジェクトにまだヒストグラムがない列について作成されます。

### <a name="auto_update_statistics"></a>AUTO_UPDATE_STATISTICS 
統計の自動更新オプション AUTO_UPDATE_STATISTICS がオンの場合、古くなっている可能性がある統計がクエリ オプティマイザーによって判断され、それらがクエリで使用されると更新されます。 挿入、更新、削除、またはマージの各操作によってテーブルまたはインデックス付きビューのデータの分布が変わると、統計は古くなったと判断されます。 クエリ オプティマイザーでは、統計が前回更新されてから発生したデータ変更の数をカウントし、その変更の数をしきい値と比較することで、統計が古くなっている可能性がないかを判断します。 このしきい値は、テーブルまたはインデックス付きビューの行数に基づいて決められます。

### <a name="auto_update_statistics_async"></a>AUTO_UPDATE_STATISTICS_ASYNC
統計の非同期更新オプション AUTO_UPDATE_STATISTICS_ASYNC によって、クエリ オプティマイザーで統計の同期更新と非同期更新のどちらを使用するかが決まります。 APS では、統計の非同期更新オプションが既定でオンになっており、クエリオプティマイザーによって統計が非同期的に更新されます。 AUTO_UPDATE_STATISTICS_ASYNC オプションは、インデックスに対して作成された統計オブジェクト、クエリ述語内の列に対して 1 列ずつ作成された統計オブジェクト、および CREATE STATISTICS ステートメントを使用して作成された統計に適用されます。

## <a name="configuration-settings-for-system-administrators"></a>システム管理者の構成設定
APS AU7 にアップグレードすると、既定で自動統計が有効になります。 システム管理者は、アプライアンス Configuration Manager の [[機能スイッチ](appliance-feature-switch.md)] オプションで自動統計を有効または無効にすることができます。  有効にすると、ユーザーはデータベースごとに統計設定を変更できます。
機能スイッチの値を変更するには、APS でサービスを再起動する必要があります。

## <a name="change-auto-statistics-settings-on-a-database"></a>データベースの自動統計設定を変更する
システム管理者によって自動統計が有効になっている場合は、 [ALTER database (並列データウェアハウス)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)を使用して、データベースの統計設定を変更できます。 自動統計機能スイッチがシステム管理者によって有効にされている場合、AU7 へのアップグレード後に新しく作成されたデータベースでは、自動統計が有効になります。 AU7 へのアップグレード前に存在していたすべてのデータベースで、自動統計が無効になっています。 次の例では、既存のデータベース myPDW で自動統計を有効にします。

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
AUTO_UPDATE STATISTICS_ASYNC オプションは AUTO_UPDATE_STATISTICS がオンの場合にのみ機能します。  そのため、AUTO_UPDATE_STATISTICS がオフで AUTO_UPDATE_STATISTICS_ASYNC がオンになっている場合、統計は更新されません。 

### <a name="error-messages"></a>エラー メッセージ
"このオプションは PDW ではサポートされていません" というエラーメッセージが表示されることがあります。  このエラーは、システム管理者が自動統計を有効にせず、ALTER DATABASE で自動統計オプションを設定しようとした場合に発生します。 

### <a name="limitations-and-restrictions"></a>制限事項と制約事項
自動統計は、外部テーブルでは機能しません。 

### <a name="check-the-current-values"></a>現在の値を確認する
次のクエリは、すべてのデータベースの自動統計設定の現在の値を返します。

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

戻り値1は、設定が on であることを意味し、0は設定がオフであることを意味します。 

## <a name="next-steps"></a>次の手順
クエリの実行方法を確認するには、「[アクティブなクエリの監視](monitoring-active-queries.md)」を参照してください。
