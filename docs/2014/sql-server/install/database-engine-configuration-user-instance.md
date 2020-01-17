---
title: データベース エンジンの構成 - ユーザー インスタンス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- database engine configuration
- database engine configuration, user instance
ms.assetid: dfc27c1e-0fe2-4221-bed5-f52667ddd3c8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ba05d426f9515793ad3a924e375ff9a6ab9f940f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095879"
---
# <a name="database-engine-configuration---user-instance"></a>データベース エンジンの構成 - ユーザー インスタンス
  **[ユーザー インスタンス]** ページを使用して、管理者権限のないユーザー用に、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の個別インスタンスを作成し、それらのユーザーを管理者ロールに追加します。  
  
## <a name="option"></a>オプション  
 [ユーザー インスタンスを有効にする]  
 既定値はオンです。 ユーザー インスタンス有効化の機能を無効にするには、このチェック ボックスをオフにします。  
  
 ユーザー インスタンスは子インスタンスまたはクライアント インスタンスとも呼ばれ、ユーザーに代わって親インスタンス ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] などのサービスを実行するプライマリ インスタンス) によって作成される [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]のインスタンスです。 ユーザー インスタンスは、そのユーザーのセキュリティ コンテキストでのユーザーのプロセスとして実行します。 親インスタンスやコンピューター上で実行するその他のユーザー インスタンスとは分離されます。 ユーザー インスタンス機能は "通常のユーザーとして実行" (Run As Normal User: RANU) とも呼ばれます。  
  
> [!NOTE]  
>  セットアップ中に **sysadmin** 固定サーバー ロールのメンバーとして準備されたログインは、テンプレート データベース内の管理者として準備されます。 削除されない限り、これらはユーザー インスタンスのメンバー **sysadmin** 固定サーバー ロールです。  
  
 [ユーザーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者ロールに追加する]  
 既定値はオフです。 現在のセットアップ ユーザーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者ロールに追加するには、このチェック ボックスをオンにします。  
  
 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] ユーザーのうち、BUILTIN\Administrators のメンバーは、[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] への接続時に sysadmin 固定サーバー ロールに自動的に追加されません。 サーバーレベルの管理者ロールに明示的に追加されている [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] ユーザーのみが、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]を管理できます。 Built-In\Users グループのすべてのメンバーが [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] インスタンスに接続できますが、データベース タスクの実行権限は制限されます。 このため、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 特権を以前のリリースの Windows の BUILTIN\Administrators および Built-In\Users から継承しているユーザーには、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] で実行している [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]のインスタンスにおいて、管理特権を明示的に付与する必要があります。  
  
 このインストール プログラムの完了後にユーザー ロールに変更を加えるには、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] セキュリティ構成ツール (SQLSAC.exe) を使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者ロールのユーザー一覧を更新するには、 **[新しい管理者の追加]** リンクをクリックします。  
  
 **[準備するユーザー]** フィールドに、権限を更新するユーザーが DomainName\UserName 形式で表示されたことを確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [使用できる特権] **ペインの** インスタンスの一覧から、更新するロールを選択して、右矢印をクリックします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の使用可能なすべてのインスタンスの、使用できるすべてのロールにユーザーを追加するには、二重右矢印をクリックします。  
  
 選択の完了後に変更を適用するには、 [!INCLUDE[clickOK](../../includes/clickok-md.md)] 変更を適用せずにツールを終了するには、 **[キャンセル]** をクリックします。  
  
  
