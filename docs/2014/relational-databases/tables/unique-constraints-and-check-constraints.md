---
title: UNIQUE 制約と CHECK 制約 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], Visual Database Tools
- Visual Database Tools [SQL Server], constraints
ms.assetid: 637098af-2567-48f8-90f4-b41df059833e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2a8dfd7da9bb1ccc60d18e68ccbe4930a6edb00d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196676"
---
# <a name="unique-constraints-and-check-constraints"></a>UNIQUE 制約と CHECK 制約
  UNIQUE 制約と CHECK 制約は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル内のデータに整合性を適用するために使用できる 2 種類の制約です。 これらは重要なデータベース オブジェクトです。  
  
 このトピックは次のセクションで構成されます。  
  
 [UNIQUE 制約](#Unique)  
  
 [CHECK 制約](#Check)  
  
 [関連タスク](#Tasks)  
  
##  <a name="Unique"></a> UNIQUE 制約  
 制約とは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] によって適用される規則です。 たとえば、UNIQUE 制約を使用して、主キーに関係しない特定の列に重複した値が入力されないようにできます。 UNIQUE 制約も PRIMARY KEY 制約も一意性を設定しますが、主キーではない列または列セットに一意性を設定する場合は、PRIMARY KEY 制約ではなく UNIQUE 制約を使用します。  
  
 PRIMARY KEY 制約とは異なり、UNIQUE 制約は NULL 値を許容できます。 ただし、UNIQUE 制約が適用される他の値と同様に、NULL 値も 1 列に 1 つしか使用できません。 UNIQUE 制約は FOREIGN KEY 制約から参照することもできます。  
  
 既定では、テーブルの既存の列に UNIQUE 制約を追加すると、すべての値が一意であることを確認するために、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] により列の既存のデータが調べられます。 重複した値を含む列に UNIQUE 制約を追加すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によりエラーが返され、制約は追加されません。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、UNIQUE 制約による一意性の要件を強制する UNIQUE インデックスを自動的に作成します。 このため、重複した行を挿入しようとすると、UNIQUE 制約に違反していることを示すエラー メッセージが [!INCLUDE[ssDE](../../includes/ssde-md.md)] により返され、テーブルには行が追加されません。 クラスター化インデックスが明示的に指定されていない限り、UNIQUE 制約を強制する一意の非クラスター化インデックスが既定で作成されます。  
  
##  <a name="Check"></a> CHECK 制約  
 CHECK 制約は、1 つ以上の列に格納できる値を制限することによってドメインの整合性を強制します。 論理演算子に基づいて TRUE または FALSE を返す論理 (ブール) 式を使って CHECK 制約を作成できます。 たとえば、 **salary** 列の値の範囲は、$15,000 ～ $100,000 のデータのみを許容する CHECK 制約を作成することにより制限できます。 これにより、この一定の給与範囲を超える給与を入力できなくなります。 論理式は、 `salary >= 15000 AND salary <= 100000`になります。  
  
 複数の CHECK 制約を 1 つの列に適用できます。 テーブル レベルで CHECK 制約を作成すると、1 つの CHECK 制約を複数の列に適用できます。 たとえば、複数列の CHECK 制約を使用して、 **country_region** 列の値が **USA** であるいずれかの行の **state** 列に 2 文字の値が格納されているかどうかを確認できます。 これにより、1 か所で複数の条件をチェックできるようになります。  
  
 CHECK 制約は、列に格納される値を制御するという点では FOREIGN KEY 制約に似ています。 違いは、有効な値を判断する方法には。FOREIGN KEY 制約は、CHECK 制約は、logical expression から有効な値を確認中に、別のテーブルから有効な値の一覧を取得します。  
  
> [!CAUTION]  
>  暗黙的または明示的なデータ型の変換が含まれる制約により、特定の操作が失敗することがあります。 たとえば、パーティションの切り替え元のテーブルに定義された制約により、ALTER TABLE...SWITCH 操作が失敗することがあります。 制約の定義ではデータ型を変換しないようにしてください。  
  
### <a name="limitations-of-check-constraints"></a>CHECK 制約の制限事項  
 CHECK 制約は、FALSE と評価された値を拒否します。 NULL 値は UNKNOWN と評価されるので、式に NULL 値が含まれていると制約がオーバーライドされる場合があります。 たとえば、制約を配置する、`int`列**MyColumn**ことを指定する**MyColumn** 10 の値のみを含めることができます (**MyColumn = 10**)。 **MyColumn**に値 NULL を挿入すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって NULL が追加され、エラーは返されません。  
  
 CHECK 制約は、チェックしている条件がテーブルのすべての行に対して FALSE でない場合、TRUE を返します。 CHECK 制約は行レベルで機能します。 作成したばかりのテーブルに行が含まれていない場合、このテーブルに適用された CHECK 制約は有効であると見なされます。 この場合、次の例に示すような予期しない結果が生成されることがあります。  
  
```  
CREATE TABLE CheckTbl (col1 int, col2 int);  
GO  
CREATE FUNCTION CheckFnctn()  
RETURNS int  
AS   
BEGIN  
   DECLARE @retval int  
   SELECT @retval = COUNT(*) FROM CheckTbl  
   RETURN @retval  
END;  
GO  
ALTER TABLE CheckTbl  
ADD CONSTRAINT chkRowCount CHECK (dbo.CheckFnctn() >= 1 );  
GO  
```  
  
 追加する `CHECK` 制約では、テーブル `CheckTbl`に 1 行以上の行が格納されていなければならないことを指定します。 ただし、テーブルにはこの制約の条件をチェックする行が存在しないので、ALTER TABLE ステートメントは成功します。  
  
 CHECK 制約では、DELETE ステートメントの実行中は検証されません。 そのため、特定の種類の CHECK 制約が適用されたテーブルで DELETE ステートメントを実行すると、予期しない結果が生成されることがあります。 たとえば、テーブル `CheckTbl`で次のステートメントを実行するとします。  
  
```  
INSERT INTO CheckTbl VALUES (10, 10);  
GO  
DELETE CheckTbl WHERE col1 = 10;  
```  
  
 `CHECK` 制約では、テーブル `CheckTbl` に `1` 行以上が格納されていなければならないことを指定していますが、`DELETE` ステートメントは成功します。  
  
##  <a name="Tasks"></a> 関連タスク  
  
> [!NOTE]  
>  テーブルをレプリケーションのためにパブリッシュする場合は、Transact-SQL ステートメントの [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) または SQL Server 管理オブジェクト (SMO) を使用してスキーマを変更する必要があります。 テーブル デザイナーまたはデータベース ダイアグラム デザイナーを使用してスキーマを変更するとき、テーブルはいったん削除されてから再作成されます。 パブリッシュされたオブジェクトは削除できないので、スキーマの変更は失敗します。  
  
|タスク|トピック|  
|----------|-----------|  
|UNIQUE 制約の作成方法について説明します。|[UNIQUE 制約の作成](../tables/create-unique-constraints.md)|  
|UNIQUE 制約の変更方法について説明します。|[UNIQUE 制約の変更](../tables/modify-unique-constraints.md)|  
|UNIQUE 制約の削除方法について説明します。|[UNIQUE 制約の削除](../tables/delete-unique-constraints.md)|  
|レプリケーション エージェントによってテーブルのデータが挿入または更新された場合に CHECK 制約を無効にする方法について説明します。|[レプリケーションの CHECK 制約の無効化](../tables/disable-check-constraints-for-replication.md)|  
|テーブルに対してデータの追加、更新、または削除を行う際に、CHECK 制約を無効にする方法について説明します。|[INSERT ステートメントまたは UPDATE ステートメントによる CHECK 制約の無効化](../tables/disable-check-constraints-with-insert-and-update-statements.md)|  
|制約式を変更するか、または特定条件の制約を有効または無効にするオプションを変更する方法について説明します。|[CHECK 制約の変更](../tables/modify-check-constraints.md)|  
|CHECK 制約の削除方法について説明します。|[CHECK 制約の削除](../tables/delete-check-constraints.md)|  
|CHECK 制約のプロパティを表示する方法について説明します。|[UNIQUE 制約と CHECK 制約](../tables/unique-constraints-and-check-constraints.md)|  
  
  
