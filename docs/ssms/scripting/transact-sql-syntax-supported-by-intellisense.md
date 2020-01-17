---
title: IntelliSense でサポートされている Transact-SQL 構文 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL IntelliSense
- IntelliSense [SQL Server], Transact-SQL syntax
ms.assetid: 194e8f4f-fd7e-4f32-a169-f23531128004
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63e8ba6c7770679ca487d945e4823f70425413ba
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68253256"
---
# <a name="transact-sql-syntax-supported-by-intellisense"></a>IntelliSense でサポートされている Transact-SQL 構文
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] の IntelliSense でサポートされる [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ステートメントと構文要素について説明します。  
  
## <a name="statements-supported-by-intellisense"></a>IntelliSense でサポートされるステートメント  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の IntelliSense では、特に一般的な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのみがサポートされます。 いくつかの一般的な[!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターの状態が原因で IntelliSense が動作しなくなる場合があります。 詳細については、「[IntelliSense のトラブルシューティング &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/troubleshooting-intellisense.md)」を参照してください。  
  
> [!NOTE]  
>  IntelliSense は、暗号化されたデータベース オブジェクト (たとえば暗号化されたストアド プロシージャまたはユーザー定義関数) に対しては利用できません。 拡張されたストアド プロシージャおよび CLR 統合のユーザー定義型のパラメーターに対しては、パラメーターのヘルプおよびクイック ヒントを利用できません。  
  
### <a name="select-statement"></a>SELECT ステートメント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターでは、IntelliSense によって、SELECT ステートメント内の次の構文要素がサポートされます。  
  
|||  
|-|-|  
|SELECT|WHERE|  
|FROM|ORDER BY|  
|HAVING|UNION|  
|FOR|GROUP BY|  
|TOP|OPTION (hint)|  
  
### <a name="additional-transact-sql-statements-that-are-supported"></a>サポートされているその他の Transact-SQL ステートメント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターでは、IntelliSense によって、次の表に示す [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントもサポートされています。  
  
|Transact-SQL ステートメント|サポートされている構文|例外|  
|-----------------------------|----------------------|----------------|  
|[INSERT](../../t-sql/statements/insert-transact-sql.md)|*execute_statement* 句を除くすべての構文。|なし|  
|[UPDATE](../../t-sql/queries/update-transact-sql.md)|すべての構文。|なし|  
|[DELETE](../../t-sql/statements/delete-transact-sql.md)|すべての構文。|なし|  
|[DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)|すべての構文。|なし|  
|[SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)|すべての構文。|なし|  
|[EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)|ユーザー定義ストアド プロシージャ、システム ストアド プロシージャ、ユーザー定義関数、およびシステム関数の実行。|なし|  
|[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)|すべての構文。|なし|  
|[CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)|すべての構文。|なし|  
|[CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)|すべての構文。|IntelliSense では EXTERNAL NAME 句をサポートしていません。<br /><br /> AS 句では、このトピックに記載されているステートメントと構文のみが IntelliSense によってサポートされます。|  
|[ALTER PROCEDURE](../../t-sql/statements/alter-procedure-transact-sql.md)|すべての構文。|IntelliSense では EXTERNAL NAME 句をサポートしていません。<br /><br /> AS 句では、このトピックに記載されているステートメントと構文のみが IntelliSense によってサポートされます。|  
|[USE](../../t-sql/language-elements/use-transact-sql.md)|すべての構文。|なし|  
  
## <a name="intellisense-in-supported-statements"></a>サポートされているステートメントでの IntelliSense  
 次の構文要素は、サポートされている [!INCLUDE[ssDE](../../includes/ssde-md.md)] ステートメントのいずれかで使用されている場合、 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ エディターの IntelliSense によってサポートされます。  
  
-   すべての結合の種類 (APPLY など)。  
  
-   PIVOT および UNPIVOT。  
  
-   次のデータベース オブジェクトへの参照。  
  
    -   データベースおよびスキーマ  
  
    -   テーブル、ビュー、テーブル値関数、およびテーブル式  
  
    -   [列]  
  
    -   プロシージャおよびプロシージャ パラメーター  
  
    -   スカラー関数およびスカラー式  
  
    -   ローカル変数  
  
    -   共通テーブル式 (CTE)  
  
-   スクリプトまたはバッチ内の CREATE ステートメントまたは ALTER ステートメントのみで参照されるデータベース オブジェクト。ただし、スクリプトまたはバッチがまだ実行されていないためデータベースには存在しません。 これらのオブジェクトを次に示します。  
  
    -   スクリプトまたはバッチ内の CREATE TABLE ステートメントまたは CREATE PROCEDURE ステートメントで指定されているテーブルおよびプロシージャ。  
  
    -   スクリプトまたはバッチ内の ALTER TABLE ステートメントまたは ALTER PROCEDURE ステートメントで指定されているテーブルおよびプロシージャに対する変更。  
  
    > [!NOTE]  
    >  IntelliSense は、CREATE VIEW ステートメントが実行されるまでは CREATE VIEW ステートメントの列に対して利用できません。  
  
 前に示した要素が他の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント内で使用されている場合、IntelliSense は提供されません。 たとえば、SELECT ステートメント内で使用されている列名に対しては IntelliSense のサポートがありますが、CREATE FUNCTION ステートメント内で使用されている列に対してはサポートがありません。  
  
## <a name="examples"></a>使用例  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] のスクリプトまたはバッチ内では、このトピックに記載されているステートメントと構文のみが [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターの IntelliSense によってサポートされています。 IntelliSense でサポートされるステートメントと構文要素を次の [!INCLUDE[tsql](../../includes/tsql-md.md)] のコード例に示します。 たとえば、次のバッチにおいて、 `SELECT` ステートメントが単独で記述されているときは IntelliSense を利用できますが、 `SELECT` が `CREATE FUNCTION` ステートメントに含まれているときは IntelliSense を利用できません。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE Name LIKE N'Road-250%' and Color = N'Red';  
GO  
CREATE FUNCTION Production.ufn_Red250 ()  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT Name  
    FROM AdventureWorks2012.Production.Product  
    WHERE Name LIKE N'Road-250%'  
      AND Color = N'Red'  
);GO  
```  
  
 この機能は、CREATE PROCEDURE ステートメントまたは ALTER PROCEDURE ステートメントの AS 句に含まれる [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのセットにも適用されます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] のスクリプトまたはバッチ内では、IntelliSense によって、CREATE ステートメントまたは ALTER ステートメントに指定されているオブジェクトがサポートされます。ただし、これらのオブジェクトは、ステートメントが実行されていないためデータベースに存在しません。 たとえば、クエリ エディターで次のコードを入力します。  
  
```  
USE MyTestDB;  
GO  
CREATE TABLE MyTable  
    (PrimaryKeyCol   INT PRIMARY KEY,  
    FirstNameCol      NVARCHAR(50),  
   LastNameCol       NVARCHAR(50));  
GO  
SELECT   
```  
  
 スクリプトが実行されていないため `SELECT`が **に存在しない場合でも、** を入力すると、IntelliSense により、使用可能な要素として **PrimaryKeyCol**、 **FirstNameCol** 、および `MyTable` LastNameCol `MyTestDB`が選択リストに表示されます。  
  
  
