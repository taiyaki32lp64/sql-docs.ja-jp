---
title: SQL フルテキスト フィルター デーモン ランチャー ([ログオン] タブ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 13e260f9-a75f-430b-88a3-959ddcead8fe
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 791079d881cf48c8eb5cdaa74f932cb29738003a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058284"
---
# <a name="sql-full-text-filter-daemon-launcher-log-on-tab"></a>SQL フルテキスト フィルター デーモン ランチャー ([ログオン] タブ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フルテキスト検索で SQL フルテキスト フィルター デーモン ランチャー (FDHOST ランチャー) サービスが使用されます。 フルテキスト検索を使用する場合はこのサービスが実行されている必要があります。 フィルター デーモン ホスト プロセスの詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「フルテキスト検索のアーキテクチャ」を参照してください。  
  
 **[SQL フルテキスト フィルター デーモン ランチャーのプロパティ]** ダイアログ ボックスの **[ログオン]** タブでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フルテキスト サービスが使用するアカウントの指定、アカウントのパスワードの変更、サービスの開始や停止を行います。 アカウントのパスワードを変更した場合、その変更はサービスの再起動後に有効になります。  
  
> [!NOTE]  
>  クラスター化されたインスタンス上のサービスで使用するアカウント名を変更する場合、新しいアカウントは、そのサービスのセットアップ時に指定したドメイン グループに属している必要があります。または、そのグループにメンバーを追加する権限が与えられている必要があります。 グループのメンバーシップを変更する権限がない場合は、ドメイン管理者に問い合わせてください。  
>   
>  サービスを実行するアカウントの選択の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「Windows サービス アカウントの設定」を参照してください。  
  
## <a name="options"></a>オプション  
 **[ビルトイン アカウント]**  
 **Local System**  
 ローカル システム アカウントを指定します。 このアカウントはパスワードを必要としません。 ただし、ローカル システム アカウントに与えられている特権によっては、そのサービスが他のサーバーと対話できないこともあります。  
  
 **Local Service**  
 ローカル サービス アカウントを指定します。 このアカウントはパスワードを必要としません。 ただし、ローカル サービス アカウントに与えられている特権によっては、そのサービスが他のサーバーと対話できないこともあります。  
  
 **Network Service**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスには、ネットワーク サービス アカウントを使用しないことをお勧めします。 これらのサービスには、ローカル ユーザー アカウントまたはドメイン ユーザー アカウントの方が適しています。  
  
 **[このアカウント]**  
 Windows 認証を使用するローカル ユーザー アカウントまたはドメイン ユーザー アカウントを指定します。 サービスを実行できる必要最小限の権限が設定されたドメイン ユーザー アカウントを使用することをお勧めします。  
  
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
 サービスを一時停止します。 このサービスでは使用できません。  
  
 **[再開]**  
 一時停止したサービスを再開します。  
  
  
