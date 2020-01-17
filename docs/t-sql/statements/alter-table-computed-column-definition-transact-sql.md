---
title: computed_column_definition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER TABLE statement
ms.assetid: 746eabda-3b4f-4940-b0b5-1c379f5cf7a5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7eaa4c35079d8eec49d7197778a01b7bac6cf9c1
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982041"
---
# <a name="alter-table-computed_column_definition-transact-sql"></a>ALTER TABLE computed_column_definition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) を使ってテーブルに追加された計算列のプロパティを指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
column_name AS computed_column_expression  
[ PERSISTED [ NOT NULL ] ]  
[   
    [ CONSTRAINT constraint_name ]  
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [ WITH FILLFACTOR = fillfactor ]  
        [ WITH ( <index_option> [, ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ) | filegroup   
            | "default" } ]  
    | [ FOREIGN KEY ]   
        REFERENCES ref_table [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE } ]   
        [ ON UPDATE { NO ACTION } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
]  
```  
  
## <a name="arguments"></a>引数  
*column_name*  
 変更、追加、または削除する列の名前を指定します。 *column_name* の有効文字数は、1 ～ 128 文字です。 **timestamp** データ型で作成された新しい列の場合、*column_name* は省略できます。 **timestamp** データ型の列に対して *column_name* を指定しない場合には、名前 **timestamp** が使われます。  
  
*computed_column_expression*  
 計算列の値を定義する式です。 計算列は仮想列であり、テーブル内に物理的に格納されている列ではありません。したがって、式を基にして同じテーブル内の別の列を使用して計算されます。 たとえば、計算列は cost AS price * qty のように定義できます。式には、非計算列の名前、定数、関数、変数、および 1 つ以上の演算子によってこれらを結合した組み合わせを使用できます。 サブクエリを式にすることはできません。また、別名データ型を含むこともできません。  
  
 計算列は、選択リスト、WHERE 句、ORDER BY 句、および正規表現を使用できるその他の場所で使用できます。ただし、次の場合は除きます。  
  
-   計算列は、DEFAULT 制約定義または FOREIGN KEY 制約定義として使用したり、NOT NULL 制約定義と共に使用したりすることはできません。 ただし、計算列の値が決定的な式によって定義され、その結果のデータ型がインデックス列で可能な場合、計算列は、インデックスのキー列として、または任意の PRIMARY KEY 制約または UNIQUE 制約の一部として使用できます。  
  
     たとえば、テーブルに整数型の列 a と b がある場合、計算列 a + b にはインデックスを作成できますが、計算列 a+DATEPART(dd, GETDATE()) にインデックスを作成することはできません。これは、この計算列の値が次以降の呼び出しで変更される可能性があるためです。  
  
-   計算列を INSERT ステートメントまたは UPDATE ステートメントの対象にすることはできません。  
  
    > [!NOTE]  
    >  テーブル内の各行は、計算列に含まれる列について、異なる値を格納している可能性があるため、計算列の結果がすべての行で同じとは限りません。  
  
PERSISTED  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]で、計算値をテーブルに物理的に保存し、依存する計算列のいずれかが更新された場合にその値を更新するように指定します。 計算列に PERSISTED とマークを付けることで、計算列に対し、完全ではないものの決定性のあるインデックスを作成することができます。 詳細については、「 [計算列のインデックス](../../relational-databases/indexes/indexes-on-computed-columns.md)」を参照してください。 パーティション テーブルのパーティション分割列として使用する計算列は、明示的に PERSISTED のマークを付ける必要があります。 PERSISTED が指定されている場合、*computed_column_expression* は決定的である必要があります。 

NULL | NOT NULL  
 列で NULL 値を許容するかどうかを指定します。 NULL は厳密には制約ではありませんが、NOT NULL と同じように指定することができます。 計算列で NOT NULL を指定できるのは、PERSISTED も指定した場合のみです。  
  
CONSTRAINT  
 PRIMARY KEY または UNIQUE 制約の定義の開始を指定します。  
  
*constraint_name*  
 新しい制約です。 制約名は[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従う必要があります。ただし、番号記号 (#) で始めることはできません。 *constraint_name* を指定しない場合、この制約にはシステムによって生成された名前が割り当てられます。  
  
PRIMARY KEY  
 一意のインデックスを使用して、指定した 1 つ以上の列にエンティティの整合性を強制する制約です。 PRIMARY KEY 制約は 1 つのテーブルに対して 1 つだけ作成できます。  
  
UNIQUE  
 一意なインデックスによって、指定した 1 つ以上の列にエンティティの整合性を持たせる制約です。  
  
CLUSTERED | NONCLUSTERED  
 PRIMARY KEY 制約または UNIQUE 制約に対して、クラスター化インデックスまたは非クラスター化インデックスを作成することを指定します。 PRIMARY KEY 制約は既定では CLUSTERED です。 UNIQUE 制約の既定値は NONCLUSTERED です。  
  
 テーブルに既存のクラスター化制約またはクラスター化インデックスがある場合、CLUSTERED は指定できません。 テーブルにクラスター化制約またはクラスター化インデックスが既に存在する場合、PRIMARY KEY 制約には既定で NONCLUSTERED が適用されます。  
  
WITH FILLFACTOR =*fillfactor*  
 インデックス データの格納に使用される個々のインデックス ページを [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] がどの程度埋めるかを指定します。 ユーザーが指定できる *fillfactor* の値は、1 ～ 100 です。 値を指定しない場合の既定値は 0 です。  
  
> [!IMPORTANT]  
>  マニュアルには、WITH FILLFACTOR = *fillfactor* が PRIMARY KEY 制約または UNIQUE 制約に適用される唯一のインデックス オプションとして記述されていますが、これは旧バージョンとの互換性を維持するために記載されており、将来のリリースではこのような記述はなくなります。 ALTER TABLE の [index_option &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md) 句で他のインデックス オプションも指定できます。  
  
FOREIGN KEY REFERENCES  
 1 つ以上の列内のデータに参照整合性を持たせる制約です。 FOREIGN KEY 制約では、列内の各値が、参照されるテーブル内の対応する参照される列 (1 つまたは複数) に存在している必要があります。 FOREIGN KEY 制約は、参照されるテーブル内の PRIMARY KEY 制約または UNIQUE 制約である列、または参照されるテーブルの UNIQUE INDEX で参照される列のみを参照できます。 計算列上の外部キーも、PERSISTED とマークする必要があります。  
  
*ref_table*  
 FOREIGN KEY 制約によって参照されるテーブルの名前です。  
  
(*ref_column*)  
 FOREIGN KEY 制約によって参照されるテーブルの列です。  
  
ON DELETE { **NO ACTION** | CASCADE }  
 テーブルの行が参照関係を持ち、参照される行が親テーブルから削除された場合に、その行に対して実行される操作を指定します。 既定値は NO ACTION です。  
  
NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] がエラーを生成し、親テーブルでの行の削除操作がロールバックされます。

CASCADE  
 親テーブルから行が削除された場合に、参照元テーブルからもその行が削除されます。  
  
 たとえば、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで、ProductVendor テーブルに Vendor テーブルとの参照関係があるとします。 ここで、ProductVendor.BusinessEntityID 外部キーは Vendor.BusinessEntityID 主キーを参照します。  
  
 DELETE ステートメントを Vendor テーブルの行で実行した場合、ON DELETE CASCADE アクションが ProductVendor.BusinessEntityID に対して指定されていると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では ProductVendor テーブルに 1 つ以上の従属行があるかどうかが確認されます。 従属行がある場合、ProductVendor テーブルの従属行が、Vendor テーブルで参照される行と共に削除されます。  
  
 これに対し、NO ACTION を指定した場合は、ProductVendor テーブルに Vendor テーブルの行を参照する行が 1 つでもあると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]ではエラーが発生し、Vendor テーブルの行に対する削除操作はロールバックされます。  
  
 論理レコードを使用するマージ パブリケーションにテーブルを含める場合、CASCADE は使用しないでください。 論理レコードの詳細については、「[論理レコードによる関連行への変更をグループ化](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」を参照してください。  
  
ON UPDATE { **NO ACTION** }  
 作成されたテーブル内の行が参照関係を持ち、親テーブルで参照先の行が更新された場合、作成されたテーブル内の行に対して発生する操作を指定します。 NO ACTION が指定されている場合、ProductVendor テーブルに Vendor テーブルの行を参照する行が 1 つでもあると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]でエラーが発生し、Vendor 行の更新操作がロールバックされます。  
  
NOT FOR REPLICATION  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 FOREIGN KEY 制約と CHECK 制約に対して指定できます。 制約でこの句を指定すると、レプリケーション エージェントが挿入、更新、削除操作を行う際に制約が適用されません。  
  
CHECK  
 1 つ以上の列に入力できる値を制限することによってドメインの整合性を設定する制約です。 計算列の CHECK 制約も、PERSISTED とマークする必要があります。  
  
*logical_expression*  
 TRUE または FALSE を返す論理式です。 この式には、別名データ型の参照を含めることはできません。  
  
ON { *partition_scheme_name*(*partition_column_name*) | *filegroup*| "default"}  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 制約に対して作成されるインデックスの格納場所を指定します。 *partition_scheme_name* を指定した場合、インデックスがパーティション分割され、分割後のパーティションは *partition_scheme_name* で指定したファイル グループにマップされます。 *filegroup* を指定すると、インデックスは指定されたファイル グループに作成されます。 "default" を指定するか、ON を指定しなかった場合、インデックスはテーブルと同じファイル グループに作成されます。 PRIMARY KEY 制約または UNIQUE 制約のクラスター化インデックスを追加する場合に ON を指定すると、クラスター化インデックスの作成時に、指定したファイル グループにテーブル全体が移動します。  
  
> [!NOTE]  
>  このコンテキストでは、default はキーワードではありません。 それは、既定ファイル グループの識別子なので、ON "default" または ON [default] のように区切る必要があります。 "default" を指定する場合は、現在のセッションに対して QUOTED_IDENTIFIER オプションが ON である必要があります。 これが既定の設定です。 詳細については、「[SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)」をご覧ください。  
  
## <a name="remarks"></a>Remarks  
 PRIMARY KEY 制約と UNIQUE 制約では、それぞれインデックスが生成されます。 UNIQUE 制約と PRIMARY KEY 制約によって生成されるテーブル上のインデックスの個数は、999 個の非クラスター化インデックスと 1 つのクラスター化インデックスに収まる必要があります。  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
