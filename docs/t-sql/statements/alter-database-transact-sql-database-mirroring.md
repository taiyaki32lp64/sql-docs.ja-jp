---
title: ALTER DATABASE データベース ミラーリング (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- witness [SQL Server], establishing
- manual failover [SQL Server]
- ALTER DATABASE statement, database mirroring
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 27a032ef-1cf6-4959-8e67-03d28c4b3465
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 32cc95fa56d909602ab66d3ddad403bf4ceacebc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065817"
---
# <a name="alter-database-transact-sql-database-mirroring"></a>ALTER DATABASE (Transact-SQL) データベース ミラーリング

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

> [!NOTE]
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] を使用します。

データベースのデータベース ミラーリングを制御します。 データベース ミラーリング オプションで指定した値は、データベースのコピーと、データベース ミラーリング セッション全体の両方に適用されます。 \<database_mirroring_option> は、ALTER DATABASE ステートメントごとに 1 つだけ指定できます。

> [!NOTE]
> 構成はパフォーマンスに影響する場合があるので、データベース ミラーリングの構成はピーク タイム以外の時間に行うことをお勧めします。

ALTER DATABASE のオプションについては、[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) に関するページを参照してください。 ALTER DATABASE SET のオプションについては、[ALTER DATABASE SET のオプション](../../t-sql/statements/alter-database-transact-sql-set-options.md)に関するページを参照してください。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```

ALTER DATABASE database_name
SET { <partner_option> | <witness_option> }
  <partner_option> ::=
    PARTNER { = 'partner_server'
            | FAILOVER
            | FORCE_SERVICE_ALLOW_DATA_LOSS
            | OFF
            | RESUME
            | SAFETY { FULL | OFF }
            | SUSPEND
            | TIMEOUT integer
            }
  <witness_option> ::=
    WITNESS { = 'witness_server'
            | OFF
            }
  
```

## <a name="arguments"></a>引数

> [!IMPORTANT]
> SET PARTNER または SET WITNESS コマンドは入力時には正常に完了できますが、後で失敗します。
> [!NOTE]
> ALTER DATABASE データベース ミラーリング オプションは、包含データベースでは使用できません。

*database_name*: 変更するデータベースの名前です。

PARTNER \<partner_option>: データベース ミラーリング セッションのフェールオーバー パートナー、およびそれらの動作を定義する、データベース プロパティを制御します。 SET PARTNER オプションには、パートナーのうちのいずれか一方で設定すればよいものと、プリンシパル サーバーとミラー サーバーのいずれか一方に限定されているものがあります。 詳細については、後述の各 PARTNER オプションを参照してください。 SET PARTNER 句は、それを指定したパートナーには関係なく、データベースの両方のコピーに影響します。

SET PARTNER ステートメントを実行するには、両方のパートナーのエンドポイントの STATE が、STARTED に設定されている必要があります。 また、それぞれのパートナー サーバー インスタンスのデータベース ミラーリング エンドポイントの ROLE は、PARTNER または ALL のいずれかに設定されている必要があります。 エンドポイントの指定方法については、[Windows 認証でのデータベース ミラーリング エンドポイントの作成](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)に関するページを参照してください。 サーバー インスタンスのデータベース ミラーリング エンドポイントのロールおよび状態を確認するには、そのインスタンス上で、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。

```sql
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints
```

**\<partner_option> ::=**

> [!NOTE]
> 1 つの SET PARTNER 句で指定できる \<partner_option> は 1 つだけです。

**'** _partner_server_ **'** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのサーバー ネットワーク アドレスが、新しいデータベース ミラーリング セッションでフェールオーバー パートナーとして動作することを指定します。 各セッションには 2 つのパートナーが必要です。一方はプリンシパル サーバーとして起動し、他方はミラー サーバーとして起動します。 これらのパートナーは、別々のコンピューター上に配置することをお勧めします。

