---
title: テーブルとストアド プロシージャのネイティブ コンパイル
ms.custom: seo-dt-2019
ms.date: 04/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f14ac7835bab80a15d1fffb3bb58bd9cdb4b44b0
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412627"
---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>テーブルとストアド プロシージャのネイティブ コンパイル
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
インメモリ OLTP により、ネイティブ コンパイルという概念が導入されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はメモリ最適化テーブルにアクセスするストアド プロシージャをネイティブにコンパイルできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はメモリ最適化テーブルをネイティブにコンパイルすることもできます。 ネイティブ コンパイルは、(従来の) 解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)]よりも高速なデータ アクセスと効率的なクエリ実行を可能にします。 テーブルとストアド プロシージャのネイティブ コンパイルを実行すると DLL が生成されます。

メモリ最適化テーブル型のネイティブ コンパイルもサポートされています。 詳細については、「 [Faster temp table and table variable by using memory optimization](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)」 (メモリ最適化を使用した一時テーブルとテーブル変数の高速化) を参照してください。

ネイティブ コンパイルとは、プログラミングの構造をネイティブ コードに変換する処理であり、追加のコンパイルまたは解釈を必要としないプロセッサ命令で構成されます。

インメモリ OLTP は、作成されたときにメモリ最適化テーブルを、そしてネイティブ DLL に読み込まれたときにネイティブ コンパイル ストアド プロシージャをコンパイルします。 また、DLL は、データベースまたはサーバーが再起動した後に再コンパイルされます。 DLL を再作成するために必要な情報がデータベース メタデータに格納されます。 DLL は、データベースに関連付けられていますが、データベースの一部ではありません。 たとえば、DLL は、データベース バックアップに含まれていません。

> [!NOTE]
> メモリ最適化テーブルは、サーバーの再起動中に再コンパイルされます。 データベースの復元を迅速に行うために、ネイティブ コンパイル ストアド プロシージャは、サーバーの再起動中に再コンパイルされず、最初の実行時にコンパイルされます。 このようにコンパイルが延期されるため、ネイティブ コンパイル ストアド プロシージャは、最初の実行後に [sys.dm_os_loaded_modules &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql.md) を呼び出した場合にのみ表示されます。

## <a name="maintenance-of-in-memory-oltp-dlls"></a>インメモリ OLTP DLL のメンテナンス

次のクエリは、サーバーのメモリに現在読み込まれているすべてのテーブルとストアド プロシージャ DLL を示します。

```sql
SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.description = 'XTP Native DLL';
```

ネイティブ コンパイルによって生成されたファイルをデータベース管理者が維持する必要はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、不要になった生成ファイルが自動的に削除されます。 たとえばテーブルやストアド プロシージャが削除されたとき、またはデータベースが削除されたときに、生成ファイルが削除されます。

> [!NOTE]
> コンパイルが失敗するか、中断した場合、生成されたファイルの一部は削除されません。 これらのファイルはサポート性のために意図的に残され、データベースが削除されるときに削除されます。

> [!NOTE]
> SQL Server によってデータベースの復旧に必要なすべてのテーブルの DLL がコンパイルされます。 データベースを再起動する直前にテーブルが削除された場合、チェックポイント ファイルかトランザクション ログにテーブルの残存物が存在するため、データベースの起動中にテーブルの DLL が再コンパイルされる場合があります。 再起動後に DLL がアンロードされ、通常のクリーンアップ プロセスによってファイルが削除されます。

## <a name="native-compilation-of-tables"></a>テーブルのネイティブ コンパイル

**CREATE TABLE** ステートメントを使用してメモリ最適化テーブルを作成すると、テーブル情報がデータベース メタデータに書き込まれ、テーブルとインデックス構造がメモリに作成されます。 また、テーブルは DLL にコンパイルされます。

データベースとメモリ最適化テーブルを作成する、次のサンプル スクリプトについて考えてみます。

```sql
USE master;
GO

CREATE DATABASE DbMemopt3;
GO

ALTER DATABASE DbMemopt3
    add filegroup DbMemopt3_mod_memopt_1_fg
        contains memory_optimized_data
;
GO

-- You must edit the front portion of filename= path, to where your DATA\ subdirectory is,
-- keeping only the trailing portion '\DATA\DbMemopt3_mod_memopt_1_fn'!

ALTER DATABASE DbMemopt3
    add file
    (
        name     = 'DbMemopt3_mod_memopt_1_name',
        filename = 'C:\DATA\DbMemopt3_mod_memopt_1_fn'

        --filename = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\DbMemopt3_mod_memopt_1_fn'
    )
        to filegroup DbMemopt3_mod_memopt_1_fg
;
GO

USE DbMemopt3;
GO

CREATE TABLE dbo.t1
(
    c1 int not null primary key nonclustered,
    c2 int
)
    with (memory_optimized = on)
;
GO



-- You can safely rerun from here to the end.

-- Retrieve the path of the DLL for table t1.


DECLARE @moduleName  nvarchar(256);

SET @moduleName =
    (
        '%xtp_t_' +
        cast(db_id() as nvarchar(16)) +
        '_' +
        cast(object_id('dbo.t1') as nvarchar(16)) +
        '%.dll'
    )
;


-- SEARCHED FOR NAME EXAMPLE:  mod1.name LIKE '%xtp_t_8_565577053%.dll'
PRINT @moduleName;


SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.name LIKE @moduleName
    order by
        mod1.name
;
-- ACTUAL NAME EXAMPLE:  mod1.name = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\xtp\8\xtp_t_8_565577053_184009305855461.dll'
GO

--   DROP DATABASE DbMemopt3;  -- Clean up.
GO
```

