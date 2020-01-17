---
title: column_constraint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- column_constraint
- column_constraint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER TABLE statement
- constraints [SQL Server], properties
- constraints [SQL Server], definitions
- column_constraint
ms.assetid: 8119b7c7-e93b-4de5-8f71-c3b7c70b993c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f45cb5b270bff9b2609ca0228c4e37a06314d368
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982002"
---
# <a name="alter-table-column_constraint-transact-sql"></a>ALTER TABLE column_constraint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) を使用してテーブルに追加された新しい列定義の一部になっている PRIMARY KEY、FOREIGN KEY、UNIQUE、または CHECK 制約のプロパティを指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [ WITH FILLFACTOR = fillfactor ]   
        [ WITH ( index_option [, ...n ] ) ]  
        [ ON { partition_scheme_name (partition_column_name)   
            | filegroup | "default" } ]   
    | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name   
            [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>引数  
 CONSTRAINT  
 PRIMARY KEY、UNIQUE、FOREIGN KEY、または CHECK 制約の定義の開始を指定します。  
  
 *constraint_name*  
 制約の名前を指定します。 制約名は[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従う必要があります。ただし、番号記号 (#) で始めることはできません。 *constraint_name* を指定しない場合、この制約にはシステムによって生成された名前が割り当てられます。  
  
 NULL | NOT NULL  
 列に null 値を使用できるかどうかを指定します。 NULL 値を許可しない列は、既定値が指定されているときだけ追加できます。 新規列が NULL 値を許可し、既定値が指定されていない場合は、テーブル内のすべての行で、新しい列は NULL 値を格納します。 新規列が NULL 値を許可し、新規列と共に既定の定義が追加される場合、WITH VALUES オプションを使用して、テーブル内の既存の各行の新規列に既定値を格納できます。  
  
 新規列が NULL 値を許可しない場合、新規列と共に DEFAULT 定義を追加する必要があります。 新規列は、各既存の行の新規列に既定値と共に自動で読み込まれます。  
  
 列の追加を行うときにテーブルのデータ行に物理的な変更が必要な場合 (各行への DEFAULT 値の追加など)、ALTER TABLE の実行中、ロックはテーブルで保持されます。 これは、ロックが適用されている間にテーブルの内容を変更する機能に影響します。 一方、NULL 値を許可し、既定値を指定しない列の追加は、メタデータ操作に限られ、ロックは関係しません。  
  
 CREATE TABLE または ALTER TABLE を使用すると、データベースとセッションの設定は、列定義で使われているデータ型に NULL 値を許すかどうかの設定に影響を及ぼし、場合によっては、NULL 値を許すかどうかの設定をオーバーライドします。 計算列ではない場合は、常に列を明示的に NULL または NOT NULL として定義することをお勧めします。ユーザー定義データ型を使用する場合は、データ型に NULL 値を許すかどうかの既定の設定を列が使用できるようにすることをお勧めします。 詳細については、「[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。  
  
 PRIMARY KEY  
 一意のインデックスを使用して、指定した 1 つ以上の列にエンティティの整合性を強制する制約です。 PRIMARY KEY 制約は 1 つのテーブルに対して 1 つだけ作成できます。  
  
 UNIQUE  
 一意なインデックスによって、特定の 1 つ以上の列にエンティティの整合性を提供する制約です。  
  
 CLUSTERED | NONCLUSTERED  
 PRIMARY KEY 制約または UNIQUE 制約に対して、クラスター化インデックスまたは非クラスター化インデックスを作成することを指定します。 PRIMARY KEY 制約は既定では CLUSTERED です。 UNIQUE 制約の既定値は NONCLUSTERED です。  
  
 テーブルに既存のクラスター化制約またはクラスター化インデックスがある場合、CLUSTERED は指定できません。 テーブルにクラスター化制約またはクラスター化インデックスが既に存在する場合、PRIMARY KEY 制約には既定で NONCLUSTERED が適用されます。  
  
 **ntext**、**text**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、**xml**、**image** データ型の列を、インデックスの列として指定することはできません。  
  
 WITH FILLFACTOR **=** _fillfactor_  
 インデックス データの格納に使用される個々のインデックス ページを [!INCLUDE[ssDE](../../includes/ssde-md.md)] がどの程度埋めるかを指定します。 ユーザー定義の FILL FACTOR 値は、1 ～ 100 の範囲で指定できます。 値を指定しない場合の既定値は 0 です。  
  
> [!IMPORTANT]  
>  マニュアルには、WITH FILLFACTOR = *fillfactor* が PRIMARY KEY 制約または UNIQUE 制約に適用される唯一のインデックス オプションとして記述されていますが、これは旧バージョンとの互換性を維持するために記載されており、将来のリリースではこのような記述はなくなります。 ALTER TABLE の [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md) 句で他のインデックス オプションも指定できます。  
  
 ON { _partition_scheme_name_ **(** _partition_column_name_ **)**  | *filegroup* |  **"** default **"** } **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 制約に対して作成されるインデックスの格納場所を指定します。 *partition_scheme_name* を指定した場合、インデックスがパーティション分割され、分割後のパーティションは *partition_scheme_name* で指定したファイル グループにマップされます。 *filegroup* を指定すると、インデックスは指定されたファイル グループに作成されます。 **"** default **"** を指定するか、ON を指定しなかった場合、インデックスはテーブルと同じファイル グループに作成されます。 PRIMARY KEY 制約または UNIQUE 制約のクラスター化インデックスを追加する場合に ON を指定すると、クラスター化インデックスの作成時に、指定したファイル グループにテーブル全体が移動します。  
  
 ここでは、default はキーワードではありません。 default は、既定ファイル グループの識別子なので、ON **"** default **"** または ON **[** default **]** のように区切る必要があります。 **"** default **"** を指定する場合は、現在のセッションに対して QUOTED_IDENTIFIER オプションが ON になっている必要があります。 これが既定の設定です。 詳細については、「[SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)」をご覧ください。  
  
 FOREIGN KEY REFERENCES  
 列内のデータに対して参照整合性を提供する制約です。 FOREIGN KEY 制約では、列内の各値が、参照テーブル内の指定された列に含まれていることが必要となります。  
  
 *schema_name*  
 FOREIGN KEY 制約が参照するテーブルが属するスキーマの名前です。  
  
 *referenced_table_name*  
 FOREIGN KEY 制約によって参照されるテーブルを指定します。  
  
 *ref_column*  
 新しい FOREIGN KEY 制約によって参照される、かっこで囲んだ列です。  
  
 ON DELETE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }  
 変更対象のテーブル内の行に参照関係があり、参照先の行が親テーブルから削除された場合に、変更対象のテーブル内の行に対して実行する操作を指定します。 既定値は NO ACTION です。  
  
 NO ACTION  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] がエラーを生成し、親テーブルでの行の削除操作がロールバックされます。  
  
 CASCADE  
 親テーブルから行が削除された場合に、参照元テーブルからもその行が削除されます。  
  
 SET NULL  
 親テーブルの対応する行が削除された場合、外部キーを形成するすべての値が NULL に設定されます。 この制約を実行するには、外部キー列が NULL 値を使用できる必要があります。  
  
 SET DEFAULT  
 親テーブルの対応する行が削除された場合、外部キーを形成するすべての値が既定値に設定されます。 この制約を実行するには、すべての外部キー列に既定値が定義されている必要があります。 列で NULL 値が許容されており、既定値が明示的に設定されていない場合、NULL が列の暗黙的な既定値になります。  
  
 論理レコードを使用するマージ パブリケーションにテーブルを含める場合、CASCADE は使用しないでください。 論理レコードの詳細については、「[論理レコードによる関連行への変更をグループ化](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」を参照してください。  
  
 変更対象のテーブルに ON DELETE での INSTEAD OF トリガーが既に存在する場合は、ON DELETE CASCADE を定義できません。  
  
 たとえば、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで、**ProductVendor** テーブルに **Vendor** テーブルとの参照関係があるとします。 ここで、**ProductVendor.VendorID** 外部キーは **Vendor.VendorID** 主キーを参照します。  
  
 **Vendor** テーブルの行に対して DELETE ステートメントを実行し、**ProductVendor.VendorID** に対して ON DELETE CASCADE アクションが指定されている場合は、[!INCLUDE[ssDE](../../includes/ssde-md.md)] は **ProductVendor** テーブルの 1 つ以上の従属行を調べます。 従属行がある場合、**ProductVendor** テーブルの従属行が、**Vendor** テーブルで参照される行と共に削除されます。  
  
 これに対し、NO ACTION を指定した場合は、**ProductVendor** テーブルに Vendor テーブルの行を参照する行が 1 つでもあると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] ではエラーが発生し、**Vendor** テーブルの行に対する削除操作はロールバックされます。  
  
 ON UPDATE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }  
 変更対象のテーブル内の行が参照関係を持ち、親テーブルで参照先の行が更新された場合、変更対象のテーブル内の行に対して発生する操作を指定します。 既定値は NO ACTION です。  
  
 NO ACTION  
 NO ACTION を指定すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]でエラーが発生し、親テーブルの行の更新操作はロールバックされます。  
  
 CASCADE  
 親テーブルで行が更新された場合に、参照元のテーブルでも対応する行が更新されます。  
  
 SET NULL  
 親テーブルの対応する行が更新された場合、外部キーを形成するすべての値が NULL に設定されます。 この制約を実行するには、外部キー列が NULL 値を使用できる必要があります。  
  
 SET DEFAULT  
 親テーブルの対応する行が更新された場合、外部キーを形成するすべての値が既定値に設定されます。 この制約を実行するには、すべての外部キー列に既定値が定義されている必要があります。 列で NULL 値が許容されており、既定値が明示的に設定されていない場合、NULL が列の暗黙的な既定値になります。  
  
 論理レコードを使用するマージ パブリケーションにテーブルを含める場合、CASCADE は使用しないでください。 論理レコードの詳細については、「[論理レコードによる関連行への変更をグループ化](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」を参照してください。  
  
 変更対象のテーブルに ON UPDATE での INSTEAD OF トリガーが既に存在する場合は、ON UPDATE CASCADE、SET NULL、または SET DEFAULT を定義できません。  
  
 たとえば、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで、**ProductVendor** テーブルに **Vendor** テーブルとの参照関係があるとします。 ここで、**ProductVendor.VendorID** 外部キーは **Vendor.VendorID** 主キーを参照します。  
  
 UPDATE ステートメントを **Vendor** テーブルの行で実行した場合、ON UPDATE CASCADE 操作が **ProductVendor.VendorID** に指定されていると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では **ProductVendor** テーブルに 1 つ以上の従属行があるかどうかが確認されます。 従属行がある場合、**ProductVendor** テーブルの従属行が、**Vendor** テーブルで参照される行と共に更新されます。  
  
 これに対して、NO ACTION を指定した場合は、**ProductVendor** テーブルに Vendor テーブルの行を参照する行が 1 つでもあると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] ではエラーが発生し、**Vendor** テーブルの行に対する更新操作はロールバックされます。  
  
 NOT FOR REPLICATION  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 FOREIGN KEY 制約と CHECK 制約に対して指定できます。 制約でこの句を指定すると、レプリケーション エージェントが挿入、更新、削除操作を行う際に制約が適用されません。  
  
 CHECK  
 1 つ以上の列に入力できる値を制限することによってドメインの整合性を設定する制約です。  
  
 *logical_expression*  
 CHECK 制約で使用する論理式を指定します。この式は TRUE または FALSE を返します。 CHECK 制約と共に使用する *logical_expression* では他のテーブルを参照できませんが、同じテーブルで同じ行の他の列は参照できます。 この式では別名データ型は参照できません。  
  