このオプションは、各パートナーでのセッションごとに 1 回指定します。 データベース ミラーリング セッションを開始するには、2 つの ALTER DATABASE <*データベース*> SET PARTNER **='** <_パートナー サーバー_> **'** ステートメントが必要です。 これらのステートメントの順序は非常に重要です。 最初に、ミラー サーバーに接続し、プリンシパル サーバー インスタンスを <*パートナー サーバー*> (SET PARTNER **='** <_プリンシパル サーバー_> **'** ) として指定します。 次に、プリンシパル サーバーに接続し、ミラー サーバー インスタンスを <*パートナー サーバー*> (SET PARTNER **='** <_ミラー サーバー_> **'** ) として指定します。これにより、これら 2 つのパートナー間で、データベース ミラーリング セッションが開始されます。 詳細については、[データベース ミラーリングの設定](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)に関するページを参照してください。

*partner_server* の値は、サーバー ネットワーク アドレスです。 構文は次のとおりです。

TCP **://** _\<system-address>_ **:** _\<port>_

パラメーターの説明

- *\<system-address>* は、システム名、完全修飾ドメイン名、IP アドレスなどの文字列です。対象のコンピューター システムを一意に識別します。
- *\<port>* は、パートナー サーバー インスタンスのミラーリング エンドポイントに関連付けられているポート番号です。

詳細については、 [サーバー ネットワーク アドレスの指定 - データベース ミラーリング](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)に関するページを参照してください。

SET PARTNER **='** <_パートナー サーバー_> **'** 句の例を次に示します。

```
'TCP://MYSERVER.mydomain.Adventure-Works.com:7777'
```

> [!IMPORTANT]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ではなく ALTER DATABASE ステートメントを使用してセットアップしたセッションでは、トランザクションの安全性が既定の完全な安全性に設定され (SAFETY の値が FULL)、セッションは自動フェールオーバーを伴わない高い安全性モードで実行されます。 自動フェールオーバーを使用するにはミラーリング監視を構成し、ハイパフォーマンス モードで実行するにはトランザクションの安全性をオフ (SAFETY OFF) にします。

FAILOVER: プリンシパル サーバーをミラー サーバーに手動でフェールオーバーします。 FAILOVER は、プリンシパル サーバー上でのみ指定できます。 このオプションは、SAFETY が FULL に設定されている (既定) 場合にのみ有効です。

FAILOVER オプションを指定する場合は、データベース コンテキストとして **master** が必要です。

FORCE_SERVICE_ALLOW_DATA_LOSS: データベースが非同期状態の場合、または同期状態で自動フェールオーバーが行われない場合、プリンシパル サーバーで障害が発生すると、ミラー データベースにデータベース サービスを強制します。

サービスの強制は、プリンシパル サーバーが停止した場合にのみ行うことを強くお勧めします。 それ以外の場合にサービスを強制すると、一部のクライアントが、新しいプリンシパル データベースではなく、元のプリンシパル データベースにアクセスし続ける可能性があります。
FORCE_SERVICE_ALLOW_DATA_LOSS は、ミラー サーバー上でのみ使用可能で、かつ次の条件をすべて満たしている必要があります。

- プリンシパル サーバーが停止している。
- WITNESS が OFF に設定されているか、または監視サーバーがミラー サーバーに接続されている。

サービスの強制は、データベースにサービスを直ちに復元するために一部のデータが失われてもかまわないという場合にのみ行ってください。

サービスを強制すると、セッションが中断され、元のプリンシパル データベース内のすべてのデータが一時的に保持されます。 元のプリンシパルが稼働し、新しいプリンシパル サーバーと通信できるようになると、データベース管理者はサービスを再開できます。 セッションを再開すると、すべての未送信ログ レコードと、それに対応する更新は失われます。

OFF: データベース ミラーリング セッションを削除し、データベースからミラーリングを削除します。 OFF は、どちらのパートナー上でも指定できます。 ミラーリングの削除による影響の詳細については、[データベース ミラーリングの削除](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)に関するページを参照してください。

RESUME: 中断状態のデータベース ミラーリング セッションを再開します。 RESUME は、プリンシパル サーバー上でのみ指定できます。

SAFETY { FULL | OFF }: トランザクションの安全性のレベルを設定します。 SAFETY は、プリンシパル サーバー上でのみ指定できます。

既定値は FULL です。 SAFETY が FULL の場合、データベース ミラーリング セッションは*高い安全性モード*で同期的に実行されます。 OFF の場合は、データベース ミラーリング セッションは*高パフォーマンス モード*で非同期的に実行されます。

