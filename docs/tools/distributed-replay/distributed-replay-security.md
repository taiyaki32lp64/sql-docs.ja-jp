---
title: 分散再生 Security |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 7e2e586d-947d-4fe2-86c5-f06200ebf139
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6279a9ff5dd965a1ca2920c13c993bf364736355
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079849"
---
# <a name="distributed-replay-security"></a>Distributed Replay のセキュリティ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 機能をインストールして使用する前に、このトピックの重要なセキュリティ情報を確認する必要があります。 このトピックでは、Distributed Replay を使用する前に必要なインストール後のセキュリティ構成手順について説明します。 また、データ保護に関する重要な考慮事項や、重要な削除手順についても説明します。  
  
## <a name="user-and-service-accounts"></a>ユーザーおよびサービスのアカウント  
 次の表に、Distributed Replay に使用するアカウントを示します。 Distributed Replay をインストールした後、コントローラーおよびクライアントのサービス アカウントを実行するセキュリティ プリンシパルを割り当てる必要があります。 したがって、Distributed Replay 機能をインストールする前に、対応するドメイン ユーザー アカウントを構成することをお勧めします。  
  
|ユーザー アカウント|必要条件|  
|------------------|------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller のサービス アカウント|ドメイン ユーザー アカウントまたはローカル ユーザー アカウントを使用できます。 ローカル ユーザー アカウントを使用する場合、管理ツール、コントローラー、およびクライアントのすべてが同じコンピューター上で実行されている必要があります。<br /><br /> **\*\* セキュリティに関する注意 \*\*** このアカウントには、Windows のローカルの Administrators グループのメンバー以外を使用することをお勧めします。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client のサービス アカウント|ドメイン ユーザー アカウントまたはローカル ユーザー アカウントを使用できます。 ローカル ユーザー アカウントを使用する場合、コントローラー、クライアント、および対象の SQL Server のすべてが同じコンピューター上で実行されている必要があります。<br /><br /> **\*\* セキュリティに関する注意 \*\*** このアカウントには、Windows のローカルの Administrators グループのメンバー以外を使用することをお勧めします。|  
|Distributed Replay 管理ツールの実行に使用する対話ユーザー アカウント|ローカル ユーザーまたはドメイン ユーザー アカウントを使用できます。 ローカル ユーザー アカウントを使用するには、管理ツールとコントローラーが同じコンピューター上で実行されている必要があります。|  
  
 **重要**: 分散再生コントローラーを構成するとき、分散再生クライアント サービスの実行に使用する 1 つ以上のユーザー アカウントを指定できます。 サポートされているアカウントの一覧を次に示します。  
  
-   ドメイン ユーザー アカウント  
  
-   ユーザーによって作成されたローカル ユーザー アカウント  
  
-   管理者  
  
-   仮想アカウントおよび管理されたサービス アカウント (MSA)  
  
-   ネットワーク サービス、ローカル サービス、およびシステム  
  
 グループ アカウント (ローカルまたはドメイン) およびその他の組み込みのアカウント (Everyone など) は使用できません。  
  
 Distributed Replay のインストール後にサービス アカウントまたはそのパスワードを設定するには、Windows サービス ツールを使用します。 Distributed Replay Controller または Client サービスに関連付けられているサービス アカウントを変更するには、次の手順を実行します。  
  
1.  オペレーティング システムに応じて、次のいずれかを実行します。  
  
    -   **[スタート]** ボタンをクリックし、 **[検索の開始]** ボックスに「 **services.msc** 」と入力して Enter キーを押します。  
  
    -   **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。「 **services.msc**」と入力して Enter キーを押します。  
  
2.  **[サービス]** ダイアログ ボックスで、構成するサービスを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで、 **[このアカウント]** をクリックします。  
  
4.  使用するユーザー アカウントを構成します。  
  
## <a name="file-and-folder-permissions"></a>ファイルおよびフォルダーの権限  
 サービス アカウントを指定したら、それらのサービス アカウントに必要なファイルおよびフォルダーの権限を付与する必要があります。 次の表に従ってファイルおよびフォルダーの権限を構成します。  
  
|アカウント|フォルダー権限|  
|-------------|------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller のサービス アカウント|`<Controller_Installation_Path>\DReplayController` (読み取り、書き込み、削除)<br /><br /> `DReplayServer.xml` ファイル (読み取り、書き込み)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client のサービス アカウント|`<Client_Installation_Path>\DReplayClient` (読み取り、書き込み、削除)<br /><br /> `DReplayClient.xml` ファイル (読み取り、書き込み)<br /><br /> クライアント構成ファイルで `WorkingDirectory` 要素および `ResultDirectory` 要素により指定された作業ディレクトリおよび結果ディレクトリ。 (読み取り、書き込み)|  
  
## <a name="dcom-permissions"></a>DCOM 権限  
 DCOM は、コントローラーと管理ツールの間、およびコントローラーとすべてのクライアントの間のリモート プロシージャ コール (RPC) 通信に使用されます。 Distributed Replay 機能をインストールした後、コント ローラーでコンピューター全体およびアプリケーション固有の DCOM 権限を構成する必要があります。  
  
 コントローラーの DCOM 権限を構成するには、次の手順を実行します。  
  
