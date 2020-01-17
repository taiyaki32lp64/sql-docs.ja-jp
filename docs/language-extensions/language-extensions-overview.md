---
title: SQL Server 言語拡張とは?
titleSuffix: ''
description: 言語拡張は、外部コードの実行に使用される SQL Server の機能です。 SQL Server 2019 では、Java がサポートされています。 リレーショナル データは、機能拡張フレームワークを使用して外部コードで使用できます。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 57755782f2907eff25db942600cebc63f09598e0
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658828"
---
# <a name="what-is-sql-server-language-extensions"></a>SQL Server 言語拡張とは?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

言語拡張は、外部コードの実行に使用される SQL Server の機能です。 リレーショナル データは、[機能拡張フレームワーク](concepts/extensibility-framework.md)を使用して外部コードで使用できます。

SQL Server 2019 では、Java がサポートされています。 既定の Java ランタイムは Zulu Open JRE です。 別の Java JRE または SDK を使用することもできます。

## <a name="what-you-can-do-with-language-extensions"></a>言語拡張でできること

言語拡張には、外部コードの実行に拡張機能フレームワークが使用されます。 コードの実行はコア エンジン プロセスから分離されていますが、SQL Server のクエリ実行と完全に統合されています。 データが存在する場所でコードを実行できるため、ネットワーク経由でデータをプルする必要はありません。

外部言語は [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql) で定義されます。 システム ストアド プロシージャ [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) は、コードを実行するためのインターフェイスとして使用されます。

言語拡張には、次のような利点があります。

+ データのセキュリティ。 外部言語の実行をデータのソースに近づけることにより、無駄な、または安全でないデータ移動を回避できます。
+ 速さ。 データベースは、セットベースの操作用に最適化されています。 インメモリ テーブルなどのデータベースの最近のイノベーションにより、サマリーと集計が高速になり、データ サイエンスを完全に補完することができます。
+ 展開と統合の容易さ。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、他の多くのデータ管理タスクおよびアプリケーションの操作の中心となるポイントです。 データベースに存在するデータを使用することで、Java で使用されるデータの一貫性と最新性を確保できます。

## <a name="how-to-get-started"></a>開始する方法

### <a name="step-1-install-the-software"></a>手順 1:ソフトウェアをインストールする

+ [Windows 上の SQL Server 言語拡張](install/install-sql-server-language-extensions-on-windows.md)
+ [Linux 上の SQL Server 言語拡張](../linux/sql-server-linux-setup-language-extensions.md)

### <a name="step-2-configure-a-development-tool"></a>手順 2:開発ツールを構成する

開発者は、通常、自分のノート PC または開発用ワークステーションでコードを書きます。 SQL Server 言語拡張を使用する場合でも、このプロセスを変更する必要はありません。 インストールが完了したら、SQL Server で Java コードを実行できます。

+ Java コードの開発には、**好みの IDE を使用**します。

+ **[Microsoft 拡張機能 SDK for Java](how-to/extensibility-sdk-java-sql-server.md) をインストール**して、SQL Server 上で Java コードを実行します

+ **[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) または [SQL Server Management Studio ](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) を使用して** SQL Server 上で外部コードを実行します

+ **システム ストアド プロシージャ [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)** を使用して SQL Server 上で Java コードを実行します。

### <a name="step-3-write-your-first-code"></a>手順 3:最初のコードを書く

T-SQL スクリプト内から Java コードを実行します。

+ [チュートリアル: Java での正規表現](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>制限事項

+ 入力および出力バッファーの値の数は、Java の配列に割り当てることができる要素の最大数であるため、`MAX_INT (2^31-1)` を超えることはできません。

## <a name="next-steps"></a>次の手順

+ [Windows 上](install/install-sql-server-language-extensions-on-windows.md)または [Linux 上に SQL Server 言語拡張をインストール](../linux/sql-server-linux-setup-language-extensions.md)します
+ [Microsoft 拡張機能 SDK for Java](how-to/extensibility-sdk-java-sql-server.md) をインストールします
