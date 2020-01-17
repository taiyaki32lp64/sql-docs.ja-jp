---
title: MSSQL_ENG014005 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014005 error
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 418628c33764c6e765e8ba855da20f0890f6191a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666882"
---
# <a name="mssqleng014005"></a>MSSQL_ENG014005
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14005|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|パブリケーションを削除できませんでした。 サブスクリプションが存在します。|  
  
## <a name="explanation"></a>説明  
 1 つ以上のサブスクリプションが関連付けられているパブリケーションを削除しようとしました。 パブリケーションは、サブスクリプションが関連付けられていない場合にのみ削除できます。  
  
## <a name="user-action"></a>ユーザーの操作  
 パブリケーションを削除する前にサブスクリプションを削除します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してパブリケーションを削除する場合は、パブリケーションを削除する前に関連するすべてのサブスクリプションを自動的に削除するオプションを使用できます。 ストアド プロシージャを使用する場合は、最初にサブスクリプションを明示的に削除する必要があります。 詳細については、「 [Delete a Push Subscription](delete-a-push-subscription.md) 」および「 [Delete a Pull Subscription](delete-a-pull-subscription.md)」を参照してください。  
  
 パブリケーションに存在するサブスクリプションが表示されない場合や、パブリケーションの作成時にこのエラーが表示される場合は、前のサブスクリプションを削除したときに完全にクリーンアップされていない可能性があります。 レプリケーションに関連するすべてのオブジェクトと設定を削除するには、データベースで [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) を実行します。  
  
## <a name="see-also"></a>関連項目  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
