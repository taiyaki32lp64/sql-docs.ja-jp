---
title: テーブルとストアド プロシージャのネイティブ コンパイル | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e70ab55fedcc5053cf82a78c040c850a23824eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63075198"
---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>テーブルとストアド プロシージャのネイティブ コンパイル
  インメモリ OLTP により、ネイティブ コンパイルという概念が導入されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はメモリ最適化テーブルにアクセスするストアド プロシージャをネイティブにコンパイルできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はメモリ最適化テーブルをネイティブにコンパイルすることもできます。 ネイティブ コンパイルは、(従来の) 解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)]よりも高速なデータ アクセスと効率的なクエリ実行を可能にします。 テーブルとストアド プロシージャのネイティブ コンパイルを実行すると DLL が生成されます。  
  
 メモリ最適化テーブル型のネイティブ コンパイルもサポートされています。 詳しくは、「 [Memory-Optimized Table Variables](../../database-engine/memory-optimized-table-variables.md)」をご覧ください。  
  
 ネイティブ コンパイルとは、プログラミングの構造をネイティブ コードに変換する処理であり、追加のコンパイルまたは解釈を必要としないプロセッサ命令で構成されます。  
  
 インメモリ OLTP は、作成されたときにメモリ最適化テーブルを、そしてネイティブ DLL に読み込まれたときにネイティブ コンパイル ストアド プロシージャをコンパイルします。 また、DLL は、データベースまたはサーバーが再起動した後に再コンパイルされます。 DLL を再作成するために必要な情報がデータベース メタデータに格納されます。 DLL は、データベースに関連付けられていますが、データベースの一部ではありません。 たとえば、DLL は、データベース バックアップに含まれていません。  
  
> [!NOTE]  
>  メモリ最適化テーブルは、サーバーの再起動中に再コンパイルされます。 データベースの復元を迅速に行うために、ネイティブ コンパイル ストアド プロシージャは、サーバーの再起動中に再コンパイルされず、最初の実行時にコンパイルされます。 このようにコンパイルが延期されるため、ネイティブ コンパイル ストアド プロシージャは、最初の実行後に [sys.dm_os_loaded_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql) を呼び出した場合にのみ表示されます。  
  
## <a name="maintenance-of-in-memory-oltp-dlls"></a>インメモリ OLTP DLL のメンテナンス  
 次のクエリは、サーバーのメモリに現在読み込まれているすべてのテーブルとストアド プロシージャ DLL を示します。  
  
```sql  
SELECT name, description FROM sys.dm_os_loaded_modules  
where description = 'XTP Native DLL'  
```  
  
 ネイティブ コンパイルによって生成されたファイルをデータベース管理者が維持する必要はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、不要になった生成ファイルが自動的に削除されます。 たとえばテーブルやストアド プロシージャが削除されたとき、またはデータベースが削除されたときに、生成ファイルが削除されます。  
  
> [!NOTE]  
>  コンパイルが失敗するか、中断した場合、生成されたファイルの一部は削除されません。 これらのファイルはサポート性のために意図的に残され、データベースが削除されるときに削除されます。  
  
> [!NOTE]  
>  データベースを起動している間に、SQL Server によってデータベースの復旧に必要なすべてのテーブルの Dll がコンパイルされます。 データベースを再起動する直前にテーブルが削除された場合、チェックポイント ファイルかトランザクション ログにテーブルの残存物が存在するため、データベースの起動中にテーブルの DLL が再コンパイルされる場合があります。 再起動後に DLL がアンロードされ、通常のクリーンアップ プロセスによってファイルが削除されます。  
  
## <a name="native-compilation-of-tables"></a>テーブルのネイティブ コンパイル  
 `CREATE TABLE` ステートメントを使用してメモリ最適化テーブルを作成すると、テーブル情報がデータベース メタデータに書き込まれ、テーブルとインデックス構造がメモリに作成されます。 また、テーブルは DLL にコンパイルされます。  
  
 データベースとメモリ最適化テーブルを作成する、次のサンプル スクリプトについて考えてみます。  
  
```sql  
use master  
go  
create database db1  
go  
alter database db1 add filegroup db1_mod contains memory_optimized_data  
go  
-- adapt filename as needed  
alter database db1 add file (name='db1_mod', filename='c:\data\db1_mod') to filegroup db1_mod  
go  
use db1  
go  
create table dbo.t1  
   (c1 int not null primary key nonclustered,  
    c2 INT)  
with (memory_optimized=on)  
go  
-- retrieve the path of the DLL for table t1  
select name, description FROM sys.dm_os_loaded_modules  
where name like '%xtp_t_' + cast(db_id() as varchar(10)) + '_' + cast(object_id('dbo.t1') as varchar(10)) + '.dll'  
go  
```  
  
 テーブルを作成すると、テーブル DLL が作成され、メモリに DLL が読み込まれます。 CREATE TABLE ステートメントの直後の DMV クエリは、テーブル DLL のパスを取得します。  
  
 テーブル DLL は、テーブルのインデックス構造と行形式を理解します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は DLL を使用してインデックスをスキャンし、行を取得し、行のコンテンツを格納します。  
  
