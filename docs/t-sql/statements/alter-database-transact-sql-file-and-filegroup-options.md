---
title: ALTER DATABASE の File および Filegroup
description: Transact-SQL を使用して、データベースの File および Filegroup を更新します。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ADD FILE
- ADD_FILE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting files
- removing files
- deleting filegroups
- file modifications [SQL Server]
- databases [SQL Server], size
- relocating files
- databases [SQL Server], modifying
- file additions [SQL Server], ALTER DATABASE
- file moving [SQL Server]
- default filegroups
- ALTER DATABASE statement, files and filegroups
- initializing files [SQL Server]
- database files [SQL Server]
- moving files
- filegroups [SQL Server], deleting
- adding filegroups
- adding files
- database filegroups [SQL Server]
- adding log files
- modifying files
- filegroups [SQL Server], adding
- file initialization [SQL Server]
- files [SQL Server], deleting
- files [SQL Server], adding
- databases [SQL Server], moving
ms.assetid: 1f635762-f7aa-4241-9b7a-b51b22292b07
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 0eae7e7f1a0a673138b58440ee9c5c8d0b6f20bc
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244425"
---
# <a name="alter-database-transact-sql-file-and-filegroup-options"></a>ALTER DATABASE (Transact-SQL) の File および Filegroup オプション

データベースに関連付けられているファイルおよびファイル グループを変更します。 データベースに対するファイルやファイル グループの追加と削除、およびデータベースおよびデータベースのファイルやファイル グループの属性の変更を行います。 ALTER DATABASE の他のオプションについては、「[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)」をご覧ください。

