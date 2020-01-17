---
title: 包含データベースの照合順序 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- contained database, collations
ms.assetid: 4b44f6b9-2359-452f-8bb1-5520f2528483
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1850f5d85baf418e0ce872f641a920514156101f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137383"
---
# <a name="contained-database-collations"></a>包含データベースの照合順序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  大文字と小文字の区別、アクセント記号の区別、使用されるベース言語など、さまざまなプロパティがテキスト データの並べ替え順序と等値セマンティクスに影響します。 これらの性質の指定は、データの照合順序の選択を通じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に示されます。 照合順序の詳細については、「[照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
 照合順序は、ユーザー テーブルに格納されているデータだけでなく、メタデータ、一時オブジェクト、変数名など、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって処理されるすべてのテキストに適用されます。これらの処理は、包含データベースと非包含データベースとでは異なります。 この変更は、多くのユーザーには影響しませんが、インスタンスに対する独立性と統一性を提供する助けになります。 これも、包含データベースと非包含データベースの両方にアクセスするセッションの問題と同様に、いくつかの混乱を生じさせる場合があります。  
  
 このトピックでは、変更の内容を明確にし、変更が問題を引き起こす状況について詳しく説明します。  
  
## <a name="non-contained-databases"></a>非包含データベース  
 すべてのデータベースには既定の照合順序があり、データベースの作成時または変更時に設定できます。 この照合順序は、データベース内のすべての文字列型の列に対する既定値と同様に、データベース内のすべてのメタデータで使用されます。 ユーザーは、 **COLLATE** 句を使用して、特定の列に対して別の照合順序を選択できます。  
  
### <a name="example-1"></a>例 1  
 たとえば、北京で作業する場合は、中国語の照合順序を使用するでしょう。  
  
```sql  
ALTER DATABASE MyDB COLLATE Chinese_Simplified_Pinyin_100_CI_AS;  
```  
  
 その場合、列を作成すると、既定の照合順序は中国語の照合順序になりますが、必要であれば別の照合順序を選択できます。  
  
```sql  
CREATE TABLE MyTable  
      (mycolumn1 nvarchar,  
      mycolumn2 nvarchar COLLATE Frisian_100_CS_AS);  
GO  
SELECT name, collation_name  
FROM sys.columns  
WHERE name LIKE 'mycolumn%' ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```sql  
name            collation_name  
--------------- ----------------------------------  
mycolumn1       Chinese_Simplified_Pinyin_100_CI_AS  
mycolumn2       Frisian_100_CS_AS  
```  
  
 これは比較的簡単に見えますが、いくつかの問題が発生します。 列の照合順序はテーブルを作成したデータベースに依存するので、 **tempdb**に格納されている一時テーブルを使用する場合に問題が発生します。 **tempdb** の照合順序は、通常、インスタンスの照合順序と一致し、データベースの照合順序と一致するとは限りません。  
  
### <a name="example-2"></a>例 2  
 たとえば、上の中国語のデータベースが、 **Latin1_General** 照合順序のインスタンス上で使用されるとします。  
  
```sql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max)) ;  
GO  
```  
  
 一見したところでは、これらの 2 つのテーブルは同じスキーマを持っているように見えます。しかし、データベースの照合順序が異なるため、値は実際には互換性がありません。  
  
```  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 メッセージ 468、レベル 16、状態 9、行 2  
  
 等しい操作の "Latin1_General_100_CI_AS_KS_WS_SC" と "Chinese_Simplified_Pinyin_100_CI_AS" 間での照合順序の競合を解決できません。  
  
 この問題は、一時テーブルの照合順序を明示的に指定することで解決できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **COLLATE** 句に **DATABASE_DEFAULT** キーワードを提供することで、この処理を簡易にしています。  
  
```sql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max) COLLATE DATABASE_DEFAULT);  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 これで、エラーなしで実行できるようになりました。  
  
 変数に関しても、照合順序に依存する動作があります。 次のような関数があるとします。  
  
```  
CREATE FUNCTION f(@x INT) RETURNS INT  
AS BEGIN   
      DECLARE @I INT = 1  
      DECLARE @İ INT = 2  
      RETURN @x * @i  
