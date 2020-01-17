---
ms.openlocfilehash: 78b372942de6ec62823dddecd08fdb7221cbe7a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68219686"
---


### <a name="index-stats-options"></a>インデックス統計オプション

<!--
This includes/paragraph-content/ file was created when processing vsts sqlbuvsts01 2999014 (5589131).  genemi  2017-07-21

Initially used in:
- relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md
- relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md
-->


以前のバージョンの Microsoft SQL Server では、システムの処理速度が低下して、大規模なインデックスを再構成または再構築することがありました。 SQL Server 2016 では、これらのインデックス操作のパフォーマンスが大幅に向上しました。

また、以前のバージョンでは、コントロールの粒度はそれほど細分化されていませんでした。 このため、インデックスがそれほど断片化されていない場合でも、システムがインデックスを再構成または再構築することがあり、無駄が生じていました。 メンテナンス プランのユーザー インターフェイス (UI) で新しいコントロールを使用すると、インデックス統計情報の条件を基にして、更新する必要がないインデックスを除外できます。 この場合、次の Transact-SQL の動的管理ビュー (Dmv) が内部的に使用されます。


- [sys.dm_db_index_usage_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)
- [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)


 **[スキャンの種類]**  
 システムは、インデックス統計情報を収集するために、リソースを使用する必要があります。 必要とするインデックス統計情報の精度に応じて、比較的少ないリソースを消費するか、多くのリソースを消費するかを選択できます。 UI には次の精度レベルの一覧があり、ユーザーはそのうち 1 つを選択する必要があります。


- [高速]
- サンプリング
- 詳細


 **次の場合に限りインデックスを最適化する**  
 UI には、まだ最新情報に更新する必要のないインデックスが更新されないようにするために使用できる、次の調節可能なフィルターが提供されています。


- 断片化&gt; *(%)*
- ページ数&gt;
- 最終使用 *(日)*

