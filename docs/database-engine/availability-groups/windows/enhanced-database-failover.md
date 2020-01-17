---
title: 可用性グループのフェールオーバーの強化
description: Always On 可用性グループ内のデータベースがトランザクションを書き込むことができなくなった場合にフェールオーバーをトリガーする、拡張データベース フェールオーバーを有効にする手順です。
ms.custom: seodec18
ms.date: 09/25/2017
ms.prod: sql
ms.reviewer: mikeray
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], enhanced database failover
- Availability Groups [SQL Server], failover
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9acd444e1ded8ab0530f605280e7aaa5c5dec907
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822247"
---
# <a name="enable-enhanced-database-failover-to-a-database-in-an-always-on-availability-group"></a>Always On 可用性グループのデータベースの拡張データベース フェールオーバーの有効化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2012 および 2014 で、プライマリ レプリカ上の可用性グループに参加しているデータベースがトランザクションを記述できなくなった場合、レプリカが同期され、自動的にフェールオーバーされるよう構成されている場合でも、フェールオーバーはトリガーされません。

SQL Server 2016 には、ウィザードまたは TRANSACT-SQL を使用して設定することができる、*拡張データベース フェールオーバー*という新しいオプションの動作が導入されています。 このオプションが有効になっており、自動フェールオーバーが構成されている場合、可用性グループに参加している 1 つのデータベースがトランザクションを書き込むことができなくなった場合、同期されているセカンダリ レプリカへのフェールオーバーがトリガーされます。

**シナリオ 1**

インスタンス A とインスタンス B 間で可用性グループが構成されています。これには、DB1 という名前のデータベースが 1 つ格納されています。 DB1 のデータ ファイルはドライブ E 上にあり、そのトランザクション ログ ファイルはドライブ F 上にあります。可用性モードは、同期コミットと自動フェールオーバー モードに設定されています。 この可用性グループには、新しい拡張データベース フェールオーバー オプションが構成されています。 現在、2 つのレプリカは同期された状態です。 問題によりドライブ E で障害が発生します。 このシナリオでは、ドライブ E にトランザクション ログが含まれないので、拡張データベース フェールオーバーは起こりません。  

**シナリオ 2**

これには、シナリオ 1 と同じ可用性グループが構成されています。 ここでは、ドライブ E ではなく、トランザクション ログ用のドライブ F で障害が発生します。 この場合は、拡張データベース フェールオーバーの条件を満たしているため (つまり、トランザクション ログにはアクセスできないため)、データベースはトランザクションを書き込むことができず、フェールオーバーがトリガーされます。

**シナリオ 3**

インスタンス A とインスタンス B 間で可用性グループが構成されています。これには、DB1 と DB2 という 2 つのデータベースが格納されています。 この可用性モードは、同期コミットと自動フェールオーバー モードに設定されており、拡張データベース フェールオーバーが有効になっています。 DB2 のデータとトランザクション ログ ファイルを含むディスクへのアクセスが失われています。 可用性グループは、問題が検出されると、インスタンス B に自動的にフェールオーバーされます。

## <a name="configure-enhanced-failover"></a>拡張フェールオーバーの構成

拡張データベース フェールオーバーは、SQL Server Management Studio または TRANSACT-SQL を使用して構成できます。 現在、PowerShell コマンドレットでは、この機能は実行できません。 既定では、拡張データベース フェールオーバーは無効です。

### <a name="sql-server-management-studio"></a>SQL Server Management Studio

拡張データベース フェールオーバーは、SQL Server Management Studio を使用し、ユーザー補助機能グループの作成時に有効にできます。 可用性グループの作成後に有効または無効にするには、TRANSACT-SQL を使用する方法しかありません。

*手動で可用性グループを作成する*

可用性グループを作成するには、記事「[[新しい可用性グループ] ダイアログ ボックスの使用 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)」の手順に従います。 拡張データベース フェールオーバーを有効にするには、 *[データベース レベルの正常性検出]* の横のチェックボックスをオンにします。

*可用性グループ ウィザードを使用する*

記事「[可用性グループ ウィザードの使用 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)」の手順に従います。 拡張データベース フェールオーバーを有効にするオプションは、[可用性グループ名の指定] ダイアログにあります。 これを有効にするには、 *[データベース レベルの正常性検出]* の横のボックスをオンにします。

### <a name="transact-sql"></a>Transact-SQL

可用性グループの作成時に拡張データベース フェールオーバーの動作を構成するには、次のように DB_FAILOVER を ON に設定する必要があります。

```SQL
CREATE AVAILABILITY GROUP [AGNAME]
WITH ( DB_FAILOVER = ON)
...
```
可用性グループの構成後に、この動作を追加するには、次のように ALTER AVAILABILITY GROUP コマンドを使用します。
```SQL
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = ON)
```
この動作を無効にするには、次の ALTER AVAILABILITY GROUP コマンドを実行します。
```SQL
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = OFF)
```
### <a name="dynamic-management-view"></a>動的管理ビュー
可用性グループでエンハンスド データベース フェールオーバーが有効かどうかを確認するには、動的管理ビュー `sys.availability_groups` に対してクエリを実行します。 列 `db_failover` は、無効の場合は 0 を、有効の場合は 1 になっています。 

## <a name="next-steps"></a>次のステップ 

- [データベース ヘルス検出の構成](sql-server-always-on-database-health-detection-failover-option.md)

- [可用性グループ ウィザードの使用 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

- [[新しい可用性グループ] ダイアログ ボックスの使用 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
- [Transact-SQL での可用性グループの作成](create-an-availability-group-transact-sql.md)

