---
title: sp_publication_validation (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
author: stevestein
ms.author: sstein
ms.openlocfilehash: bdfe70e3df86f792d250cd7abcc3ef3013e9df19
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056235"
---
# <a name="sp_publication_validation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  指定されたパブリケーション内の各アーティクルに対して、アーティクル検証要求を開始します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname** 、既定値はありません。  
  
`[ @rowcount_only = ] 'rowcount_only'`、テーブルの行数のみを返すかどうかを指定します。 *rowcount_only*は**smallint**であり、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 互換性のあるチェックサムを実行します。<br /><br /> 注: アーティクルが行方向にフィルター選択されている場合、チェックサム操作ではなく rowcount 操作が実行されます。|  
|**1** (既定値)|行数チェックのみを実行します。|  
|**2**|行数とバイナリチェックサムを実行します。<br /><br /> 注: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョン7.0 のサブスクライバーの場合、行数の検証のみが実行されます。|  
  
`[ @full_or_fast = ] 'full_or_fast'` は、rowcount の計算に使用される方法です。 *full_or_fast*は**tinyint**で、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**0**|COUNT(*) を使用してフル カウントします。|  
|**1**|Sysindexes から高速にカウントさ**れ**ます。 [Sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md)内の行のカウントは、実際のテーブルの行をカウントするよりもはるかに高速です。 ただし、 [sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md)は遅延更新されるため、行数が正確でない場合があります。|  
|**2** (既定値)|最初に高速カウントを試み、条件高速カウントを行います。 Fast メソッドが相違点を示している場合、は完全なメソッドに戻ります。 場合*expected_rowcount*ストアド プロシージャの中を NULL 値を取得する、フル カウント(\*) が常に使用します。|  
  
`[ @shutdown_agent = ] 'shutdown_agent'` は、検証の完了後すぐにディストリビューションエージェントをシャットダウンするかどうかを指定します。 *shutdown_agent*は**ビット**,、既定値は**0**です。 **0**の場合、レプリケーションエージェントはシャットダウンされません。 **1**の場合、最後の記事が検証された後にレプリケーションエージェントがシャットダウンします。  
  
`[ @publisher = ] 'publisher'` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリッシャーの検証を要求するときは、 *publisher*を使用しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_publication_validation**は、トランザクションレプリケーションで使用します。  
  
 **sp_publication_validation**は、パブリケーションに関連付けられているアーティクルがアクティブ化された後でいつでも呼び出すことができます。 この手順は、データを検証する定期的にスケジュールされたジョブの一部として、手動で (1 回) または実行することができます。  
  
 アプリケーションに即時更新サブスクライバーがある場合、 **sp_publication_validation**は誤ったエラーを検出することがあります。 **sp_publication_validation**は、最初にパブリッシャーで行数またはチェックサムを計算し、次にサブスクライバーで計算します。 行数またはチェックサムがパブリッシャーで完了していて、サブスクライバーでは完了していない場合、即時更新トリガーはサブスクライバーからパブリッシャーに更新を通知できるため、値が変更される可能性があります。 パブリケーションの検証中にサブスクライバーとパブリッシャーの値が変更されないようにするには、検証中のパブリッシャーでの Microsoft 分散トランザクション コーディネーター (MS DTC) サービスを停止します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_publication_validation**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [サブスクライバーでのデータの検証](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [transact-sql &#40;  の&#41; sp_article_validation](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_table_validation](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