構文表記規則の詳細については、「[Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。

## <a name="click-a-product"></a>製品をクリックしてください

次の行から興味がある製品名をクリックしてみてください。 この Web ページでは、クリックした製品に合わせて、異なるコンテンツが表示されます。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

|||
|-|-|-|
|**_\* SQL Server \*_** &nbsp;|[SQL Database<br />マネージド インスタンス](alter-database-transact-sql-file-and-filegroup-options.md?view=azuresqldb-mi-current)|
|||

&nbsp;

## <a name="syntax"></a>構文

```
ALTER DATABASE database_name
{
    <add_or_modify_files>
  | <add_or_modify_filegroups>
}
[;

<add_or_modify_files>::=
{
    ADD FILE <filespec> [ ,...n ]
        [ TO FILEGROUP { filegroup_name } ]
  | ADD LOG FILE <filespec> [ ,...n ]
  | REMOVE FILE logical_file_name
  | MODIFY FILE <filespec>
}

<filespec>::=
(
    NAME = logical_file_name
    [ , NEWNAME = new_logical_name ]
    [ , FILENAME = {'os_file_name' | 'filestream_path' | 'memory_optimized_data_path' } ]
    [ , SIZE = size [ KB | MB | GB | TB ] ]
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB| % ] ]
    [ , OFFLINE ]
)

<add_or_modify_filegroups>::=
{
    | ADD FILEGROUP filegroup_name
        [ CONTAINS FILESTREAM | CONTAINS MEMORY_OPTIMIZED_DATA ]
    | REMOVE FILEGROUP filegroup_name
    | MODIFY FILEGROUP filegroup_name
        { <filegroup_updatability_option>
        | DEFAULT
        | NAME = new_filegroup_name
        | { AUTOGROW_SINGLE_FILE | AUTOGROW_ALL_FILES }
        }
}
<filegroup_updatability_option>::=
{
    { READONLY | READWRITE }
    | { READ_ONLY | READ_WRITE }
}

```

## <a name="arguments"></a>引数

**\<add_or_modify_files>::=**

追加、削除、または変更するファイルを指定します。

*database_name*: 変更するデータベースの名前です。

ADD FILE: データベースにファイルを追加します。

TO FILEGROUP { *filegroup_name* }: 指定されたファイルを追加するファイル グループを指定します。 現在のファイル グループ、および現在の既定のファイル グループを表示するには、[sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) カタログ ビューを使用してください。

ADD LOG FILE: 指定されたデータベースにログ ファイルを追加します。

REMOVE FILE *logical_file_name*: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスから論理ファイルの説明を削除し、物理ファイルを削除します。 ファイルが空でない場合は削除できません。

*logical_file_name*: ファイルを参照するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用される論理名を指定します。

> [!WARNING]
> `FILE_SNAPSHOT` のあるデータベース ファイルを削除する関連付けられているバックアップは成功しますが、関連付けられたスナップショットを参照するデータベース ファイルのバックアップを無効化を回避するのには削除されません。 ファイルは切り捨てられますが、FILE_SNAPSHOT のバックアップをそのままの状態に保つために物理的には削除されません。 詳細については、「[Windows Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。

変更するファイルを指定します。 一度に 1 つの \<filespec> プロパティだけを変更できます。 変更するファイルを識別するには、\<filespec> に NAME を指定する必要があります。 SIZE を指定する場合、ファイルの現在のサイズより新しいサイズの方が大きくなければなりません。

データ ファイルまたはログ ファイルの論理名を変更するには、変更するファイルの論理名を `NAME` 句で指定し、`NEWNAME` 句にそのファイルの新しい論理名を指定します。 次に例を示します。

```sql
MODIFY FILE ( NAME = logical_file_name, NEWNAME = new_logical_name )
```

データ ファイルまたはログ ファイルを別の場所に移動するには、`NAME` 句にファイルの現在の論理名を指定し、`FILENAME` 句に新しいパスとオペレーティング システム ファイル名を指定します。 次に例を示します。

```sql
MODIFY FILE ( NAME = logical_file_name, FILENAME = ' new_path/os_file_name ' )
```

フルテキスト カタログを移動する場合は、FILENAME 句に新しいパスだけを指定します。 オペレーティング システム ファイル名は指定しないでください。

詳しくは、「[データベース ファイルの移動](../../relational-databases/databases/move-database-files.md)」をご覧ください。

FILESTREAM ファイル グループの場合、NAME をオンラインで変更できます。 FILENAME はオンラインで変更できますが、コンテナーを物理的に再配置し、サーバーをシャットダウンして再起動するまで、変更は有効になりません。

FILESTREAM ファイルを OFFLINE に設定できます。 FILESTREAM ファイルをオフラインにすると、その親ファイル グループがオフラインとして内部的にマークされるため、そのファイル グループ内の FILESTREAM データへのアクセスはすべて失敗します。

> [!NOTE]
> \<add_or_modify_files> オプションは、包含データベースでは使用できません。

**\<filespec>::=**

ファイル プロパティを制御します。

NAME: *logical_file_name* ファイルの論理名を指定します。

*logical_file_name*: ファイルを参照するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで使用される論理名を指定します。

NEWNAME *new_logical_file_name*: ファイルの新しい論理名を指定します。

*new_logical_file_name*: 既存の論理ファイル名と置換する新しい名前を指定します。 論理ファイル名は、データベース内で一意であり、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 この名前は、文字定数、Unicode 定数、標準の識別子、区切られた識別子のいずれでもかまいません。

FILENAME { **'** _os\_file\_name_ **'** | **'** _filestream\_path_ **'** | **'** _memory\_optimized\_data\_path_ **'** }: オペレーティング システムの (物理) ファイル名を指定します。

' *os_file_name* ': 標準の (ROWS) ファイル グループの場合、ファイルの作成時にオペレーティング システムで使用されるパスとファイル名を指定します。 ファイルは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているサーバー上に存在する必要があります。 ALTER DATABASE ステートメントを実行するには、指定したパスが実際に存在するパスであることが必要です。

> [!NOTE]
> ファイルに UNC パスが指定されている場合、`SIZE`、`MAXSIZE`、および `FILEGROWTH` パラメーターは設定できません。
>
> システム データベースを UNC 共有ディレクトリに置くことはできません。

データ ファイルが読み取り専用のセカンダリ ファイルであるか、データベースが読み取り専用である場合を除き、データ ファイルを圧縮ファイル システム上には置かないでください。 ログ ファイルは、圧縮ファイル システム上に置くことはできません。

ファイルが未処理のパーティション上にある場合、*os_file_name* には、未処理になっている既存のパーティションのドライブ文字のみを指定する必要があります。 未処理の各パーティションに配置できるファイルは、それぞれ 1 ファイルだけです。

**'** *filestream_path* **'** : FILESTREAM ファイル グループの場合、FILENAME は FILESTREAM データが格納されるパスを参照します。 最後のフォルダーまでのパスが存在する必要がありますが、最後のフォルダーは存在できません。 たとえば、パス `C:\MyFiles\MyFilestreamData` を指定する場合は、ALTER DATABASE を実行する前に、`C:\MyFiles` が存在している必要がありますが、`MyFilestreamData` フォルダーは存在できません。

> [!NOTE]
> SIZE プロパティおよび FILEGROWTH プロパティは、FILESTREAM ファイル グループには適用されません。

**'** *memory_optimized_data_path* **'** : メモリ最適化ファイル グループでは、FILENAME はメモリ最適化データが格納されるパスを示します。 最後のフォルダーまでのパスが存在する必要がありますが、最後のフォルダーは存在できません。 たとえば、パス `C:\MyFiles\MyData` を指定する場合は、ALTER DATABASE を実行する前に、`C:\MyFiles` が存在している必要がありますが、`MyData` フォルダーは存在できません。

ファイル グループとファイル (`<filespec>`) は、同じステートメントで作成する必要があります。

> [!NOTE]
> SIZE と FILEGROWTH の各プロパティは、MEMORY_OPTIMIZED_DATA ファイル グループには適用されません。

メモリ最適化ファイル グループの詳細については、「[メモリ最適化ファイル グループ](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)」を参照してください。

SIZE *size*: ファイルのサイズを指定します。 SIZE は、FILESTREAM ファイル グループには適用されません。

*size*: ファイルのサイズです。

ADD FILE と共に指定する場合、*size* はファイルの初期サイズになります。 MODIFY FILE と共に指定する場合、*size* はファイルの新しいサイズになります。この値には、ファイルの現在のサイズより大きい値を指定する必要があります。

プライマリ ファイルに *size* が指定されていない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**model** データベースのプライマリ ファイルのサイズを使用します。 セカンダリ データ ファイルまたはログ ファイルが指定されているにもかかわらず、そのファイルに対して *size* が指定されていない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では、そのファイルのサイズが 1 MB になります。

KB、MB、GB、および TB の各サフィックスを使用して、キロバイト、メガバイト、ギガバイト、またはテラバイトを指定できます。 既定値は MB です。 整数を指定します。小数は含めないでください。 小数部を持つメガバイトの値を指定するには、その値に 1024 を乗算することによって、キロバイトの単位に変換します。 たとえば、1.5 MB ではなく 1536 KB と指定します (1.5 × 1024 = 1536)。

> [!NOTE]
> 次の場合、`SIZE` を設定することはできません。
>
> - ファイルに UNC パスが指定されている場合
> - `FILESTREAM` および `MEMORY_OPTIMIZED_DATA` のファイル グループ

MAXSIZE { *max_size*| UNLIMITED }: ファイルのサイズの上限を指定します。

*max_size*: ファイルの最大サイズです。 KB、MB、GB、および TB の各サフィックスを使用して、キロバイト、メガバイト、ギガバイト、またはテラバイトを指定できます。 既定値は MB です。 整数を指定します。小数は含めないでください。 *max_size* を指定しない場合、ファイル サイズはディスクがいっぱいになるまで拡張されます。

UNLIMITED: ディスクがいっぱいになるまでファイルを拡張するように指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、無制限に拡張するファイル固有のログの最大サイズは 2 TB で、データ ファイルの最大サイズは 16 TB です。 FILESTREAM コンテナーに対してこのオプションを指定した場合、最大サイズはありません。 ディスクがいっぱいになるまでファイル サイズが拡張します。

> [!NOTE]
> ファイルに UNC パスが指定されている場合、`MAXSIZE` は設定できません。

FILEGROWTH *growth_increment*: ファイルを自動拡張するときの増加量を指定します。 ファイルの FILEGROWTH の設定を MAXSIZE の設定より大きくすることはできません。 FILEGROWTH は、FILESTREAM ファイル グループには適用されません。

*growth_increment*: 新しい領域が必要とされるたびにファイルに追加される領域の容量です。

値は MB、KB、GB、TB または % の単位で指定できます。 サフィックス MB、KB、または % を付けないで数値を指定した場合の既定値は MB です。 % を指定すると、1 回の増加量は、増加時のファイル サイズに指定されたパーセンテージを掛けた値になります。 指定されたサイズは、最も近い 64 KB 単位の値に切り上げられます。

0 の値は、自動拡張がオフで、領域を追加できないことを示します。

FILEGROWTH が指定されていない場合、既定値は次のとおりです。

|Version|既定値|
|-------------|--------------------|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降|データ 64 MB。 ログ ファイル 64 MB。|
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降|データ 1 MB。 ログ ファイル 10%。|
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] の前|データ 10%。 ログ ファイル 10%。|

> [!NOTE]
> 次の場合、`FILEGROWTH` を設定することはできません。
>
> - ファイルに UNC パスが指定されている場合
> - `FILESTREAM` および `MEMORY_OPTIMIZED_DATA` のファイル グループ

OFFLINE: ファイルをオフラインに設定し、ファイル グループ内のすべてのオブジェクトをアクセス不可にします。

> [!CAUTION]
> このオプションは、ファイルは破損しているが、復元可能な場合にのみ使用してください。 OFFLINE に設定したファイルは、そのファイルをバックアップから復元することによってのみ、オンラインに設定されます。 単一ファイルの復元の詳細については、「[RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)」を参照してください。
>
> \<filespec> オプションは、包含データベースでは使用できません。

**\<add_or_modify_filegroups>::=**

データベースに対してファイル グループの追加、変更、または削除を行います。

ADD FILEGROUP *filegroup_name*: データベースにファイル グループを追加します。

CONTAINS FILESTREAM: ファイル グループで FILESTREAM バイナリ ラージ オブジェクト (BLOB) をファイル システムに格納することを指定します。

CONTAINS MEMORY_OPTIMIZED_DATA

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降)

