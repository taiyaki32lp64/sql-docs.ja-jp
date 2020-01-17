---
title: SET SHOWPLAN_XML (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_XML
- SET_SHOWPLAN_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- SET SHOWPLAN_XML statement
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- XML [SQL Server], statement execution information
- SHOWPLAN_XML option
- estimated execution information [SQL Server]
ms.assetid: a467a1b3-10a5-43c4-9085-13d8aed549c9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 890c84330005c3d9f6c4b30a06662d67dfef46f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941658"
---
# <a name="set-showplanxml-transact-sql"></a>SET SHOWPLAN_XML (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが実行されなくなります。 代わりに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はステートメントの実行方法に関する詳細情報を、整形式の XML ドキュメントで返します。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
SET SHOWPLAN_XML { ON | OFF }
```

## <a name="remarks"></a>Remarks

SET SHOWPLAN_XML は、解析時ではなく実行時に設定されます。

SET SHOWPLAN_XML が ON の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では各ステートメントの実行プラン情報だけが返され、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは実行されません。 返される情報は、このオプションが ON に設定されてから OFF に設定されるまでに発行されたすべての [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに関する実行プラン情報です。 たとえば、SET SHOWPLAN_XML が ON のとき、CREATE TABLE ステートメントを実行した後で、同じテーブルを参照する SELECT ステートメントを実行すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では指定したテーブルが存在しないというエラー メッセージが返されます。 その後、このテーブルに対して行われる参照は失敗します。 SET SHOWPLAN_XML が OFF の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではレポートを作成せずに、ステートメントを実行します。

SET SHOWPLAN_XML では、**sqlcmd** ユーティリティなどのアプリケーション用に、出力が **nvarchar(max)** 型で返されます。この XML 出力は、他のツールがクエリ プランの情報の表示や処理を行う場合に使用されます。

> [!NOTE]
> 動的管理ビュー **sys.dm_exec_query_plan** では、SET SHOWPLAN_XML と同じ情報が **xml** データ型で返されます。 この情報は、**sys.dm_exec_query_plan** の **query_plan** 列から返されます。 詳しくは、「[sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)」をご覧ください。

SET SHOWPLAN_XML はストアド プロシージャ内では指定できません。 このステートメントは、バッチ内にのみ指定できます。

SET SHOWPLAN_XML では、情報が XML ドキュメントのセットとして返されます。 SET SHOWPLAN_XML を ON にした後で実行された各バッチの情報は、それぞれ 1 つの出力ドキュメントに反映されます。 各ドキュメントには、バッチ内のステートメントのテキストと実行ステップの詳細が含まれ、 推定コスト、行数、アクセスしたインデックス、実行された演算子の種類、結合順序、および実行プランに関するその他の情報が示されます。

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で **[実際の実行プランを含める]** を選ぶと、この SET オプションによって XML プラン表示出力が生成されません。 SET オプションを使う前に、 **[実際の実行プランを含める]** ボタンの選択を解除してください。

### <a name="location-of-showplan-output"></a>SHOWPLAN 出力の場所

SET SHOWPLAN_XML による XML 出力用の XML スキーマを含んだドキュメントは、セットアップ時に、Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているコンピューター上のローカル ディレクトリへコピーされます。 このドキュメントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ファイルを含むドライブ上の次のようなパスにあります。

- `\Microsoft SQL Server\130\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd`

前述のパスで、ノード `130\` は SQL Server 2016 によって使用されています。 数値 130 は、`SELECT @@VERSION` から返される値の最初のノード (13) から派生しています。 SQL Server 2017 の場合、パスには `140\` が使用されます。これは、その @@VERSION 値の最初のノードが 14 であるためです。 SQL Server 2019 の場合、@@VERSION の最初の値は 15 です。

プラン表示スキーマは、[こちらの Web サイト](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)にもあります。

## <a name="permissions"></a>アクセス許可

SET SHOWPLAN_XML を使用するには、SET SHOWPLAN_XML の実行ステートメントを実行するための適切な権限が与えられている必要があります。また、参照されるオブジェクトを含むすべてのデータベースに対して、SHOWPLAN 権限が必要です。

SELECT、INSERT、UPDATE、DELETE、EXEC "*ストアド プロシージャ*"、EXEC "*ユーザー定義関数*" の各ステートメントの場合、プラン表示を作成するには、ユーザーに次の権限が必要です。

- [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限。

- [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで参照されるテーブルやビューなどのオブジェクトを含んでいるすべてのデータベースでの SHOWPLAN 権限。

DDL、USE "*データベース名*"、SET、DECLARE、動的 SQL など、その他すべてのステートメントでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限だけが必要です。

## <a name="examples"></a>使用例

次の 2 つのステートメントは、SET SHOWPLAN_XML の設定を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でクエリ内のインデックスの使用状況を分析し最適化する方法を示しています。

最初のクエリでは、インデックス列の WHERE 句で = (等しい) 比較演算子を使用しています。 2 番目のクエリでは、WHERE 句で LIKE 演算子を使用します。 このように指定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではクラスター化インデックス スキャンが行われ、WHERE 句の条件を満たすデータが検索されます。 **EstimateRows** 属性と **EstimatedTotalSubtreeCost** 属性の値は、インデックスが設定された最初のクエリの方が小さくなるので、インデックスが設定されていないクエリよりも速く処理が行われ、使用リソースが少なかったことがわかります。

```sql
USE AdventureWorks2012;
GO
SET SHOWPLAN_XML ON;
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
SET SHOWPLAN_XML OFF;
```

## <a name="see-also"></a>参照

[SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)
