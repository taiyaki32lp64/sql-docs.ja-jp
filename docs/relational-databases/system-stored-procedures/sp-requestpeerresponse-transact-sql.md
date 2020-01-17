---
title: sp_requestpeerresponse (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords:
- sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
author: stevestein
ms.author: sstein
ms.openlocfilehash: f8d75b208cc91d52d20fb4e94340809cd6857fa1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129731"
---
# <a name="sprequestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ピア ツー ピア トポロジ内のノードから実行と、この手順は、トポロジ内の他のすべてのノードからの応答を要求します。 このプロシージャを実行して、対応する応答のレビューで、前のすべてのコマンド応答のノードに配信されたことを保証できます。 このストアド プロシージャは、要求元のノードで任意のデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_requestpeerresponse [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
    [ , [ @request_id = ] request_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 状態の確認をピア ツー ピア トポロジ内のパブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @description = ] 'description'` 個々 の状態要求を識別するために使用できるユーザー定義情報。 *説明*は**nvarchar (4000)** 、既定値は NULL です。  
  
`[ @request_id = ] request_id` 新しい要求の ID を返します。 *request_id*は**int**は出力パラメーター。 実行するときに、この値を使用できます[sp_helppeerresponses &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)状態要求に応答するすべての表示にします。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_requestpeerresponse**はピア ツー ピア トランザクション レプリケーションで使用します。  
  
 **sp_requestpeerresponse**ピア ツー ピア トポロジでパブリッシュされたデータベースを復元する前に、すべてのコマンドがその他のすべてのノードで受信されたことを確認するために使用します。 また、ノードがオフラインの間に行われたデータ定義言語 (DDL) の変更をレプリケートするときに、これらの変更が他のノードに到達する時間を推定する場合にも使用できます。  
  
 **sp_requestpeerresponse**ユーザー定義のトランザクション内で実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_requestpeerresponse**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_deletepeerrequesthistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
