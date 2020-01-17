---
title: sp_addextendedproperty (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproperty
- sp_addextendedproperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproperty
ms.assetid: 565483ea-875b-4133-b327-d0006d2d7b4c
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2600543715bffaba36e29305b0893a9f17cca59c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072690"
---
# <a name="spaddextendedproperty-transact-sql"></a>sp_addextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  新しい拡張プロパティをデータベース オブジェクトに追加します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addextendedproperty  
    [ @name = ] { 'property_name' }  
    [ , [ @value = ] { 'value' }   
        [ , [ @level0type = ] { 'level0_object_type' }   
          , [ @level0name = ] { 'level0_object_name' }   
                [ , [ @level1type = ] { 'level1_object_type' }   
                  , [ @level1name = ] { 'level1_object_name' }   
                        [ , [ @level2type = ] { 'level2_object_type' }   
                          , [ @level2name = ] { 'level2_object_name' }   
                        ]   
                ]  
        ]   
    ]   
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @name ] = {'*property_name*'}  
 追加するプロパティの名前です。 *property_name*は**sysname** NULL にすることはできません。 名前には、空白や英数字以外の文字列、およびバイナリ値も含めることができます。  
  
 [ @value=] {'*値*'}  
 プロパティに関連する値です。 *値*は**sql_variant**、既定値は NULL です。 *value* のサイズは、7,500 バイト以下にする必要があります。  
  
 [ @level0type=] {'*level0_object_type*'}  
 レベル 0 のオブジェクトの型です。 *level0_object_type*は**varchar (128)** 、既定値は NULL です。  
  
 有効な値は、ASSEMBLY、CONTRACT、EVENT NOTIFICATION、FILEGROUP、MESSAGE TYPE、PARTITION FUNCTION、PARTITION SCHEME、REMOTE SERVICE BINDING、ROUTE、SCHEMA、SERVICE、USER、TRIGGER、TYPE、PLAN GUIDE、および NULL です。  
  
> [!IMPORTANT]  
>  レベル 1 の種類のオブジェクトの拡張プロパティで、USER をレベル 0 の種類として指定できる機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の将来のバージョンで削除されます。 代わりに、レベル 0 の種類として SCHEMA を使用してください。 たとえば、テーブルで拡張プロパティを定義するときに、ユーザー名の代わりにテーブルのスキーマを指定します。 レベル 0 の種類として TYPE を指定できる機能は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の将来のバージョンで削除されます。 TYPE については、レベル 0 の種類として SCHEMA、レベル 1 の種類として TYPE を使用してください。  
  
 [ @level0name=] {'*level0_object_name*'}  
 指定したレベル 0 のオブジェクトの種類の名前です。 *level0_object_name*は**sysname**既定値は NULL です。  
  
 [ @level1type=] {'*level1_object_type*'}  
 レベル 1 のオブジェクトの種類です。 *level1_object_type*は**varchar (128)** 、既定値は NULL です。 有効な入力値は、集計、既定値、関数、論理ファイル名、プロシージャ、キュー、ルール、シーケンス、シノニム、テーブル、TABLE_TYPE、型、ビュー、XML スキーマ コレクション、および NULL です。    
 [ @level1name=] {'*level1_object_name*'}  
 指定したレベル 1 のオブジェクトの種類の名前です。 *level1_object_name*は**sysname**、既定値は NULL です。  
  
 [ @level2type=] {'*level2_object_type*'}  
 レベル 2 のオブジェクトの型です。 *level2_object_type*は**varchar (128)** 、既定値は NULL です。 有効な値は、COLUMN、CONSTRAINT、EVENT NOTIFICATION、INDEX、PARAMETER、TRIGGER、および NULL です。  
  
 [ @level2name=] {'*level2_object_name*'}  
 指定したレベル 2 のオブジェクトの種類の名前です。 *level2_object_name*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 内のオブジェクトの拡張プロパティを指定するため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース 3 つのレベルに分類されます。0、1、および 2 です。 レベル 0 は、データベース スコープに含まれる最上位レベルのオブジェクトとして定義されます。 レベル 1 のオブジェクトはスキーマ スコープまたはユーザー スコープに含まれ、レベル 2 のオブジェクトはレベル 1 のオブジェクトに含まれます。 これら、どのレベルのオブジェクトに対しても、拡張プロパティを定義できます。  
  
 1 つのレベルにあるオブジェクトを参照する場合は、そのオブジェクトを所有または格納する上位レベルのオブジェクトの名前で修飾する必要があります。 たとえば、拡張プロパティをテーブル列 (レベル 2) に追加する場合、その列を含むテーブル名 (レベル 1) とそのテーブルを含むスキーマ (レベル 0) も指定する必要があります。  
  
 すべてのオブジェクトの種類および名前が NULL である場合、プロパティは現在のデータベースそのものに属します。  
  
 拡張プロパティは、システム オブジェクト、ユーザー定義データベースのスコープ外のオブジェクト、または「引数」で有効な入力として示されないオブジェクトでは使用できません。  
  
 拡張プロパティは、メモリ最適化テーブルでは許可されません。  
  
## <a name="replicating-extended-properties"></a>拡張プロパティのレプリケート  
 拡張プロパティは、パブリッシャーとサブスクライバー間で初期同期を実行するときにのみレプリケートされます。 初期同期の完了後に拡張プロパティを追加または変更した場合、その変更はレプリケートされません。 データベース オブジェクトをレプリケートする方法の詳細については、次を参照してください。[発行データおよびデータベース オブジェクト](../../relational-databases/replication/publish/publish-data-and-database-objects.md)します。  
  
