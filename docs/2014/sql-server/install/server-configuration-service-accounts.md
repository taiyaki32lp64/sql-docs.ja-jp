---
title: サーバーの構成 - サービス アカウント |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- service account configuration, SQL Server
ms.assetid: c283702d-ab20-4bfa-9272-f0c53c31cb9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8435b0c677f80bf4f26acd4411d90ab63c7473d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092268"
---
# <a name="server-configuration---service-accounts"></a>サーバーの構成 - サービス アカウント
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードの [サーバーの構成] ページを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスにログイン アカウントを割り当てます。 このページで構成する実際のサービスは、インストール時に選択した機能によって異なります。  
  
 起動し、実行するために使用する開始アカウント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]HYPERLINK"ms help://SQL11_I1033/s11sq_GetStart_I/html/309b9dac-0b3a-4617-85ef-c4519ce9d014.htm"\l"Domain_User"ドメイン ユーザー アカウント、ローカル ユーザー アカウント、管理されたサービスのアカウントを指定できます仮想アカウント、またはビルトイン システム アカウント。  
  
## <a name="options"></a>および  
 すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに同じログイン アカウントを割り当てることも、各サービス アカウントを個々に構成することもできます。 サービスを自動的に開始するか、手動で開始するか、または無効にするかを指定することもできます。 ほとんどのインストールでは、既定のアカウントをお勧めします。  
  
 Windows 7 および [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 では、ほとんどのアカウントが既定で仮想アカウントに設定されます。  
  
 サービスを構成してドメイン アカウントを使用する場合、[!INCLUDE[msCoName](../../includes/msconame-md.md)] では、各サービスに最小の権限を与えるために、サービス アカウントを個別に構成することをお勧めします。サービス アカウントを個別に構成すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスには、サービスでのタスクの実行に必要な最小権限が付与されます。 アカウントの種類の説明などの詳細については、「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
 **構成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービス アカウントを個別に (推奨)**  
 グリッドを使用して各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスにログオン ユーザー名とパスワードを提供し、サービスのスタートアップの種類を設定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスには、ビルトイン システム アカウント、ローカル アカウント、ローカル グループ アカウント、ドメイン グループ アカウント、またはドメイン ユーザー アカウントを使用できます。  
  
 以下のサービスのいずれかを選択し、設定をカスタマイズします。  
  
|選択するサービス|認証設定を構成する対象|  
|-------------------------|----------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント|ジョブ、モニター、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行し、管理タスクの自動化を可能にするサービス。<br /><br /> このサービスの既定のログオン アカウントはありません。<br /><br /> 既定のスタートアップの種類は [手動] です。|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|既定のスタートアップの種類は [自動] です。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|既定のスタートアップの種類は [自動] です。<br /><br /> SharePoint 統合モードの場合、Windows のドメイン ユーザー アカウントを指定する必要があります。 指定したアカウントは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サービスに使用されます。 現在のインスタンスに指定するアカウントは、その後に同じファームに追加した [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスにも使用する必要があります。|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|サービス アカウントはレポート サーバー データベースの接続を構成するために使用されます。 既定の認証設定を使用する場合は、組み込みのネットワーク サービスを選択します。 ドメイン ユーザー アカウントを指定する場合、レポート サーバーで Windows 認証を使用しているときは、そのドメイン ユーザー アカウントのサービス プリンシパル名 (SPN) を登録します。 詳細については、「[レポート サーバーで Windows 認証を構成する](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)」を参照してください。<br /><br /> 既定のスタートアップの種類は [自動] です。|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、データを移動、コピー、変換するためのグラフィカル ツールおよびプログラミング可能なオブジェクトのセットです。<br /><br /> 既定のスタートアップの種類は [自動] です。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生クライアント|分散再生クライアントのサービスで使用されるサービス アカウント。<br /><br /> 分散再生クライアントのサービスを実行するアカウントを指定します。 このアカウントには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに使用するアカウントとは別のアカウントを指定する必要があります。<br /><br /> 既定のスタートアップの種類は [手動] です。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生コントローラー|分散再生コントローラー サービスのサービス アカウント。<br /><br /> 分散再生コントローラー サービスを実行するアカウントを指定します。 このアカウントには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに使用するアカウントとは別のアカウントを指定する必要があります。<br /><br /> 既定のスタートアップの種類は [手動] です。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フルテキスト フィルター デーモン ランチャー|fdhost.exe プロセスを作成するサービスです。 このサービスは、フルテキスト インデックスのテキスト データを処理する、ワード ブレーカーおよびフィルターをホストするために必要です。<br /><br /> FDHOST ランチャー サービスを実行するドメイン アカウントを指定する場合は、権限の低いアカウントを使用することを強くお勧めします。 このアカウントには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに使用するアカウントとは別のアカウントを指定する必要があります。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ブラウザー|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は、クライアント コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続情報を提供する名前解決サービスです。 このサービスは複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] インスタンス間で共有されます。 既定のログオン アカウントは NT Authority\Local Service で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ中には変更できません。 アカウントはセットアップの完了後に変更できます。 スタートアップの種類をセットアップ中に指定しない場合、種類は次のようにして決まります。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser が [自動] に設定され、次に示すインストール シナリオで実行されます。<br />-<br />                            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス<br />-<br />                            TCP または NP が有効になっている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンス<br />-<br />                            クラスター化されていない分析サーバーの名前付きインスタンス<br /><br /> 上記のシナリオのいずれにも該当せず、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser が既にインストールされている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser の現在の状態が継続されます。<br /><br /> インストールの前に古い [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンの既存のインスタンスが存在しない場合、スタートアップの種類が [無効] に設定され、停止します。|  
  
## <a name="see-also"></a>参照  
 [SQL Server インストールにおけるセキュリティの考慮事項](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
