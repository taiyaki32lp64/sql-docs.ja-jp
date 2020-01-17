---
title: レポート サーバーのプロパティ ([ログオン] タブ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: f54be594-f290-4db2-bf18-fd2521728a4a
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 85b62a07b691492f9980574f1607fbb302071497
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058394"
---
# <a name="report-server-properties-log-on-tab"></a>[SQL Server Reporting Services のプロパティ] ダイアログ ボックス ([ログオン] タブ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  **[SQL Server Reporting Services のプロパティ]** ダイアログ ボックスの **[ログオン]** タブでは、レポート サーバー サービスが使用するアカウントの指定や、そのサービスの開始、停止を行います。  
  
## <a name="options"></a>オプション  
 **[ローカル システム アカウント]**  
 ローカル システム アカウントを指定します。このアカウントはパスワードを必要としません。 ただし、ローカル システム アカウントに与えられている特権によっては、そのサービスと他のサーバーとの対話が制限されることもあります。  
  
 **[このアカウント]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証を使用するローカル ユーザー アカウントまたはドメイン ユーザー アカウントを指定します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、サービスを実行できる必要最小限の権限が設定されたドメイン ユーザー アカウントを使用することをお勧めします。 アカウントの選択の詳細については、オンライン ブックの「Windows サービス アカウントの設定」を検索してください。  
  
 **アカウント名**  
 ローカル ユーザー アカウント名またはドメイン ユーザー アカウント名を指定します。  
  
 **パスワード**  
 アカウントのパスワードを入力します。  
  
 **[パスワードの確認入力]**  
 アカウントのパスワードを再度入力します。  
  
 **[開始]**  
 サービスを開始します。  
  
 **[停止]**  
 サービスを停止します。  
  
 **[一時停止]**  
 サービスを一時停止します。  
  
 **[再開]**  
 一時停止したサービスを再開します。  
  
  
