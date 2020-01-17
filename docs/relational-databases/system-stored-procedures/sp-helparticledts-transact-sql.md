---
title: sp_helparticledts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticledts
- sp_helparticledts_TSQL
helpviewer_keywords:
- sp_helparticledts
ms.assetid: cd1aed60-e056-4ff3-86ee-62b19433d890
author: stevestein
ms.author: sstein
ms.openlocfilehash: a9c489a08291aea3d1c50a6418dc8e1e853dce12
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771074"
---
# <a name="sphelparticledts-transact-sql"></a>sp_helparticledts (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Visual Basic を使用して[!INCLUDE[msCoName](../../includes/msconame-md.md)]変換サブスクリプションを作成するときに使用する、正しいカスタムタスク名に関する情報を取得するために使用します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helparticledts [ @publication = ] 'publication', [ @article = ] 'article'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'`パブリケーション内のアーティクルの名前を指定します。 *アーティクル*は**sysname**で、既定値はありません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pre_script_ignore_error_task_name**|**sysname**|スナップショットデータがコピーされる前に発生するプログラミングタスクのタスク名。 スクリプト エラーが発生しても、プログラムはそのまま実行されます。|  
|**pre_script_task_name**|**sysname**|スナップショットデータがコピーされる前に発生するプログラミングタスクのタスク名。 プログラムの実行はエラー発生時に停止します。|  
|**transformation_task_name**|**sysname**|データドリブンクエリタスクを使用するときのプログラミングタスクのタスク名。|  
|**post_script_ignore_error_task_name**|**sysname**|スナップショット データをコピーした後に発生するプログラミング タスクのタスク名。 スクリプト エラーが発生しても、プログラムはそのまま実行されます。|  
|**post_script_task_name**|**sysname**|スナップショット データをコピーした後に発生するプログラミング タスクのタスク名。 プログラムの実行はエラー発生時に停止します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helparticledts**は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 レプリケーション データ変換サービス (DTS) プログラム内のタスクに名前を付ける場合は、レプリケーション エージェントで要求される名前付け規則に従う必要があります。 SQL 実行タスクなどのカスタムタスクの場合、名前は、アーティクル名、プレフィックス、および省略可能な部分で構成される連結文字列になります。 コードを記述するときに、タスク名がわからない場合、結果セットには使用する必要があるタスク名が示されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helparticledts**を実行できるのは、 **sysadmin**固定サーバーロールおよび**db_owner**固定データベースロールのメンバーだけです。  
  
  
