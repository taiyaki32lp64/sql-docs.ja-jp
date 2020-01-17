---
title: '[キュー リーダー エージェントのセキュリティ] | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 92b80f727ce87606b0c1c58954b0743734880422
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021257"
---
# <a name="queue-reader-agent-security"></a>[キュー リーダー エージェントのセキュリティ]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[キュー リーダー エージェントのセキュリティ]** ダイアログ ボックスを使用すると、キュー リーダー エージェントを実行したり、ディストリビューターへのローカル接続を行ったりするための [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントを指定できます。 エージェントは、( **[ディストリビューターのプロパティ]** ダイアログ ボックスから呼び出される) **[パブリッシャーのプロパティ]** ダイアログ ボックスで指定されたアカウントを使用してパブリッシャーに接続します。エージェントは、同じコンテキストを使用して、サブスクリプションのディストリビューション エージェントとしてサブスクライバーに接続します。 詳細については、「[レプリケーションのセキュリティ設定の表示および変更](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)」を参照してください。  
  
 アカウントは、適切なパスワードが指定された有効なアカウントである必要があります。 アカウントとパスワードは、エージェントが実行されるまで検証されません。  
  
## <a name="options"></a>オプション  
 **[プロセス アカウント]**  
 ディストリビューターでキュー リーダー エージェントを実行するための Windows アカウントを入力します。 指定した Windows アカウントは少なくともディストリビューション データベースで **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
 **[パスワード]** と **[パスワードの確認入力]**  
 Windows アカウントのパスワードを入力します。  
  
## <a name="see-also"></a>参照  
 [ID およびアクセス制御 (レプリケーション)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [レプリケーション エージェントのセキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
