---
title: フルテキスト フィルター デーモン ランチャーのサービス アカウントの設定
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: eed8020872b3d2a3babc0581054bef0dbed64a4d
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055947"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>フルテキスト フィルター デーモン ランチャーのサービス アカウントの設定
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 このトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、SQL フルテキスト フィルター デーモン ランチャー サービス (MSSQLFDLauncher) のサービス アカウントを設定または変更する方法について説明します。 SQL Server のセットアップで使われる既定のサービス アカウントは、`NT Service\MSSQLFDLauncher` です。
  
  
## <a name="about-the-sql-full-text-filter-daemon-launcher-service"></a>SQL フルテキスト フィルター デーモン ランチャー サービスについて
SQL フルテキスト フィルター デーモン ランチャー サービスは、SQL Server のフルテキスト検索でフィルター処理や単語区切りを行うフィルター デーモン ホスト プロセスを開始するために使用されます。 フルテキスト検索を使用するには、ランチャー サービスが実行されている必要があります。  
  
SQL フルテキスト フィルター デーモン ランチャー サービスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の特定のインスタンスに関連付けられているインスタンス対応のサービスです。 SQL フルテキスト フィルター デーモン ランチャー サービスにより、起動される各フィルター デーモン ホスト プロセスにサービス アカウント情報が反映されます。  

##  <a name="setting"></a> サービス アカウントの設定  
  
1.  **[スタート]** メニューの **[すべてのプログラム]** をポイントし、[[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] を展開して、 **[SQL Server 2016 構成マネージャー]** をクリックします。  
  
2.  **[SQL Server 構成マネージャー]** で、 **[SQL Server のサービス]** をクリックし、 **[SQL フルテキスト フィルター デーモン ランチャー (** _インスタンス名_ **)]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  ダイアログ ボックスの **[ログオン]** タブをクリックし、SQL フルテキスト フィルター デーモン ランチャー サービスが開始するプロセスを実行するアカウントを選択または入力します。  
  
4.  ダイアログ ボックスを閉じた後、 **[再起動]** をクリックすると、SQL フルテキスト フィルター デーモン ランチャー サービスが再起動されます。  
  
![SQL フルテキスト フィルター デーモン ランチャー プロセスのプロパティ](../../relational-databases/search/media/sql-full-text-filter-daemon-launch-process-properties.png)
  
##  <a name="error"></a> SQL フルテキスト フィルター デーモン ランチャー サービスが開始しない場合にトラブルシューティングする  
 SQL フルテキスト フィルター デーモン ランチャー サービスが開始しない場合は、次の原因が考えられます。  
  
### <a name="permissions-issues"></a>アクセス許可の問題
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス グループに、SQL フルテキスト フィルター デーモン ランチャー サービスを開始する権限がない。  

     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス グループに、SQL フルテキスト フィルター デーモン ランチャー サービス アカウントに対する権限があることを確認してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインストール時、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス グループには、SQL フルテキスト フィルター デーモン ランチャー サービスを管理、クエリ、および開始する既定の権限が与えられます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール後に SQL フルテキスト フィルター デーモン ランチャー サービス アカウントに対する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス グループの権限が削除されている場合、SQL フルテキスト フィルター デーモン ランチャー サービスは開始されず、フルテキスト検索は無効になります。     

-   サービスへのログインに使用されるアカウントに権限がない。  
  
     サーバー インスタンスがインストールされているコンピューターに対するログイン権限のないアカウントを使用している可能性があります。 ローカル コンピューターのユーザー権利および権限を持つアカウントでログインしていることを確認してください。  

### <a name="service-account-and-password-issues"></a>サービス アカウントとパスワードの問題
-   サービス アカウントのユーザー アカウントまたはパスワードが正しくない。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 構成マネージャーで、サービスが正しいサービス アカウントとパスワードを使っていることを確認します。  
  
-   SQL フルテキスト フィルター デーモン ランチャー サービスのアカウントに関連付けられたパスワードの期限が切れている。  
  
     SQL フルテキスト フィルター デーモン ランチャー サービスにローカル ユーザー アカウントを使用している場合にパスワードの期限が切れたときは、次の作業を行う必要があります。  
  
    1.  アカウントに新しい Windows パスワードを設定します。  
  
    2.  新しいパスワードが使用されるように、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 構成マネージャーで SQL フルテキスト フィルター デーモン ランチャー サービスを更新します。  
  
### <a name="named-pipes-configuration-issues"></a>名前付きパイプの構成に関する問題
-   フルテキスト検索で SQL フルテキスト フィルター デーモン ランチャー サービスが正しく構成されていない。  
  
     名前付きパイプの機能がローカル コンピューターで無効になっているか、既定の名前付きパイプ以外の名前付きパイプを使用するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が構成されていると、SQL フルテキスト フィルター デーモン ランチャー サービスが開始されないことがあります。  
  
-   同じ名前付きパイプの別のインスタンスが既に実行されている。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスは、SQL フルテキスト フィルター デーモン ランチャー サービス クライアントの名前付きパイプ サーバーとして機能します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が開始される前に名前付きパイプが別のプロセスで作成されていると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログと Windows イベント ログにエラーが記録され、フルテキスト検索を使用できません。  同じ名前付きパイプを使用しようとしているプロセスまたはアプリケーションを特定し、そのアプリケーションを停止してください。  
  
## <a name="see-also"></a>参照  
 [サービスの管理方法に関するトピック &#40;SQL Server 構成マネージャー&#41;](https://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)   
 [フルテキスト検索のアップグレード](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