1.  **コンポーネント サービス スナップイン dcomcnfg.exe を開く**: dcomcnfg.exe は、DCOM 権限を構成するために使用するツールです。  
  
    1.  コントローラーのコンピューターで、 **[スタート]** ボタンをクリックします。  
  
    2.  **[検索]** ボックスに「 **dcomcnfg.exe** 」と入力します。  
  
    3.  Enter キーを押します。  
  
2.  **コンピューター全体の DCOM 権限を構成する**: 次の表に示す各アカウントに対し、対応するコンピューター全体の DCOM 権限を付与します。 コンピューター全体の権限を設定する方法の詳細については、「 [チェック リスト: DCOM アプリケーションを管理する](https://go.microsoft.com/fwlink/?LinkId=185842)」を参照してください。  
  
3.  **アプリケーション固有の DCOM 権限を構成する**: 次の表に示す各アカウントに対し、対応するアプリケーション固有の DCOM 権限を付与します。 コントローラー サービスの DCOM アプリケーション名は **DReplayController**です。 アプリケーション固有の権限を設定する方法の詳細については、「 [チェック リスト: DCOM アプリケーションを管理する](https://go.microsoft.com/fwlink/?LinkId=185842)」を参照してください。  
  
 次の表に、管理ツールの対話ユーザー アカウントとクライアント サービス アカウントに必要な DCOM 権限を示します。  
  
|機能|アカウント|コントローラーで必要な DCOM 権限|  
|-------------|-------------|---------------------------------------------|  
|Distributed Replay 管理ツール|対話ユーザー アカウント|ローカル アクセス<br /><br /> リモート アクセス<br /><br /> ローカルからの起動<br /><br /> リモートからの起動<br /><br /> ローカルからのアクティブ化<br /><br /> リモートからのアクティブ化|  
|[分散再生クライアント]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client のサービス アカウント|ローカル アクセス<br /><br /> リモート アクセス<br /><br /> ローカルからの起動<br /><br /> リモートからの起動<br /><br /> ローカルからのアクティブ化<br /><br /> リモートからのアクティブ化|  
  
> [!IMPORTANT]  
>  悪意のあるクエリまたはサービス拒否攻撃を防ぐために、クライアント サービス アカウントには信頼できるユーザー アカウントのみを使用してください。 このアカウントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の対象のインスタンスに対して接続とワークロードの再生を実行できるようになります。  
  
## <a name="sql-server-permissions"></a>SQL Server 権限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client のサービス アカウントは、ワークロードの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]対象インスタンスに接続するために使用されます。 これらの接続では、Windows 認証モードのみがサポートされます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client サービスを一連のコンピューターにインストールした後、それらのサービス アカウントに使用されるセキュリティ プリンシパルに、トレース ワークロードの再生対象である [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス上の sysadmin サーバー ロールを付与する必要があります。 この手順は、Distributed Replay のセットアップで自動的に実行されません。  
  
## <a name="data-protection"></a>データ保護  
 Distributed Replay 環境では、次のユーザー アカウントに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のターゲット サーバー インスタンス、入力トレース データ、および結果トレース ファイルへのフル アクセスが付与されます。  
  
-   管理ツールの実行に使用される対話ユーザー アカウント。  
  
-   コントローラーのサービス アカウント。  
  
-   クライアントのサービス アカウント。  
  
-   コントローラー上のローカルの Administrators グループのメンバー。  
  
-   クライアント上のローカルの Administrators グループのメンバー。  
  
    > [!IMPORTANT]  
    >  これらのアカウントは、Distributed Replay によって使用されるトレース ファイル、中間ファイル、ディスパッチ ファイル、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ファイルに含まれるすべての個人情報 (PII) または機密情報へのフル アクセス権を保持します。  
  
 次のセキュリティ対策をとることをお勧めします。  
  
-   NTFS ファイル システム (NTFS) を使用する場所に、入力トレース データ、出力トレース結果、およびデータベース ファイルを格納し、適切なアクセス制御リスト (ACL) を適用します。 必要に応じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターに格納されるデータを暗号化します。 ACL はトレース ファイルに適用されず、データのマスキングや難読化もないことに注意してください。 これらのファイルは使用後すぐに削除する必要があります。  
  
-   Distributed Replay によって生成されたすべての中間ファイルおよびディスパッチ ファイルに、適切な ACL と保有ポリシーを適用します。  
  
-   Secure Sockets Layer (SSL) を使用して、ネットワーク トランスポートを保護します。  
  
## <a name="important-removal-steps"></a>重要な削除手順  
 Distributed Replay はテスト環境のみで使用することをお勧めします。 テストが完了したら、それらのコンピューターを別のタスク用に準備する前に、次の作業を必ず行います。  
  
-   Distributed Replay 機能をアンインストールし、関連する構成ファイルをコントローラーおよびすべてのクライアントから削除します。  
  
-   テストに使用したトレース ファイル、中間ファイル、ディスパッチ ファイル、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ファイルをすべて削除します。 中間ファイルとディスパッチ ファイルは、コントローラーとクライアントの作業ディレクトリにそれぞれ格納されます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [分散再生のインストール - 概要](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
  