## <a name="schema-vs-user"></a>スキーマとユーザー  
 名前解決にあいまいさが発生する可能性があるため、拡張プロパティをデータベース オブジェクトに適用するときに USER をレベル 0 の種類として指定することをお勧めしません。 たとえば、ユーザー Mary が 2 つのスキーマ (Mary と MySchema) を所有し、これらのスキーマの両方に MyTable という名前のテーブルがある場合を考えます。 Mary が拡張プロパティをテーブル MyTable に追加しを指定するかどうか **@level0type = N'USER'** 、  **@level0name = Mary**、拡張プロパティを適用するテーブルのチェック ボックスをオフにではなくなります。 旧バージョンとの互換性を維持するために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では Mary という名前のスキーマに含まれているテーブルにプロパティが適用されます。  
  
## <a name="permissions"></a>アクセス許可  
 固定サーバー ロール db_owner および db_ddladmin のメンバーは、任意のオブジェクトに拡張プロパティを追加できます。ただし、例外として、db_ddladmin はデータベース自体、ユーザー、またはロールにプロパティを追加できません。  
  
 ユーザーは、自身が所有するオブジェクトや、ALTER 権限または CONTROL 権限を持つオブジェクトの拡張プロパティを追加できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-adding-an-extended-property-to-a-database"></a>A. 拡張プロパティをデータベースに追加する  
 次の例では、値 `'Caption'` を持つプロパティ名 `'AdventureWorks2012 Sample OLTP Database'` を `AdventureWorks2012` サンプル データベースに追加します。  
  
```  
USE AdventureWorks2012;  
GO  
--Add a caption to the AdventureWorks2012 Database object itself.  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'AdventureWorks2012 Sample OLTP Database';  
```  
  
### <a name="b-adding-an-extended-property-to-a-column-in-a-table"></a>B. 拡張プロパティをテーブル内の列に追加する  
 次の例では、テーブル `PostalCode` 内の列 `Address`にタイトルのプロパティを追加します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'Postal code is a required column.',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table',  @level1name = 'Address',  
@level2type = N'Column', @level2name = 'PostalCode';  
GO  
```  
  
### <a name="c-adding-an-input-mask-property-to-a-column"></a>C. 定型入力プロパティを列に追加する  
 次の例では、定型入力プロパティ '`99999 or 99999-9999 or #### ###`' をテーブル `PostalCode` 内の列 `Address`に追加します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Input Mask ', @value = '99999 or 99999-9999 or #### ###',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table', @level1name = 'Address',   
@level2type = N'Column',@level2name = 'PostalCode';  
GO  
```  
  
### <a name="d-adding-an-extended-property-to-a-filegroup"></a>D. 拡張プロパティをファイル グループに追加する  
 次の例では、拡張プロパティが `PRIMARY` ファイル グループに追加されます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Primary filegroup for the AdventureWorks2012 sample database.',   
@level0type = N'FILEGROUP', @level0name = 'PRIMARY';  
GO  
```  
  
### <a name="e-adding-an-extended-property-to-a-schema"></a>E. 拡張プロパティをスキーマに追加する  
 次の例では、拡張プロパティが `HumanResources` スキーマに追加されます。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',  
@value = N'Contains objects related to employees and departments.',  
@level0type = N'SCHEMA',   
@level0name = 'HumanResources';  
```  
  
### <a name="f-adding-an-extended-property-to-a-table"></a>F. 拡張プロパティをテーブルに追加する  
 次の例では、拡張プロパティが `Address` スキーマ内の `Person` テーブルに追加されます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Street address information for customers, employees, and vendors.',   
@level0type = N'SCHEMA', @level0name = 'Person',  
@level1type = N'TABLE',  @level1name = 'Address';  
GO  
```  
  
### <a name="g-adding-an-extended-property-to-a-role"></a>G. 拡張プロパティをロールに追加する  
 次の例では、アプリケーション ロールが作成され、拡張プロパティがロールに追加されます。  
  
```  
USE AdventureWorks2012;   
GO  
CREATE APPLICATION ROLE Buyers  
WITH Password = '987G^bv876sPY)Y5m23';   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Application Role for the Purchasing Department.',  
@level0type = N'USER',  
@level0name = 'Buyers';  
```  
  
### <a name="h-adding-an-extended-property-to-a-type"></a>H. 拡張プロパティを型に追加する  
 次の例では、拡張プロパティが型に追加されます。  
  
```  
USE AdventureWorks2012;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Data type (alias) to use for any column that represents an order number. For example a sales order number or purchase order number.',   
@level0type = N'SCHEMA',   
@level0name = N'dbo',   
@level1type = N'TYPE',   
@level1name = N'OrderNumber';  
```  
  
### <a name="i-adding-an-extended-property-to-a-user"></a>I. 拡張プロパティをユーザーに追加する  
 次の例では、ユーザーが作成され、拡張プロパティがユーザーに追加されます。  
  
```  
USE AdventureWorks2012;   
GO  
CREATE USER CustomApp WITHOUT LOGIN ;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'User for an application.',   
@level0type = N'USER',   
@level0name = N'CustomApp';  
```  
  
## <a name="see-also"></a>参照  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.fn_listextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)  
  
  
