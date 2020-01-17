---
title: CREATE FULLTEXT CATALOG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CATALOG_TSQL
- CREATE_FULLTEXT_TSQL
- FULLTEXT_TSQL
- FULLTEXT CATALOG
- CREATE FULLTEXT CATALOG
- CREATE_FULLTEXT_CATALOG_TSQL
- CATALOG
- FULLTEXT_CATALOG_TSQL
- CREATE FULLTEXT
- FULLTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- CREATE FULLTEXT CATALOG statement
ms.assetid: d7a8bd93-e2d7-4a40-82ef-39069e65523b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1e8fa047a65663f918bfcce4a92692f1c443f77a
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064661"
---
# <a name="create-fulltext-catalog-transact-sql"></a>CREATE FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベースのフルテキスト カタログを作成します。 1 つのフルテキスト カタログには複数のフルテキスト インデックスを格納できますが、1 つのフルテキスト インデックスは 1 つのフルテキスト カタログにしか格納できません。 各データベースには、任意の数のフルテキスト カタログを格納できます。  
  
 **master**、**model**、または **tempdb** の各データベースには、フルテキスト カタログは作成できません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降では、フルテキスト カタログは仮想オブジェクトであり、ファイル グループには属しません。 フルテキスト カタログは、フルテキスト インデックスのグループを指す論理的概念です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE FULLTEXT CATALOG catalog_name  
     [ON FILEGROUP filegroup ]  
     [IN PATH 'rootpath']  
     [WITH <catalog_option>]  
     [AS DEFAULT]  
     [AUTHORIZATION owner_name ]  
  
<catalog_option>::=  
     ACCENT_SENSITIVITY = {ON|OFF}  
  
```  
  
## <a name="arguments"></a>引数  
 *catalog_name*  
 新しいカタログの名前を指定します。 このカタログ名は、現在のデータベース内にあるすべてのカタログ名の中で一意であることが必要です。 また、フルテキスト カタログに対応するファイルの名前 (ON FILEGROUP を参照) は、データベース内にある全ファイルの中で一意であることが必要です。 指定したカタログ名が、データベース内の別のカタログで既に使用されている場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はエラーを返します。  
  
 カタログ名は半角 120 文字以内で指定してください。  
  
 ON FILEGROUP *filegroup*  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、この句は無効です。  
  
 IN PATH **'** _rootpath_ **'**  
 > [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、この句は無効です。  
  
 ACCENT_SENSITIVITY = {ON|OFF}  
 カタログのフルテキスト インデックス作成でアクセントを区別するかどうかを指定します。 このプロパティを変更すると、インデックスの再構築が必要になります。 既定では、データベースの照合順序の指定に従って、アクセントの区別が決定されます。 データベースの照合順序を表示するには、**sys.databases** カタログ ビューを使います。  
  
 フルテキスト カタログのアクセントの区別に関する現在のプロパティ設定を確認するには、*catalog_name* に対して、FULLTEXTCATALOGPROPERTY 関数を **accentsensitivity** プロパティ値と共に使用します。 値 '1' が返された場合、フルテキスト カタログではアクセントが区別され、値 '0' が返された場合、アクセントは区別されません。  
  
 AS DEFAULT  
 カタログが既定のカタログであることを指定します。 フルテキスト カタログを明示的に指定せずにフルテキスト インデックスを作成するときには、既定のカタログが使用されます。 既存のフルテキスト カタログが既に AS DEFAULT となっている場合、この新しいカタログを AS DEFAULT として設定すると、新しいカタログが既定のフルテキスト カタログになります。  
  
 AUTHORIZATION *owner_name*  
 フルテキスト カタログの所有者として、データベース ユーザーまたはロールの名前を設定します。 *owner_name* がロールの場合、現在のユーザーがメンバーとなっているロールの名前を指定するか、ステートメントを実行するユーザーがデータベース所有者またはシステム管理者であることが必要です。  
  
 *owner_name* がユーザー名の場合、次のいずれかを指定する必要があります。  
  
-   ステートメントを実行するユーザーの名前。  
  
-   コマンドを実行するユーザーが持つ借用権限に対応するユーザーの名前。  
  
-   コマンドを実行するユーザーがデータベース所有者またはシステム管理者であること。  
  
 *owner_name* には、指定したフルテキスト カタログの TAKE OWNERSHIP 権限も与えられている必要があります。  
  
## <a name="remarks"></a>Remarks  
 フルテキスト カタログ ID は、00005 から始まり、新しいカタログが作成されるたびに 1 ずつ増加します。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、データベースに対して CREATE FULLTEXT CATALOG 権限を持つか、**db_owner** 固定データベース ロールまたは **db_ddladmin** 固定データベース ロールのメンバーであることが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、フルテキスト カタログとフルテキスト インデックスを作成します。  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume) KEY INDEX PK_JobCandidate_JobCandidateID;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sys.fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)   
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 
  
  
