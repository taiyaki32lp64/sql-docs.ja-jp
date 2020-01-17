---
title: データベース ファイルとファイル グループ | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6ccf21bcc3e0657123aa4f0fdcfe9b2d3cb0861a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037595"
---
# <a name="database-files-and-filegroups"></a>データベース ファイルとファイル グループ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各データベースには、データ ファイルとログ ファイルという少なくとも 2 つのオペレーティング システム ファイルがあります。 データ ファイルには、テーブル、インデックス、ストアド プロシージャ、およびビューなどのデータおよびオブジェクトが含まれます。 ログ ファイルには、データベース内のすべてのトランザクションを復旧するために必要な情報が含まれます。 データ ファイルは、割り当てと管理の目的でファイル グループにまとめることができます。  
  
## <a name="database-files"></a>データベース ファイル  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースには、次の表で示すように 3 種類のファイルがあります。  
  
|ファイル|[説明]|  
|----------|-----------------|  
|プライマリ|プライマリ データ ファイルにはデータベースの起動情報が含まれており、データベース内の他のファイルを指し示します。 ユーザー データおよびオブジェクトは、このファイルまたはセカンダリ データ ファイルに格納できます。 各データベースには 1 つのプライマリ データ ファイルがあります。 プライマリ データ ファイルに推奨されるファイル名拡張子は .mdf です。|  
|セカンダリ|セカンダリ データ ファイルは省略可能です。また、ユーザー定義であり、ユーザー データが格納されます。 セカンダリ ファイルを使用すると、各ファイルを異なるディスク ドライブに配置することにより、複数のディスクにデータを分散できます。 また、データベースが 1 つの Windows ファイルの最大サイズを超えた場合には、セカンダリ データ ファイルを使用してデータベースを拡張できます。<br /><br /> セカンダリ データ ファイルに推奨されるファイル名拡張子は .ndf です。|  
|トランザクション ログ|トランザクション ログ ファイルには、データベースの復旧に使用されるログ情報が格納されます。 1 つのデータベースにトランザクション ログ ファイルが少なくとも 1 つ必要です。 トランザクション ログに推奨されるファイル名拡張子は .ldf です。|  
  
 たとえば、データとオブジェクトをすべて格納するプライマリ ファイルを 1 つとトランザクション ログ情報を格納するログ ファイルを 1 つ含む **Sales** という単純なデータベースを作成することができます。 または、プライマリ ファイルを 1 つとセカンダリ ファイルを 5 つ含む **Orders** というより複雑なデータベースを作成できます。 データベース内のデータとオブジェクトは 6 つすべてのファイルに分散され、4 つのログ ファイルにトランザクション ログ情報が含まれます。  
  
 既定では、データとトランザクション ログは同一のドライブおよびパス上に配置されます。 これは、単一のディスク システムを処理するために行われますが、 実稼働環境では最適ではない場合があります。 そのため、データとログ ファイルは別のディスクに配置することをお勧めします。  

### <a name="logical-and-physical-file-names"></a>論理ファイル名と物理ファイル名
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ファイルにはファイル名の種類が 2 つあります。 

