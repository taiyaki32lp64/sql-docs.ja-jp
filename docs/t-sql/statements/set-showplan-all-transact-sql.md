---
title: SET SHOWPLAN_ALL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_ALL
- SET_SHOWPLAN_ALL_TSQL
- SHOWPLAN_ALL
- SHOWPLAN_ALL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- SET SHOWPLAN_ALL statement
- SHOWPLAN_ALL option
- canceling statement execution
- stopping statement execution
- estimated execution information [SQL Server]
ms.assetid: a500b682-bae4-470f-9e00-47de905b851b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 063c4c94fc457b6b9bb69fa0395398c62bf49516
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941693"
---
# <a name="set-showplan_all-transact-sql"></a>SET SHOWPLAN_ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行せず、 代わりに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、ステートメントのリソース要件の見積もりを示し、ステートメントの実行方法に関する詳細情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET SHOWPLAN_ALL { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 SET SHOWPLAN_ALL の設定は、解析時ではなく実行時に設定されます。  
  
 SET SHOWPLAN_ALL が ON の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では各ステートメントの実行情報だけが返され、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは実行されません。 返される情報は、このオプションが ON に設定されてから OFF に設定されるまでに実行されたすべての [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに関する情報です。 たとえば、SET SHOWPLAN_ALL が ON のときに CREATE TABLE ステートメントを実行し、その後この同じテーブルを参照する SELECT ステートメントを実行すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では指定したテーブルが存在しないというエラー メッセージが返されます。 その後、このテーブルに対して行われる参照は失敗します。 SET SHOWPLAN_ALL が OFF の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではレポートを作成せずに、ステートメントを実行します。  
  
 SET SHOWPLAN_ALL は、その出力を処理するように作成されたアプリケーションから使用されることを意図しています。 SET SHOWPLAN_TEXT は、**osql** ユーティリティなどの Microsoft Win32 コマンド プロンプト アプリケーションが読み取れる形式の出力を返す場合に使用します。  
  
 SET SHOWPLAN_TEXT および SET SHOWPLAN_ALL をストアド プロシージャ内で指定することはできません。これらはバッチ内の唯一のステートメントである必要があります。  
  
 SET SHOWPLAN_ALL では情報が行セットとして返されます。これは階層構造になっており、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ プロセッサで各ステートメントが実行されるときのステップを表しています。 出力結果には、ステートメントごとに、ステートメントのテキストを示す 1 行と、実行ステップの詳細を示す複数行が含まれます。 次の表に、出力結果に含まれる列を示します。  
  
|列名|[説明]|  
|-----------------|-----------------|  
|**StmtText**|PLAN_ROW 型でない行の場合、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのテキストが含まれます。 PLAN_ROW 型の行の場合、この列には操作の説明が含まれます。 またこの列には物理操作と、必要に応じて論理操作が含まれます。 この列の後に説明が続くこともありますが、その説明は物理操作によって決定されます。 詳細については、「[プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)」を参照してください。|  
|**StmtId**|現在のバッチに含まれるステートメント数。|  
|**NodeId**|現在のクエリに含まれるノードの ID。|  
|**Parent**|親ステップのノード ID。|  
|**PhysicalOp**|ノードの物理実装アルゴリズム。 型 PLAN_ROWS の行のみ。|  
|**LogicalOp**|ノードが表す関係代数操作。 型 PLAN_ROWS の行のみ。|  
|**Argument**|実行されている操作に関する補足情報を指定します。 この列の内容は、物理操作に応じて異なります。|  
|**DefinedValues**|この演算子によって導入された値のコンマ区切りの一覧を含みます。 これらの値は、現在のクエリ (たとえば、SELECT リストや WHERE 句) に指定された計算式であるか、またはこのクエリを処理するためにクエリ プロセッサで導入された内部値です。 これらの定義された値は、このクエリ内の他の場所で参照される可能性があります。 型 PLAN_ROWS の行のみ。|  
|**EstimateRows**|操作によって出力される行数の見積もり。 型 PLAN_ROWS の行のみ。|  
|**EstimateIO**|この演算子の推定 I/O コスト*。 型 PLAN_ROWS の行のみ。|  
|**EstimateCPU**|操作の CPU コスト* の見積もり。 型 PLAN_ROWS の行のみ。|  
|**AvgRowSize**|この演算子に渡される行の推定平均行サイズ (バイト単位)。|  
|**TotalSubtreeCost**|この操作とすべての子操作の推定 (累積) コスト*。|  
|**OutputList**|現在の演算によって示される列のコンマ区切りの一覧。|  
|**Warnings**|現在の演算に関係する警告メッセージのコンマ区切りの一覧。 警告メッセージには、列の一覧が指定された文字列 "NO STATS:()" が含まれる場合があります。 この警告メッセージは、クエリ オプティマイザーによって、この列の統計に基づいて判断が試行され、使用できるものがなかったことを意味します。 その結果、クエリ オプティマイザーで推測する必要があり、結果として非効率的なクエリ プランが選択された可能性がありました。 クエリ オプティマイザーで効率的なクエリ プランを選択できるような列統計を作成し更新する方法の詳細については、「[UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)」を参照してください。 この列には、必要に応じて文字列 "MISSING JOIN PREDICATE" を含めることができます。これは、(テーブルを含む) 結合が結合述語なしで行われていることを意味します。 結合述部を誤ってドロップすると、クエリの実行に予想よりも時間がかかり、膨大な結果セットが返される可能性があります。 この警告が返された場合は、結合述語が意図的に省略されているかどうかを確認してください。|  
|**Type**|ノード型です。 各クエリの親ノードの場合は、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの種類 (SELECT、INSERT、EXECUTE など) を表します。 実行プランを表すサブノードの場合、種類は PLAN_ROW です。|  
|**Parallel**|**0** = 操作は並列実行されません。<br /><br /> **1** = 操作は並列実行されます。|  
|**EstimateExecutions**|現在のクエリの実行中に、操作が実行される推定回数。|  
  
 \* コスト単位は、実時間ではなく、時間の内部測定に基づいています。 コスト単位は、プランの相対コストを他のプランと比較して決定するために使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 SET SHOWPLAN_ALL を使用するには、SET SHOWPLAN_ALL の実行ステートメントを実行するための適切な権限が与えられている必要があります。また、参照されるオブジェクトを含むすべてのデータベースに対して、SHOWPLAN 権限が必要です。  
  
 SELECT、INSERT、UPDATE、DELETE、EXEC "*ストアド プロシージャ*"、EXEC "*ユーザー定義関数*" の各ステートメントの場合、プラン表示を作成するには、ユーザーに次の権限が必要です。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで参照されるテーブルやビューなどのオブジェクトを含んでいるすべてのデータベースでの SHOWPLAN 権限。  
  
 DDL、USE "*データベース名*"、SET、DECLARE、動的 SQL など、その他すべてのステートメントでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限だけが必要です。  
  
## <a name="examples"></a>使用例  
 次の 2 つのステートメントは、SET SHOWPLAN_ALL の設定を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でクエリ内のインデックスの使用状況を分析し最適化する方法を示しています。  
  
 最初のクエリでは、インデックス列の WHERE 句で = (等しい) 比較演算子を使用しています。 この結果、**LogicalOp** 列に Clustered Index Seek 値が格納され、**Argument** 列にインデックスの名前が格納されます。  
  
 2 番目のクエリでは、WHERE 句で LIKE 演算子を使用します。 このように指定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではクラスター化インデックス スキャンが行われ、WHERE 句の条件を満たすデータが検索されます。 この結果、**LogicalOp** 列に Clustered Index Scan 値、**Argument** 列にインデックスの名前、**LogicalOp** 列にフィルター値、**Argument** 列に WHERE 句の条件がそれぞれ格納されます。  
  
 **EstimateRows** 列と **TotalSubtreeCost** 列の値は、インデックスが設定された最初のクエリの方が小さくなるので、インデックスが設定されていないクエリよりも速く処理が行われ、使用リソースが少なかったことがわかります。  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_ALL ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, EmergencyContactID   
FROM HumanResources.Employee  
WHERE EmergencyContactID LIKE '1%';  
GO  
SET SHOWPLAN_ALL OFF;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_TEXT &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)   
 [SET SHOWPLAN_XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)  
  
  