ファイル グループでメモリ最適化データをファイル システムに格納することを指定します。 詳細については、「 [インメモリ OLTP - インメモリ最適化](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。 データベースあたり 1 つの `MEMORY_OPTIMIZED_DATA` ファイル グループのみが許可されます。 メモリ最適化テーブルを作成する場合は、ファイル グループを空にすることはできません。 ファイルが少なくとも 1 つ必要です。 *filegroup_name* パスを参照します。 最後のフォルダーまでのパスが存在する必要がありますが、最後のフォルダーは存在できません。

REMOVE FILEGROUP *filegroup_name*: データベースからファイルグループを削除します。 ファイル グループが空でない場合は削除できません。 最初に、ファイル グループからすべてのファイルを削除してください。 詳細については、前の「REMOVE FILE *logical_file_name*」を参照してください。

> [!NOTE]
> FILESTREAM ガベージ コレクターによって FILESTREAM コンテナーからすべてのファイルが削除されない限り、`ALTER DATABASE REMOVE FILE` 操作で FILESTREAM コンテナーを削除する試みは失敗し、エラーが返されます。 このトピックの「[FILESTREAM コンテナーの削除](#removing-a-filestream-container)」セクションを参照してください。

MODIFY FILEGROUP *filegroup_name* { \<filegroup_updatability_option> | DEFAULT | NAME **=** _new\_filegroup\_name_ } ファイル グループに変更を加えます。ここでは、状態を READ_ONLY または READ_WRITE に設定したり、ファイル グループをデータベースの既定のファイル グループに指定したり、ファイル グループ名を変更することができます。

\<filegroup_updatability_option>: ファイル グループに読み取り専用、または読み取り/書き込みのプロパティを設定します。

DEFAULT: 既定のデータベース ファイル グループを *filegroup_name* に変更します。 データベース内の 1 つのファイル グループだけを、既定のファイル グループにすることができます。 詳細については、「 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)」を参照してください。

NAME = *new_filegroup_name*: ファイル グループ名を *new_filegroup_name* に変更します。

AUTOGROW_SINGLE_FILE **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)

ファイル グループ内のファイルが自動拡張のしきい値を満たす場合は、そのファイルのみが拡張されます。 これは既定値です。

AUTOGROW_ALL_FILES

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)

ファイル グループ内のファイルが自動拡張のしきい値を満たすときに、ファイル グループ内のすべてのファイルを拡張します。

> [!NOTE]
> これは TempDB の既定値です。

**\<filegroup_updatability_option>::=**

ファイル グループに読み取り専用、または読み取り/書き込みのプロパティを設定します。

READ_ONLY | READONLY: ファイル グループが読み取り専用であることを指定します。 この中のオブジェクトを更新することはできません。 プライマリ ファイル グループを読み取り専用にすることはできません。 この状態を変更するには、データベースに対する排他的アクセスが必要になります。 詳細については、SINGLE_USER 句をご覧ください。

読み取り専用データベースのデータを変更することはできないため、次のようになります。

- システム起動時に自動復旧がスキップされます。
- データベースの圧縮が不可能になります。
- 読み取り専用データベースでは、ロックは発生しません。 これにより、クエリのパフォーマンスが向上することがあります。

> [!NOTE]
> キーワード `READONLY` は、将来のバージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 新しい開発作業では、`READONLY` の使用は避け、現在 `READONLY` を使用しているアプリケーションは修正するようにしてください。 代わりに `READ_ONLY` を使用してください

