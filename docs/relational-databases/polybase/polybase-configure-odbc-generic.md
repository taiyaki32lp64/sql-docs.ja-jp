---
title: 外部データへのアクセス:ODBC ジェネリック型 - PolyBase
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 5017dc54a1e7858786413b2fcc164e4949f77646
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255423"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>SQL Server 上の外部データにアクセスするための PolyBase の構成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2019 で PolyBase を使用すると、ODBC コネクタから ODBC と互換性のあるデータ ソースに接続できます。 

## <a name="prerequisites"></a>前提条件

"=" 機能は Windows 上の SQL Server でのみ機能することに注意してください。 

PolyBase をインストールしていない場合は、「[PolyBase のインストール](polybase-installation.md)」をご覧ください。

 データベース スコープ資格情報より前に、[マスター キー](../../t-sql/statements/create-master-key-transact-sql.md)を作成しておく必要があります。 

まず、それぞれの PolyBase ノードで接続するデータ ソースの ODBC ドライバーをダウンロードしてインストールします。 ドライバーが適切にインストールされたら、[ODBC データ ソースの管理者] からドライバーを表示してテストできます。

![PolyBase スケールアウト グループ](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

> **重要:**
> 
> クエリのパフォーマンスを向上させるために、ドライバーで接続プールを有効にしていることを確認します。 この操作は [ODBC データ ソースの管理者] から実現できます。
> 
> **注**
> 
> ドライバーの名前 (上記の囲まれた例) は、外部データ ソースの作成時 (以下の手順 3) に指定する必要がります。

## <a name="create-an-external-table"></a>外部テーブルの作成

ODBC データ ソースのデータに対してクエリを実行するには、外部テーブルを作成して外部データを参照する必要があります。 このセクションでは、外部テーブルを作成するサンプル コードを示します。

このセクションでは以下の Transact-SQL コマンドが使用されます。

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. ODBC ソースにアクセスするために、データベース スコープ資格情報を作成します。

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) を使用して外部データ ソースを作成します。

    ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_nam );
    ```

1. **省略可能:** 外部テーブルの統計を作成します。

クエリのパフォーマンスを最適化するには、外部テーブルの列、特に結合、フィルター、集計に使用される列に統計を作成することをお勧めします。

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>外部データ ソースを作成すると、[CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) コマンドを使用して、そのソース上でクエリ可能なテーブルを作成することができます。 

## <a name="next-steps"></a>次のステップ

PolyBase の詳細については、[SQL Server PolyBase の概要](polybase-guide.md)に関する記事をご覧ください。
