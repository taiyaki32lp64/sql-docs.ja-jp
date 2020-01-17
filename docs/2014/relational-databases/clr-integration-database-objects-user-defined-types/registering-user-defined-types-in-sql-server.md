---
title: SQL Server でのユーザー定義型の登録 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [CLR integration], maintaining
- user-defined types [CLR integration], maintaining
- dependencies [CLR integration]
- deploying user-defined types [CLR integration]
- CurrencyConversion function
- user-defined types [CLR integration], deploying
- Transact-SQL deploying UDTs
- assemblies [CLR integration], user-defined types
- cross-database UDT support
- CREATE ASSEMBLY statement
- DROP TYPE statement
- Currency UDT
- CREATE TYPE statement
- registering user-defined types
- UDTs [CLR integration], deploying
- removing user-defined types
- user-defined types [CLR integration], registering
- ALTER ASSEMBLY statement
- UDTs [CLR integration], registering
- ADD FILE clause
ms.assetid: f7da3e92-e407-4f0b-b3a3-f214e442b37d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 19ea6e9f077b5097b8c5daa6d967a17336553ba7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919947"
---
# <a name="registering-user-defined-types-in-sql-server"></a>SQL Server でのユーザー定義型の登録
  ユーザー定義型 (UDT) を使用するには[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、登録する必要があります。 UDT を登録するには、UDT を使用するデータベースにアセンブリを登録し、型を作成する必要があります。 UDT は、1 つのデータベースにスコープが設定されるので、同一のアセンブリと UDT を各データベースに登録しない限り、複数のデータベースでは使用できません。 UDT アセンブリを登録し、型を作成すると、[!INCLUDE[tsql](../../includes/tsql-md.md)] やクライアント コードでその UDT を使用できます。 詳細については、「 [CLR ユーザー定義型](clr-user-defined-types.md)」を参照してください。  
  
## <a name="using-visual-studio-to-deploy-udts"></a>Visual Studio を使用した UDT の配置  
 UDT を配置する最も簡単な方法は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio を使用することです。 ただし、より複雑な配置シナリオで最も優れた柔軟性を得るためには、このトピックで説明するように [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用します。  
  
 Visual Studio を使用して UDT を作成および配置するには、次の手順を実行します。  
  
1.  新規作成**データベース**プロジェクト、 **Visual Basic**または**Visual c#** 言語ノード。  
  
2.  UDT を格納する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの参照を追加します。  
  
3.  追加、**ユーザー定義型**クラス。  
  
4.  コードを記述して UDT を実装します。  
  
5.  **ビルド**メニューの **デプロイ**します。 この結果、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにアセンブリが登録され、型が作成されます。  
  
## <a name="using-transact-sql-to-deploy-udts"></a>Transact-SQL を使用した UDT の配置  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 構文は、UDT を使用するデータベースにアセンブリを登録する場合に使用します。 アセンブリは、ファイル システムに外部的に格納されるのではなく、データベース システム テーブルに内部的に格納されます。 UDT が外部アセンブリに依存する場合は、それらのアセンブリもデータベースに読み込む必要があります。 CREATE TYPE ステートメントは、UDT を使用するデータベースに UDT を作成する場合に使用します。 詳細については、[CREATE ASSEMBLY & #40 を参照してください。TRANSACT-SQL と #41 です。](/sql/t-sql/statements/create-assembly-transact-sql)と[型 & #40; を作成します。TRANSACT-SQL と #41 です](/sql/t-sql/statements/create-type-transact-sql)。  
  
### <a name="using-create-assembly"></a>CREATE ASSEMBLY の使用  
 CREATE ASSEMBLY 構文では、UDT を使用するデータベースにアセンブリが登録されます。 アセンブリを登録すると、そのアセンブリに依存関係がなくなります。  
  
 指定された 1 つのデータベースに複数のバージョンの同じアセンブリを作成することはできません。 ただし、特定の 1 つのデータベースに、カルチャに基づいて、複数のバージョンの同じアセンブリを作成することはできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに登録されているとおりに、異なる名前で、アセンブリの複数のカルチャ バージョンが区別されます。 詳細については、.NET Framework SDK の「厳密な名前付きアセンブリの作成と使用」を参照してください。  
  
 SAFE 権限セットまたは EXTERNAL_ACCESS 権限セットを指定して CREATE ASSEMBLY を実行すると、アセンブリが検証可能でタイプ セーフであることを確認するためのチェックが行われます。 権限セットを指定しないと、SAFE が指定されていると想定されます。 UNSAFE 権限セットを指定したコードはチェックされません。 アセンブリの権限セットの詳細については、「[アセンブリのデザイン](../../relational-databases/clr-integration/assemblies-designing.md)」をご覧ください。  
  
#### <a name="example"></a>例  
 次[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントに Point アセンブリを登録します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で、 **AdventureWorks** SAFE 権限セットを持つデータベース。 WITH PERMISSION_SET 句を省略すると、SAFE 権限セットでアセンブリが登録されます。  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 次[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントを使用してアセンブリを登録します *< assembly_bits >* FROM 句の引数。 この `varbinary` 値は、ファイルをバイト ストリームで表しています。  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 ... 21ac78  
```  
  
### <a name="using-create-type"></a>CREATE TYPE の使用  
 アセンブリをデータベースに読み込むと、[!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE ステートメントを使用して型を作成できます。 型を作成すると、そのデータベースで使用できる型のリストに、作成した型が追加されます。 型にはデータベース スコープがあり、型はその型を作成したデータベースでしか使用できません。 データベース内に UDT が既に存在する場合は、CREATE TYPE ステートメントがエラーで失敗します。  
  
> [!NOTE]  
>  CREATE TYPE 構文は、ネイティブな [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 別名データ型を作成する場合にも使用され、別名データ型を作成する手段として `sp_addtype` に置き換わるものです。 CREATE TYPE 構文の省略可能な一部の引数は CLR の UDT の作成に関係しており、(基本型などの) 別名データ型の作成には適用されません。  
  
 詳細については、[の種類の作成 & #40 を参照してください。TRANSACT-SQL と #41 です](/sql/t-sql/statements/create-type-transact-sql)。  
  
#### <a name="example"></a>例  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、`Point` 型を作成します。 2 つの部分の名前付け構文を使用して外部名が指定された*AssemblyName*.*UDTName*します。  
  
```  
CREATE TYPE dbo.Point   
EXTERNAL NAME Point.[Point];  
```  
  
## <a name="removing-a-udt-from-the-database"></a>データベースからの UDT の削除  
 DROP TYPE ステートメントを使用すると、現在のデータベースから UDT が削除されます。 UDT を削除すると、DROP ASSEMBLY ステートメントを使用してデータベースからアセンブリを削除できます。  
  
 DROP TYPE ステートメントは、次の状況では実行されません。  
  
-   UDT を使用して定義した列を含むデータベース内のテーブル。  
  
-   WITH SCHEMABINDING 句を使用してデータベースに作成した UDT の変数またはパラメーターを使用する関数、ストアド プロシージャ、またはトリガー。  
  
### <a name="example"></a>例  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] は、この順序どおりに実行する必要があります。 最初に `Point` UDT を参照するテーブルを削除し、次に型を削除して、最後にアセンブリを削除する必要があります。  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>UDT 依存関係の検出  
 UDT の列定義を含むテーブルなどの依存オブジェクトがある場合、DROP TYPE ステートメントは失敗します。 また、WITH SCHEMABINDING 句を使用してデータベースに作成した関数、ストアド プロシージャ、またはトリガーがあり、これらのルーチンでユーザー定義型の変数やパラメーターが使用される場合にも失敗します。 最初にすべての依存オブジェクトを削除してから、DROP TYPE ステートメントを実行する必要があります。  
  
 次[!INCLUDE[tsql](../../includes/tsql-md.md)]クエリは、すべての列とで UDT を使用するパラメーターを検索、 **AdventureWorks**データベース。  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;  
```  
  
## <a name="maintaining-udts"></a>UDT の管理  
 UDT を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに作成した後は、型の基になるアセンブリを変更することはできますが、UDT は変更できません。 ほとんどの場合、[!INCLUDE[tsql](../../includes/tsql-md.md)] DROP TYPE ステートメントを使用してデータベースから UDT を削除し、基になるアセンブリに変更を加えて、ALTER ASSEMBLY ステートメントを使用してアセンブリを再読み込みする必要があります。 その後、UDT とすべての依存オブジェクトを再作成する必要があります。  
  
### <a name="example"></a>例  
 ALTER ASSEMBLY ステートメントは、UDT アセンブリのソース コードに変更を加え、ソース コードを再コンパイルした後に使用します。 ALTER ASSEMBLY ステートメントを使用すると、サーバーに .dll ファイルがコピーされ、新しいアセンブリに再バインドされます。 完全な構文を参照してください。 [ALTER ASSEMBLY & #40 です。TRANSACT-SQL と #41 です](/sql/t-sql/statements/alter-assembly-transact-sql)。  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY ステートメントでは、ディスク上の指定された場所から Point.dll アセンブリを再読み込みしています。  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>ALTER ASSEMBLY を使用したソース コードの追加  
 ALTER ASSEMBLY 構文の ADD FILE 句は、CREATE ASSEMBLY 構文には存在しません。 ADD FILE 句を使用すると、アセンブリに関連付けられるソース コードやその他のファイルを追加できます。 ファイルは元の場所からコピーされ、データベース内のシステム テーブルに格納されます。 これにより、現在のバージョンの UDT を再作成またはドキュメント化する必要があれば、ソース コードや他のファイルをいつでも使用できます。  
  
 次[!INCLUDE[tsql](../../includes/tsql-md.md)]の Point.cs クラスのソース コードを追加する ALTER ASSEMBLY ステートメント、 `Point` UDT します。 Point.cs ファイルに含まれているテキストがコピーされ、"PointSource" という名前でデータベースに格納されます。  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 アセンブリ情報が格納されている、 **sys.assembly_files**アセンブリがインストールされているデータベースのテーブル。 **Sys.assembly_files**テーブルには、次の列が含まれています。  
  
 **assembly_id**  
 アセンブリに定義される ID。 この番号は、同じアセンブリに関連するすべてのオブジェクトに割り当てられます。  
  
 **name**  
 オブジェクトの名前。  
  
 **file_id**  
 最初のオブジェクトに関連付けられている各オブジェクトを識別する番号を指定した**assembly_id** 1 の値が指定されています。 かどうかは、複数のオブジェクトに関連付けられた同じ**assembly_id**以降の各し、 **file_id**値が 1 ずつインクリメントされます。  
  
 **content**  
 アセンブリまたはファイルの 16 進数表記。  
  
 内容を変換する、CAST または CONVERT 関数を使用することができます、**コンテンツ**判読できるテキストの列。 次のクエリでは、結果セットを 1 行に制限するために WHERE 句で name を使用して、Point.cs ファイルの内容を読み取り可能なテキストに変換しています。  
  
```  
SELECT CAST(content AS varchar(8000))   
  FROM sys.assembly_files   
  WHERE name='PointSource';  
```  
  
 結果をテキスト エディターにコピーして貼り付けると、元のファイルに含まれていた改行とスペースが保持されていることがわかります。  
  
## <a name="managing-udts-and-assemblies"></a>UDT とアセンブリの管理  
 UDT の実装を計画するときは、どのメソッドが UDT アセンブリ自体に必要であり、どのメソッドを独立したアセンブリに作成してユーザー定義関数やストアド プロシージャとして実装する必要があるかを検討します。 メソッドを個別のアセンブリに分離すると、テーブルの UDT 列に格納されるデータに影響を与えずに、コードを更新できます。 新しい定義で UDT 列の以前の値を読み取ることができ、型の署名が変更されない場合にのみ、UDT 列や他の依存オブジェクトを削除しないで UDT アセンブリを変更できます。  
  
 UDT の実装に必要なコードから、変更される可能性がある手続き型コードを分離すると、メンテナンスが大幅に簡素化されます。 UDT が機能するのに必要なコードのみを含め、UDT の定義をできる限り単純にしておくと、コード リビジョンやバグ修正のために UDT 自体をデータベースから削除する必要が生じるリスクが軽減されます。  
  
### <a name="the-currency-udt-and-currency-conversion-function"></a>Currency UDT と通貨換算関数  
 **通貨**で UDT、 **AdventureWorks**サンプル データベースを UDT とその関連機能を構築することをお勧めの方法の便利な例を提供します。 **通貨**UDT は、特定のカルチャの通貨システムに基づいて金額を処理に使用され、ドルやユーロなど、さまざまな通貨型のストレージでは、します。 UDT クラスでは、カルチャ名を文字列として、金額を `decimal` データ型として公開します。 必要なシリアル化メソッドは、クラスを定義するアセンブリ内にすべて含まれます。 1 つのカルチャから別の通貨換算を実装する関数という外部関数として実装されます**ConvertCurrency**、この関数は、別のアセンブリにあるとします。 **ConvertCurrency**関数内のテーブルから換算率を取得するでは、 **AdventureWorks**データベース。 コンバージョン率のソースを変更する必要があります、または影響を与えずに、アセンブリを簡単に変更、既存のコードに何らかの変更は場合、**通貨**UDT します。  
  
 コード リストは、**通貨**UDT と**ConvertCurrency**共通言語ランタイム (CLR) サンプルをインストールすることによって機能があります。  
  
### <a name="using-udts-across-databases"></a>複数のデータベース間での UDT の使用  
 定義上、UDT のスコープは 1 つのデータベースに設定されています。 このため、あるデータベースで定義されている UDT を別のデータベースの列定義に使用することはできません。 UDT を複数のデータベースで使用するには、各データベースで同一のアセンブリに対して CREATE ASSEMBLY ステートメントと CREATE TYPE ステートメントを実行する必要があります。 アセンブリの名前、厳密な名前、カルチャ、バージョン、権限セット、およびバイナリの内容が同じ場合、それらのアセンブリは同一であると見なされます。  
  
 両方のデータベースに UDT を登録し、UDT にアクセスできるようになると、あるデータベースの UDT 値を別のデータベースで使用するために変換できます。 次のシナリオでは、同一の UDT を複数のデータベース間で使用できます。  
  
-   異なるデータベースで定義されているストアド プロシージャの呼び出し。  
  
-   異なるデータベースで定義されているテーブルのクエリ。  
  
-   あるデータベース テーブルの UDT 列から UDT データを選択し、その UDT データを同一の UDT 列を使用して 2 つ目のデータベースに挿入する場合。  
  
 このような状況では、必要なすべての変換がサーバーで自動的に行われます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 関数または CONVERT 関数を使用して、明示的に変換を実行することはできません。  
  
 Udt を使用するための操作を行う必要がないことに注意するくださいと[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]作業テーブルを作成、 **tempdb**システム データベースです。 テーブル変数、カーソルの場合の処理が含まれます、ユーザー定義テーブル値関数を含む Udt を透過的を使用するを使用して、 **tempdb**します。 ただしで一時テーブルを明示的に作成する場合**tempdb** 、UDT 列を定義する、UDT を登録する必要があります**tempdb**ユーザー データベースと同じ方法です。  
  
## <a name="see-also"></a>参照  
 [CLR ユーザー定義型](clr-user-defined-types.md)  
  
  
