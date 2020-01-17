---
title: sp_help (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fb5e9a1ab72140a08423fa50c10eeb1f2d06ad79
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909091"
---
# <a name="sp_help-transact-sql"></a>sp_help (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベースオブジェクト ( **sysobjects**互換性ビューに一覧表示されているオブジェクト)、ユーザー定義データ型、またはデータ型に関する情報をレポートします。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'name'` は、 **sysobjects**内のオブジェクト、または**systypes**テーブル内のユーザー定義データ型の名前です。 *名前*は**nvarchar (** 776 **)** ,、既定値は NULL です。 データベース名は使用できません。  'Person.AddressType' や [Person.AddressType] など、2 つまたは 3 つの部分名を区切る必要があります。   
   
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 返される結果セットは、*名前*が指定されているかどうか、指定されているかどうか、およびデータベースオブジェクトがどのデータベースオブジェクトであるかによって異なります。  
  
1.  引数を指定せずに**sp_help**を実行すると、現在のデータベースに存在するすべての型のオブジェクトの概要情報が返されます。  
  
    |列名|データ型|[説明]|  
    |-----------------|---------------|-----------------|  
    |**名前**|**nvarchar(** 128 **)**|オブジェクト名です。|  
    |**所有者**|**nvarchar(** 128 **)**|オブジェクトの所有者 (これは、オブジェクトを所有するデータベースプリンシパルです。 既定値は、オブジェクトを含むスキーマの所有者です)。|  
    |**Object_type**|**nvarchar(** 31 **)**|オブジェクトの種類|  
  
2.  *名前*が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型またはユーザー定義データ型である場合、 **sp_help**はこの結果セットを返します。  
  
    |列名|データ型|[説明]|  
    |-----------------|---------------|-----------------|  
    |**Type_name**|**nvarchar(** 128 **)**|データ型の名前。|  
    |**Storage_type**|**nvarchar(** 128 **)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型名。|  
    |**[データ型]**|**smallint**|データ型の物理的な長さ (バイト単位)。|  
    |**Prec**|**int**|有効桁数 (桁数の合計数)。|  
    |**小数点以下桁数**|**int**|小数点の右側の桁数。|  
    |**NULL 値の使用**|**varchar(** 35 **)**|NULL 値が許可されるかどうかを示します。 Yes または No。|  
    |**Default_name**|**nvarchar(** 128 **)**|このデータ型にバインドされた既定値の名前です。<br /><br /> NULL = 既定値がバインドされていません。|  
    |**Rule_name**|**nvarchar(** 128 **)**|このデータ型にバインドされたルールの名前です。<br /><br /> NULL = 既定値がバインドされていません。|  
    |**[照合順序]**|**sysname**|データ型の照合順序。 文字以外のデータ型の場合は NULL です。|  
  
3.  *名前*がデータ型以外のデータベースオブジェクトである場合、 **sp_help**は、指定されたオブジェクトの型に基づいて、この結果セットと追加の結果セットを返します。  

    |列名|データ型|[説明]|  
    |-----------------|---------------|-----------------|  
    |**名前**|**nvarchar(** 128 **)**|テーブル名|  
    |**所有者**|**nvarchar(** 128 **)**|テーブルの所有者|  
    |**種類**|**nvarchar(** 31 **)**|テーブルの種類です。|  
    |**Created_datetime**|**datetime**|作成された日付テーブル|  
  
     指定されたデータベースオブジェクトによっては、 **sp_help**によって追加の結果セットが返されます。  
  
     *Name*がシステムテーブル、ユーザーテーブル、またはビューの場合、 **sp_help**は次の結果セットを返します。 ただし、ビューに対しては、データ ファイルがファイル グループ内のどこに配置されているかを表す結果セットは返されません。  
  
    -   列オブジェクトに関して次の結果セットが返されます。  
  
        |列名|データ型|[説明]|  
        |-----------------|---------------|-----------------|  
        |**Column_name**|**nvarchar(** 128 **)**|列名|  
        |**種類**|**nvarchar(** 128 **)**|列のデータ型。|  
        |**L8**|**varchar(** 35 **)**|列の値が計算されるかどうかを示します。 Yes または No。|  
        |**[データ型]**|**int**|列の長さ (バイト単位)。<br /><br /> 注: 列のデータ型が大きな値の型 (**varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、または**xml**) の場合、値は-1 と表示されます。|  
        |**Prec**|**char(** 5 **)**|列の有効桁数。|  
        |**小数点以下桁数**|**char(** 5 **)**|列の小数点以下桁数です。|  
        |**NULL 値の使用**|**varchar(** 35 **)**|列で NULL 値を使用できるかどうかを示します。 Yes または No。|  
        |**TrimTrailingBlanks**|**varchar(** 35 **)**|末尾の空白をトリミングします。 Yes または No を返します。|  
        |**FixedLenNullInSource**|**varchar(** 35 **)**|これは旧バージョンとの互換性のためにだけ用意されています。|  
        |**[照合順序]**|**sysname**|列の照合順序。 非文字データ型の場合は NULL です。|  
  
    -   Id 列に対して次の結果セットが返されます。  
  
        |列名|データ型|[説明]|  
        |-----------------|---------------|-----------------|  
        |**Identity**|**nvarchar(** 128 **)**|データ型が id として宣言されている列の名前。|  
        |**シード**|**numeric**|Id 列の開始値。|  
        |**Increment**|**numeric**|この列の値に使用する増分です。|  
        |**[レプリケーションでは使用しない]**|**int**|**Sqlrepl**などのレプリケーションログインでテーブルにデータを挿入するときに、IDENTITY プロパティは適用されません。<br /><br /> 1 = True<br /><br /> 0 = False|  
  
    -   列に対して次の結果セットが返されます。  
  
        |列名|データ型|[説明]|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|一意なグローバル識別子列の名前です。|  
  
    -   ファイルグループで返される追加の結果セット:  
  
        |列名|データ型|[説明]|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**nvarchar(** 128 **)**|データが配置されているファイルグループ: プライマリ、セカンダリ、またはトランザクションログ。|  
  
    -   インデックスに対して次の結果セットが返されます。  
  
        |列名|データ型|[説明]|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|インデックス名。|  
        |**Index_description**|**varchar(** 210 **)**|インデックスの説明です。|  
        |**index_keys**|**nvarchar(** 2078 **)**|インデックスが作成される列の名前。 XVelocity メモリ最適化列ストアインデックスの場合は NULL を返します。|  
  
    -   制約に関して次の結果セットが返されます。  
  
        |列名|データ型|[説明]|  
        |-----------------|---------------|-----------------|  
        |**constraint_type**|**nvarchar(** 146 **)**|制約の種類。|  
        |**constraint_name**|**nvarchar(** 128 **)**|制約の名前。|  
        |**delete_action**|**nvarchar(** 9 **)**|DELETE 操作が NO_ACTION、CASCADE、SET_NULL、SET_DEFAULT、該当なし、のどれであるかを示します。<br /><br /> ただし、FOREIGN KEY 制約にだけ適用されます。|  
        |**update_action**|**nvarchar(** 9 **)**|更新アクションが NO_ACTION、CASCADE、SET_NULL、SET_DEFAULT、または N/A のいずれであるかを示します。<br /><br /> ただし、FOREIGN KEY 制約にだけ適用されます。|  
        |**status_enabled**|**varchar(** 8 **)**|制約が有効であるかどうかを示します。この値は Enabled、Disabled、N/A のいずれかです。<br /><br /> CHECK 制約と FOREIGN KEY 制約にのみ適用されます。|  
        |**status_for_replication**|**varchar(** 19 **)**|制約がレプリケーションを対象とするのかどうかを示します。<br /><br /> CHECK 制約と FOREIGN KEY 制約にのみ適用されます。|  
        |**constraint_keys**|**nvarchar(** 2078 **)**|制約を構成する列の名前です。デフォルトおよびルールの場合は、デフォルトまたはルールを定義するテキストです。|  
  
    -   参照しているオブジェクトについて、追加の結果セットが返されます。  
  
        |列名|データ型|[説明]|  
        |-----------------|---------------|-----------------|  
        |**テーブルの参照元**|**nvarchar(** 516 **)**|テーブルを参照する他のデータベースオブジェクトを識別します。|  
  
    -   ストアド プロシージャ、関数、または拡張ストアド プロシージャに関して次の結果セットが返されます。  
  
        |列名|データ型|[説明]|  
        |-----------------|---------------|-----------------|  
        |**Parameter_name**|**nvarchar(** 128 **)**|ストアドプロシージャのパラメーター名。|  
        |**種類**|**nvarchar(** 128 **)**|ストアドプロシージャパラメーターのデータ型。|  
        |**[データ型]**|**smallint**|物理ストレージの最大長 (バイト単位)。|  
        |**Prec**|**int**|桁数または合計桁数。|  
        |**小数点以下桁数**|**int**|小数点の右側の桁数。|  
        |**Param_order**|**smallint**|パラメーターの順番です。|  
  
## <a name="remarks"></a>Remarks  
 **Sp_help**プロシージャは、現在のデータベースでのみオブジェクトを検索します。  
  
 *名前*が指定されていない場合**sp_help**現在のデータベース内のすべてのオブジェクトのオブジェクト名、所有者、およびオブジェクトの種類が一覧表示されます。 **sp_helptrigger**は、トリガーに関する情報を提供します。  
  
 **sp_help**は、順序付け可能インデックス列のみを公開します。そのため、XML インデックスや空間インデックスに関する情報は公開されません。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 ユーザーは、 *objname*に対して少なくとも1つのアクセス許可を持っている必要があります。 列の制約キー、既定値、またはルールを表示するには、テーブルに対する VIEW DEFINITION 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-information-about-all-objects"></a>A. すべてのオブジェクトに関する情報を返す  
 次の例では、`master` データベース内の各オブジェクトに関する情報を一覧表示します。  
  
```  
USE master;  
GO  
EXEC sp_help;  
GO  
```  
  
### <a name="b-returning-information-about-a-single-object"></a>b. 1つのオブジェクトに関する情報を返す  
 次の例では、`Person` テーブルに関する情報を表示します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help 'Person.Person';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベース エンジン ストアド プロシージャ&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [transact-sql &#40;  の&#41; sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)  
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [システム&#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  
