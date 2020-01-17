---
title: フルテキスト フィルター デーモン ランチャーのサービス アカウントの設定 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f327cefbb916bf83f695db40a1d3c3025b7a5d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010936"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>フルテキスト フィルター デーモン ランチャーのサービス アカウントの設定
  このトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、SQL フルテキスト フィルター デーモン ランチャー サービス (MSSQLFDLauncher) のサービス アカウントを設定する方法について説明します。 SQL フルテキスト フィルター デーモン ランチャー サービスは、ssNoVersion のフルテキスト検索でフィルター処理や単語区切りを行うフィルター デーモン ホスト プロセスを開始するために使用されます。 フルテキスト検索を使用するには、このサービスが実行されている必要があります。  
  
 SQL フルテキスト フィルター デーモン ランチャー サービスは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のインスタンスに関連付けられているインスタンス対応のサービスです。 SQL フルテキスト フィルター デーモン ランチャー サービスにより、各フィルター デーモン ホスト プロセスにサービス アカウント情報が反映されます。  
  
  
##  <a name="setting"></a> サービス アカウントの設定  
  
#### <a name="to-set-the-sql-full-text-filter-daemon-launcher-service-account-for-full-text-search"></a>フルテキスト検索の SQL フルテキスト フィルター デーモン ランチャー サービス アカウントを設定するには  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  **SQL Server 構成マネージャー**、 をクリックして**SQL Server サービス**、右クリックして**SQL フルテキスト フィルター デーモン ランチャー ( *`instance name`* )** 、 をクリックし、**プロパティ**します。  
  
3.  ダイアログ ボックスの **[ログオン]** タブをクリックし、SQL フルテキスト フィルター デーモン ランチャー サービスによって作成される各プロセスについて、その実行に使用するアカウントを選択または入力します。  
  
4.  ダイアログ ボックスを閉じた後、 **[再起動]** をクリックすると、SQL フルテキスト フィルター デーモン ランチャー サービスが再起動されます。  
  
  
##  <a name="error"></a> 場合、SQL フルテキスト フィルター デーモン ランチャー サービスは起動されません。  
 SQL フルテキスト フィルター デーモン ランチャー サービスが開始されない場合は、次の原因が考えられます。  
  
-   SQL フルテキスト フィルター デーモン ランチャー サービスのアカウントに関連付けられたパスワードの期限が切れている。  
  
     SQL フルテキスト フィルター デーモン ランチャー サービスにローカル ユーザー アカウントを使用している場合にパスワードの期限が切れたときは、次の作業を行う必要があります。  
  
    1.  アカウントに新しい Windows パスワードを設定します。  
  
    2.  新しいパスワードが使用されるように、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで SQL フルテキスト フィルター デーモン ランチャー サービスを更新します。  
  
-   サービス アカウントのユーザー アカウントまたはパスワードが正しくない。  
  
     SQL フルテキスト フィルター デーモン ランチャー サービスが、正しくないユーザー アカウントおよびパスワードでログインしようとしている可能性があります。 上記の手順に従って、サービスのユーザー アカウントが変更されていないことを確認してください。  
  
-   サービスへのログインに使用されるアカウントに権限がない。  
  
     サーバー インスタンスがインストールされているコンピューターに対するログイン権限のないアカウントを使用している可能性があります。 ローカル コンピューターのユーザー権利および権限を持つアカウントでログインしていることを確認してください。  
  
-   同じ名前付きパイプの別のインスタンスが既に実行されている。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスは、SQL フルテキスト フィルター デーモン ランチャー サービス クライアントの名前付きパイプ サーバーとして機能します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が開始される前に名前付きパイプが別のプロセスで作成されていると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログと Windows イベント ログにエラーが記録され、フルテキスト検索を使用できません。  同じ名前付きパイプを使用しようとしているプロセスまたはアプリケーションを特定し、そのアプリケーションを停止してください。  
  
-   フルテキスト検索で SQL フルテキスト フィルター デーモン ランチャー サービスが正しく構成されていない。  
  
     サービスが、ローカル コンピューターで正しく構成されていない可能性があります。  
  
     名前付きパイプの機能がローカル コンピューターで無効になっているか、既定の名前付きパイプ以外の名前付きパイプを使用するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が構成されていると、SQL フルテキスト フィルター デーモン ランチャー サービスが開始されないことがあります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス グループに、SQL フルテキスト フィルター デーモン ランチャー サービスを開始する権限がない。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインストール時、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス グループには、SQL フルテキスト フィルター デーモン ランチャー サービスを管理、クエリ、および開始する既定の権限が与えられます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール後に SQL フルテキスト フィルター デーモン ランチャー サービス アカウントに対する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス グループの権限が削除されている場合、SQL フルテキスト フィルター デーモン ランチャー サービスは開始されず、フルテキスト検索は無効になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス グループに、SQL フルテキスト フィルター デーモン ランチャー サービス アカウントに対する権限があることを確認してください。  
  
  
## <a name="see-also"></a>参照  
 [サービスの管理方法に関するトピック &#40;SQL Server 構成マネージャー&#41;](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)  
 [フルテキスト検索のアップグレード](upgrade-full-text-search.md)  
  
  
