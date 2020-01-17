---
title: インストール後の手順を実行します。Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 934c38028bf187ed0b78f0ad3facccf692022965
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121546"
---
# <a name="complete-the-post-installation-steps"></a>インストール後の手順の実行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  分散再生をインストールした後、分散再生コントローラー サービスおよび分散再生クライアント サービスのアカウントを変更する必要があります。  
  
### <a name="to-complete-the-post-installation-steps"></a>インストール後の手順を実行するには  
  
1.  **ファイアウォール ルールを作成する**: コントローラー コンピューターとクライアント コンピューターで、対応するサービスのファイアウォール経由の受信トラフィックを許可する必要があります。 インストール フォルダーに配置されているサービス実行可能ファイルのファイアウォール ルールを指定します。  
  
    1.  コントローラー サービスの場合は、インストール フォルダーにある **DReplayController.exe**のルールを作成します。 たとえば、次のコマンドを実行すると、このルールが有効になります ( `%InstallPath%` はサービスのインストール フォルダーです)。  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2.  クライアント サービスの場合は、クライアント コンピューターごとに、インストール フォルダーにある **DReplayClient.exe**のルールを作成します。 たとえば、次のコマンドを実行すると、このルールが有効になります ( `%InstallPath%` はサービスのインストール フォルダーです)。  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2.  **ターゲット サーバーで各クライアントの権限を与える**: クライアント コンピューターへのクライアント サービスのインストールが完了したら、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の対象インスタンスの sysadmin ロールにクライアント サービス アカウントを手動で追加する必要があります。  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
 分散再生の機能をインストールするには、管理権限が必要です。 sysadmin 権限を持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのみが、テスト サーバーの sysadmin サーバー ロールにクライアント サービス アカウントを追加できます。 Distributed Replay のセキュリティ上の考慮事項の詳細については、「 [Distributed Replay のセキュリティ](../../tools/distributed-replay/distributed-replay-security.md)」を参照してください。  
  
  
