---
title: SET STATISTICS XML (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_XML_TSQL
- SET STATISTICS XML
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- STATISTICS XML option
- SET STATISTICS XML statement
- statements [SQL Server], statistical information
- XML [SQL Server], statement execution information
ms.assetid: 2b6d4c5a-a7f5-4dd1-b10a-7632265b1af7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 015ba90a6f2cad79483e52d5caa23ad06784c055
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004711"
---
# <a name="set-statistics-xml-transact-sql"></a>SET STATISTICS XML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行し、ステートメントの実行方法に関する詳細情報を整形式の XML ドキュメント形式で生成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET STATISTICS XML { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 SET STATISTICS XML は、解析時ではなく実行時に設定されます。  
  
 SET STATISTICS XML が ON の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では各ステートメントの実行に関する情報がステートメントの実行後に返されます。 返される情報は、このオプションが ON に設定されてから OFF に設定されるまでに実行されたすべての [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに関する情報です。 SET STATISTICS XML 以外のステートメントを同時にバッチで実行することもできます。  
  
 SET STATISTICS XML では、**sqlcmd** ユーティリティなどのアプリケーション用に、出力が **nvarchar(max)** で返されます。この XML 出力は、他のツールがクエリ プランの情報の表示や処理を行う場合に使用されます。  
  
 SET STATISTICS XML では、情報が XML ドキュメントのセットとして返されます。 SET STATISTICS XML ON ステートメントの後の各ステートメントは、それぞれ 1 つの出力ドキュメントに反映されます。 それぞれのドキュメントには、ステートメントのテキストと、実行ステップの詳細が含まれます。 この出力では、コスト、アクセスしたインデックス、実行された操作の種類、結合順序、物理操作が実行された回数、それぞれの物理操作で作成された行の数など、実行時の情報が示されます。  
  
 SET STATISTICS XML による XML 出力用の XML スキーマを含んだドキュメントは、セットアップ時に、Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているコンピューター上のローカル ディレクトリへコピーされます。 このドキュメントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール ファイルと同じドライブ上にあります。場所は次のとおりです。  
  
 \Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd  
  
 プラン表示スキーマは、[こちらの Web サイト](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)にもあります。  
  
 SET STATISTICS PROFILE と SET STATISTICS XML は、同時に使用できません。 前者ではテキスト形式の出力が生成され、後者では XML 形式の出力が生成されます。 将来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、新しいクエリ実行プランの情報は STATISTICS XML ステートメントでのみ表示され、SET STATISTICS PROFILE ステートメントでは表示されなくなります。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で **[実際の実行プランを含める]** を選ぶと、この SET オプションによって XML プラン表示出力が生成されません。 SET オプションを使う前に、 **[実際の実行プランを含める]** ボタンの選択を解除してください。  
  
## <a name="permissions"></a>アクセス許可  
 SET STATISTICS XML を使用して出力を表示するには、ユーザーに次の権限が必要です。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限。  
  
-   SHOWPLAN 権限。これは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで参照されるオブジェクトを含むすべてのデータベースに対して必要です。  
  
 STATISTICS XML の結果セットを生成しない [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの場合は、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限のみで十分です。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで STATISTICS XML の結果セットを生成する場合は、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行する権限と、SHOWPLAN の権限の両方があることを確認してください。これらの 2 つの権限がないと、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実行は中断され、プラン表示に関する情報は生成されません。  
  
## <a name="examples"></a>使用例  
 次に示す 2 つのステートメントでは、SET STATISTICS XML の設定を使用し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でクエリ内のインデックスの使用状況を分析し最適化する方法を示しています。 最初のクエリでは、インデックス付き列の WHERE 句で = (等しい) 比較演算子を使用します。 2 番目のクエリでは、WHERE 句で LIKE 演算子を使用します。 このように指定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではクラスター化インデックス スキャンが行われ、WHERE 句の条件を満たすデータが検索されます。 **EstimateRows** 属性と **EstimatedTotalSubtreeCost** 属性の値は、インデックスが設定された最初のクエリの方が小さくなっています。これは、インデックスを設定されていないクエリよりも速く処理が行われ、使用リソースが少なかったことを示しています。  
  
```  
USE AdventureWorks2012;  
GO  
SET STATISTICS XML ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, JobTitle   
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Production%';  
GO  
SET STATISTICS XML OFF;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SET SHOWPLAN_XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [sqlcmd Utility](../../tools/sqlcmd-utility.md)  
  
  