END;  
```  
  
 これは少し変わった関数です。 大文字と小文字を区別する照合順序では、return 句の中の @i が @I にも @ İ にもバインドできません。 大文字と小文字を区別しない Latin1_General 照合順序では、@i が @I にバインドされ、関数は 1 を返します。 しかし、大文字と小文字を区別しない Turkish 照合順序では、@i が @İ にバインドされ、関数は 2 を返します。 このことは、照合順序が異なるインスタンス間で移動されるデータベースでは、大きな問題になります。  
  
## <a name="contained-databases"></a>包含データベース  
 包含データベースの設計目標は、データベースを自己完結させることなので、インスタンスと **tempdb** の照合順序への依存は解消する必要があります。 そのために、包含データベースにはカタログ照合順序の概念が導入されました。 カタログ照合順序は、システム メタデータと一時的なオブジェクトに使用されます。 詳細については、以下で説明します。  
  
 包含データベースでは、カタログ照合順序は **Latin1_General_100_CI_AS_WS_KS_SC**です。 この照合順序は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのインスタンスのすべての包含データベースで共通であり、変更できません。  
  
 データベースの照合順序は保持されますが、ユーザー データの既定の照合順序としてのみ使用されます。 既定では、データベースの照合順序は model データベースの照合順序と同じですが、ユーザーが **CREATE** または **ALTER DATABASE** コマンドを使用して、非包含データベースと同様に変更できます。  
  
 **COLLATE**句では、新しいキーワード **CATALOG_DEFAULT** を使用できます。 これは、包含データベースと非包含データベースの両方のメタデータにおける現在の照合順序へのショートカットとして使用されます。 つまり、非包含データベースでは、メタデータがデータベースの照合順序で照合されるので、 **CATALOG_DEFAULT** は現在のデータベースの照合順序を返します。 包含データベースでは、ユーザーがデータベースの照合順序をカタログ照合順序と一致しないように変更できるため、これらの 2 つの値は異なる場合があります。  
  
 以下の表は、非包含データベースと包含データベースのさまざまなオブジェクトの動作をまとめたものです。  
  
||||  
|-|-|-|  
|**アイテム**|**非包含データベース**|**包含データベース**|  
|ユーザー データ (既定値)|COLLATE|COLLATE|  
|一時データ (既定値)|TempDB の照合順序|COLLATE|  
|メタデータ|DATABASE_DEFAULT / CATALOG_DEFAULT|COLLATE|  
|一時的なメタデータ|TempDB の照合順序|COLLATE|  
|変数:|インスタンスの照合順序|COLLATE|  
|Goto ラベル|インスタンスの照合順序|COLLATE|  
|カーソル名|インスタンスの照合順序|COLLATE|  
  
 前に説明した一時テーブルの例でわかるように、この照合順序の動作によって、多くの一時テーブルでは明示的に **COLLATE** 句を使用する必要がなくなります。 包含データベースでは、データベースとインスタンスの照合順序が異なる場合でも、このコードはエラーにならずに実行されます。  
  
```sql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max));  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 このコードがうまく機能するのは、 `T1_txt` と `T2_txt` の両方が、包含データベースのデータベース照合順序で照合されるためです。  
  
## <a name="crossing-between-contained-and-uncontained-contexts"></a>包含コンテキストと非包含コンテキスト間の移動  
 包含データベース内のセッションが包含されたままである限り、そのセッションは接続されているデータベース内で維持されます。 この場合の動作は非常に単純です。 しかし、セッションが包含コンテキストと非包含コンテキスト間にまたがると、2 つの規則のセットに対応する必要があるので、動作はより複雑になります。 この問題は、部分的包含データベースで発生する場合があります。ユーザーが **USE** で別のデータベースを使用できるためです。 この場合、照合順序の規則の違いは、以下の原則に従って処理されます。  
  
