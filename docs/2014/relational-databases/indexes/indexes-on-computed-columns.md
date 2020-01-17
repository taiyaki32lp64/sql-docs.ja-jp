---
title: 計算列のインデックス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- computed columns, index creation
- index creation [SQL Server], computed columns
- imprecise columns
- persisted computed columns
- precise [SQL Server]
ms.assetid: 8d17ac9c-f3af-4bbb-9cc1-5cf647e994c4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c5aa2bd118d99afea6a1ee6ea8f41c646146c32f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162454"
---
# <a name="indexes-on-computed-columns"></a>計算列のインデックス
  次の要件を満たしている限り、計算列にインデックスを定義できます。  
  
-   所有権の要件  
  
-   決定性の要件  
  
-   正確さの要件  
  
-   データ型の要件  
  
-   SET オプションの要件  
  
 **Ownership Requirements**  
  
 計算列のすべての関数参照の所有者がテーブルの所有者と同じである必要があります。  
  
 **Determinism Requirements**  
  
> [!IMPORTANT]  
>  指定された一連の入力に対して式から必ず同じ結果が返される場合、その式は決定的です。 **COLUMNPROPERTY** 関数の [IsDeterministic](/sql/t-sql/functions/columnproperty-transact-sql) プロパティは、 *computed_column_expression* が決定的であるかどうかを示します。  
  
 *computed_column_expression* は、決定的である必要があります。 次の 1 つ以上の条件に該当する場合、 *computed_column_expression* は決定的です。  
  