READ_WRITE | READWRITE: ファイル グループを READ_WRITE に指定します。 ファイル グループ内のオブジェクトを更新できます。 この状態を変更するには、データベースに対する排他的アクセスが必要になります。 詳細については、SINGLE_USER 句をご覧ください。

> [!NOTE]
> キーワード `READWRITE` は、将来のバージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 新しい開発作業では、`READWRITE` の使用は避け、現在 `READWRITE` を使用しているアプリケーションは `READ_WRITE` を使用するように修正することを計画してください。
> [!TIP]
> これらのオプションの状態を確認するには、**sys.databases** カタログ ビューの **is_read_only** 列、または `DATABASEPROPERTYEX` 関数の **Updateability** プロパティを調べてください。

## <a name="remarks"></a>解説

データベースのサイズを縮小するには、[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md) を使用します。

`BACKUP` ステートメントの実行中にファイルを追加したり削除したりすることはできません。

各データベースに、最大 32,767 のファイルと 32,767 のファイル グループを指定できます。

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降では、データベース ファイルの状態 (オンラインかオフラインかなど) は、データベースの状態とは別に保持されます。 詳しくは、「[ファイルの状態](../../relational-databases/databases/file-states.md)」をご覧ください。

- ファイル グループ内のファイルの状態は、ファイル グループ全体の可用性を決定します。 ファイル グループを使用可能にするには、ファイル グループ内のすべてのファイルがオンラインである必要があります。
- ファイル グループがオフラインの場合、SQL ステートメントでそのファイル グループにアクセスを試行するとエラーが発生します。 `SELECT` ステートメントのクエリ プランを作成する場合、クエリ オプティマイザーは、オフラインのファイル グループにある非クラスター化インデックスやインデックス付きビューを回避します。 これにより、これらのステートメントは正常に実行できます。 ただし、オフラインのファイル グループに、ターゲット テーブルのヒープやクラスター化インデックスが含まれている場合には、`SELECT` ステートメントは失敗します。 また、オフラインのファイル グループ内にあるインデックス付きのテーブルを変更する `INSERT`、`UPDATE`、または `DELETE` ステートメントは失敗します。

ファイルに対して UNC パスが指定されている場合、SIZE、MAXSIZE、および FILEGROWTH パラメーターは設定できません。

メモリ最適化ファイル グループには、SIZE および FILEGROWTH パラメーターを設定することはできません。

キーワード `READONLY` は、将来のバージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 新しい開発作業では、`READONLY` の使用は避け、現在 READONLY を使用しているアプリケーションは修正するようにしてください。 代わりに `READ_ONLY` を使用してください

キーワード `READWRITE` は、将来のバージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 新しい開発作業では、`READWRITE` の使用は避け、現在 `READWRITE` を使用しているアプリケーションは `READ_WRITE` を使用するように修正することを計画してください。

## <a name="moving-files"></a>ファイルの移動

FILENAME に新しい場所を指定することにより、システムまたはユーザー定義のデータ、およびログ ファイルを移動することができます。 これは、次のようなシナリオで役立ちます。

- 障害復旧。 たとえば、ハードウェア障害により、データベースが問題のあるモードになる場合やシャットダウンされるた場合など。
- 計画に従った再配置。
- スケジュールされたディスク メンテナンスとしての再配置。

詳しくは、「[データベース ファイルの移動](../../relational-databases/databases/move-database-files.md)」をご覧ください。

## <a name="initializing-files"></a>ファイルの初期化

既定では、データ ファイルおよびログ ファイルは、次のいずれかの操作を実行したときに、ファイルを 0 で埋め込むことにより初期化されます。

- データベースを作成します。
- 既存データベースへのファイルの追加
- 既存のファイルのサイズの拡張
- データベースまたはファイル グループの復元。

データ ファイルを瞬時に初期化できます。 そのため、このようなファイル操作を高速に実行できます。 詳細については、「 [データベース ファイルの初期化](../../relational-databases/databases/database-instant-file-initialization.md)」をご覧ください。

## <a name="removing-a-filestream-container"></a> FILESTREAM コンテナーの削除

"DBCC SHRINKFILE" 操作によって FILESTREAM コンテナーが空にされた場合でも、データベースは、さまざまなシステム保守上の理由から、削除されたファイルへの参照を維持する必要があります。 [sp_filestream_force_garbage_collection](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) を使用すると、FILESTREAM ガベージ コレクターが実行され、これらのファイルを削除しても安全な場合は削除されます。 FILESTREAM ガベージ コレクターによって FILESTREAM コンテナーからすべてのファイルが削除されない限り、ALTER DATABASE REMOVE FILE 操作で FILESTREAM コンテナーを削除する試みは失敗し、エラーが返されます。 FILESTREAM コンテナーを削除する場合は、次の手順をお勧めします。

1. EMPTYFILE オプションを指定して [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) を実行し、このコンテナーのアクティブなコンテンツを他のコンテナーに移動します。
2. ログ バックアップが完全または一括ログ復旧モデルで作成されたことを確認します。
3. レプリケーション ログ リーダー ジョブが実行されていることを確認します (該当する場合)。
4. [sp_filestream_force_garbage_collection](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) を実行して、このコンテナー内の不要になったファイルをガベージ コレクターで強制的に削除します。
5. REMOVE FILE オプションを指定して ALTER DATABASE を実行し、このコンテナーを削除します。
6. もう一度手順 2. ～ 4. を繰り返して、ガベージ コレクションを完了します。
7. ALTER Database...REMOVE FILE を使用して、このコンテナーを削除します。

## <a name="examples"></a>例

### <a name="a-adding-a-file-to-a-database"></a>A. データベースにファイルを追加する

