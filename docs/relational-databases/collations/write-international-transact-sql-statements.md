---
title: 国際化に対応した Transact-SQL ステートメントの記述 | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- writing international statements
- Transact-SQL international considerations
- international considerations [SQL Server], Transact-SQL
- Database Engine international considerations [SQL Server], Transact-SQL
- statements [SQL Server], international
- database international considerations [SQL Server], Transact-SQL
- dates [SQL Server], international considerations
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4cbc237ad0df16dbb854fb5bd062d7d37375294f
ms.sourcegitcommit: 3bd813ab2c56b415a952e5fbd5cfd96b361c72a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2019
ms.locfileid: "70913548"
---
# <a name="write-international-transact-sql-statements"></a>国際化に対応した Transact-SQL ステートメントの記述
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  以下のガイドラインに従うと、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用するデータベースやデータベース アプリケーションをある言語から別の言語に移行することが容易になり、複数の言語をサポートできます。  

-   [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、次のいずれかを使用します。
    -   <bpt id="p1">**</bpt>char<ept id="p1">**</ept>、<bpt id="p2">**</bpt>varchar<ept id="p2">**</ept>、<bpt id="p3">**</bpt>varchar(max)<ept id="p3">**</ept> の各データ型では <bpt id="p4">[</bpt>UTF-8<ept id="p4">](../../relational-databases/collations/collation-and-unicode-support.md#utf8)</ept> 対応の照合順序が使用され、データは UTF-8 を使用してエンコードされます。
    -   **nchar**、**nvarchar**、**nvarchar(max)** の各データ型では[補助文字 (SC)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) 対応の照合順序が使用され、データは UTF-16 を使用してエンコードされます。 SC 以外の照合順序を使用すると、データは UCS-2 を使用してエンコードされます。      

    これによりコード ページ変換の問題を回避できます。 他の考慮事項については、「[UTF-8 と UTF-16 でのストレージの相違点](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences)」をご覧ください。  

-   [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] までは、**char**、**varchar**、**varchar(max)** の各データ型を使用しているすべての個所をそれぞれ **nchar**、**nvarchar**、**nvarchar(max)** データ型に置き換えます。 [補助文字 (SC)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) 対応の照合順序を使用する場合、データは UTF-16 を使用してエンコードされます。 SC 以外の照合順序を使用すると、データは UCS-2 を使用してエンコードされます。 これによりコード ページ変換の問題を回避できます。 詳細については、「 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。 

    > [!IMPORTANT]
    > **text** データ型は非推奨で、新しい開発作業では使用できません。 **text** データの **varchar(max)** への変換を検討してください。
  
-   月単位または曜日単位で比較や操作を行う場合、名前の文字列ではない数字の日付要素を使用します。 言語設定が異なると、月や曜日の名前が異なります。 たとえば、`DATENAME(MONTH,GETDATE())` は、言語の設定が英語 (U.S.) になっていれば `May` を返します。設定がドイツ語になっていれば `Mai`、フランス語になっていれば `mai` を返します。 代わりに、[DATEPART](../../t-sql/functions/datepart-transact-sql.md) のような関数を使用すると、月の名前の代わりに数字が返されます。 多くの場合、日付を数字で表記するよりも名前で表記する方がよりわかりやすくなるので、ユーザーに表示する結果セットを構築するときは、DATEPART 名を使用してください。 ただし、特定の言語の表示名に依存するロジックはコーディングしないでください。  
  
-   日付を比較する場合、または INSERT ステートメントまたは UPDATE ステートメントで日付を指定する場合は、どの言語設定でも同じ解釈が行われる制約を使用します。  
  
    -   ADO、OLE DB、および ODBC アプリケーションでは、以下に示す ODBC タイムスタンプ、日付、時刻のエスケープ句を使用する必要があります。  
  
         **{ ts'** _yyyy_ **-** _mm_ **-** _dd_ _hh_ **:** _mm_ **:** _ss_ [ **.** _fff_] **'}** 、例: **{ ts'1998-09-24 10:02:20'}**  
  
         **{ d'** _yyyy_ **-** _mm_ **-** _dd_ **'}** 、例: **{ d'1998-09-24'}**
  
         **{ t'** _hh_ **:** _mm_ **:** _ss_ **'}** 、例: **{ t'10:02:20'}**  
  
    -   他の API、または [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト、ストアド プロシージャ、およびトリガーを使用するアプリケーションでは、区切られていない数字列を使用してください。 たとえば、 *yyyymmdd* には 19980924 を使用します。  
  
    -   他の API、または [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト、ストアド プロシージャ、トリガーを使用するアプリケーションでは、**time** 型、**date** 型、**smalldate** 型、**datetime** 型、**datetime2** 型、**datetimeoffset** のデータ型と文字列データ型間の変換にはすべて、明示的なスタイル パラメーターを指定して [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) ステートメントを使用してください。 たとえば、次のステートメントは、すべての言語または日付形式の接続設定で同じように解釈されます。  
  
        ```sql  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)     
[DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md)        
[照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)      