## <a name="native-compilation-of-stored-procedures"></a>ストアド プロシージャのネイティブ コンパイル  
 NATIVE_COMPILATION が設定されているストアド プロシージャはネイティブでコンパイルされます。 つまり、パフォーマンスが重要なビジネス ロジックの効率的な実行のために、プロシージャの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがすべてネイティブ コードにコンパイルされます。  
  
 ネイティブ コンパイル ストアド プロシージャの詳細については、「 [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md)」をご覧ください。  
  
 前の例のテーブル t1 に行を挿入する、次のサンプル ストアド プロシージャについて考えてみます。  
  
```sql  
create procedure dbo.native_sp  
with native_compilation, schemabinding, execute as owner  
as  
begin atomic  
with (transaction isolation level=snapshot, language=N'us_english')  
  
  declare @i int = 1000000  
  while @i > 0  
  begin  
    insert dbo.t1 values (@i, @i+1)  
    set @i -= 1  
  end  
  
end  
go  
exec dbo.native_sp  
go  
-- reset  
delete from dbo.t1  
go  
```  
  
 行をできる限り高速に挿入するために、native_sp の DLL は t1 の DLL およびインメモリ OLTP ストレージ エンジンと直接やり取りできます。  
  
 インメモリ OLTP コンパイラは、ストアド プロシージャの各クエリに有効な実行プランを作成するためにクエリ オプティマイザーを活用します。 テーブルのデータが変更された場合はネイティブ コンパイル ストアド プロシージャは自動的に再コンパイルされないことに注意してください。 インメモリ OLTP の統計とストアド プロシージャの管理の詳細については、「 [メモリ最適化テーブルの統計](memory-optimized-tables.md)」を参照してください。  
  
## <a name="security-considerations-for-native-compilation"></a>ネイティブ コンパイルにおけるセキュリティの注意点  
 テーブルおよびストアド プロシージャのネイティブ コンパイルでは、インメモリ OLTP コンパイラを使用します。 このコンパイラはファイルを生成し、そのファイルがディスクに書き込まれて、メモリに読み込まれます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、これらのファイルへのアクセスを制限するために、次のメカニズムを使用しています。  
  
### <a name="native-compiler"></a>ネイティブ コンパイラ  
 コンパイラの実行可能ファイルと、ネイティブ コンパイルに必要なバイナリおよびヘッダー ファイルは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの一部として MSSQL\Binn\Xtp フォルダー内にインストールされます。 そのため、C:\Program Files の下で、既定のインスタンスをインストールする場合、コンパイラ ファイルが C:\Program Files にインストールされます\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12. します。MSSQLSERVER\MSSQL\Binn\Xtp します。  
  
 コンパイラへのアクセスを制限するために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、バイナリ ファイルへのアクセスを制限するアクセス制御リスト (ACL) が使用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのバイナリは、変更や改ざんが起こらないよう ACL で保護されています。 ネイティブ コンパイラの ACL では、コンパイラの使用も制限されます。ネイティブ コンパイラ ファイルに対する読み取り権限と実行権限を持っているのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントとシステム管理者のみです。  
  
### <a name="files-generated-by-a-native-compilation"></a>ネイティブ コンパイルによって生成されるファイル  
 テーブルまたはストアド プロシージャのコンパイル時に生成されるファイルには、DLL のほか、.c、.obj、.xml、.pdb などの拡張子を持つ中間ファイルがあります。 生成されたファイルは、既定のデータ フォルダーのサブフォルダーに保存されます。 サブフォルダーは Xtp と呼ばれます。 既定のデータ フォルダーの既定のインスタンスをインストールするときに生成されたファイルが C:\Program files に配置されます\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12. します。MSSQLSERVER\MSSQL\DATA\Xtp します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は 3 とおりの方法で、生成した DLL に対する改ざんを回避します。  
  
-   テーブルまたはストアド プロシージャが DLL にコンパイルされると、この DLL は直ちにメモリに読み込まれ、sqlserver.exe プロセスにリンクされます。 プロセスにリンクされている間、その DLL は変更できません。  
  
-   データベースを再起動すると、データベースのメタデータに基づいて、すべてのテーブルとストアド プロシージャが再コンパイル (削除後、再作成) されます。 これにより、生成されたファイルに対して悪意のあるエージェントによって行われた変更があれば、すべて削除されます。  
  
-   生成されたファイルはユーザー データの一部と見なされ、ACL を介して、データベース ファイルと同じセキュリティ制限が適用されます。これらのファイルにアクセスできるのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントとシステム管理者のみです。  
  
 これらのファイルの管理には、ユーザー操作は不要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、必要に応じてファイルの作成および削除が行われます。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブル](memory-optimized-tables.md)   
 [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md)  
  
  