高い安全性モードの動作は、次のように部分的にミラーリング監視に依存します。

- SAFETY が FULL に設定され、ミラーリング監視がセッションに対して設定されている場合、セッションは自動フェールオーバーを伴う高い安全性モードで実行されます。 データベースが同期され、ミラー サーバー インスタンスとミラーリング監視が引き続き相互接続している場合 (つまりクォーラムを保持している場合)、プリンシパル サーバーが失われると、セッションでは自動的にフェールオーバーが発生します。 詳細については、「[クォーラム: データベースの可用性にミラーリング監視が与える影響 - データベース ミラーリング](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)に関するページを参照してください。

  ミラーリング監視がセッションに対して設定されていても、ミラーリング監視サーバーが切断されていると、ミラー サーバーが利用できなくなるためプリンシパル サーバーがダウンします。

- SAFETY が FULL に設定され、ミラーリング監視が OFF に設定されている場合、セッションは自動フェールオーバーを伴わない高い安全性モードで実行されます。 ミラー サーバー インスタンスがダウンしても、プリンシパル サーバー インスタンスは影響を受けません。 プリンシパル サーバー インスタンスがダウンした場合、ミラー サーバー インスタンスにサービスの提供を強制的に移行できます (データが損失する可能性があります)。

- SAFETY が OFF に設定されている場合、セッションはハイパフォーマンス モードで実行されます。この場合、自動フェールオーバーも手動フェールオーバーもサポートされません。 ただし、ミラー サーバーで発生した問題が、プリンシパル サーバーに影響を及ぼすことはありません。WITNESS が OFF に設定されているか、ミラーリング監視サーバーがミラーに現在接続されているときに、プリンシパル サーバー インスタンスがダウンした場合、必要に応じてミラー サーバー インスタンスにサービスの提供を強制的に移行できます (データが損失する可能性があります)。 サービスの強制の詳細については、前の「FORCE_SERVICE_ALLOW_DATA_LOSS」を参照してください。

> [!IMPORTANT]
> ハイパフォーマンス モードは、ミラーリング監視の使用を想定していません。 ただし、SAFETY を OFF に設定した場合は常に、WITNESS も OFF に設定することを強くお勧めします。

SUSPEND: データベース ミラーリング セッションを一時停止します。

SUSPEND は、どちらのパートナー上でも指定できます。

TIMEOUT *integer*: タイムアウト時間を秒単位で指定します。 タイムアウト時間は、ミラーリング セッションの別のインスタンスからの PING メッセージを受信するために、サーバー インスタンスが待機する最大時間です。この時間を過ぎると、その別のインスタンスは接続解除されたものと見なされます。

TIMEOUT オプションは、プリンシパル サーバー上でのみ指定できます。 このオプションを指定しない場合、この時間は既定で 10 秒に設定されます。 5 以上の値を指定すると、タイムアウト時間は指定した秒数に設定されます。 タイムアウト値に 0 から 4 秒を指定すると、タイムアウト時間は自動的に 5 秒に設定されます。

> [!IMPORTANT]
> タイムアウト期間を 10 秒以上にしておくことをお勧めします。 値を 10 秒未満に設定すると、負荷の高いシステムでは PING を受信できず、誤認エラーが示される可能性があります。

詳細については、「 [データベース ミラーリング中に発生する可能性のあるエラー](../../database-engine/database-mirroring/possible-failures-during-database-mirroring.md)」を参照してください。

WITNESS \<witness_option>: データベースのミラーリング監視を定義するデータベース プロパティを制御します。 SET WITNESS 句は、データベースの両方のコピーに影響しますが、SET WITNESS はプリンシパル サーバー上でのみ指定できます。 ミラーリング監視がセッションに対して設定されている場合にデータベースを使用できるようにするには、SAFETY の設定に関係なく、クォーラムが必要です。詳細については、「[クォーラム: データベースの可用性にミラーリング監視が与える影響 - データベース ミラーリング](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)に関するページを参照してください。