-   式で参照される関数が決定的かつ正確である場合。 このような関数には、ユーザー定義関数と組み込み関数の両方があります。 詳細については、「 [決定的関数と非決定的関数](../user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。 計算列が PERSISTED の場合、関数は不正確になる場合があります。 詳細については、このトピックの後半の「 [保存される計算列でのインデックスの作成](#BKMK_persisted) 」を参照してください。  
  
-   式で参照されるすべての列が計算列を含むテーブルの列である場合。  
  
-   列参照が複数の行からデータを取り出していない場合。 たとえば、SUM や AVG などの集計関数は複数の行のデータに依存して計算を行うので、 *computed_column_expression* は非決定的になります。  
  
-   *computed_column_expression* がシステム データ アクセスやユーザー データ アクセスを伴わない場合。  
  
 共通言語ランタイム (CLR) 式を含むすべての計算列は決定的であり、インデックスを作成する前に PERSISTED に設定されている必要があります。 CLR ユーザー定義型の式を、計算列の定義に使用できます。 計算列の型が CLR ユーザー定義型の場合、その型が比較可能である限り、計算列にインデックスを作成できます。 詳細については、「 [CLR ユーザー定義型](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインデックス付き計算列で日付データ型の文字列リテラルを参照するときは、決定的な日付形式スタイルを使用して、そのリテラルを目的の日付型に明示的に変換することをお勧めします。 決定的な日付形式の一覧については、「 [CAST および CONVERT](/sql/t-sql/functions/cast-and-convert-transact-sql)」を参照してください。 日付データ型への文字列の暗黙的な変換が必要な式は、データベース互換性レベルが 80 以下に設定されている場合を除いて、非決定的であると見なされます。 これは、サーバー セッションの [LANGUAGE](/sql/t-sql/statements/set-language-transact-sql) および [DATEFORMAT](/sql/t-sql/statements/set-dateformat-transact-sql) の設定によって結果が異なるためです。 たとえば、式 `CONVERT (datetime, '30 listopad 1996', 113)` では、言語が異なると文字列 '`30 listopad 1996`' が異なる月を意味するので、結果が LANGUAGE の設定によって異なります。 同様に、式 `DATEADD(mm,3,'2000-12-01')`では、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] により、文字列 `'2000-12-01'` が DATEFORMAT の設定に基づいて解釈されます。  
>   
>  照合順序間で行われる Unicode 以外の文字データの暗黙的な変換も、互換性レベルが 80 以下の場合を除いて、非決定的であると見なされます。  
>   
>  データベース互換性レベルの設定が 90 の場合は、それらの式を含む計算列にインデックスを作成することはできません。 ただし、アップグレードされたデータベースから、このような式を含む既存の計算列をメンテナンスできます。 文字列から日付への暗黙的な変換を行うインデックス付き計算列を使用する場合は、インデックスが破損しないように、データベースやアプリケーション内で LANGUAGE と DATEFORMAT の設定の一貫性を確保してください。  
  
 **Precision Requirements**  
  
 *computed_column_expression* は正確である必要があります。 *computed_column_expression* は、次の 1 つ以上の条件に該当する場合は正確です。  
  
-   `float` データ型または `real` データ型の式ではない。  
  
-   式の定義に `float` データ型や `real` データ型を使用していない。 たとえば、次のステートメントでは、列 `y` は `int` 型で決定的ですが、正確ではありません。  
  
    ```  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
>  `float` 型や `real` 型の式はすべて不正確であると見なされ、インデックスのキーにできません。つまり、`float` 型または `real` 型の式はインデックス付きビューで使用できますが、キーとしては使用できません。 このことは、計算列にも当てはまります。 `float` 型や `real` 型の任意の式が含まれている関数、式、またはユーザー定義関数はすべて不正確であると見なされます。 これには、論理式 (比較) も含まれます。  
  
 COLUMNPROPERTY 関数の **IsPrecise** プロパティは、 *computed_column_expression* が正確であるかどうかを示します。  
  
 **Data Type Requirements**  
  
-   *Computed_column_expression*として評価できません、計算列の定義、 `text`、 `ntext`、または`image`データ型。  
  
-   `image`、`ntext`、`text`、`varchar(max)`、`nvarchar(max)`、`varbinary(max)`、および `xml` データ型から派生した計算列には、計算列のデータ型をインデックス キー列として使用できる限り、インデックスを作成できます。  
  
-   `image`、`ntext`、および `text` データ型から派生した計算列は、計算列のデータ型を非キー インデックス列として使用できる限り、非クラスター化インデックスの非キー列 (付加列) にすることができます。  
  
 **SET Option Requirements**  
  
-   計算列を定義する CREATE TABLE ステートメントまたは ALTER TABLE ステートメントの実行時に、ANSI_NULLS 接続レベルのオプションが ON に設定されている必要があります。 [OBJECTPROPERTY](/sql/t-sql/functions/objectpropertyex-transact-sql) 関数の **IsAnsiNullsOn** プロパティは、このオプションが ON に設定されているかどうかを示します。  
  
-   インデックスを作成する接続、およびインデックス内の値を変更する INSERT、UPDATE、または DELETE ステートメントを実行するすべての接続では、SET オプションのうち 6 つを ON に設定し、1 つを OFF に設定する必要があります。 これらのオプションの設定が同一ではない接続で実行されるすべての SELECT ステートメントでは、オプティマイザーにより計算列のインデックスが無視されます。  
  
    -   NUMERIC_ROUNDABORT オプションは OFF に設定し、次のオプションは ON に設定する必要があります。  
  
    -   ANSI_NULLS  
  
    -   ANSI_PADDING  
  
    -   ANSI_WARNINGS  
  
    -   ARITHABORT  
  
    -   CONCAT_NULL_YIELDS_NULL  
  
    -   QUOTED_IDENTIFIER  
  
     ANSI_WARNINGS を ON に設定すると、データベース互換性レベルが 90 以上に設定されている場合、暗黙的に ARITHABORT が ON に設定されます。  
  
##  <a name="BKMK_persisted"></a> 保存される計算列でのインデックスの作成  
 決定的でも不正確である式を使用して定義されている計算列が CREATE TABLE ステートメントまたは ALTER TABLE ステートメントで PERSISTED に設定されている場合、計算列にインデックスを作成できます。 つまり、[!INCLUDE[ssDE](../../../includes/ssde-md.md)]列のインデックスを作成し、インデックスがクエリで参照されている場合は、これらの永続化された値を使用します。 このオプションでは、計算列にインデックスを作成することができる場合[!INCLUDE[ssDE](../../../includes/dnprdnshort-md.md)]、決定的かつ正確には。  
  
## <a name="related-content"></a>関連コンテンツ  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)  
  
  
