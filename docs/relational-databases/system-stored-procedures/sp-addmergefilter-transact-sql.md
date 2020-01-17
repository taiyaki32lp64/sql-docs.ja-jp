---
title: sp_addmergefilter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergefilter
- sp_addmergefilter_TSQL
helpviewer_keywords:
- sp_addmergefilter
ms.assetid: 4c118cb1-2008-44e2-a797-34b7dc34d6b1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0ba0e2384ec63d29d3a5030c0b018998896dc8cb
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769178"
---
# <a name="spaddmergefilter-transact-sql"></a>sp_addmergefilter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  別のテーブルとの結合に基づいてパーティションを作成するために、新しいマージ フィルターを追加します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmergefilter [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @filtername = ] 'filtername'   
        , [ @join_articlename = ] 'join_articlename'   
        , [ @join_filterclause = ] join_filterclause  
    [ , [ @join_unique_key = ] join_unique_key ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @filter_type = ] filter_type ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`マージフィルターを追加するパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'`マージフィルターを追加するアーティクルの名前を指定します。 *アーティクル*は**sysname**で、既定値はありません。  
  
`[ @filtername = ] 'filtername'`フィルターの名前を指定します。 *filtername*は必須パラメーターです。 *filtername*は**sysname**,、既定値はありません。  
  
`[ @join_articlename = ] 'join_articlename'`マージフィルターのフィルター条件を満たす子アーティクル内の行を決定するために、*アーティクル*で指定した子アーティクルを*join_filterclause*で指定された結合句を使用して結合する必要がある親アーティクルを指定します。 *join_articlename*は**sysname**,、既定値はありません。 アーティクルは、*パブリケーション*によって指定されたパブリケーションに含まれている必要があります。  
  
`[ @join_filterclause = ] join_filterclause`マージフィルターに適合する行を決定するために、 *join_article*で指定された*アーティクル*および親アーティクルによって指定された子アーティクルを結合するために使用する必要がある join 句です。 *join_filterclause*は**nvarchar (1000)** です。  
  
`[ @join_unique_key = ] join_unique_key`子アーティクル*アーティクル*と親アーティクル*join_article*間の結合が一対多、一対一、多対一、多対多のいずれであるかを指定します。 *join_unique_key*は**int**,、既定値は0です。 **0**は、多対一または多対多の結合を示します。 **1**一対一または一対多の結合を示します。 この値は、結合する列が*join_article*内で一意のキーを形成する場合、または*join_filterclause*が*アーティクル*内の外部キーと*join_article*内の主キーの間にある場合に**1**になります。  
  
> [!CAUTION]  
>  一意性を保証する親アーティクルの基になるテーブルの結合する列に制約がある場合にのみ、このパラメーターを**1**に設定します。 *Join_unique_key*が誤って**1**に設定されている場合、データの非収束が発生する可能性があります。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot*は**ビット**,、既定値は**0**です。  
  
 **0**を指定すると、マージアーティクルへの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は行われません。  
  
 **1**に設定すると、マージアーティクルへの変更によってスナップショットが無効になることがあります。また、新しいスナップショットを必要とする既存のサブスクリプションが存在する場合は、既存のスナップショットが古いスナップショットとしてマークされ、新しいスナップショットが生成されることを示します。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`このストアドプロシージャによって実行されるアクションで、既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription*は**ビット**,、既定値は0です。  
  
 **0**を指定すると、マージアーティクルへの変更によってサブスクリプションが再初期化されることはありません。 変更にサブスクリプションの再初期化が必要であることをストアド プロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**を指定すると、マージアーティクルへの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を実行する権限が与えられます。  
  
`[ @filter_type = ] filter_type`追加するフィルターの種類を指定します。 *filter_type*は**tinyint**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|結合フィルターのみです。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] のサブスクライバーをサポートするために必要です。|  
|**2**|論理レコードリレーションシップのみ。|  
|**3**|結合フィルターと論理レコードリレーションシップの両方。|  
  
 詳細については、「[Group Changes to Related Rows with Logical Records](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」 (論理レコードによる関連行への変更のグループ化) を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addmergefilter**は、マージレプリケーションで使用します。  
  
 **sp_addmergefilter**は、テーブルアーティクルでのみ使用できます。 ビューおよびインデックス付きビューアーティクルはサポートされていません。  
  
 また、このプロシージャを使用すると、2つのアーティクル間に結合フィルターを持つことができる論理リレーションシップを追加することもできます。 *filter_type*は、追加するマージフィルターが結合フィルター、論理リレーション、またはその両方であるかどうかを指定するために使用されます。  
  
 論理レコードを使用するには、パブリケーションとアーティクルが多くの要件を満たしている必要があります。 詳細については、「[Group Changes to Related Rows with Logical Records](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」 (論理レコードによる関連行への変更のグループ化) を参照してください。  
  
 通常、パブリッシュされている主キー テーブルを参照する外部キーを持ち、その主キーがそのアーティクルで定義されたフィルターを持つようなアーティクルに対してこのオプションを使用します。 主キー行のサブセットは、サブスクライバーにレプリケートされる外部キー行を決定するために使用されます。  
  
 2つのアーティクルのソーステーブルが同じテーブルオブジェクト名を共有している場合、パブリッシュされた2つのアーティクル間に結合フィルターを追加することはできません。 このような場合、それぞれのテーブルを所有するスキーマが異なっていて、それぞれが一意のアーティクル名を持っていても、結合フィルターの作成は失敗します。  
  
 パラメーター化された行フィルターと結合フィルターの両方をテーブルアーティクルで使用すると、サブスクライバーのパーティションに行が属しているかどうかがレプリケーションによって判断されます。 これは、( [and](../../t-sql/language-elements/and-transact-sql.md)演算子を使用して) 2 つの条件の交差部分を評価するのではなく、フィルター処理関数または結合フィルター ( [or](../../t-sql/language-elements/or-transact-sql.md)演算子を使用) のいずれかを評価することによって行われます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_addmergefilter](../../relational-databases/replication/codesnippet/tsql/sp-addmergefilter-transa_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addmergefilter**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [マージ アーティクル間の結合フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [sp_changemergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