次の例では、5 MB のデータ ファイルを [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースに追加します。

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
    NAME = Test1dat2,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat2.ndf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
);
GO
```

### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>B. 2 つのファイルから成るファイル グループをデータベースに追加する

次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースに `Test1FG1` ファイル グループを作成し、そのファイル グループに 5 MB のファイルを 2 つ追加します。

```sql
USE master
GO
ALTER DATABASE AdventureWorks2012
ADD FILEGROUP Test1FG1;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
    NAME = test1dat3,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat3.ndf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
),  
(  
    NAME = test1dat4,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat4.ndf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
)  
TO FILEGROUP Test1FG1;
GO
```

### <a name="c-adding-two-log-files-to-a-database"></a>C. 2 つのログ ファイルをデータベースに追加する

次の例では、5 MB のログ ファイルを 2 つ、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースに追加します。

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
ADD LOG FILE
(
    NAME = test1log2,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\test2log.ldf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
),
(
    NAME = test1log3,
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\DATA\test3log.ldf',
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
);
GO
```

### <a name="d-removing-a-file-from-a-database"></a>D. データベースからファイルを削除する

次の例では、例 B で追加したファイルの一方を削除します。

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
REMOVE FILE test1dat4;
GO
```

### <a name="e-modifying-a-file"></a>E. ファイルを変更する

次の例では、例 B で追加したファイルのうち、1 つのサイズを拡張します。MODIFY FILE を指定した ALTER DATABASE コマンドではファイル サイズを大きくすることだけが可能なため、ファイル サイズを小さくする必要がある場合は、DBCC SHRINKFILE を使用する必要があります。

```sql
USE master;
GO

ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

この例では、データ ファイルのサイズを 100 MB に縮小してから、その量のサイズを指定します。

```sql
USE AdventureWorks2012;
GO

DBCC SHRINKFILE (AdventureWorks2012_data, 100);
GO

USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

### <a name="f-moving-a-file-to-a-new-location"></a>F. ファイルを新しい場所に移動する

次の例では、例 A で作成した `Test1dat2` ファイルを、新しいディレクトリに移動します。

> [!NOTE]
> この例を実行する前に、ファイルを新しいディレクトリに物理的に移動しておく必要があります。 その後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをいったん停止してから起動するか、または [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースをいったん OFFLINE にしてから ONLINE にして、変更を実装します。

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILE
(
    NAME = Test1dat2,
    FILENAME = N'c:\t1dat2.ndf'
);
GO
```

### <a name="g-moving-tempdb-to-a-new-location"></a>G. tempdb を新しい場所に移動する

次の例では、`tempdb` をディスク上の現在の場所から別の場所に移動します。 `tempdb` は MSSQLSERVER サービスが開始されるたびに再作成されるので、データ ファイルとログ ファイルを物理的に移動する必要はありません。 これらのファイルは、MSSQLSERVER サービスが手順 3. で再開したときに作成されます。 MSSQLSERVER サービスを再開しない限り、`tempdb` は引き続き元の場所で機能します。

1. `tempdb` データベースの論理ファイル名と、ディスク上での現在の場所を確認します。

    ```sql
    SELECT name, physical_name
    FROM sys.master_files
    WHERE database_id = DB_ID('tempdb');
    GO
    ```

2. `ALTER DATABASE`を使用して、各ファイルの場所を変更します。

    ```sql
    USE master;
    GO
    ALTER DATABASE tempdb
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');
    GO
    ALTER DATABASE tempdb
    MODIFY FILE (NAME = templog, FILENAME = 'E:\SQLData\templog.ldf');
    GO
    ```

3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスをいったん停止してから再起動します。

4. ファイルの変更を確認します。

    ```sql
    SELECT name, physical_name
    FROM sys.master_files
    WHERE database_id = DB_ID('tempdb');
    ```

5. tempdb.mdf ファイルと templog.ldf ファイルを元の場所から削除します。

### <a name="h-making-a-filegroup-the-default"></a>H. ファイル グループを既定にする

次の例では、例 B で作成した `Test1FG1` ファイル グループを、既定のファイル グループにします。 次に、既定のファイル グループを、`PRIMARY` ファイル グループに再設定します。 `PRIMARY` は、角かっこまたは引用符で区切る必要があります。

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP Test1FG1 DEFAULT;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP [PRIMARY] DEFAULT;
GO
```

### <a name="i-adding-a-filegroup-using-alter-database"></a>I. ALTER DATABASE を使用してファイル グループを追加する

次の例では、`FILEGROUP` 句が含まれる `FILESTREAM` を、`FileStreamPhotoDB` データベースに追加します。

```sql
--Create and add a FILEGROUP that CONTAINS the FILESTREAM clause.
ALTER DATABASE FileStreamPhotoDB
ADD FILEGROUP TodaysPhotoShoot
CONTAINS FILESTREAM;
GO

--Add a file for storing database photos to FILEGROUP
ALTER DATABASE FileStreamPhotoDB
ADD FILE
(
  NAME= 'PhotoShoot1',
  FILENAME = 'C:\Users\Administrator\Pictures\TodaysPhotoShoot.ndf'
)
TO FILEGROUP TodaysPhotoShoot;
GO
```

次の例では、`FILEGROUP` 句が含まれる `MEMORY_OPTIMIZED_DATA` を、`xtp_db` データベースに追加します。 このファイル グループには、メモリ最適化データを格納します。

```sql
--Create and add a FILEGROUP that CONTAINS the MEMORY_OPTIMIZED_DATA clause.
ALTER DATABASE xtp_db
ADD FILEGROUP xtp_fg
CONTAINS MEMORY_OPTIMIZED_DATA;
GO

