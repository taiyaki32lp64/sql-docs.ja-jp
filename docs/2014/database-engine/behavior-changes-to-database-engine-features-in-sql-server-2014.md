---
title: SQL Server 2014 | のデータベースエンジン機能の動作の変更Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- behavior changes [SQL Server]
- Database Engine [SQL Server], what's new
- Transact-SQL behavior changes
ms.assetid: 65eaafa1-9e06-4264-b547-cbee8013c995
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfaaea1b07c17fbf5c47bbcccf20a3ca55862123
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278205"
---
# <a name="behavior-changes-to-database-engine-features-in-sql-server-2014"></a>SQL Server 2014 におけるデータベース エンジン機能の動作の変更
  このトピックでは、[!INCLUDE[ssDE](../includes/ssde-md.md)]の動作変更について説明します。 動作変更によって、 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] の機能や操作方法が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の以前のバージョンと異なっています。  
  
## <a name="SQL14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] での動作の変更  
 以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、特定の長さ (4020 文字) を超える文字列を含む XML ドキュメントに対してクエリを実行すると、返される結果が正しくない場合があります。 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] では、このようなクエリから正しい結果が返されます。  
  
## <a name="Denali"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] での動作の変更  
  
### <a name="metadata-discovery"></a>メタデータの検出  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 以降の [!INCLUDE[ssDE](../includes/ssde-md.md)] の機能強化により、SQLDescribeCol は以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の SQLDescribeCol から返されたものよりも正確な結果を取得できます。 詳細については、「[メタデータの検出](../relational-databases/native-client/features/metadata-discovery.md)」を参照してください。  
  
 実際にクエリを実行せずに応答の形式を決定するための[SET FMTONLY](/sql/t-sql/statements/set-fmtonly-transact-sql)オプション[は&#40;sp_describe_first_result_set transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql)、 [sp_describe_undeclared_parameters &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql)、 [sys. dm_exec_describe_first_result_set &#40;&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql)transact-sql、および[sys. dm_exec_describe_first_result_set_for_object &#40;transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql)に置き換えられます。  
  
### <a name="changes-to-behavior-in-scripting-a-sql-server-agent-task"></a>SQL Server エージェント タスクのスクリプト作成における動作の変更  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] では、既存のジョブからスクリプトをコピーして新しいジョブを作成した場合、新しいジョブが既存のジョブに悪影響を与える可能性があります。 既存のジョブのスクリプトを使用して新しいジョブを作成するには、パラメーター *schedule_uid\@* を手動で削除します。これは通常、既存のジョブでジョブスケジュールを作成するセクションの最後のパラメーターです。 これにより、既存のジョブに影響することなく、新しいジョブ用に別に新しいスケジュールが作成されます。  
  
### <a name="constant-folding-for-clr-user-defined-functions-and-methods"></a>CLR ユーザー定義関数およびメソッドの定数たたみ込み  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] では、次のユーザー定義 CLR オブジェクトがたたみ込み可能になりました。  
  
-   決定的スカラー値 CLR ユーザー定義関数  
  
-   CLR ユーザー定義型の決定的メソッド  
  
 この機能強化は、これらの関数またはメソッドが同じ引数で複数回呼び出されたときのパフォーマンスの向上を目的としています。 ただし、この変更により、非決定的関数またはメソッドが誤って決定的とマークされている場合に予期しない結果が生じる可能性があります。 CLR 関数またはメソッドが決定的であるかどうかは、`IsDeterministic` または `SqlFunctionAttribute` の `SqlMethodAttribute` プロパティの値によって示されます。  
  
### <a name="behavior-of-stenvelope-method-has-changed-with-empty-spatial-types"></a>空の空間型を指定された STEnvelope() メソッドの動作の変更  
 空のオブジェクトを指定された `STEnvelope` メソッドの動作が、他の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 空間メソッドの動作と一致するようになりました。  
  
 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] では、空のオブジェクトを指定して `STEnvelope` メソッドを呼び出すと次の結果が返されました。  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns POINT EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns LINESTRING EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns POLYGON EMPTY  
