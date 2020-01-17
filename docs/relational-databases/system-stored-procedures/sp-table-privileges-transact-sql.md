---
title: sp_table_privileges (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_table_privileges
- sp_table_privileges_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges
ms.assetid: 0512e688-4fc0-4557-8dc8-016672c1e3fe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 595f8adb46602109751b1912feed99ae4702fb55
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702842"
---
# <a name="sptableprivileges-transact-sql"></a>sp_table_privileges (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定されたテーブルのテーブル権限 (INSERT、DELETE、UPDATE、SELECT、REFERENCES など) の一覧を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_table_privileges [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @table_name= ] '*table_name*'  
 カタログ情報を返すために使用するテーブルを指定します。 *table_name*は**nvarchar (** 384 **)** ,、既定値はありません。 ワイルドカードパターンマッチングがサポートされています。  
  
 [ @table_owner= ] '*table_owner*'  
 カタログ情報を返すために使用するテーブルのテーブル所有者を示します。 *table_owner*は**nvarchar (** 384 **)** ,、既定値は NULL です。 ワイルドカードパターンマッチングがサポートされています。 所有者が指定されていない場合は、基になる DBMS の既定のテーブル可視性ルールが適用されます。  
  
 現在のユーザーが指定された名前のテーブルを所有している場合、そのテーブルの列が返されます。 *Owner*が指定されておらず、現在のユーザーが指定された*名前*のテーブルを所有していない場合、このプロシージャは、データベース所有者が所有する、指定された*table_name*を持つテーブルを検索します。 そのテーブルが存在する場合、そのテーブルの列が返されます。  
  
 [ @table_qualifier= ] '*table_qualifier*'  
 テーブル修飾子の名前を指定します。 *table_qualifier*は**sysname**,、既定値は NULL です。 さまざまな DBMS 製品では、3部構成のテーブル名 (*qualifier.owner.name*) がサポートしています。 で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は、この列はデータベース名を表します。 一部の製品では、テーブルのデータベース環境のサーバー名を表します。  
  
 [ @fUsePattern=] '*fusepattern*'  
 アンダースコア (_)、パーセント (%)、および角かっこ ([または]) の各文字がワイルドカード文字として解釈されるかどうかを決定します。 有効な値は 0 (パターン一致がオフ) および 1 (パターン一致がオン) です。 *Fusepattern*は**ビット**,、既定値は1です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|テーブル修飾子の名前。 で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は、この列はデータベース名を表します。 このフィールドは NULL にすることができます。|  
|TABLE_OWNER|**sysname**|テーブル所有者の名前。 このフィールドは常に値を返します。|  
|TABLE_NAME|**sysname**|テーブル名です。 このフィールドは常に値を返します。|  
|GRANTOR|**sysname**|この TABLE_NAME の権限を、表示される GRANTEE に与えたデータベース ユーザーの名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この列は常に TABLE_OWNER と同じです。 このフィールドは常に値を返します。 また、権限の許可者の列は、データベース所有者 (TABLE_OWNER) か、GRANT ステートメントで WITH GRANT OPTION 句を使用してデータベース所有者が権限を許可したユーザーのいずれかである可能性があります。|  
|GRANTEE|**sysname**|この TABLE_NAME の権限を、表示される GRANTOR によって与えられたデータベース ユーザーの名前。 で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は、この列には常に、database_principalssystem ビューのデータベースユーザーが含まれています。 このフィールドは常に値を返します。|  
|PRIVILEGE|**sysname**|使用可能なテーブル権限の 1 つ。 テーブル権限は、次に挙げる値 (または実装が定義されるときにデータ ソースによってサポートされるその他の値) のいずれかになります。<br /><br /> SELECT。GRANTEE は、1 列以上のデータを取得できます。<br /><br /> INSERT。GRANTEE は、新しい行の 1 列以上にデータを提供できます。<br /><br /> UPDATE。GRANTEE は、1 列以上の既存のデータを修正できます。<br /><br /> DELETE。GRANTEE は、テーブルから行を削除できます。<br /><br /> REFERENCES。GRANTEE は、主キー/外部キーのリレーションシップで外部テーブル内の列を参照できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、主キー/外部キーのリレーションシップはテーブル制約で定義されます。<br /><br /> 特定のテーブル特権によって GRANTEE に与えられる操作の範囲は、データ ソースに依存します。 たとえば、UPDATE 特権の場合、GRANTEE は、あるデータ ソース上ではテーブルのすべての列を更新することが許可されても、別のデータ ソース上では、GRANTOR が UPDATE 特権を持っている列しか更新できないことがあります。|  
|IS_GRANTABLE|**sysname**|GRANTEE が他のユーザーに権限を与えることが許可されているかどうかを示します。これは "許可の許可" 権限とも呼ばれます。 YES、NO、または NULL を指定できます。 不明な値 (NULL) は、"grant with grant" が適用されないデータソースを指しています。|  
  
## <a name="remarks"></a>コメント  
 sp_table_privileges ストアド プロシージャは、ODBC の SQLTablePrivileges に相当します。 返される結果は、TABLE_QUALIFIER、TABLE_OWNER、TABLE_NAME、PRIVILEGE の値に従って並べ替えられます。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、という単語`Contact`で始まる名前を持つすべてのテーブルに関する特権情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_table_privileges   
   @table_name = 'Contact%';  
```  
  
## <a name="see-also"></a>関連項目  
 [カタログストアドプロシージャ&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