ミラーリング監視とフェールオーバー パートナーは、別々のコンピューターに配置することをお勧めします。 ミラーリング監視サーバーの詳細については、「[データベース ミラーリング監視サーバー](../../database-engine/database-mirroring/database-mirroring-witness.md)」を参照してください。

SET WITNESS ステートメントを実行するには、プリンシパル サーバー インスタンスおよびミラーリング監視サーバー インスタンスのエンドポイントの STATE が STARTED に設定されている必要があります。 また、ミラーリング監視サーバー インスタンスのデータベース ミラーリング エンドポイントの ROLE は、WITNESS または ALL のいずれかに設定されている必要があります。 エンドポイントの指定方法については、[データベース ミラーリング エンドポイント](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)に関するページを参照してください。

サーバー インスタンスのデータベース ミラーリング エンドポイントのロールおよび状態を確認するには、そのインスタンス上で、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。

```sql
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints
```

> [!NOTE]
> データベースのプロパティは、ミラーリング監視では設定できません。

 **\<witness_option> ::=**

> [!NOTE]
> 1 つの SET WITNESS 句で指定できる \<witness_option> は 1 つだけです。

 **'** _witness_server_ **'** : [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスが、データベース ミラーリング セッションのミラーリング管理サーバーとして動作することを指定します。 SET WITNESS ステートメントは、プリンシパル サーバー上でのみ指定できます。

SET WITNESS **='** <_ミラーリング監視サーバー_> **'** ステートメントでは、<*ミラーリング監視サーバー*> の構文は、<*パートナー サーバー*> の構文と同じです。

OFF: データベース ミラーリング セッションから、ミラーリング監視を削除します。 ミラーリング監視を OFF に設定すると、自動フェールオーバーが無効化されます。 データベースが FULL SAFETY に設定され、ミラーリング監視が OFF に設定されている場合、ミラー サーバーに障害が発生すると、プリンシパル サーバーはデータベースを使用不可にします。

## <a name="remarks"></a>Remarks

## <a name="examples"></a>使用例

### <a name="a-creating-a-database-mirroring-session-with-a-witness"></a>A. ミラーリング監視を使用したデータベース ミラーリング セッションを作成する

ミラーリング監視を使用したデータベース ミラーリングをセットアップするには、セキュリティを構成し、ミラー データベースを準備し、ALTER DATABASE を使用してパートナーを設定する必要があります。 完全なセットアップ プロセスの例は、[データベース ミラーリングの設定](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)に関するページを参照してください。

### <a name="b-manually-failing-over-a-database-mirroring-session"></a>B. データベース ミラーリング セッションを手動でフェールオーバーする

手動フェールオーバーは、どちらのデータベース ミラーリング パートナーからでも開始できます。 フェールオーバーする前に、現在プリンシパル サーバーであると思われるサーバーが、実際にプリンシパル サーバーであるかどうかを確認する必要があります。 たとえば、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの場合、現在プリンシパル サーバーであると思われるサーバー インスタンスで、次のクエリを実行します。

```sql
SELECT db.name, m.mirroring_role_desc
FROM sys.database_mirroring m
JOIN sys.databases db
ON db.database_id = m.database_id
WHERE db.name = N'AdventureWorks2012';
GO
```

そのサーバー インスタンスが実際にプリンシパルである場合、`mirroring_role_desc` の値は `Principal` になります。 このサーバー インスタンスがミラー サーバーの場合には、`SELECT` ステートメントは `Mirror` を返します。

次の例では、そのサーバーが現在のプリンシパルであることを前提としています。

1. データベース ミラーリング パートナーに手動でフェールオーバーするには、次のステートメントを実行します。

    ```sql
    ALTER DATABASE AdventureWorks2012 SET PARTNER FAILOVER;
    GO
    ```
  
2. 新しいミラーでのフェールオーバーの結果を確認するには、次のクエリを実行します。
  
    ```sql
    SELECT db.name, m.mirroring_role_desc
    FROM sys.database_mirroring m
    JOIN sys.databases db
    ON db.database_id = m.database_id
    WHERE db.name = N'AdventureWorks2012';
    GO
    ```
  `mirroring_role_desc` の現在の値は、`Mirror` です。

## <a name="see-also"></a>参照

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
