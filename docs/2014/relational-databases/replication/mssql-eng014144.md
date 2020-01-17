---
title: MSSQL_ENG014144 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014144 error
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f85903658025f3ea1e5df805bb0593da9d840f25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192429"
---
# <a name="mssqleng014144"></a>MSSQL_ENG014144
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14144|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|サブスクライバー '%s' を削除できません。 そのサブスクライバーのサブスクリプションがパブリケーション データベース '%s' にあります。|  
  
## <a name="explanation"></a>説明  
 サブスクライバーとして構成されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、そのインスタンスに対して構成されているアクティブなサブスクリプションがあると、サブスクライバーの役割から削除できません。  
  
## <a name="user-action"></a>ユーザーの操作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのサブスクライバーの状態を変更する前に、関連付けられているすべてのサブスクリプションを削除します。  
  
1.  パブリッシャーのパブリケーション データベースで [sp_helpsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) を実行して、サブスクリプションを検索します。  
  
2.  パブリケーション データベースで [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql) を実行して、サブスクリプションを削除します。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)   
 [パブリケーションのサブスクライブ](subscribe-to-publications.md)  
  
  
