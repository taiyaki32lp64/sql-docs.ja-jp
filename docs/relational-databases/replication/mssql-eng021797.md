---
title: MSSQL_ENG021797 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021797 error
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: db0911d4af8d8cbd4860a07bc8c48305ffae0648
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71711013"
---
# <a name="mssql_eng021797"></a>MSSQL_ENG021797
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|21797|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|'%s' には 'MACHINE\Login' または 'DOMAIN\Login' の形式で有効な Windows ログインを指定してください。 '%s' については、マニュアルを参照してください。|  
  
## <a name="explanation"></a>説明  
 このエラーは、`@job_login` パラメーターに指定された値が NULL または無効の場合に、以下のレプリケーション ストアド プロシージャにより発生します。 このエラーは、 **db_owner** 固定データベース ロールのメンバーが、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からのスクリプトを実行すると発生する場合があります。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ではセキュリティ モデルが変更されたため、これらのスクリプトは更新する必要があります。  
  
-   [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
-   [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
-   [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
-   [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)  
  
-   [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 これらのストアド プロシージャは、適切なサーバー上の **sysadmin** 固定サーバー ロールのメンバー、または適切なデータベース内の **db_owner** 固定データベース ロールのメンバーにより実行されます。 ストアド プロシージャはそれぞれエージェント ジョブを作成します。これにより、エージェントの実行に使用される [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントを指定できます。 **sysadmin** ロールのユーザーに対し、エージェント ジョブは、Windows アカウントが指定されていなくても (アカウントが指定されている場合、そのアカウントは有効である必要があります)、暗黙的に作成されます。エージェントは、適切なサーバーでの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントのコンテキストの下で実行されます。 アカウントは必要ありませんが、セキュリティ上、エージェントごとに異なるアカウントを指定することをお勧めします。 詳細については、「 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 各プロシージャの `@job_login` パラメーターに対し、有効な Windows アカウントが指定されていることを確認します。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からのレプリケーション スクリプトがある場合は、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]に必要なストアド プロシージャやパラメーターをこれらのスクリプトに含めるように更新します。 詳細については、「[レプリケーション スクリプトのアップグレード &#40;レプリケーション Transact-SQL プログラミング&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
