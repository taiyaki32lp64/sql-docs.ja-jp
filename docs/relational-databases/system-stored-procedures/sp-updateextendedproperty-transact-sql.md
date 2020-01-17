---
title: sp_updateextendedproperty (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updateextendedproperty_TSQL
- sp_updateextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updateextendedproperty
ms.assetid: 7f02360f-cb9e-48b4-b75f-29b4bc9ea304
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2f1c1c856cadbb4f005a99d5a5d49dc0c1280a8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898413"
---
# <a name="spupdateextendedproperty-transact-sql"></a>sp_updateextendedproperty (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  既存の拡張プロパティの値を更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_updateextendedproperty  
    [ @name = ]{ 'property_name' }   
    [ , [ @value = ]{ 'value' }  
        [, [ @level0type = ]{ 'level0_object_type' }  
         , [ @level0name = ]{ 'level0_object_name' }  
              [, [ @level1type = ]{ 'level1_object_type' }  
               , [ @level1name = ]{ 'level1_object_name' }  
                     [, [ @level2type = ]{ 'level2_object_type' }  
                      , [ @level2name = ]{ 'level2_object_name' }  
                     ]  
              ]  
        ]  
    ]  
```  
  
## <a name="arguments"></a>引数  
 [ @name=] {'*property_name*'}  
 更新するプロパティの名前です。 *property_name*は**sysname**NULL にすることはできません。  
  
 [ @value=] {'*値*'}  
 プロパティに関連付けられている値です。 *値*は**sql_variant**、既定値は NULL です。 サイズ*値*7,500 バイト以下ができない可能性があります。  
  
 [ @level0type=] {'*level0_object_type*'}  
 ユーザーまたはユーザー定義型です。 *level0_object_type*は**varchar (128)** 、既定値は NULL です。 有効な入力値は、アセンブリ、コントラクト、イベント通知、ファイル グループ、メッセージの種類、パーティション関数、パーティション構成、PLAN GUIDE、REMOTE SERVICE BINDING、ROUTE、スキーマ、サービス、ユーザー、トリガー、型、および NULL です。  
  
> [!IMPORTANT]  
>  USER および TYPE はレベル 0 の種類は、の将来のバージョンで削除される予定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。 USER の代わりに、レベル 0 の種類として SCHEMA を使用してください。 TYPE については、レベル 0 の種類として SCHEMA、レベル 1 の種類として TYPE を使用してください。  
  
 [ @level0name=] {'*level0_object_name*'}  
 指定したレベル 1 のオブジェクトの種類の名前です。 *level0_object_name*は**sysname**既定値は NULL です。  
  
 [ @level1type=] {'*level1_object_type*'}  
 レベル 1 のオブジェクトの種類です。 *level1_object_type*は**varchar (128)** 既定値は NULL です。 有効な入力値は、集計、既定値、関数、論理ファイル名、プロシージャ、キュー、ルール、シノニム、テーブル、TABLE_TYPE、タイプ、ビュー、XML スキーマ コレクション、および NULL です。  
  
 [ @level1name=] {'*level1_object_name*'}  
 指定したレベル 1 のオブジェクトの種類の名前です。 *level1_object_name*は**sysname**既定値は NULL です。  
  
 [ @level2type=] {'*level2_object_type*'}  
 レベル 2 のオブジェクトの型です。 *level2_object_type*は**varchar (128)** 既定値は NULL です。 有効な値は、COLUMN、CONSTRAINT、EVENT NOTIFICATION、INDEX、PARAMETER、TRIGGER、および NULL です。  
  
 [ @level2name=] {'*level2_object_name*'}  
 指定したレベル 2 のオブジェクトの種類の名前です。 *level2_object_name*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 内のオブジェクトの拡張プロパティを指定するために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースは、次の 3 つのレベル (0、1、および 2) に分類されます。 レベル 0 は、最上位のレベルし、データベース スコープに含まれるオブジェクトとして定義されます。 レベル 1 のオブジェクトはスキーマ スコープまたはユーザー スコープに含まれ、レベル 2 のオブジェクトはレベル 1 のオブジェクトに含まれます。 これら、どのレベルのオブジェクトに対しても、拡張プロパティを定義できます。 1 つのレベルにあるオブジェクトを参照する場合は、そのオブジェクトを所有または格納する上位レベルのオブジェクトの名前で修飾する必要があります。  
  
 指定する有効な*property_name*と*値*プロパティが更新されましたが、現在のデータベースに属するすべてのオブジェクトの種類および名前が null の場合。  
  
## <a name="permissions"></a>アクセス許可  
 固定データベース ロール db_owner および db_ddladmin のメンバーは、任意のオブジェクトの拡張プロパティを更新できます。ただし、例外として、db_ddladmin はデータベース自体、ユーザー、およびロールに対しては、プロパティを追加できません。  
  
 ユーザーは、拡張プロパティを更新できます所有するオブジェクトをおよび ALTER または CONTROL 権限を持ちます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-updating-an-extended-property-on-a-column"></a>A. 列の拡張プロパティを更新しています  
 次の例では、プロパティの値を更新する`Caption`列`ID`テーブルで`T1`します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
    @name = N'Caption'  
    ,@value = N'Employee ID'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
--Update the extended property.  
EXEC sp_updateextendedproperty   
    @name = N'Caption'  
    ,@value = 'Employee ID must be unique.'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
```  
  
### <a name="b-updating-an-extended-property-on-a-database"></a>B. データベースでの拡張プロパティを更新しています  
 次の例は最初に、拡張プロパティを作成、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]サンプル データベースし、そのプロパティの値を更新します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample OLTP Database';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_updateextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample Database';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.fn_listextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