```  
  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] では、空のオブジェクトを指定して `STEnvelope` メソッドを呼び出すと次の結果が返されます。  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
```  
  
 空間オブジェクトが空かどうかを判断するには、 [STIsEmpty &#40;geometry&#41;データ型](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type)メソッドを呼び出します。  
  
### <a name="log-function-has-new-optional-parameter"></a>LOG 関数の省略可能なパラメーターの追加  
 `LOG` 関数に、オプションの*基本*パラメーターが追加されました。 詳細については、「 [transact-sql &#40;&#41;をログに記録](/sql/t-sql/functions/log-transact-sql)する」を参照してください。  
  
### <a name="statistics-computation-during-partitioned-index-operations-has-changed"></a>パーティション インデックス操作中の統計計算の変更  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]では、パーティションインデックスが作成または再構築されるときに、テーブル内のすべての行をスキャンして統計を作成することはできません。 代わりに、クエリ オプティマイザーが既定のサンプリング アルゴリズムを使用して統計を生成します。 パーティション インデックスでデータベースをアップグレードした後で、これらのインデックスのヒストグラム データに違いが見つかる場合があります。 この動作の変更はクエリ パフォーマンスに影響しない可能性があります。 テーブル内のすべての行をスキャンしてパーティション インデックスの統計を作成するには、FULLSCAN 句で CREATE STATISTICS または UPDATE STATISTICS を使用します。  
  
### <a name="data-type-conversion-by-the-xml-value-method-has-changed"></a>XML value メソッドによるデータ型変換の変更  
 `value` データ型の `xml` メソッドの内部動作が変更になりました。 このメソッドは、XML に対して XQuery を実行し、指定された [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ型のスカラー値を返します。 xs 型は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ型に変換する必要があります。 以前は、`value` メソッドが元の値を内部で xs:string に変換した後、その xs:string を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ型に変換していました。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] では、次の場合に xs:string への変換がスキップされます。  
  
|元の XS データ型|変換後の SQL Server データ型|  
|-------------------------|--------------------------------------|  
|byte<br /><br /> short<br /><br /> Int<br /><br /> 整数 (integer)<br /><br /> long<br /><br /> unsignedByte<br /><br /> unsignedShort<br /><br /> unsignedInt<br /><br /> unsignedLong<br /><br /> positiveInteger<br /><br /> nonPositiveInteger<br /><br /> negativeInteger<br /><br /> nonNegativeInteger|tinyint<br /><br /> SMALLINT<br /><br /> Int<br /><br /> bigint<br /><br /> DECIMAL<br /><br /> numeric|  
|DECIMAL|DECIMAL<br /><br /> numeric|  
|float|REAL|  
|double|float|  
  
 この新しい動作により、中間の変換をスキップできるときのパフォーマンスが向上します。 ただし、データ型変換が失敗した場合は、中間の xs:string 値からの変換で発生していたエラー メッセージとは異なるエラー メッセージが表示されます。 たとえば、value メソッドが `int` 値 100000 から `smallint` への変換に失敗した場合、以前は次のようなエラー メッセージが表示されました。  
  
 `The conversion of the nvarchar value '100000' overflowed an INT2 column. Use a larger integer column.`  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] では、xs:string への中間の変換が行われず、次のようなエラー メッセージが表示されます。  
  
 `Arithmetic overflow error converting expression to data type smallint.`  
  
### <a name="sqlcmdexe-behavior-change-in-xml-mode"></a>XML モードでの sqlcmd.exe の動作変更  
 SELECT * from T FOR XML... を実行するときに、XML モード (: XML ON コマンド) で sqlcmd を使用すると、動作が変更されます。  
  
### <a name="dbcc-checkident-revised-message"></a>DBCC CHECKIDENT のメッセージの変更  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]では、DBCC CHECKIDENT コマンドによって返されるメッセージは、再シード*new_reseed_value*と共に使用して現在の id 値を変更した場合にのみ変更されました。 新しいメッセージは、"id 情報を確認しています: 現在の id 値 '\<現在の id 値 > ' です。 DBCC の実行が完了しました。 DBCC がエラー メッセージを出力した場合は、システム管理者に相談してください。"  
  
 以前のバージョンでは、メッセージは "id 情報を確認しています: 現在の id 値 '\<現在の id 値 > '、現在の列の値 '\<現在の列の値 > ' です。 DBCC の実行が完了しました。 DBCC がエラー メッセージを出力した場合は、システム管理者に相談してください。" このメッセージは、DBCC CHECKIDENT で NORESEED が指定されている場合、2 番目のパラメーターが指定されていない場合、または reseed 値が指定されていない場合に関しては変更されていません。 詳細については、「[DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql)」をご覧ください。  
  
### <a name="behavior-of-exist-function-on-xml-datatype-has-changed"></a>XML データ型に対する exist() 関数の動作の変更  
 **Exist ()** 関数の動作は、null 値を持つ XML データ型を 0 (ゼロ) と比較するときに変更されます。 次の例を参照してください。  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 0;  
```  
  
 以前のバージョンでは、この比較で 1 (true) が返されましたが、0 (ゼロ、false) が返されるようになりました。  
  
 以下の比較では変更されていません。  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 1; -- 0 expected, 0 returned  
SELECT COUNT(1) WHERE @test.exist('/dogs') IS NULL; -- 1 expected, 1 returned  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 でのデータベースエンジン機能の重大な変更](breaking-changes-to-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014  の非推奨のデータベースエンジン機能](deprecated-database-engine-features-in-sql-server-2016.md)  
 [SQL Server 2014 で廃止](discontinued-database-engine-functionality-in-sql-server-2016.md)されたデータベースエンジン機能   
 [ALTER DATABASE 互換性レベル &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
