---
title: inserted テーブルと deleted テーブルの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- inserted tables
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- INSTEAD OF triggers
- deleted tables
- INSERT statement [SQL Server], DML triggers
- DML triggers, deleted or inserted tables
ms.assetid: ed84567f-7b91-4b44-b5b2-c400bda4590d
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e070cfc4b02ae52ab755306a29eb90c6afc912cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075498"
---
# <a name="use-the-inserted-and-deleted-tables"></a>inserted テーブルと deleted テーブルの使用
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  DML トリガー ステートメントでは、deleted テーブルおよび inserted テーブルという 2 つの特殊なテーブルが使用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、これらのテーブルを自動的に作成および管理します。 これらの一時的なメモリ常駐型のテーブルを使用して、特定のデータ変更の影響をテストしたり、DML トリガー操作に条件を設定したりできます。 これらのテーブル内のデータを直接変更したり、これらのテーブルに対して CREATE INDEX などのデータ定義言語 (DDL) 操作を実行することはできません。  
  
 DML トリガーでは、inserted テーブルと deleted テーブルは主に次のことを実行するために使用されます。  
  
-   テーブル間の参照整合性の拡張。  
  
-   ビューを構成するベース テーブルでのデータの挿入または更新。  
  
-   エラーのテストとエラー内容に基づく動作の実行。  
  
-   データ変更前と変更後のテーブルの状態の違いを検出し、その違いに基づいた動作の実行。  
  
 deleted テーブルには、DELETE ステートメントと UPDATE ステートメントの実行で影響を受けた行のコピーが格納されます。 DELETE ステートメントまたは UPDATE ステートメントの実行中、行はトリガー テーブルから削除され、deleted テーブルに転送されます。 通常、deleted テーブルとトリガー テーブルには共通する行はありません。  
  
 inserted テーブルには、INSERT ステートメントおよび UPDATE ステートメントの実行で影響を受けた行のコピーが格納されます。 挿入トランザクションまたは更新トランザクションの実行時には、新しい行が inserted テーブルとトリガー テーブルの両方に追加されます。 inserted テーブルの行はトリガー テーブルの新しい行のコピーです。  
  
 更新トランザクションは、削除処理とそれに続く挿入処理の組み合わせと考えることができます。まず、deleted テーブルに古い行がコピーされ、その後、新しい行がトリガー テーブルと inserted テーブルにコピーされます。  
  
 トリガーの条件を設定するときには、トリガーを起動した操作に合わせて inserted テーブルと deleted テーブルを使用します。 INSERT ステートメントをテストするときに deleted テーブルを参照したり、DELETE ステートメントをテストするときに inserted テーブルを参照してもエラーは発生しませんが、このような場合は、これらのトリガー テスト用テーブルには行が含まれていません。  
  
