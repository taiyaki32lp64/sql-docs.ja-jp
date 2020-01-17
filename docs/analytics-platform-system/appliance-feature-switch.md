---
title: 機能スイッチ
description: Analytics Platform System AU7 に導入された2つの機能スイッチに関する情報を表示します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 8642f27a329da8819acf0ab99a648c4979ed40d0
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401452"
---
# <a name="appliance-feature-switches"></a>アプライアンスの機能スイッチ

[**機能の切り替え**] ページには、Analytics PLATFORM System AU7 以降で導入されている機能スイッチに関する情報が表示されます。 この構成ページを使用して、Analytics Platform System の機能と設定を更新または有効/無効にします。

> [!NOTE]
> 機能スイッチの値を変更するには、サービスを再起動する必要があります。

![DWConfig アプライアンス機能スイッチ](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConfig アプライアンス機能スイッチ")

## <a name="autostatsenabled"></a>AutoStatsEnabled

自動統計機能を制御します。 AU7 にアップグレードすると、この機能スイッチは既定で true に設定されます。 アップグレード後に作成されたすべてのデータベースは、統計の自動作成と非同期更新を継承します。 既存のデータベースの場合、データベース管理者は[ALTER database (Parallel Data Warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)で自動統計を有効にすることができます。 統計の詳細については、「[統計](../relational-databases/statistics/statistics.md)」を参照してください。

## <a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries

挿入/選択操作に対して1を超える maxdop 設定を選択できます。 この設定のオプションは0、1、2、4で、既定値は1です。

## <a name="optimizecommonsubexpressions"></a>OptimizeCommonSubExpressions

では、SQL クエリオプティマイザーで共通部分式のデータ移動が行われなくなるため、クエリのパフォーマンスが向上します。 この機能の詳細については、[こちら](common-sub-expression-elimination.md)を参照してください。

## <a name="usecatalogqueries"></a>UseCatalogQueries

SMO を使用する代わりに、一部のメタデータ呼び出しに catalog オブジェクトを使用すると、パフォーマンスが向上しています。 CU 7.1 で既定で true に設定されている場合、このスイッチはその動作を制御します。

## <a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds

データ移動サービス (DMS) が、データ移動を含むクエリが取り消されたときに、ビジー状態のシステムでの同期を待機する時間を制御します。 AU7 に更新すると、既定では、この値は900秒 (15 分) に設定されます。 有効な範囲は 0-3600 秒です。
