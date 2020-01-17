---
title: '[サブスクライバーのプロパティ] | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 1631c725fb089b96825ea71a550b5d13fe7f400c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769494"
---
# <a name="subscriber-properties"></a>[サブスクライバーのプロパティ]
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **[サブスクライバーのプロパティ]** ダイアログ ボックスには、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] より前のバージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているサブスクライバーに関連する情報が表示されます。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]

  
## <a name="options"></a>オプション  
 **[サブスクライバーへのエージェント接続]**  
 ディストリビューターからサブスクライバーに、ディストリビューション エージェントとマージ エージェントを接続する際のコンテキストです。これは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]より前のバージョンにのみ適用されます。  
  
 **[エージェント プロセス アカウントを借用する]** を選択して、ディストリビューターで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのアカウントのコンテキストを使用してサブスクライバーへの接続を作成するか、 **[SQL Server 認証]** を指定して **[ログイン]** および **[パスワード]** の値を入力します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、 **[エージェント プロセス アカウントを借用する]** を選択することをお勧めします。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンでは、サブスクリプションの新規作成ウィザードで各サブスクリプションについて接続情報を指定します。接続情報の変更は **[サブスクリプションのプロパティ]** ダイアログ ボックスで行います。  
  
 **[既定のエージェントのスケジュール]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]を実行しているサブスクライバーでは、サブスクリプションの新規作成ウィザードで既定のスケジュールが使用されます。  
  
 **その他**  
 サブスクライバーとサブスクライバーの種類に関する情報が含まれています。  
  
## <a name="see-also"></a>参照  
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
