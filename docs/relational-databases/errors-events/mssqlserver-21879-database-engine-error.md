---
title: MSSQLSERVER_21879 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21879 (Database Engine error)
ms.assetid: fcfab735-05ca-423a-89f1-fdee7e2ed8c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7068229bcfcf63bb08fe46272cf308cee60be022
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056707"
---
# <a name="mssqlserver21879"></a>MSSQLSERVER_21879
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|21879|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum21879|  
|メッセージ テキスト|元のパブリッシャー '%s' およびパブリッシャー データベース '%s' をリダイレクトされたサーバー '%s' でクエリできないため、リモート サーバーの名前を特定できません。エラー %d、エラー メッセージ '%s'。|  
  
## <a name="explanation"></a>説明  
**sp_validate_redirected_publisher** は、リモート サーバーの名前を検出するため、一時リンク サーバーを作成し、これを使用してリダイレクトされたパブリッシャーに接続します。 リンク サーバー クエリが失敗すると、エラー 21879 が返されます。 リモート サーバー名を要求する呼び出しは通常、一時リンク サーバーを最初に使用するため、接続の問題がある場合はこの呼び出しで初めて問題が現れる可能性があります。 このリモート呼び出しは単に、リモート サーバーで select **@@servername** を実行します。  
  
リダイレクトされたパブリッシャーにクエリを実行するために使用されるリンク サーバーは、元のパブリッシャーに対して **sp_adddistpublisher** を呼び出したときに指定したセキュリティ モード、ログイン、およびパスワードを使用します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した場合 (セキュリティ モード 0)、リモート サーバーへの接続には指定されたログインおよびパスワードが使用されます。  
  
-   Windows 認証を使用した場合 (セキュリティ モード 1)、接続にはセキュリティ接続が使用されます。  
  
    -   **sp_validate_redirected_publisher** がユーザーによって明示的に呼び出された場合、接続にはユーザーが実行している Windows ログインが使用されます。  
  
    -   **sp_validate_redirected_** publisher がレプリケーション エージェントによって **sp_get_redirected_publisher** から呼び出された場合、エージェントに関連付けられている Windows ログインが使用されます。  
  
エラー 21879 は、リダイレクトされた対象のパブリッシャーで認識されないログインを使用して **sp_validate_redirected_publisher** が呼び出されたことを示している可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインまたは Windows 認証ログインが可用性グループ レプリカのすべてで有効であり、パブリッシャー データベースのサブスクリプション メタデータ テーブル (syssubscriptions および sysmergesubscriptions) にアクセスするための十分な権限があることを確認します。  
  
ディストリビューター以外のノードで実行されているレプリケーション エージェント (サブスクライバーで実行されているマージ エージェントなど) によって開始された **sp_get_redirected_publisher** に対する呼び出しからエラー 21879 が返される場合、特別な注意事項があります。 リダイレクトされたパブリッシャーへの接続に Windows 認証が使用される場合、接続を正常に確立するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に Kerberos 認証を構成する必要があります。 Windows 認証が使用され、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に Kerberos 認証が構成されていない場合、サブスクライバーで実行されているマージ エージェントは、'NT AUTHORITY\ANONYMOUS LOGON' ログインが失敗したことを示すエラー 18456 を受け取ります。 この問題を解決するには、以下の 3 種類の方法があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に Kerberos 認証を構成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「**Kerberos 認証と SQL Server**」を参照してください。  
  
-   **sp_changedistpublisher** を使用して、MSdistpublishers の元のパブリッシャーに関連付けられているセキュリティ モードを変更し、接続に使用するログインおよびパスワードも指定します。  
  
-   マージ エージェント コマンド ラインでコマンド ライン パラメーター *BypassPublisherValidation* を指定し、ディストリビューターで **sp_get_redirected_publisher** が呼び出されるときの検証を省略します。  
  
