---
title: カタログビュー (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql13.SysViewExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- catalog metadata [SQL Server]
- system views [SQL Server], catalog
- metadata [SQL Server], views
- catalogs [SQL Server], metadata
- catalog views [SQL Server]
- Database Engine [SQL Server], metadata
- catalog views [SQL Server], about catalog views
ms.assetid: 13bccc2f-ed3c-4b58-abd0-ca8bf34a66b8
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9532ee19ec8489caa51d090feaff464e030a0da0
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670555"
---
# <a name="system-catalog-views-transact-sql"></a>システムカタログビュー (Transact-sql)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

カタログ ビューは、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]によって使用される情報を返します。 カタログ ビューはカタログ メタデータへの最も一般的なインターフェイスであり、この情報を取得、変換、およびカスタマイズした形式で表示するための、最も効率的な方法となります。したがって、カタログ ビューを使用することをお勧めします。 ユーザーが利用できるすべてのカタログ メタデータがカタログ ビューを通じて公開されています。

> [!NOTE]
> カタログ ビューには、レプリケーション、バックアップ、データベース メンテナンス プラン、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントなどのカタログ データに関する情報は含まれていません。

 カタログ ビューの中には、他のカタログ ビューの行を継承するものもあります。 たとえば、、[テーブル](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)カタログビューは、の[各カタログビュー](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)を継承します。 Sys. objects カタログビューはベースビューと呼ばれ、sys ビューは派生ビューと呼ばれます。 sys.tables カタログ ビューではテーブルに固有の列のほか、sys.objects カタログ ビューで返されるすべての列が返されます。 Sys. objects カタログビューでは、ストアドプロシージャやビューなど、テーブル以外のオブジェクトの行が返されます。 テーブルが作成されると、両方のビューでテーブルのメタデータが返されます。 2つのカタログビューでは、テーブルに関する異なるレベルの情報が返されますが、このテーブルのメタデータには、1つの名前と1つの object_id を持つエントリが1つだけあります。 まとめると次のようになります。

- ベース ビューには列のサブセットと行のスーパーセットが含まれます。
- 派生ビューには列のスーパーセットと行のサブセットが含まれます。

> [!IMPORTANT]
> 今後の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] のリリースでは、列のリストの末尾に列を追加することにより、システム カタログ ビューの定義が拡張される可能性があります。 返される列の数が変更\*され、アプリケーションが中断される可能性があるため、実稼働コードで SELECT FROM *catalog_view_name*を使用することをお勧めします。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のカタログ ビューは、次のカテゴリに分類されます。

|||
|-|-|
|[Always On 可用性グループのカタログ&#40;ビュー transact-sql&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)|[ &#40;エラー&#41;のメッセージカタログビュー &#40;transact-sql&#41;](../system-catalog-views/messages-for-errors-catalog-views-sys-messages.md))|
|[カタログビューの Azure SQL Database](../../relational-databases/system-catalog-views/azure-sql-database-catalog-views.md)|[オブジェクトカタログビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)|
|[Change Tracking カタログビュー &#40;transact-sql&#41;](../system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)|[パーティション関数のカタログ&#40;ビュー transact-sql&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)|
|[CLR アセンブリカタログビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)|[ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)|
|[データコレクタービュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)|[Resource Governor カタログビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)|
|[データスペース&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)|[クエリ ストアのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)|
|[データベースメールビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)|[スカラー型カタログビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)|
|[データベースミラーリング監視サーバーの&#40;カタログビュー transact-sql&#41;](../system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)|[スキーマカタログビュー &#40;transact-sql&#41;](../system-catalog-views/schemas-catalog-views-sys-schemas.md)|
|[データベースとファイルのカタログ&#40;ビュー transact-sql&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)|[セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|
|[エンドポイントカタログ&#40;ビュー transact-sql&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)|[Service Broker カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)|
|[拡張イベント カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)|[サーバー全体の構成カタログビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)|
|[拡張プロパティ カタログ ビュー &#40;Transact-SQL&#41;](../system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)|[空間 Data Catalog ビュー](../../relational-databases/system-catalog-views/spatial-data-catalog-views.md)|
|[外部の操作カタログ&#40;ビュー transact-sql&#41;](../../relational-databases/system-catalog-views/external-operations-catalog-views-transact-sql.md)|[SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)|
|[Filestream および FileTable のカタログ&#40;ビュー transact-sql&#41;](../../relational-databases/system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)|[Stretch Database カタログビュー &#40;transact-sql&#41;](../system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-databases.md)|
|[フルテキスト検索とセマンティック検索カタログビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)|[XML スキーマ&#40;Xml 型システム&#41;カタログビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)|
|[リンクサーバーのカタログ&#40;ビュー transact-sql&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)||

## <a name="see-also"></a>関連項目

- [情報スキーマビュー &#40;transact-sql&#41;](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
- [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)