--Add a file for storing memory optimized data to FILEGROUP
ALTER DATABASE xtp_db
ADD FILE
(
  NAME='xtp_mod',
  FILENAME='d:\data\xtp_mod'
)
TO FILEGROUP xtp_fg;
GO
```

### <a name="j-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>J. ファイル グループ内のファイルが自動拡張のしきい値を満たす場合にファイル グループ内のすべてのファイルが拡張されるようにファイル グループを変更する

 次の例では、必要な `ALTER DATABASE` ステートメントを生成して、読み取り/書き込みファイル グループを `AUTOGROW_ALL_FILES` 設定で変更します。

```sql
--Generate ALTER DATABASE ... MODIFY FILEGROUP statements
--so that all read-write filegroups grow at the same time.
SET NOCOUNT ON;

DROP TABLE IF EXISTS #tmpdbs
CREATE TABLE #tmpdbs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, isdone bit);

DROP TABLE IF EXISTS #tmpfgs
CREATE TABLE #tmpfgs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, fgname sysname, isdone bit);

INSERT INTO #tmpdbs ([dbid], [dbname], [isdone])
SELECT database_id, name, 0 FROM master.sys.databases (NOLOCK) WHERE is_read_only = 0 AND state = 0;

DECLARE @dbid int, @query VARCHAR(1000), @dbname sysname, @fgname sysname