テーブルを作成すると、テーブル DLL が作成され、メモリに DLL が読み込まれます。 CREATE TABLE ステートメントの直後の DMV クエリは、テーブル DLL のパスを取得します。

テーブル DLL は、テーブルのインデックス構造と行形式を理解します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は DLL を使用してインデックスをスキャンし、行を取得し、行のコンテンツを格納します。

## <a name="native-compilation-of-stored-procedures"></a>ストアド プロシージャのネイティブ コンパイル

NATIVE_COMPILATION が設定されているストアド プロシージャはネイティブでコンパイルされます。 つまり、パフォーマンスが重要なビジネス ロジックの効率的な実行のために、プロシージャの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがすべてネイティブ コードにコンパイルされます。

ネイティブ コンパイル ストアド プロシージャの詳細については、「 [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)」をご覧ください。

前の例のテーブル t1 に行を挿入する、次のサンプル ストアド プロシージャについて考えてみます。

```sql
CREATE PROCEDURE dbo.native_sp
    with native_compilation,
         schemabinding,
         execute as owner
as
begin atomic
    with (transaction isolation level = snapshot,
          language = N'us_english')

    DECLARE @i int = 1000000;

    WHILE @i > 0
    begin
        INSERT dbo.t1 values (@i, @i+1);
        SET @i -= 1;
    end
end;
GO

EXECUTE dbo.native_sp;
GO

-- Reset.

DELETE from dbo.t1;
GO
```

行をできる限り高速に挿入するために、native_sp の DLL は t1 の DLL およびインメモリ OLTP ストレージ エンジンと直接やり取りできます。

インメモリ OLTP コンパイラは、ストアド プロシージャの各クエリに有効な実行プランを作成するためにクエリ オプティマイザーを活用します。 テーブルのデータが変更された場合はネイティブ コンパイル ストアド プロシージャは自動的に再コンパイルされないことに注意してください。 インメモリ OLTP の統計とストアド プロシージャの管理の詳細については、「 [メモリ最適化テーブルの統計](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md)」を参照してください。

## <a name="security-considerations-for-native-compilation"></a>ネイティブ コンパイルにおけるセキュリティの注意点

テーブルおよびストアド プロシージャのネイティブ コンパイルでは、インメモリ OLTP コンパイラを使用します。 このコンパイラはファイルを生成し、そのファイルがディスクに書き込まれて、メモリに読み込まれます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、これらのファイルへのアクセスを制限するために、次のメカニズムを使用しています。

### <a name="native-compiler"></a>ネイティブ コンパイラ

コンパイラの実行可能ファイルと、ネイティブ コンパイルに必要なバイナリおよびヘッダー ファイルは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの一部として MSSQL\Binn\Xtp フォルダー内にインストールされます。 このため、既定のインスタンスが C:\Program Files 内にインストールされている場合、コンパイラ ファイルは C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\Binn\Xtp にインストールされています。

コンパイラへのアクセスを制限するために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、バイナリ ファイルへのアクセスを制限するアクセス制御リスト (ACL) が使用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのバイナリは、変更や改ざんが起こらないよう ACL で保護されています。 ネイティブ コンパイラの ACL では、コンパイラの使用も制限されます。ネイティブ コンパイラ ファイルに対する読み取り権限と実行権限を持っているのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントとシステム管理者のみです。

### <a name="files-generated-by-a-native-compilation"></a>ネイティブ コンパイルによって生成されるファイル

テーブルまたはストアド プロシージャのコンパイル時に生成されるファイルには、DLL のほか、.c、.obj、.xml、.pdb などの拡張子を持つ中間ファイルがあります。 生成されたファイルは、既定のデータ フォルダーのサブフォルダーに保存されます。 サブフォルダーは Xtp と呼ばれます。 既定のデータ フォルダーを指定して既定のインスタンスをインストールした場合、生成されたファイルは C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\DATA\Xtp に配置されます。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は 3 とおりの方法で、生成した DLL に対する改ざんを回避します。

- テーブルまたはストアド プロシージャが DLL にコンパイルされると、この DLL は直ちにメモリに読み込まれ、sqlserver.exe プロセスにリンクされます。 プロセスにリンクされている間、その DLL は変更できません。

- データベースを再起動すると、データベースのメタデータに基づいて、すべてのテーブルとストアド プロシージャが再コンパイル (削除後、再作成) されます。 これにより、生成されたファイルに対して悪意のあるエージェントによって行われた変更があれば、すべて削除されます。

- 生成されたファイルはユーザー データの一部と見なされ、ACL を介して、データベース ファイルと同じセキュリティ制限が適用されます。これらのファイルにアクセスできるのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントとシステム管理者のみです。

これらのファイルの管理には、ユーザー操作は不要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、必要に応じてファイルの作成および削除が行われます。

## <a name="see-also"></a>参照

[メモリ最適化テーブル](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)

[ネイティブ コンパイル ストアド プロシージャ](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)
