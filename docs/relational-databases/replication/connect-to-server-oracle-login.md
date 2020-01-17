---
title: '[サーバーへの接続] (Oracle)、[ログイン] | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.oracleconnection.login.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 86ed91a1-a07c-46f2-a913-67317ef2255e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3b765f663e190f5f36621f0f73655824467a3998
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903080"
---
# <a name="connect-to-server-oracle-login"></a>[サーバーへの接続] \(Oracle)、[ログイン]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[サーバーへの接続]** ダイアログ ボックスの **[ログイン]** タブを使用すると、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディストリビューターから Oracle パブリッシャーへの接続を確立するためのアカウントを指定できます。 パブリッシャーの構成時にレプリケーション管理ユーザー スキーマ用に指定したものと同じアカウントを使用する必要があります。 詳細については、「[Configure an Oracle Publisher](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)」(Oracle パブリッシャーの構成) をご覧ください。  
  
## <a name="options"></a>オプション  
 **サーバー インスタンス**  
 ディストリビューターにインストールされた Oracle クライアント ソフトウェアの構成時に指定される、Oracle パブリッシャーの TNS (Transparent Network Substrate) 名です。  
  
 **[認証]**  
 **[Oracle 標準認証]** (推奨) または **[Windows 認証]** を選択してください。 **[Windows 認証]** を選択した場合 :  
  
-   Oracle サーバーは、Windows 資格情報を使用して接続を許可するように構成する必要があります。 詳細については Oracle のマニュアルを参照してください。  
  
-   現在、レプリケーション管理ユーザー スキーマ用に指定した [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントと同じものを使用してログインしている必要があります。  
  
 **[ログイン]** と **[パスワード]**  
 **[認証]** オプションの **[Oracle 標準認証]** を選択した場合は、使用するログインとパスワードを指定してください。レプリケーション管理ユーザー スキーマに指定したものと同じである必要があります。  
  
## <a name="see-also"></a>参照  
 [Glossary of Terms for Oracle Publishing](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)  
  
  