WHILE (SELECT COUNT(id) FROM #tmpdbs WHERE isdone = 0) > 0
BEGIN
  SELECT TOP 1 @dbname = [dbname], @dbid = [dbid] FROM #tmpdbs WHERE isdone = 0

  SET @query = 'SELECT ' + CAST(@dbid AS NVARCHAR) + ', ''' + @dbname + ''', [name], 0 FROM [' + @dbname + '].sys.filegroups WHERE [type] = ''FG'' AND is_read_only = 0;'
  INSERT INTO #tmpfgs
  EXEC (@query)

  UPDATE #tmpdbs
  SET isdone = 1
  WHERE [dbid] = @dbid
END;

IF (SELECT COUNT(ID) FROM #tmpfgs) > 0
BEGIN
  WHILE (SELECT COUNT(id) FROM #tmpfgs WHERE isdone = 0) > 0
  BEGIN
    SELECT TOP 1 @dbname = [dbname], @dbid = [dbid], @fgname = fgname FROM #tmpfgs WHERE isdone = 0

    SET @query = 'ALTER DATABASE [' + @dbname + '] MODIFY FILEGROUP [' + @fgname + '] AUTOGROW_ALL_FILES;'

    PRINT @query

    UPDATE #tmpfgs
    SET isdone = 1
    WHERE [dbid] = @dbid AND fgname = @fgname
  END
END;
GO
```

## <a name="see-also"></a>参照

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [バイナリ ラージ オブジェクト](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)
- [DBCC SHRINKFIL](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)
- [sp_filestream_force_garbage_collection](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)
- [データベース ファイルの初期化](../../relational-databases/databases/database-instant-file-initialization.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||
> |-|-|-|
> |[SQL Server](alter-database-transact-sql-file-and-filegroup-options.md?view=sql-server-2017)|**_\* SQL Database<br />マネージド インスタンス \*_**<br />&nbsp;|

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Azure SQL Database マネージド インスタンス

このステートメントは、Azure SQL Database マネージド インスタンス内のデータベースで使います。

## <a name="syntax-for-databases-in-a-managed-instance"></a>マネージド インスタンスのデータベースでの構文

```
ALTER DATABASE database_name
{
    <add_or_modify_files>
  | <add_or_modify_filegroups>
}
[;]

<add_or_modify_files>::=
{
    ADD FILE <filespec> [ ,...n ]
        [ TO FILEGROUP { filegroup_name } ]
  | REMOVE FILE logical_file_name
  | MODIFY FILE <filespec>
}
  
<filespec>::=
(
    NAME = logical_file_name
    [ , SIZE = size [ KB | MB | GB | TB ] ]
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB| % ] ]
)

<add_or_modify_filegroups>::=
{
    | ADD FILEGROUP filegroup_name
    | REMOVE FILEGROUP filegroup_name
    | MODIFY FILEGROUP filegroup_name
        { <filegroup_updatability_option>
        | DEFAULT
        | NAME = new_filegroup_name
        | { AUTOGROW_SINGLE_FILE | AUTOGROW_ALL_FILES }
        }
}  
<filegroup_updatability_option>::=
{
    { READONLY | READWRITE }
    | { READ_ONLY | READ_WRITE }
}

```

## <a name="arguments"></a>引数

**\<add_or_modify_files>::=**

追加、削除、または変更するファイルを指定します。

*database_name*: 変更するデータベースの名前です。

ADD FILE: データベースにファイルを追加します。

TO FILEGROUP { *filegroup_name* }: 指定されたファイルを追加するファイル グループを指定します。 現在のファイル グループ、および現在の既定のファイル グループを表示するには、[sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) カタログ ビューを使用してください。

REMOVE FILE *logical_file_name*: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスから論理ファイルの説明を削除し、物理ファイルを削除します。 ファイルが空でない場合は削除できません。

*logical_file_name*: ファイルを参照するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用される論理名を指定します。

変更するファイルを指定します。 一度に 1 つの \<filespec> プロパティだけを変更できます。 変更するファイルを識別するには、\<filespec> に NAME を指定する必要があります。 SIZE を指定する場合、ファイルの現在のサイズより新しいサイズの方が大きくなければなりません。

**\<filespec>::=**

ファイル プロパティを制御します。

NAME: *logical_file_name* ファイルの論理名を指定します。

*logical_file_name*: ファイルを参照するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで使用される論理名を指定します。

NEWNAME *new_logical_file_name*: ファイルの新しい論理名を指定します。

*new_logical_file_name*: 既存の論理ファイル名と置換する新しい名前を指定します。 論理ファイル名は、データベース内で一意であり、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 この名前は、文字定数、Unicode 定数、標準の識別子、区切られた識別子のいずれでもかまいません。

SIZE *size*: ファイルのサイズを指定します。

*size*: ファイルのサイズです。

ADD FILE と共に指定する場合、*size* はファイルの初期サイズになります。 MODIFY FILE と共に指定する場合、*size* はファイルの新しいサイズになります。この値には、ファイルの現在のサイズより大きい値を指定する必要があります。

プライマリ ファイルに *size* が指定されていない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**model** データベースのプライマリ ファイルのサイズを使用します。 セカンダリ データ ファイルまたはログ ファイルが指定されているにもかかわらず、そのファイルに対して *size* が指定されていない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では、そのファイルのサイズが 1 MB になります。

KB、MB、GB、および TB の各サフィックスを使用して、キロバイト、メガバイト、ギガバイト、またはテラバイトを指定できます。 既定値は MB です。 整数を指定します。小数は含めないでください。 小数部を持つメガバイトの値を指定するには、その値に 1024 を乗算することによって、キロバイトの単位に変換します。 たとえば、1.5 MB ではなく 1536 KB と指定します (1.5 × 1024 = 1536)。

MAXSIZE { *max_size*| UNLIMITED }: ファイルのサイズの上限を指定します。

*max_size*: ファイルの最大サイズです。 KB、MB、GB、および TB の各サフィックスを使用して、キロバイト、メガバイト、ギガバイト、またはテラバイトを指定できます。 既定値は MB です。 整数を指定します。小数は含めないでください。 *max_size* を指定しない場合、ファイル サイズはディスクがいっぱいになるまで拡張されます。

UNLIMITED: ディスクがいっぱいになるまでファイルを拡張するように指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、無制限に拡張するファイル固有のログの最大サイズは 2 TB で、データ ファイルの最大サイズは 16 TB です。

FILEGROWTH *growth_increment*: ファイルを自動拡張するときの増加量を指定します。 ファイルの FILEGROWTH の設定を MAXSIZE の設定より大きくすることはできません。

*growth_increment*: 新しい領域が必要とされるたびにファイルに追加される領域の容量です。

値は MB、KB、GB、TB または % の単位で指定できます。 サフィックス MB、KB、または % を付けないで数値を指定した場合の既定値は MB です。 % を指定すると、1 回の増加量は、増加時のファイル サイズに指定されたパーセンテージを掛けた値になります。 指定されたサイズは、最も近い 64 KB 単位の値に切り上げられます。

0 の値は、自動拡張がオフで、領域を追加できないことを示します。

FILEGROWTH が指定されていない場合、既定値は次のとおりです。

- データ: 64 MB
- ログ ファイル: 64 MB

**\<add_or_modify_filegroups>::=**

データベースに対してファイル グループの追加、変更、または削除を行います。

ADD FILEGROUP *filegroup_name*: データベースにファイル グループを追加します。

次の例では、sql_db_mi というデータベースに追加するファイル グループを作成し、そのファイル グループにファイルを追加します。

```sql
ALTER DATABASE sql_db_mi ADD FILEGROUP sql_db_mi_fg;
GO
ALTER DATABASE sql_db_mi ADD FILE (NAME='sql_db_mi_mod') TO FILEGROUP sql_db_mi_fg;
```

REMOVE FILEGROUP *filegroup_name*: データベースからファイルグループを削除します。 ファイル グループが空でない場合は削除できません。 最初に、ファイル グループからすべてのファイルを削除してください。 詳細については、前の「REMOVE FILE *logical_file_name*」を参照してください。

MODIFY FILEGROUP _filegroup\_name_ { \<filegroup_updatability_option> | DEFAULT | NAME **=** _new\_filegroup\_name_ } ファイル グループに変更を加えます。ここでは、状態を READ_ONLY または READ_WRITE に設定したり、ファイル グループをデータベースの既定のファイル グループに指定したり、ファイル グループ名を変更することができます。

\<filegroup_updatability_option>: ファイル グループに読み取り専用、または読み取り/書き込みのプロパティを設定します。

DEFAULT: 既定のデータベース ファイル グループを *filegroup_name* に変更します。 データベース内の 1 つのファイル グループだけを、既定のファイル グループにすることができます。 詳細については、「 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)」を参照してください。

NAME = *new_filegroup_name*: ファイル グループ名を *new_filegroup_name* に変更します。

AUTOGROW_SINGLE_FILE

ファイル グループ内のファイルが自動拡張のしきい値を満たす場合は、そのファイルのみが拡張されます。 これは既定値です。

AUTOGROW_ALL_FILES

ファイル グループ内のファイルが自動拡張のしきい値を満たすときに、ファイル グループ内のすべてのファイルを拡張します。

**\<filegroup_updatability_option>::=**

ファイル グループに読み取り専用、または読み取り/書き込みのプロパティを設定します。

READ_ONLY | READONLY: ファイル グループが読み取り専用であることを指定します。 この中のオブジェクトを更新することはできません。 プライマリ ファイル グループを読み取り専用にすることはできません。 この状態を変更するには、データベースに対する排他的アクセスが必要になります。 詳細については、SINGLE_USER 句をご覧ください。

読み取り専用データベースのデータを変更することはできないため、次のようになります。

- システム起動時に自動復旧がスキップされます。
- データベースの圧縮が不可能になります。
- 読み取り専用データベースでは、ロックは発生しません。 これにより、クエリのパフォーマンスが向上することがあります。

> [!NOTE]
> キーワード READONLY は、将来のバージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 新しい開発作業では READONLY の使用は避け、現在 READONLY を使用しているアプリケーションは修正するようにしてください。 代わりに、READ_ONLY を使用してください。

READ_WRITE | READWRITE: ファイル グループを READ_WRITE に指定します。 ファイル グループ内のオブジェクトを更新できます。 この状態を変更するには、データベースに対する排他的アクセスが必要になります。 詳細については、SINGLE_USER 句をご覧ください。

> [!NOTE]
> キーワード `READWRITE` は、将来のバージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 新しい開発作業では、`READWRITE` の使用は避け、現在 `READWRITE` を使用しているアプリケーションは `READ_WRITE` を使用するように修正することを計画してください。

これらのオプションの状態を確認するには、**sys.databases** カタログ ビューの **is_read_only** 列、または `DATABASEPROPERTYEX` 関数の **Updateability** プロパティを調べてください。

## <a name="remarks"></a>解説

データベースのサイズを縮小するには、[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md) を使用します。

`BACKUP` ステートメントの実行中にファイルを追加したり削除したりすることはできません。

各データベースに、最大 32,767 のファイルと 32,767 のファイル グループを指定できます。

## <a name="examples"></a>例

### <a name="a-adding-a-file-to-a-database"></a>A. データベースにファイルを追加する

次の例では、5 MB のデータ ファイルを [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースに追加します。

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
  NAME = Test1dat2,
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
);
GO
```

### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>B. 2 つのファイルから成るファイル グループをデータベースに追加する

次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースに `Test1FG1` ファイル グループを作成し、そのファイル グループに 5 MB のファイルを 2 つ追加します。

```sql
USE master
GO
ALTER DATABASE AdventureWorks2012
ADD FILEGROUP Test1FG1;
GO
ALTER DATABASE AdventureWorks2012
ADD FILE
(
    NAME = test1dat3,
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
),
(
    NAME = test1dat4,
    SIZE = 5MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
)  
TO FILEGROUP Test1FG1;
GO

```

### <a name="c-removing-a-file-from-a-database"></a>C. データベースからファイルを削除する

次の例では、例 B で追加したファイルの一方を削除します。

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
REMOVE FILE test1dat4;
GO
```

### <a name="d-modifying-a-file"></a>D. ファイルを変更する

次の例では、例 B で追加したファイルのうち、1 つのサイズを拡張します。MODIFY FILE を指定した ALTER DATABASE コマンドではファイル サイズを大きくすることだけが可能なため、ファイル サイズを小さくする必要がある場合は、DBCC SHRINKFILE を使用する必要があります。

```sql
USE master;
GO

ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

この例では、データ ファイルのサイズを 100 MB に縮小してから、その量のサイズを指定します。

```sql
USE AdventureWorks2012;
GO

DBCC SHRINKFILE (AdventureWorks2012_data, 100);
GO

USE master;
GO

ALTER DATABASE AdventureWorks2012
MODIFY FILE
(NAME = test1dat3,
SIZE = 200MB);
GO
```

### <a name="e-making-a-filegroup-the-default"></a>E. ファイル グループを既定にする

次の例では、例 B で作成した `Test1FG1` ファイル グループを、既定のファイル グループにします。 次に、既定のファイル グループを、`PRIMARY` ファイル グループに再設定します。 `PRIMARY` は、角かっこまたは引用符で区切る必要があります。

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP Test1FG1 DEFAULT;
GO
ALTER DATABASE AdventureWorks2012
MODIFY FILEGROUP [PRIMARY] DEFAULT;
GO
```

### <a name="f-adding-a-filegroup-using-alter-database"></a>F. ALTER DATABASE を使用してファイル グループを追加する

次の例では、`FILEGROUP` を `MyDB` データベースに追加します。

```sql
--Create and add a FILEGROUP
ALTER DATABASE MyDB
ADD FILEGROUP NewFG;
GO

--Add a file to FILEGROUP
ALTER DATABASE MyDB
ADD FILE
(
    NAME= 'MyFile',
)
TO FILEGROUP NewFG;
GO
```

### <a name="g-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>G. ファイル グループ内のファイルが自動拡張のしきい値を満たす場合にファイル グループ内のすべてのファイルが拡張されるようにファイル グループを変更する

次の例では、必要な `ALTER DATABASE` ステートメントを生成して、読み取り/書き込みファイル グループを `AUTOGROW_ALL_FILES` 設定で変更します。

```sql
--Generate ALTER DATABASE ... MODIFY FILEGROUP statements
--so that all read-write filegroups grow at the same time.
SET NOCOUNT ON;

DROP TABLE IF EXISTS #tmpdbs
CREATE TABLE #tmpdbs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, isdone bit);

DROP TABLE IF EXISTS #tmpfgs
CREATE TABLE #tmpfgs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, fgname sysname, isdone bit);

INSERT INTO #tmpdbs ([dbid], [dbname], [isdone])
SELECT database_id, name, 0 FROM master.sys.databases (NOLOCK) WHERE is_read_only = 0 AND state = 0;

DECLARE @dbid int, @query VARCHAR(1000), @dbname sysname, @fgname sysname

WHILE (SELECT COUNT(id) FROM #tmpdbs WHERE isdone = 0) > 0
BEGIN
    SELECT TOP 1 @dbname = [dbname], @dbid = [dbid] FROM #tmpdbs WHERE isdone = 0

    SET @query = 'SELECT ' + CAST(@dbid AS NVARCHAR) + ', ''' + @dbname + ''', [name], 0 FROM [' + @dbname + '].sys.filegroups WHERE [type] = ''FG'' AND is_read_only = 0;'
    INSERT INTO #tmpfgs
    EXEC (@query)

    UPDATE #tmpdbs
    SET isdone = 1
    WHERE [dbid] = @dbid
END;

IF (SELECT COUNT(ID) FROM #tmpfgs) > 0
BEGIN
    WHILE (SELECT COUNT(id) FROM #tmpfgs WHERE isdone = 0) > 0
    BEGIN
        SELECT TOP 1 @dbname = [dbname], @dbid = [dbid], @fgname = fgname FROM #tmpfgs WHERE isdone = 0

        SET @query = 'ALTER DATABASE [' + @dbname + '] MODIFY FILEGROUP [' + @fgname + '] AUTOGROW_ALL_FILES;'

        PRINT @query

        UPDATE #tmpfgs
        SET isdone = 1
        WHERE [dbid] = @dbid AND fgname = @fgname
    END
END;
GO
```

## <a name="see-also"></a>参照

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-mi-current)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)
- [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)
- [メモリ最適化ファイル グループ](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)

::: moniker-end
