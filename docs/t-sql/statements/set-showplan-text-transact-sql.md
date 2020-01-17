---
title: SET SHOWPLAN_TEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SHOWPLAN_TEXT
- SET_SHOWPLAN_TEXT_TSQL
- SET SHOWPLAN_TEXT
- SHOWPLAN_TEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- SET SHOWPLAN_TEXT statement
- canceling statement execution
- SHOWPLAN_TEXT option
- stopping statement execution
- estimated execution information [SQL Server]
ms.assetid: 2c4f3fc8-ff2c-4790-8b74-e7e8ef58f9a6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7dc31f0a7fde3e4ff73dbf6d1a927275a68f65d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941662"
---
# <a name="set-showplantext-transact-sql"></a>SET SHOWPLAN_TEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行せず、 代わりに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はステートメントの実行方法に関する詳細情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET SHOWPLAN_TEXT { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 SET SHOWPLAN_TEXT の設定は、解析時ではなく実行時に設定されます。  
  
 SET SHOWPLAN_TEXT が ON の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが実行されずに、各ステートメントの実行に関する情報が返されます。 返される情報は、このオプションが ON に設定されてから OFF に設定されるまでに発行されたすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントに関する実行プラン情報です。 たとえば、SET SHOWPLAN_TEXT が ON のときに CREATE TABLE ステートメントが実行され、その後この同じテーブルを参照する SELECT ステートメントが発行されると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では指定したテーブルが存在しないというエラー メッセージが返されます。 その後、このテーブルに対して行われる参照は失敗します。 SET SHOWPLAN_TEXT が OFF の場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は実行プラン情報に関するレポートを生成しないでステートメントを実行します。  
  
 SET SHOWPLAN_TEXT の目的は、**sqlcmd** ユーティリティなどの Microsoft Win32 コマンド プロンプト アプリケーションが読み取れる形式の出力を返すことです。 SET SHOWPLAN_ALL を使用するとさらに詳細な出力が返され、その出力を取り扱うように設計されたプログラムで使用できます。  
  
 SET SHOWPLAN_TEXT と SET SHOWPLAN_ALL は、ストアド プロシージャ内に指定できません。 またバッチ内で同時に他のステートメントを実行することもできません。  
  
 SET SHOWPLAN_TEXT では情報が行セットとして返されます。これは階層構造になっており、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ プロセッサで各ステートメントが実行されるときのステップを表しています。 出力結果には、ステートメントごとに、ステートメントのテキストを示す 1 行と、実行ステップの詳細を示す複数行が含まれます。 次の表に、出力に含まれる列を示します。  
  
|列名|[説明]|  
|-----------------|-----------------|  
|**StmtText**|PLAN_ROW 型でない行の場合、この列には [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのテキストが含まれます。 PLAN_ROW 型の行の場合、この列には操作の説明が含まれます。 またこの列には物理操作と、必要に応じて論理操作が含まれます。 場合によっては、この列の後に説明が含まれます。説明が後に続くかどうかは、物理操作によって決まります。 物理操作の詳細については、「[SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)」の「**Argument**」列を参照してください。|  
  
 プラン表示の出力に含まれる物理操作と論理操作の詳細については、「[プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 SET SHOWPLAN_TEXT を使用するには、SET SHOWPLAN_TEXT の実行ステートメントを実行するための適切な権限が与えられている必要があります。また、参照されるオブジェクトを含むすべてのデータベースに対して、SHOWPLAN 権限が必要です。  
  
 SELECT、INSERT、UPDATE、DELETE、EXEC "*ストアド プロシージャ*"、EXEC "*ユーザー定義関数*" の各ステートメントの場合、プラン表示を作成するには、ユーザーに次の権限が必要です。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限。  
  
-   SHOWPLAN 権限。これは、Transact-SQL ステートメントで参照されるオブジェクト (テーブルやビューなど) を含むすべてのデータベースに対して必要です。  
  
 DDL、USE "*データベース名*"、SET、DECLARE、動的 SQL など、その他すべてのステートメントでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限だけが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でステートメントを処理するときのインデックスの使用方法を示します。  
  
 インデックスを使用するクエリは次のとおりです。  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 結果セットは次のようになります。  
  
```  
StmtText                                             
---------------------------------------------------  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;   
  
StmtText                                                                                                                                                                                        
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Seek(OBJECT:([AdventureWorks2012].[Production].[Product].[PK_Product_ProductID]), SEEK:([AdventureWorks2012].[Production].[Product].[ProductID]=CONVERT_IMPLICIT(int,[@1],0)) ORDERED FORWARD)   
```  
  
 インデックスを使用しないクエリは次のとおりです。  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 結果セットは次のようになります。  
  
```  
StmtText                                                                  
------------------------------------------------------------------------  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;   
  
StmtText                                                                                                                                                                                                  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Scan(OBJECT:([AdventureWorks2012].[Production].[ProductCostHistory].[PK_ProductCostHistory_ProductCostID]), WHERE:([AdventureWorks2012].[Production].[ProductCostHistory].[StandardCost]<[@1]))  
```  
  
## <a name="see-also"></a>参照  
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)  
  
  
