---
title: 計算列のインデックス | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cf54565115df53dc7d502f48aad68f9974adebd0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909689"
---
# <a name="indexes-on-computed-columns"></a>計算列のインデックス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

次の要件を満たしている限り、計算列にインデックスを定義できます。  
  
-   所有権の要件  
-   決定性の要件  
-   正確さの要件  
-   データ型の要件  
-   SET オプションの要件  
  
#### <a name="ownership-requirements"></a>所有権の要件
  
計算列のすべての関数参照の所有者がテーブルの所有者と同じである必要があります。  
  
## <a name="determinism-requirements"></a>決定性の要件  

指定された一連の入力に対して式から必ず同じ結果が返される場合、その式は決定的です。 **COLUMNPROPERTY** 関数の [IsDeterministic](../../t-sql/functions/columnproperty-transact-sql.md) プロパティは、 *computed_column_expression* が決定的であるかどうかを示します。  
*computed_column_expression* は、決定的である必要があります。 次のすべての条件に該当する場合、*computed_column_expression* は決定的です。  
  
-   式で参照される関数が決定的かつ正確である場合。 このような関数には、ユーザー定義関数と組み込み関数の両方があります。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。 計算列が PERSISTED の場合、関数は不正確になる場合があります。 詳細については、このトピックの後半の「 [保存される計算列でのインデックスの作成](#BKMK_persisted) 」を参照してください。  
  
-   式で参照されるすべての列が計算列を含むテーブルの列である場合。  
  
-   列参照が複数の行からデータを取り出していない場合。 たとえば、SUM や AVG などの集計関数は複数の行のデータに依存して計算を行うので、 *computed_column_expression* は非決定的になります。  
  
-   *computed_column_expression* がシステム データ アクセスやユーザー データ アクセスを伴わない場合。  
  
共通言語ランタイム (CLR) 式を含むすべての計算列は決定的であり、インデックスを作成する前に PERSISTED に設定されている必要があります。 CLR ユーザー定義型の式を、計算列の定義に使用できます。 計算列の型が CLR ユーザー定義型の場合、その型が比較可能である限り、計算列にインデックスを作成できます。 詳細については、「 [CLR ユーザー定義型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)」を参照してください。  

#### <a name="cast-and-convert"></a>CAST および CONVERT

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインデックス付き計算列で日付データ型の文字列リテラルを参照するときは、決定的な日付形式スタイルを使用して、そのリテラルを目的の日付型に明示的に変換することをお勧めします。 決定的な日付形式の一覧については、「 [CAST および CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)」を参照してください。 

詳細については、「[リテラル日付文字列を DATE 値に非決定論的に変換する](../../t-sql/data-types/nondeterministic-convert-date-literals.md)」を参照してください。

#### <a name="compatibility-level"></a>互換性レベル

照合順序間で行われる Unicode 以外の文字データの暗黙的な変換は、互換性レベルが 80 以下の場合を除いて、非決定論的であると見なされます。  

データベース互換性レベルの設定が 90 の場合は、それらの式を含む計算列にインデックスを作成することはできません。 ただし、アップグレードされたデータベースから、このような式を含む既存の計算列をメンテナンスできます。 文字列から日付への暗黙的な変換を行うインデックス付き計算列を使用する場合は、インデックスが破損しないように、データベースやアプリケーション内で LANGUAGE と DATEFORMAT の設定の一貫性を確保してください。

互換性レベル 90 は SQL Server 2005 に該当します。



## <a name="precision-requirements"></a>正確さの要件
  
 *computed_column_expression* は正確である必要があります。 *computed_column_expression* は、次の 1 つ以上の条件に該当する場合は正確です。  
  
-   **float** データ型または **real** データ型の式ではない。  
-   式の定義に **float** データ型や **real** データ型を使用していない。 たとえば、次のステートメントでは、列 `y` は **int** 型で決定的ですが、正確ではありません。  
  
    ```sql  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
> **float** 型や **real** 型の式はすべて不正確であると見なされ、インデックスのキーにできません。つまり、 **float** 型または **real** 型の式はインデックス付きビューで使用できますが、キーとしては使用できません。 このことは、計算列にも当てはまります。 **float** 型や **real** 型の任意の式が含まれている関数、式、またはユーザー定義関数はすべて不正確であると見なされます。 これには、論理式 (比較) も含まれます。  
  
COLUMNPROPERTY 関数の **IsPrecise** プロパティは、 *computed_column_expression* が正確であるかどうかを示します。  


## <a name="data-type-requirements"></a>データ型の要件
  
-   計算列で定義された *computed_column_expression* は、 **text**データ型、 **ntext**データ型、または **image** データ型として評価できません。  
-   **image**、 **ntext**、 **text**、 **varchar(max)** 、 **nvarchar(max)** 、 **varbinary(max)** 、および **xml** データ型から派生した計算列には、計算列のデータ型をインデックス キー列として使用できる限り、インデックスを作成できます。  
-   **image**、 **ntext**、および **text** データ型から派生した計算列は、計算列のデータ型を非キー インデックス列として使用できる限り、非クラスター化インデックスの非キー列 (付加列) にすることができます。  


## <a name="set-option-requirements"></a>SET オプションの要件
  
-   計算列を定義する CREATE TABLE ステートメントまたは ALTER TABLE ステートメントの実行時に、ANSI_NULLS 接続レベルのオプションが ON に設定されている必要があります。 [OBJECTPROPERTY](../../t-sql/functions/objectproperty-transact-sql.md) 関数の **IsAnsiNullsOn** プロパティは、このオプションが ON に設定されているかどうかを示します。  
-   インデックスを作成する接続、およびインデックス内の値を変更する INSERT、UPDATE、または DELETE ステートメントを実行するすべての接続では、SET オプションのうち 6 つを ON に設定し、1 つを OFF に設定する必要があります。 これらのオプションの設定が同一ではない接続で実行されるすべての SELECT ステートメントでは、オプティマイザーにより計算列のインデックスが無視されます。  
  
    -   NUMERIC_ROUNDABORT オプションは OFF に設定し、次のオプションは ON に設定する必要があります。  
    -   ANSI_NULLS  
    -   ANSI_PADDING  
    -   ANSI_WARNINGS  
    -   ARITHABORT  
    -   CONCAT_NULL_YIELDS_NULL  
    -   QUOTED_IDENTIFIER  
  
> [!NOTE]
> ANSI_WARNINGS を ON に設定すると、データベース互換性レベルが 90 以上に設定されている場合、暗黙的に ARITHABORT が ON に設定されます。  
  
## <a name="BKMK_persisted"></a> 保存される計算列でのインデックスの作成  

不正確であるが決定的な式で定義される計算列を作成できることがあります。 これは、CREATE TABLE または ALTER TABLE ステートメントで列に PERSISTED マークが付いているときに可能です。

その場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によってテーブルに計算値が格納され、計算列が依存している他の列が更新されるとその計算値も更新されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、列にインデックスを作成するとき、およびインデックスがクエリで参照されるときに、これらの保存値を使用します。

このオプションにより、特に [!INCLUDE[ssDE](../../includes/ssde-md.md)] で作成されている CLR 関数など、計算列の式を返す関数が決定的かつ正確であるかどうかを [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]で正確に確認できないときに、計算列にインデックスを作成できます。  


  
## <a name="related-content"></a>関連コンテンツ  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)    
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
  
  
