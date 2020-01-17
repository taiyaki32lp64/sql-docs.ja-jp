---
title: table_constraint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table_constraint
ms.assetid: ac2a11e0-cc77-4e27-b107-4fe5bc6f5195
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 92e12a2991d03c125e3247d1dd681b0a5754e2f9
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981991"
---
# <a name="alter-table-table_constraint-transact-sql"></a>ALTER TABLE table_constraint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) を使用してテーブルに追加される PRIMARY KEY、UNIQUE、FOREIGN KEY、CHECK 制約、または DEFAULT 定義のプロパティを指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        [ WITH ( <index_option>[ , ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ... )  
          | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )  
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | CONNECTION
        ( { node_table TO node_table } 
          [ , {node_table TO node_table }]
          [ , ...n ]
        )
        [ ON DELETE { NO ACTION | CASCADE } ]
    | DEFAULT constant_expression FOR column [ WITH VALUES ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>引数  
 CONSTRAINT  
 PRIMARY KEY 制約、UNIQUE 制約、FOREIGN KEY 制約、CHECK 制約、または DEFAULT の定義の開始を指定します。  
  
 *constraint_name*  
 制約の名前を指定します。 制約名は[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従う必要があります。ただし、番号記号 (#) で始めることはできません。 constraint_name を指定しない場合、この制約にはシステムによって生成された名前が割り当てられます。  
  
 PRIMARY KEY  
 一意のインデックスを使用して、指定した 1 つ以上の列にエンティティの整合性を強制する制約です。 PRIMARY KEY 制約は 1 つのテーブルに対して 1 つだけ作成できます。  
  
 UNIQUE  
 一意なインデックスによって、特定の 1 つ以上の列にエンティティの整合性を提供する制約です。  
  
 CLUSTERED | NONCLUSTERED  
 PRIMARY KEY 制約または UNIQUE 制約に対して、クラスター化インデックスまたは非クラスター化インデックスを作成することを指定します。 PRIMARY KEY 制約は既定では CLUSTERED です。 UNIQUE 制約の既定値は NONCLUSTERED です。  
  
 テーブルに既存のクラスター化制約またはクラスター化インデックスがある場合、CLUSTERED は指定できません。 テーブルにクラスター化制約またはクラスター化インデックスが既に存在する場合、PRIMARY KEY 制約には既定で NONCLUSTERED が適用されます。  
  
 **ntext**、**text**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、**xml**、**image** データ型の列を、インデックスの列として指定することはできません。  
  
 *column*  
 新しい制約で使用される列または列の一覧を指定します。一覧の場合はかっこで囲みます。  
  
 [ **ASC** | DESC ]  
 テーブル制約に参加している 1 つ以上の列が並べ替えられる順序を指定します。 既定値は ASC です。  
  
 WITH FILLFACTOR **=** _fillfactor_  
 インデックス データの格納に使用される個々のインデックス ページを [!INCLUDE[ssDE](../../includes/ssde-md.md)] がどの程度埋めるかを指定します。 ユーザーが指定できる *fillfactor* の値は、1 ～ 100 です。 値を指定しない場合の既定値は 0 です。  
  
> [!IMPORTANT]  
>  マニュアルには、WITH FILLFACTOR = *fillfactor* が PRIMARY KEY 制約または UNIQUE 制約に適用される唯一のインデックス オプションとして記述されていますが、これは旧バージョンとの互換性を維持するために記載されており、将来のリリースではこのような記述はなくなります。 ALTER TABLE の [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md) 句で他のインデックス オプションも指定できます。  
  
 ON { _partition\_scheme\_name_ **(** _partition\_column\_name_ **)**  | _filegroup_|  **"** default **"** }  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 制約に対して作成されるインデックスの格納場所を指定します。 *partition_scheme_name* を指定した場合、インデックスがパーティション分割され、分割後のパーティションは *partition_scheme_name* で指定したファイル グループにマップされます。 *filegroup* を指定すると、インデックスは指定されたファイル グループに作成されます。 **"** default **"** を指定するか、ON を指定しなかった場合、インデックスはテーブルと同じファイル グループに作成されます。 PRIMARY KEY 制約または UNIQUE 制約のクラスター化インデックスを追加する場合に ON を指定すると、クラスター化インデックスの作成時に、指定したファイル グループにテーブル全体が移動します。  
  
 ここでは、default はキーワードではなく既定のファイル グループの識別子であり、ON **"** default **"** または ON **[** default **]** のように区切る必要があります。 **"** default **"** を指定する場合は、現在のセッションに対して QUOTED_IDENTIFIER オプションが ON になっている必要があります。 これが既定の設定です。  
  
 FOREIGN KEY REFERENCES  
 列内のデータに対して参照整合性を提供する制約です。 FOREIGN KEY 制約では、列内の各値が、参照テーブル内の指定された列に含まれていることが必要となります。  
  
 *referenced_table_name*  
 FOREIGN KEY 制約によって参照されるテーブルを指定します。  
  
 *ref_column*  
 新しい FOREIGN KEY 制約によって参照される列または列のリストを指定します。リストの場合はかっこで囲みます。  
  
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
  
 変更するテーブルに INSTEAD OF トリガーの ON DELETE が既に存在する場合、ON DELETE CASCADE を定義することはできません。  
  
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
 親テーブルの対応する行が更新された場合、外部キーを形成するすべての値が既定値に設定されます。 この制約を実行するには、すべての外部キー列に既定値が定義されている必要があります。 列が NULL 値を許容し、明示的な既定値が設定されていない場合は、列の既定値として NULL が暗黙的に使用されます。  
  
 論理レコードを使用するマージ パブリケーションにテーブルを含める場合、CASCADE は使用しないでください。 論理レコードの詳細については、「[論理レコードによる関連行への変更をグループ化](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」を参照してください。  
  
 変更対象のテーブルに ON UPDATE での INSTEAD OF トリガーが既に存在する場合は、ON UPDATE CASCADE、SET NULL、または SET DEFAULT を定義できません。  
  
 たとえば、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで、**ProductVendor** テーブルに **Vendor** テーブルとの参照関係があるとします。 ここで、**ProductVendor.VendorID** 外部キーは **Vendor.VendorID** 主キーを参照します。  
  
 UPDATE ステートメントを **Vendor** テーブルの行で実行した場合、ON UPDATE CASCADE 操作が **ProductVendor.VendorID** に指定されていると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では **ProductVendor** テーブルに 1 つ以上の従属行があるかどうかが確認されます。 従属行が存在する場合、**Vendor** テーブル内の参照先の行に加えて、**ProductVendor** テーブル内の従属行も更新されます。  
  
 これに対して、NO ACTION を指定した場合は、**ProductVendor** テーブルに Vendor テーブルの行を参照する行が 1 つでもあると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] ではエラーが発生し、**Vendor** テーブルの行に対する更新操作はロールバックされます。  
  
 NOT FOR REPLICATION  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 FOREIGN KEY 制約と CHECK 制約に対して指定できます。 制約でこの句を指定すると、レプリケーション エージェントが挿入、更新、削除操作を行う際に制約が適用されません。  

 CONNECTION 特定のエッジ制約が接続を許可されるノード テーブルのペアを指定します。 ON DELETE では、エッジ テーブルのエッジ経由で接続されたノードが削除されたとき、そのエッジ テーブルの行に対して行われる動作が指定されます。 
 
 DEFAULT  
 列の既定値を指定します。 DEFAULT 定義を使用すると、既存のデータ行に新しい列の値を設定できます。 DEFAULT 定義は、**timestamp** データ型、IDENTITY プロパティ、既存の DEFAULT 定義、またはバインドされている既定値が指定されている列には追加できません。 列に既定値が既に存在する場合、新しい既定値を追加するには既存の既定値をあらかじめ削除する必要があります。 ユーザー定義型の列に既定値を指定する場合は、その型で *constant_expression* 型からユーザー定義型への暗黙的な変換がサポートされている必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の旧バージョンとの互換性を保つため、DEFAULT に制約名を割り当てることができます。  
  
 *constant_expression*  
 リテラル値、NULL 値、または列の既定値として使用するシステム関数を指定します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ユーザー定義型として定義されている列と共に *constant_expression* を使用する場合は、その型を実装したときに、*constant_expression* からユーザー定義型への暗黙的な変換がサポートされる必要があります。  
  
 FOR *column*  
 テーブル レベルの DEFAULT 定義に関連付けられた列を指定します。  
  
 WITH VALUES  
 DEFAULT 制約と共に列を追加する際に列が NULL を許容している場合、WITH VALUES を使用すると、既存の行の新しい列の値は DEFAULT の *constant_expression* で指定される値に設定されます。 追加する列が NULL を許容していない場合、既存の行のその列の値は常に DEFAULT の *constant expression* で指定される値に設定されます。 SQL Server 2012 以降、これはメタ データの操作 [adding-not-null-columns-as-an-online-operation](alter-table-transact-sql.md?view=sql-server-2017#adding-not-null-columns-as-an-online-operation) である場合があります。
関連する列が追加されない場合にこれを使用しても、影響はありません。 
  
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
  
  
