---
title: T-SQL ステートメント
description: 並列データウェアハウス (PDW) SQL Server の、分析プラットフォームシステム (APS) の t-sql ステートメント。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ce80d7a27384f628af02bfa58abcaa351b569d56
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399811"
---
# <a name="t-sql-statements-for-parallel-data-warehouse"></a>Parallel Data Warehouse の t-sql ステートメント
分析プラットフォームシステム (APS) の transact-sql (T-sql) ステートメントでは、並列データウェアハウス (PDW) SQL Server ます。

## <a name="data-definition-language-ddl-statements"></a>データ定義言語 (DDL) ステートメント
* [データベースの変更](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER PROCEDURE](../t-sql/statements/alter-procedure-transact-sql.md)
* [スキーマの変更](../t-sql/statements/alter-schema-transact-sql.md)
* [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)
* [列ストアインデックスの作成](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [データベースの作成](../t-sql/statements/create-database-azure-sql-data-warehouse.md)
* [データベーススコープ資格情報の作成](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [外部データソースの作成](../t-sql/statements/create-external-data-source-transact-sql.md)
* [外部ファイル形式の作成](../t-sql/statements/create-external-file-format-transact-sql.md)
* [外部テーブルの作成](../t-sql/statements/create-external-table-transact-sql.md)
* [関数の作成](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md)
* [プロシージャの作成](../t-sql/statements/create-procedure-transact-sql.md)
* [スキーマの作成](../t-sql/statements/create-schema-transact-sql.md)
* [統計の作成](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [SELECT として CREATE TABLE](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [ビューの作成](../t-sql/statements/create-view-transact-sql.md)
* [外部データソースの削除](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [外部のファイル形式を削除します。](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [外部テーブルの削除](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [DROP PROCEDURE](../t-sql/statements/drop-procedure-transact-sql.md)
* [統計の削除](../t-sql/statements/drop-statistics-transact-sql.md)
* [テーブルの削除](../t-sql/statements/drop-table-transact-sql.md)
* [スキーマの削除](../t-sql/statements/drop-schema-transact-sql.md)
* [ビューの削除](../t-sql/statements/drop-view-transact-sql.md)
* [リネーム](../t-sql/statements/rename-transact-sql.md)
* [TRUNCATE TABLE](../t-sql/statements/truncate-table-transact-sql.md)
* [統計の更新](../t-sql/statements/update-statistics-transact-sql.md)

## <a name="data-manipulation-language-dml-statements"></a>データ操作言語 (DML) ステートメント
* [デリート](../t-sql/statements/delete-transact-sql.md)
* [INSERT](../t-sql/statements/insert-transact-sql.md)
* [UPDATE](../t-sql/queries/update-transact-sql.md)

## <a name="database-console-commands"></a>データベース コンソール コマンド
* [DBCC DROPCLEANBUFFERS](../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)
* [DBCC フリープロセッサキャッシュ](https://msdn.microsoft.com/library/mt204018.aspx)
* [DBCC SHRINKLOG](https://msdn.microsoft.com/library/mt204020.aspx)
* [DBCC PDW_SHOWEXECUTIONPLAN](https://msdn.microsoft.com/library/mt204017.aspx)
* [DBCC PDW_SHOWPARTITIONSTATS](https://msdn.microsoft.com/library/mt204013.aspx)
* [DBCC PDW_SHOWSPACEUSED](../t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql.md)
* [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/mt204043.aspx)

## <a name="query-statements"></a>クエリ ステートメント
* [クリック](../t-sql/queries/select-transact-sql.md)
* [Common_table_expression](../t-sql/queries/with-common-table-expression-transact-sql.md)
* [EXCEPT および INTERSECT](../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)
* [受講](../t-sql/queries/explain-transact-sql.md)
* [差出人](../t-sql/queries/from-transact-sql.md)
* [PIVOT および UNPIVOT の使用](../t-sql/queries/from-using-pivot-and-unpivot.md)
* [GROUP BY](../t-sql/queries/select-group-by-transact-sql.md)
* [HAVING](../t-sql/queries/select-having-transact-sql.md)
* [並べ替え](../t-sql/queries/select-order-by-clause-transact-sql.md)
* [オプション](../t-sql/queries/option-clause-transact-sql.md)
* [組合](../t-sql/language-elements/set-operators-union-transact-sql.md)
* [どこ](../t-sql/queries/where-transact-sql.md)
* [TOP](../t-sql/queries/top-transact-sql.md)
* [別名](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [検索条件](../t-sql/queries/search-condition-transact-sql.md)
* [サブクエリ](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>セキュリティ ステートメント
* 権限: [GRANT](../t-sql/statements/grant-transact-sql.md)、[DENY](../t-sql/statements/deny-transact-sql.md)、[REVOKE](../t-sql/statements/revoke-transact-sql.md)
* [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)
* [証明書の変更](../t-sql/statements/alter-certificate-transact-sql.md)
* [データベース暗号化キーの変更](../t-sql/statements/alter-database-encryption-key-transact-sql.md)
* [ログインの変更](../t-sql/statements/alter-login-transact-sql.md)
* [マスターキーの変更](../t-sql/statements/alter-master-key-transact-sql.md)
* [ロールの変更](../t-sql/statements/alter-role-transact-sql.md)
* [ユーザーの変更](../t-sql/statements/alter-user-transact-sql.md)
* [バックアップ証明書](../t-sql/statements/backup-certificate-transact-sql.md)
* [マスターキーを閉じる](../t-sql/statements/close-master-key-transact-sql.md)
* [証明書の作成](../t-sql/statements/create-certificate-transact-sql.md)
* [データベース暗号化キーの作成](../t-sql/statements/create-database-encryption-key-transact-sql.md)
* [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)
* [マスターキーの作成](../t-sql/statements/create-master-key-transact-sql.md)
* [ロールの作成](../t-sql/statements/create-role-transact-sql.md)
* [ユーザーの作成](../t-sql/statements/create-user-transact-sql.md)
* [証明書の削除](../t-sql/statements/drop-certificate-transact-sql.md)
* [データベース暗号化キーの削除](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [ログインの削除](../t-sql/statements/drop-login-transact-sql.md)
* [マスターキーの削除](../t-sql/statements/drop-master-key-transact-sql.md)
* [ロールの削除](../t-sql/statements/drop-role-transact-sql.md)
* [ユーザーの削除](../t-sql/statements/drop-user-transact-sql.md)
* [マスターキーを開く](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>次の手順
詳細については、「 [t-sql 言語要素](tsql-language-elements.md)」および「 [t-sql システムビュー](tsql-system-views.md)」を参照してください。

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