> [!NOTE]  
>  トリガーの動作が、データ変更の影響のある行の数に依存する場合、複数行データ変更 (SELECT ステートメントに基づく INSERT、DELETE、または UPDATE) に @@ROWCOUNT の検査などのテストを使用し、適切な動作を実行する必要があります。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、AFTER トリガー用の inserted テーブルおよび deleted テーブル内で **text**列、 **ntext**列、または **image** 列を参照することを禁止しています。 これらのデータ型は旧バージョンとの互換性のためだけに用意されているものです。 大きなデータを格納するには、 **varchar(max)** 、 **nvarchar(max)** 、および **varbinary(max)** データ型を使用することをお勧めします。 AFTER トリガーと INSTEAD OF トリガーでは両方とも、inserted テーブルおよび deleted テーブルで **varchar(max)** 、**nvarchar(max)** 、および **varbinary(max)** 型のデータがサポートされます。 詳細については、「[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)」を参照してください。  
  
 **トリガーで inserted テーブルを使用してビジネス ルールを適用する例**  
  
 CHECK 制約で参照できるのは、列レベルまたはテーブル レベルの制約が定義されている列のみであるため、テーブル間にまたがる制約 (ここでは、ビジネス ルール) はすべてトリガーとして定義する必要があります。  
  
 次の例では、DML トリガーを作成します。 このトリガーでは、 `PurchaseOrderHeader` テーブルに新しい発注を挿入しようとしたときに、ベンダーの信用格付けが良好であるかどうかがチェックされます。 挿入した発注に対応するベンダーの信用格付けを取得するには、 `Vendor` テーブルを参照し、inserted テーブルと結合する必要があります。 信用格付けが低い場合は、メッセージが表示され、挿入は実行されません。 この例では、複数行のデータの変更を許可していません。 詳細については、「 [複数行のデータを処理するための DML トリガーの作成](../../relational-databases/triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md)」を参照してください。  
  
 [!code-sql[TriggerDDL#CreateTrigger3](../../relational-databases/triggers/codesnippet/tsql/use-the-inserted-and-del_1.sql)]  
  
## <a name="using-the-inserted-and-deleted-tables-in-instead-of-triggers"></a>INSTEAD OF トリガー内での inserted テーブルと deleted テーブルの使用  
 テーブルに定義された INSTEAD OF トリガーへ渡される inserted テーブルおよび deleted テーブルは、AFTER トリガーに渡される inserted テーブルおよび deleted テーブルと同じルールに従います。 inserted テーブルと deleted テーブルのフォーマットは、INSTEAD OF トリガーを定義したテーブルのフォーマットと同じです。 inserted テーブルおよび deleted テーブルの各列は、ベース テーブルの列に直接マップされます。  
  
 INSTEAD OF トリガーを含むテーブルを参照する INSERT ステートメントまたは UPDATE ステートメントで、列に値を指定するときに適用されるルールは、次に示すように、INSTEAD OF トリガーのないテーブルに適用されるルールと同じです。  
  
-   計算列または **timestamp** データ型の列の場合、値は指定できません。  
  
-   IDENTITY プロパティを持つ列の場合、そのテーブルに対して IDENTITY_INSERT が ON になっていない限り、値は指定できません。 IDENTITY_INSERT が ON になっている場合は、INSERT ステートメントで値を指定する必要があります。  
  
-   INSERT ステートメントでは、DEFAULT 制約のないすべての NOT NULL 列に対して値を指定する必要があります。  
  
-   計算列、ID 列、または **timestamp** 型の列以外で、NULL 値を許容する列、または DEFAULT 定義を持つ NOT NULL 列については、値の指定を省略できます。  
  
 INSERT、UPDATE、または DELETE の各ステートメントが INSTEAD OF トリガーを含むビューを参照する場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、どのテーブルに対しても直接に動作を実行するのではなく、そのトリガーを呼び出します。 呼び出されたトリガーは、inserted テーブルおよび deleted テーブルの情報を使用して、ベース テーブルで要求された動作を実装するために必要なステートメントを作成する必要があります。その際、ビューに作成された inserted テーブルおよび deleted テーブルの情報の形式がベース テーブルのデータ形式と異なっていてもかまいません。  
  
 ビューに定義された INSTEAD OF トリガーに渡される inserted テーブルおよび deleted テーブルの形式は、ビューに定義された SELECT ステートメントの選択リストに一致します。 例:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.EmployeeNames (BusinessEntityID, LName, FName)  
AS  
SELECT e.BusinessEntityID, p.LastName, p.FirstName  
FROM HumanResources.Employee AS e   
JOIN Person.Person AS p  
ON e.BusinessEntityID = p.BusinessEntityID;  
```  
  
 このビューの結果セットには 3 列があり、1 つは **int** 列で、後の 2 つは **nvarchar** 列です。 ビューで定義された INSTEAD OF トリガーに渡される inserted テーブルと deleted テーブルには、 **という名前の** int `BusinessEntityID`列、 **という名前の** nvarchar `LName`列、および **という名前の** nvarchar `FName`列があります。  
  
 ビューの選択リストには、単一のベース テーブルの列に直接マップされない式を含めることができます。 ビューの式の中には、定数や関数の呼び出しなど、列を参照しない可能性があり、無視できるものがあります。 複合式を使用して複数の列を参照できます。ただし、inserted テーブルおよび deleted テーブルでは、挿入された行ごとに 1 つの値のみを持つことができます。 このことは、複合式を持つ計算列を参照するビューの単純式にも当てはまります。 このような種類の式は、ビューの INSTEAD OF トリガーが処理する必要があります。  
  
  
