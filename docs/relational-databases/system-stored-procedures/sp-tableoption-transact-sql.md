---
title: sp_tableoption (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tableoption_TSQL
- sp_tableoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tableoption
ms.assetid: 0a57462c-1057-4c7d-bce3-852cc898341d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c72d07873e2e07ee7f6f095f677625a18cdb5a7
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982265"
---
# <a name="sp_tableoption-transact-sql"></a>sp_tableoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  ユーザー定義テーブルのオプション値を設定します。 sp_tableoption を使用すると、 **varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、 **xml**、 **text**、 **ntext**、 **image**、または大きなユーザー定義型の列を含むテーブルの行内での動作を制御できます。  
  
> [!IMPORTANT]  
>  text in row 機能は、将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 大きな値のデータを格納するには、 **varchar (max)** 、 **nvarchar (max)** 、および**varbinary (max)** の各データ型を使用することをお勧めします。  
  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_tableoption [ @TableNamePattern = ] 'table'   
     , [ @OptionName = ] 'option_name'   
     ,[ @OptionValue =] 'value'  
```  
  
## <a name="arguments"></a>引数  
 [@TableNamePattern =]'*table*'  
 ユーザー定義データベーステーブルの修飾名または修飾され名を指定します。 データベース名も含めてフル パスで指定した場合は、そのデータベース名は現在のデータベース名である必要があります。 複数のテーブルのテーブルオプションを同時に設定することはできません。 *テーブル*は**nvarchar (776)** ,、既定値はありません。  
  
 [@OptionName =]'*option_name*'  
 テーブル オプション名を指定します。 *option_name*は**varchar (35)** ,、既定値は NULL です。 *option_name* 、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|一括読み込み時のテーブルロック|無効である場合 (既定)、ユーザー定義テーブル上で行ロックを取得するための一括読み込み処理が行われます。 有効にすると、ユーザー定義テーブルの一括読み込みプロセスによって一括更新ロックが取得されます。|  
|行ロックの挿入|サポートされなくなりました。<br /><br /> このオプションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のロック動作には影響しません。また、既存のスクリプトおよびプロシージャとの互換性のためだけに含まれています。|  
|行内のテキスト|OFF または 0 (無効、既定値) の場合、現在の動作は変更されず、行内に BLOB は存在しません。<br /><br /> 指定した場合 @OptionValue が ON (有効) または 24 ~ 7000 の整数値の場合、新しい**text**、 **ntext**、または**image**文字列は、データ行に直接格納されます。 すべての既存の BLOB (バイナリラージオブジェクト: **text**、 **ntext**、または**IMAGE**データ) は、blob 値が更新されると、text in row 形式に変更されます。 詳細については、「解説」を参照してください。|  
|large value types out of row|1 = **varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、 **xml** 、および大きなユーザー定義型 (UDT) の列は、ルートへの16バイトのポインターと共に、行外に格納されます。<br /><br /> 0 = **varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、 **xml** 、および大きな UDT 値は、データ行に直接格納されます。ただし、値がレコードに収まりきらない限り、8000バイトの制限があります。 値がレコードに収まらない場合には、ポインターが行内に格納され、残りは行外の LOB ストレージ領域に格納されます。 0 が既定値です。<br /><br /> 大きなユーザー定義型 (UDT) は、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降に適用されます。 <br /><br /> [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)の TEXTIMAGE_ON オプションを使用して、大きなデータ型を格納する場所を指定します。 |  
|vardecimal ストレージ形式|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> TRUE、ON、または 1 の場合、指定されたテーブルでは vardecimal ストレージ形式が有効です。 FALSE、OFF、または0の場合、テーブルは vardecimal ストレージ形式に対して有効ではありません。 Vardecimal ストレージ形式は、データベースで[sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)を使用して vardecimal ストレージ形式が有効になっている場合にのみ有効にすることができます。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降では、 **vardecimal**ストレージ形式は非推奨とされます。 代わりに行の圧縮を使用してください。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。 0 が既定値です。|  
  
 [@OptionValue =]'*value*'  
 *Option_name*が有効 (TRUE、ON、または 1) であるか、無効 (FALSE、OFF、または 0) であるかを示します。 *値*は**varchar (12)** ,、既定値はありません。 *値*は大文字と小文字を区別しません。  
  
 text in row オプションの有効値は、0、ON、OFF、または 24 ～ 7,000 の整数です。 *値*が ON の場合、既定値は256バイトに制限されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) またはエラー番号 (失敗)  
  
## <a name="remarks"></a>Remarks  
 sp_tableoption は、ユーザー定義テーブルのオプション値を設定するためにのみ使用できます。 テーブルのプロパティを表示するには、OBJECTPROPERTY またはクエリのテーブルを使用します。  
  
 sp_tableoption の text in row オプションを有効または無効にできるのは、テーブルにテキスト列が含まれている場合だけです。 テーブルにテキスト列がない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってエラーが発生します。  
  
 Text in row オプションが有効になっている場合、@OptionValue パラメーターを使用すると、BLOB の行に格納される最大サイズをユーザーが指定できます。 既定値は256バイトですが、値の範囲は 24 ~ 7000 バイトです。  
  
 **text**型、 **ntext**型、または**image**型の文字列は、次の条件に該当する場合にデータ行に格納されます。  
  
-   text in row が有効になっています。  
  
-   文字列の長さが、に指定された制限値より短い @OptionValue  
  
-   データ行に十分な使用可能領域がある。  
  
 BLOB 文字列がデータ行に格納されている場合、 **text**、 **ntext**、または**image**文字列の読み取りと書き込みは、文字やバイナリ文字列の読み取りや書き込みと同じくらい高速に行うことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、BLOB 文字列の読み取りまたは書き込みを行うために別のページにアクセスする必要はありません。  
  
 **Text**、 **ntext**、または**image**型の文字列が、指定された制限値より大きいか、行内で使用可能な領域を超えている場合は、代わりにポインターが行内に格納されます。 ただし、BLOB 文字列を行に格納する場合の条件は引き続き適用されます。ただし、データ行にはポインターを格納するのに十分な領域が必要です。  
  
 テーブルの行に格納されている BLOB 文字列とポインターは、可変長文字列と同様に扱われます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、文字列またはポインターを格納するために必要なバイト数のみを使用します。  
  
 既存の BLOB 文字列は、text in row が最初に有効になったときにはすぐには変換されません。 文字列は、それらが更新されたときに初めて変換されます。 同様に、text in row オプションの制限値を大きくしても、データ行に既に存在する**text**、 **ntext**、または**image**型の文字列は、更新されるまで新しい制限に準拠するように変換されません。  
  
> [!NOTE]  
>  text in row オプションを無効にする、またはオプションの制限値を小さくした場合は、BLOB を変換する必要があります。したがって、変換される BLOB 文字列の数によっては、処理に時間がかかる場合があります。 変換処理中にテーブルがロックされます。  
  
 テーブル変数を返す関数を含むテーブル変数では、text in row オプションが既定のインライン制限256で自動的に有効になります。 このオプションは変更できません。  
  
 Text in row オプションは、TEXTPTR、WRITETEXT、UPDATETEXT、および READTEXT 関数をサポートしています。 ユーザーは、SUBSTRING () 関数を使用して BLOB の一部を読み取ることができますが、行内テキストポインターの期間と数の制限は、他のテキストポインターとは異なることに注意する必要があります。  
  
 テーブルを vardecimal ストレージ形式から通常の decimal ストレージ形式に戻すには、データベースを単純復旧モードにする必要があります。 復旧モードを変更すると、バックアップに必要なログ チェーンが途切れてしまいます。したがって、テーブルから vardecimal ストレージ形式を削除した後で、データベースの完全バックアップを作成する必要があります。  
  
 既存の LOB データ型の列 (text、ntext、または image) を小規模から中規模の大きな値型 (varchar (max)、nvarchar (max)、または varbinary (max)) に変換する場合は、ほとんどのステートメントで、パフォーマンスを最適化するために**large_value_types_out_of_row**を**1**に変更することを検討してください。 **Large_value_types_out_of_row**オプションの値が変更された場合、既存の varchar (max)、nvarchar (max)、varbinary (max)、および xml の値はすぐには変換されません。 文字列のストレージは、後で文字列が更新されたときに変更されます。 テーブルに挿入される新しい値は、有効なテーブル オプションに従って格納されます。 ただちに結果を得るには、データのコピーを作成してから、 **large_value_types_out_of_row**設定を変更した後でテーブルを再作成するか、または小 ~ 中規模の大きな値の型の列をそれぞれ更新して、文字列のストレージが有効なテーブルオプションで変更されるようにします。 更新または再作成の後でテーブルのインデックスを再構築し、テーブルを圧縮することを検討します。 
    
  
## <a name="permissions"></a>アクセス許可  
 Sp_tableoption を実行するには、テーブルに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-storing-xml-data-out-of-the-row"></a>A. XML データの行外への格納  
 次の例では、`HumanResources.JobCandidate` テーブルの**xml**データを行外に格納するように指定します。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'HumanResources.JobCandidate', 'large value types out of row', 1;  
```  
  
### <a name="b-enabling-vardecimal-storage-format-on-a-table"></a>b. テーブルでの vardecimal ストレージ形式の有効化  
 次の例では、`decimal` データ型を `vardecimal` ストレージ形式で格納するように `Production.WorkOrderRouting` テーブルを変更します。  

```sql  
USE master;  
GO  
-- The database must be enabled for vardecimal storage format  
-- before a table can be enabled for vardecimal storage format  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'Production.WorkOrderRouting',   
   'vardecimal storage format', 'ON';  
```  
  
## <a name="see-also"></a>参照  
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [ストアドプロシージャ&#40;のデータベースエンジン transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