**logical_file_name:** logical_file_name は、すべての Transact-SQL ステートメントで物理ファイルを参照するために使用する名前です。 論理ファイル名は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の識別子の規則に従っている必要があります。また、データベース内の論理ファイル名は互いに一意にする必要があります。 これは `ALTER DATABASE` の `NAME` 引数で設定されます。 詳細については、「[ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」を参照してください。

**os_file_name:** os_file_name は、ディレクトリ パスを含む物理ファイルの名前です。 この名前はオペレーティング システムのファイル名の規則に従っている必要があります。 これは `ALTER DATABASE` の `FILENAME` 引数で設定されます。 詳細については、「[ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」を参照してください。

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータとログ ファイルは、FAT または NTFS のいずれかのファイル システムに配置できます。 Windows システムの場合、NTFS のセキュリティの方が強力なので、NTFS ファイル システムを使用することをお勧めします。 

> [!WARNING]
> 読み書き可能なデータ ファイル グループとログ ファイルは、圧縮された NTFS ファイル システムに配置できません。 圧縮された NTFS ファイル システムに配置できるのは、読み取り専用データベースと読み取り専用セカンダリ ファイル グループだけです。
> 領域を節約するために、ファイル システムの圧縮ではなく、[データの圧縮](../../relational-databases/data-compression/data-compression.md)を強くお勧めします。

1 台のコンピューターで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスを実行すると、インスタンスごとに異なる既定のディレクトリが与えられ、そのインスタンスで作成したデータベースのファイルがその既定のディレクトリで保持されます。 詳細については、「 [SQL Server の既定のインスタンスおよび名前付きインスタンスのファイルの場所](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)」を参照してください。

### <a name="data-file-pages"></a>データ ファイルのページ
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ファイルのページには、ファイル内の最初のページを 0 として、順に番号が付けられています。 データベース内の各ファイルには一意のファイル ID 番号が付けられています。 データベース内のページを一意に識別するには、ファイル ID とページ番号の両方が必要です。 次の例は、4 MB のプライマリ データ ファイルと 1 MB のセカンダリ データ ファイルがあるデータベースのページ番号を示しています。

![data_file_pages](../../relational-databases/databases/media/data-file-pages.gif)

各ファイルの 1 ページ目はファイル ヘッダー ページで、そのファイルの属性に関する情報が格納されています。 また、ファイルの先頭にある数ページには、アロケーション マップなどのシステム情報が格納されています。 プライマリ データ ファイルと最初のログ ファイルの両方に格納されているシステム ページの 1 つは、データベースの属性情報が格納されているデータベース ブート ページです。 ページとページの種類の詳細については、「[ページとエクステントのアーキテクチャ ガイド](../..//relational-databases/pages-and-extents-architecture-guide.md)」を参照してください。

### <a name="file-size"></a>ファイル サイズ
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のファイルは、最初に指定したサイズから自動拡張するように設定できます。 ファイルを定義するときに、拡張の増分値を指定できます。 ファイルの空き容量がなくなるたびに、ファイルのサイズは指定した増分値だけ拡張されます。 ファイル グループに複数のファイルが存在する場合、すべてのファイルの空き容量がなくなるまで、ファイル グループ内のファイルは自動拡張しません。 すべてのファイルに空き容量がなくなると、ラウンド ロビン方式の[比例配分](../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill)で拡張されます。

各ファイルに最大サイズを指定することもできます。 最大サイズを指定しなかった場合、ファイルはディスクの空き領域を使い果たすまで拡張し続けます。 この機能は、ユーザーがシステム管理者と簡単に連絡を取れない状況にあり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアプリケーションに埋め込んだデータベースとして使用している場合に特に便利です。 ユーザーは、必要に応じてファイルを自動拡張するようにし、データベースの空き領域の監視や追加領域を手動で割り当てる管理上の負担を軽減できます。  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で[ファイルの瞬時初期化 (IFI)](../../relational-databases/databases/database-instant-file-initialization.md) を有効にすると、データ ファイルに新しい領域を割り当てるとき、最小限のオーバーヘッドが発生します。

トランザクション ログ ファイル管理の詳細については、「[トランザクション ログ ファイルのサイズの管理](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations)」を参照してください。   

## <a name="database-snapshot-files"></a>データベース スナップショット ファイル
スナップショットがユーザーによって作成されるか、内部的に使用されるかに応じて、copy-on-write (書き込まれるたびにコピー) のデータを保存するためにデータベース スナップショットで使用されるファイル形式が決まります。

* ユーザーによって作成されるデータベース スナップショットでは、1 つまたは複数のスパース ファイルにデータを保存します。 スパース ファイル技術は NTFS ファイル システムの機能です。 初期状態のスパース ファイルにはユーザー データが含まれておらず、ユーザー データ用のディスク領域も割り当てられていません。 データベース スナップショットでのスパース ファイルの使用方法と、データベース スナップショットがどのように拡張されるかについては、「 [データベース スナップショットのスパース ファイルのサイズを表示する方法 (Transact-SQL)](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)」を参照してください。 
* データベース スナップショットは特定の DBCC コマンドによって内部的に使用されます。 このようなコマンドには、DBCC CHECKDB、DBCC CHECKTABLE、DBCC CHECKALLOC、DBCC CHECKFILEGROUP などがあります。 内部データベース スナップショットでは、元のデータベース ファイルのスパース代替データ ストリームを使用します。 スパース ファイル同様、代替データ ストリームも NTFS ファイル システムの機能です。 スパース代替データ ストリームを使用すると、ファイル サイズやボリューム統計に影響を与えることなく、複数のデータ割り当てを単一のファイルまたはフォルダーに関連付けることができます。 
  
## <a name="filegroups"></a>ファイル グループ  
 各データベースには、1 つのプライマリ ファイル グループがあります。 プライマリ ファイル グループには、プライマリ データ ファイル、および他のファイル グループに配置されていないセカンダリ ファイルが含まれます。 ユーザー定義のファイル グループを作成して、データベースの管理、データの割り当て、および配置をしやすくするために、データ ファイルをグループ化できます。  
  
 たとえば、3 つのファイル (`Data1.ndf`、`Data2.ndf`、`Data3.ndf`) をそれぞれ 3 つのディスク ドライブ上に作成し、ファイル グループ `fgroup1` に割り当てることができます。 その後、ファイル グループ `fgroup1` にテーブルを作成することができます。 このテーブル内にあるデータに対するクエリが 3 つのディスクにわたって分散されるため、パフォーマンスが向上します。 RAID (Redundant Array of Independent Disks) ストライプ セットにファイルを 1 つ作成しても、同じくらいパフォーマンスを向上させることができます。 ただし、ファイルとファイル グループを使用すれば、新しいファイルを新しいディスクに容易に追加できます。  
  
 すべてのデータ ファイルは、次の表に一覧表示されているファイル グループに格納されます。  
  
|[ファイル グループ]|[説明]|  
|---------------|-----------------|  
|プライマリ|プライマリ ファイルが含まれているファイル グループ。 すべてのシステム テーブルがプライマリ ファイル グループに割り当てられます。|  
|メモリ最適化データ|メモリ最適化ファイル グループは filestream ファイル グループに基づきます。|  
|Filestream||    
|ユーザー定義|ユーザーがデータベースを最初に作成したとき、または後で変更したときに、ユーザーが特別に作成したファイル グループ。|  
  
### <a name="default-primary-filegroup"></a>既定の (プライマリ) ファイル グループ  
 所属させるファイル グループを指定せずにデータベース内にオブジェクトを作成すると、そのオブジェクトは既定のファイル グループに割り当てられます。 どのような場合でも、必ず 1 つのファイル グループが既定のファイル グループとして指定されます。 既定のファイル グループ内のファイルは、他のファイル グループに割り当てられない新しいオブジェクトを十分に格納できる大きさである必要があります。  
  
 PRIMARY ファイル グループは、ALTER DATABASE ステートメントを使用して変更しない限り、既定のファイル グループです。 システム オブジェクトとシステム テーブルは、変更後の既定のファイル グループではなく、引き続き PRIMARY ファイル グループに格納されます。  
 
### <a name="memory-optimized-data-filegroup"></a>メモリ最適化データ ファイル グループ

メモリ最適化ファイル グループの詳細については、「[メモリ最適化ファイル グループ](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)」を参照してください。

### <a name="filestream-filegroup"></a>filestream ファイル グループ

filestream ファイル グループの詳細については、「[FILESTREAM](../../relational-databases/blob/filestream-sql-server.md#filestream-storage)」と「[FILESTREAM が有効なデータベースを作成する方法](../../relational-databases/blob/create-a-filestream-enabled-database.md)」を参照してください。

### <a name="file-and-filegroup-example"></a>ファイルおよびファイル グループの例
 次の例では、SQL Server のインスタンスにデータベースを作成します。 このデータベースにはプライマリ データ ファイル、ユーザー定義のファイル グループ、およびログ ファイルが含まれます。 プライマリ データ ファイルはプライマリ ファイル グループ内にあり、ユーザー定義ファイル グループには 2 つのセカンダリ データ ファイルがあります。 ALTER DATABASE ステートメントにより、このユーザー定義のファイル グループは既定のファイル グループになります。 その後、ユーザー定義のファイル グループを指定してテーブルを作成します。 (この例では、SQL Server のバージョンの指定を回避するため、一般的なパス `c:\Program Files\Microsoft SQL Server\MSSQL.1` を使用しています。)

```sql
USE master;
GO
-- Create the database with the default data
-- filegroup, filstream filegroup and a log file. Specify the
-- growth increment and the max size for the
-- primary data file.
CREATE DATABASE MyDB
ON PRIMARY
  ( NAME='MyDB_Primary',
    FILENAME=
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_Prm.mdf',
    SIZE=4MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP MyDB_FG1
  ( NAME = 'MyDB_FG1_Dat1',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_1.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
  ( NAME = 'MyDB_FG1_Dat2',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_2.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM
  ( NAME = 'MyDB_FG_FS',
    FILENAME = 'c:\Data\filestream1')
LOG ON
  ( NAME='MyDB_log',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB.ldf',
    SIZE=1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB);
GO
ALTER DATABASE MyDB 
  MODIFY FILEGROUP MyDB_FG1 DEFAULT;
GO

-- Create a table in the user-defined filegroup.
USE MyDB;
CREATE TABLE MyTable
  ( cola int PRIMARY KEY,
    colb char(8) )
ON MyDB_FG1;
GO

-- Create a table in the filestream filegroup
CREATE TABLE MyFSTable
(
    cola int PRIMARY KEY,
  colb VARBINARY(MAX) FILESTREAM NULL
)
GO
```

次の図は、上の例の結果をまとめたものです (filestream データを除く)。

![filegroup_example](../../relational-databases/databases/media/filegroup-example.gif)

## <a name="file-and-filegroup-fill-strategy"></a>ファイルとファイル グループのデータの格納方法
ファイル グループには、ファイル グループ内のすべてのファイルを対象として、各ファイルの空き領域に比例したデータ格納方法が使用されます。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]は、データをファイル グループに書き込む際には、最初のファイルがいっぱいになるまでそのファイルにすべてのデータを書き込むのではなく、ファイル内の空き領域に比例してファイル グループ内の各ファイルにデータを書き込みます。 その後で、次のファイルにデータを書き込みます。 たとえば、ファイル f1 の空き領域が 100 MB で、ファイル f2 の空き領域が 200 MB の場合、ファイル f1 のエクステント 1 つとファイル f2 のエクステント 2 つが割り当てられます。 これにより、2 つのファイルがほぼ同時にいっぱいになり、簡易ストライピングが実現されます。

ファイル グループ内のすべてのファイルがいっぱいになると、より多くのデータに対応できるように、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]によってファイルが 1 つずつラウンドロビン方式で自動的に拡張されます (データベースが自動拡張されるように設定されている場合)。 たとえば、1 つのファイル グループが 3 つのファイルから構成されていて、すべてのファイルが自動拡張されるように設定されているとします。 ファイル グループ内のすべてのファイルの領域がいっぱいになると、最初のファイルだけが拡張されます。 最初のファイルがいっぱいになり、ファイル グループにデータが書き込めなくなると、2 番目のファイルが拡張されます。 2 番目のファイルがいっぱいになり、ファイル グループにデータが書き込めなくなると、3 番目のファイルが拡張されます。 3 番目のファイルがいっぱいになり、ファイル グループにデータが書き込めなくなると、最初のファイルが再度拡張され、その後データの書き込み領域がなくなると順次各ファイルの拡張が行われます。

## <a name="rules-for-designing-files-and-filegroups"></a>ファイルとファイル グループのデザインに関する規則
ファイルとファイル グループに関連する規則は次のとおりです。
- 1 つのファイルまたはファイル グループを複数のデータベースで使用することはできません。 たとえば、sales データベース内のデータとオブジェクトが格納されているファイル sales.mdf と sales.ndf を他のデータベースが使用することはできません。
- ファイルは 1 つのファイル グループにしか所属できません。
- トランザクション ログ ファイルをファイル グループに格納することはできません。

## <a name="Recommendations"></a> 推奨事項
ファイルとファイル グループを使用して作業するときの一般的な推奨事項を次に示します。 
- 大部分のデータベースは、1 つのデータ ファイルと 1 つのトランザクション ログ ファイルで正常に機能します。
- 複数のデータ ファイルを使用する場合は、追加ファイル用に 2 番目のファイル グループを作成し、既定のファイル グループとして設定します。 これにより、プライマリ ファイルにはシステム テーブルとシステム オブジェクトだけが格納されます。
- パフォーマンスを最適化するには、できるだけ、使用可能な異なるディスクにファイルまたはファイル グループを作成します。 また、大きな記憶域を占有する可能性のあるオブジェクトは、別々のファイル グループに配置します。
- ファイル グループを使用すると、特定の物理ディスク上にオブジェクトを配置できます。
- 同じ結合クエリで使用する各テーブルは別のファイル グループに配置してください。 これにより、結合されるデータが並列ディスク I/O によって検索されるので、パフォーマンスが向上します。
- アクセス頻度が高いテーブルとそれらのテーブルに属する非クラスター化インデックスは、別々のファイル グループに配置してください。 これにより、ファイルが別の物理ディスク上にある場合に並列 I/O が行われるので、パフォーマンスが向上します。
- トランザクション ログ ファイルは、他のファイルやファイル グループと同じ物理ディスク上に配置しないでください。

トランザクション ログ ファイル管理の推奨事項については、「[トランザクション ログ ファイルのサイズの管理](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations)」を参照してください。   

## <a name="related-content"></a>関連コンテンツ  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)    
 [ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)      
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
 [SQL Server トランザクション ログのアーキテクチャと管理ガイド](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)    
 [ページとエクステントのアーキテクチャ ガイド](../../relational-databases/pages-and-extents-architecture-guide.md)    
 [トランザクション ログ ファイルのサイズの管理](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)     
