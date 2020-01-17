---
title: Data Migration Assistant の設定を構成する
description: 構成ファイルの値を更新して Data Migration Assistant の設定を構成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: fc280fa541e2a6b5ea984086d694ffdd3f7c39a8
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056542"
---
# <a name="configure-settings-for-data-migration-assistant"></a>Data Migration Assistant の設定を構成する

Data Migration Assistant の特定の動作を微調整するには、machine.config ファイルで構成値を設定します。 この記事では、キーの構成値について説明します。

コンピューター上の次のフォルダーにある、Data Migration Assistant デスクトップアプリケーションとコマンドラインユーティリティのための、dma ファイルを見つけることができます。

- デスクトップアプリケーション

  % ProgramFiles%\\Microsoft Data Migration Assistant\\の machine.config. .config

- コマンドラインユーティリティ

  % ProgramFiles%\\Microsoft Data Migration Assistant\\dmacmd .exe. .config 

変更を加える前に、元の構成ファイルのコピーを保存してください。 変更を行った後、Data Migration Assistant を再起動して、新しい構成値を有効にします。

## <a name="number-of-databases-to-assess-in-parallel"></a>並列で評価するデータベースの数

Data Migration Assistant は、複数のデータベースを並行して評価します。 評価時に、データベーススキーマを理解するためにデータ層アプリケーション (dacpac) を抽出 Data Migration Assistant ます。 同じサーバー上の複数のデータベースが同時に評価されると、この操作はタイムアウトすることがあります。 

Data Migration Assistant v2.0 以降では、parallelDatabases 構成値を設定することによってこれを制御できます。 既定値は8です。

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>並列で移行するデータベースの数

Data Migration Assistant は、ログインを移行する前に、複数のデータベースを並行して移行します。 移行中、Data Migration Assistant はソースデータベースのバックアップを作成し、必要に応じてバックアップをコピーして、ターゲットサーバーに復元します。 複数のデータベースが移行用に選択されていると、タイムアウトエラーが発生することがあります。 

Data Migration Assistant v2.0 以降では、この問題が発生した場合に、parallelDatabases の構成値を減らすことができます。 値を大きくすると、移行にかかる時間を短縮できます。

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases="8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX の設定

評価時に、Data Migration Assistant はデータ層アプリケーション (dacpac) を抽出してデータベーススキーマを理解します。 この操作は、非常に大規模なデータベースのタイムアウトが発生した場合、またはサーバーに負荷がかかっている場合に失敗することがあります。 Data Migration v1.0 以降では、エラーを回避するために、次の構成値を変更できます。 

> [!NOTE]
> 既定では、&lt;dacfx&gt; エントリ全体にコメントが付いています。 コメントを削除し、必要に応じて値を変更します。

- commandTimeout

   このパラメーターは、IDbCommand プロパティを*秒*単位で設定します。 (既定値 = 60)

- databaseLockTimeout

   このパラメーターは、 [SET LOCK\_timeout timeout\_の期間](../t-sql/statements/set-lock-timeout-transact-sql.md) *(ミリ秒単位)* に相当します。 (既定値は 5000)

- maxDataReaderDegreeOfParallelism

  このパラメーターは、使用する SQL 接続プール接続の数を設定します。 (既定値 = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database: 推奨設定のしきい値

[SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database)を使用すると、Microsoft SQL Server 2016 から Azure にウォームおよびコールドトランザクションデータを動的に拡張できます。 Stretch Database は、大量のコールドデータを含むトランザクションデータベースを対象としています。 Stretch Database 推奨事項では、ストレージ機能の推奨事項の下で、この機能によってメリットが得られるテーブルを特定し、この機能のためにテーブルを有効にするために必要な変更を特定します。

Data Migration Assistant v2.0 以降では、recommendedNumberOfRows 構成値を使用して、Stretch Database 機能に適合するようにテーブルのしきい値を制御できます。 既定値は10万行です。 より小さなテーブルの拡張機能を分析する場合は、それに応じて値を小さくします。

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 接続のタイムアウト

評価または移行の実行中に、ソースとターゲットのインスタンスの[SQL 接続](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx)のタイムアウトを制御するには、接続タイムアウト値を指定した秒数に設定します。 既定値は 15 秒です。

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```

## <a name="ignore-error-codes"></a>エラーコードを無視する

各ルールのタイトルにはエラーコードがあります。 規則が不要で、それらを無視する場合は、ignoreErrorCodes プロパティを使用します。 1つのエラーまたは複数のエラーを無視するように指定できます。 複数のエラーを無視するには、セミコロン (例: ignoreErrorCodes = "46010; 71501") を使用します。 既定値は71501です。これは、オブジェクトがプロシージャ、ビューなどのシステムオブジェクトを参照するときに識別される未解決の参照に関連付けられています。

```
<workflowSettings>

<assessment parallelDatabases="8" ignoreErrorCodes="71501" />

</workflowSettings>
```

## <a name="see-also"></a>参照

[Data Migration Assistant のダウンロード](https://www.microsoft.com/download/details.aspx?id=53595)
