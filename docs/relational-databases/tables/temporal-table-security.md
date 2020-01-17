---
title: テンポラル テーブル セキュリティ | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 60e5d6f6-a26d-4bba-aada-42e382bbcd38
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b22210bdcabf1972e7fa76d7871ebd94e1f23ff5
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452903"
---
# <a name="temporal-table-security"></a>テンポラル テーブル セキュリティ

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

テンポラル テーブルに適用されるセキュリティを理解するには、テンポラル テーブルに適用されるセキュリティ原則を理解することが重要です。 これらのセキュリティ原則について理解したら、 **CREATE TABLE**、 **ALTER TABLE**、 **SELECT** ステートメントのセキュリティの学習に入ることができます。

## <a name="security-principles"></a>セキュリティ原則

 次の表は、テンポラル テーブルに適用されるセキュリティ原則についてまとめたものです。

|原則|[説明]|
|---------------|-----------------|
|システムによるバージョン管理の有効/無効を切り替えるには、影響を受けるオブジェクトに対する最高の権限が必要になる|SYSTEM_VERSIONING の有効/無効を切り替えるには、現行テーブルと履歴テーブルの両方の CONTROL 権限が必要になります。|
|履歴データを直接変更できない|SYSTEM_VERSIONING がオンのときは、現行テーブルまたは履歴テーブルの実際の権限に関係なく、履歴データを変更することはできません。 データとスキーマのいずれも変更できません。|
|履歴データにクエリを実行するには、履歴テーブルの **SELECT** 権限が必要になる|現行テーブルに **SELECT** 権限が与えられているから、履歴テーブルに **SELECT** 権限が与えられているとは限りません。|
|監査は特定の方法で履歴テーブルに影響を与える操作を発見する|現在のテーブルからの監査設定は、履歴テーブルに自動的には適用されません。 監査は、履歴テーブルに対して明示的に有効にする必要があります。<br /><br /> 有効にすると、履歴テーブルの監査では、データにアクセスするための直接的な試みがすべて記録されます (成功/失敗に関係なく)。<br /><br /> **SELECT** と一時的なクエリ拡張で、その操作で履歴テーブルが影響を受けたことが示されます。<br /><br /> **CREATE/ALTER** テンポラル テーブルでは、履歴テーブルでも権限チェックが行われる情報が公開されます。 監査ファイルには、履歴テーブルの追加レコードが含まれます。<br /><br /> 現行テーブルの DML 操作で、履歴テーブルが影響を受けたが、additional_info で必要なコンテキストが提供されることが判明します (DML は system_versioning の結果でした)。|

## <a name="performing-schema-operations"></a>スキーマ操作を実行する

SYSTEM_VERSIONING がオンに設定されているとき、スキーマ変更操作は限定されます。

### <a name="disallowed-alter-schema-operations"></a>許可されていない ALTER スキーマ操作

|演算|現行テーブル|履歴テーブル|
|---------------|-------------------|-------------------|
|**DROP TABLE**|禁止|禁止|
|**ALTER TABLE...SWITCH PARTITION**|SWITCH IN のみ (「 [テンポラル テーブルでのパーティション分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)」参照)|SWITCH OUT のみ (「 [テンポラル テーブルでのパーティション分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)」参照)|
|**ALTER TABLE...DROP PERIOD**|禁止|-|
|**ALTER TABLE...ADD PERIOD**|-|禁止|

## <a name="allowed-alter-table-operations"></a>許可される ALTER TABLE 操作

|演算|Current|履歴|
|---------------|-------------|-------------|
|**ALTER TABLE...REBUILD**|許可 (非依存)|許可 (非依存)|
|**CREATE INDEX**|許可 (非依存)|許可 (非依存)|
|**CREATE STATISTICS**|許可 (非依存)|許可 (非依存)|

## <a name="security-of-the-create-temporal-table-statement"></a>CREATE Temporal TABLE ステートメントのセキュリティ

||新しい履歴テーブルを作成する|既存の履歴テーブルを再利用する|
|-|------------------------------|----------------------------------|
|必要な権限|データベースの**CREATE TABLE** 権限<br /><br /> 現行テーブルと履歴テーブルが作成されるスキーマの**ALTER** 権限|データベースの**CREATE TABLE** 権限<br /><br /> 現行テーブルが作成されるスキーマの**ALTER** 権限<br /><br /> テンポラル テーブルを作成する**CONTROL** ステートメントの一部として指定される履歴テーブルの **CONTROL** 権限|
|監査|監査により、ユーザーが 2 つのオブジェクトを作成しようとしたことが示されます。 データベースにテーブルを作成する権限がないため、あるいはどちらかのテーブルのスキーマを変更する権限がないため、操作が失敗することがあります。|監査により、テンポラル テーブルが作成されたことが示されます。 データベースにテーブルを作成する権限がないため、テンポラル テーブルのスキーマを変更する権限がないため、あるいは履歴テーブルに対する権限がないため、操作が失敗することがあります。|

## <a name="security-of-the-alter-temporal-table-set-system_versioning-onoff-statement"></a>ALTER Temporal TABLE SET (SYSTEM_VERSIONING オン/オフ) ステートメントのセキュリティ

||新しい履歴テーブルを作成する|既存の履歴テーブルを再利用する|
|-|------------------------------|----------------------------------|
|必要な権限|データベースの**CONTROL** 権限<br /><br /> データベースの**CREATE TABLE** 権限<br /><br /> 履歴テーブルが作成されるスキーマの**ALTER** 権限|変更される元のテーブルの**CONTROL** 権限<br /><br /> **ALTER TABLE** ステートメントの一部として指定される履歴テーブルの **CONTROL** 権限|
|監査|監査により、テンポラル テーブルが変更され、同時に履歴テーブルが作成されたことが示されます。 データベースにテーブルを作成する権限がないため、履歴テーブルのスキーマを変更する権限がないため、あるいはテンポラル テーブルを変更する権限がないため、操作が失敗することがあります。|監査により、テンポラル テーブルが変更されたが、操作には履歴テーブルへのアクセス許可が必要であったことが示されます。 履歴テーブルに対する権限がないため、あるいは現行テーブルに対する権限がないため、操作が失敗することがあります。|

## <a name="security-of-select-statement"></a>SELECT ステートメントのセキュリティ

履歴テーブルに影響を与えない**SELECT** ステートメントの **SELECT** 権限は変更されません。 履歴テーブルに影響を与える **SELECT** ステートメントについては、現行テーブルと履歴テーブルの両方で **SELECT** 権限が必要になります。

## <a name="see-also"></a>参照

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md) 
- [システム バージョン管理されたテンポラル テーブルの概要](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [テンポラル テーブルのシステム一貫性のチェック](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [テンポラル テーブルでのパーティション分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [テンポラル テーブルの考慮事項と制約](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [テンポラル テーブル メタデータのビューおよび関数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