-   バッチの照合順序の動作は、バッチを開始したデータベースによって決定されます。  
  
 この決定は、最初の **USE**も含めて、どのコマンドの実行よりも前に行われることに注意してください。 つまり、バッチが包含データベース内で開始されると、最初のコマンドが非包含データベースに対する **USE** であっても、バッチで使用されるのは包含の照合順序の動作のままです。 このため、たとえば変数への参照が、次のような複数の結果を持つ可能性があります。  
  
-   参照がただ 1 つの一致を見つけられる。 この場合、参照はエラーにならずに動作します。  
  
-   参照が現在の照合順序では一致を見つけられないが、前の照合順序では 1 つ見つかった。 この場合は、変数が作成されたことが明らかであっても、変数が存在しないというエラーが生成されます。  
  
-   参照が、本来は区別可能であった複数の一致を見つけられる。 この場合も、エラーが生成されます。  
  
 この問題を、いくつかの例で説明します。 これらの例では、 `MyCDB` という名前の部分的包含データベースがあり、そのデータベースの照合順序が既定の照合順序の **Latin1_General_100_CI_AS_WS_KS_SC**に設定されているものとします。 また、インスタンスの照合順序は **Latin1_General_100_CS_AS_WS_KS_SC**であるとします。 2 つの照合順序の違いは、大文字と小文字を区別するかどうかだけです。  
  
### <a name="example-1"></a>例 1  
 次の例は、参照がただ 1 つの一致を見つける場合を示しています。  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #a VALUES(1);  
GO  
  
USE master;  
GO  
  
SELECT * FROM #a;  
GO  
  
Results:  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
x  
-----------  
1  
```  
  
 この例では、識別された #a が、大文字と小文字を区別しないカタログ照合順序と、大文字と小文字を区別するインスタンス照合順序の両方でバインドされ、コードは正常に動作します。  
  
### <a name="example-2"></a>例 2  
 次の例は、参照が現在の照合順序では一致を見つけられず、前の照合順序では 1 つ見つけた場合を示しています。  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #A VALUES(1);  
GO  
```  
  
 ここでは、大文字と小文字を区別しない既定の照合順序で #A が #a にバインドされ、挿入を正常に実行できます。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
```  
  
 しかし、スクリプトを続行すると ...  
  
```  
USE master;  
GO  
  
SELECT * FROM #A;  
GO  
```  
  
 大文字と小文字を区別するインスタンスの照合順序で #A にバインドしようとして、エラーになります。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 メッセージ 208、レベル 16、状態 0、行 2  
  
 オブジェクト名 '#A' が無効です。  
  
### <a name="example-3"></a>例 3  
 次の例は、参照が本来は区別可能であった複数の一致を見つける場合を示しています。 まず、 **tempdb** 内 (インスタンスと同様に、大文字と小文字を区別する照合順序) から、以下のステートメントを実行します。  
  
```  
USE tempdb;  
GO  
  
CREATE TABLE #a(x int);  
GO  
CREATE TABLE #A(x int);  
GO  
INSERT INTO #a VALUES(1);  
GO  
INSERT INTO #A VALUES(2);  
GO  
```  
  
 この照合順序では、テーブルが区別可能であるため、問題なく動作します。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
(1 row(s) affected)  
```  
  
 しかし、包含データベース内に移動すると、これらのテーブルへのバインドができなくなります。  
  
```  
USE MyCDB;  
GO  
SELECT * FROM #a;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 メッセージ 12800、レベル 16、状態 1、行 2  
  
 一時テーブル名 '#a' への参照があいまいで、解決できません。 候補となるのは '#a' と '#A' です。  
  
## <a name="conclusion"></a>まとめ  
 包含データベースの照合順序の動作は、非包含データベースの場合と微妙に異なります。 この動作は、インスタンスに対する独立性と簡易性を提供し、一般的には有益です。 ただし、場合によっては、特にセッションが包含データベースと非包含データベースの両方にアクセスする場合には、問題が発生することもあります。  
  
## <a name="see-also"></a>参照  
 [包含データベース](../../relational-databases/databases/contained-databases.md)  
  
  