## <a name="remarks"></a>Remarks  
 FOREIGN 制約または CHECK 制約を追加すると、WITH NOCHECK オプションが指定されない限り、既存のすべてのデータに対して、制約違反の確認が行われます。 違反がある場合、ALTER TABLE は失敗し、エラーが返されます。 既存の列に新しい PRIMARY KEY 制約または UNIQUE 制約を追加するとき、列内のデータは一意であることが必要です。 重複する値が見つかると、ALTER TABLE は失敗します。 PRIMARY KEY 制約または UNIQUE 制約を追加する場合、WITH NOCHECK オプションによる影響はありません。  
  
 PRIMARY KEY 制約と UNIQUE 制約では、それぞれインデックスが生成されます。 UNIQUE 制約と PRIMARY KEY 制約によって生成されるテーブル上のインデックスの個数は、999 個の非クラスター化インデックスと 1 つのクラスター化インデックスに収まる必要があります。 外部キー制約では、自動的にインデックスが生成されることはありません。 ただし、クエリ内で、一方のテーブルの外部キー制約内の列を、他方のテーブルの主キー列または一意なキー列と照合することによって、クエリ内の結合条件で外部キー列は頻繁に使用されます。 外部キー列のインデックスを使用すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]により、外部キー テーブルの関連データがすばやく検索されます。  
  
## <a name="examples"></a>使用例  
 例については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_definition &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-definition-transact-sql.md)  
  
  
