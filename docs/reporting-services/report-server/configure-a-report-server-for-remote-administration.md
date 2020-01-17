---
title: リモート管理用のレポート サーバーの構成 | Microsoft Docs
ms.date: 09/14/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- WMI provider [Reporting Services], remote configuration
- configuration management [WMI]
- report servers [Reporting Services], configuring
- remote server administration [Reporting Services]
ms.assetid: 8c7f145f-3ac2-4203-8cd6-2a4694395d09
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 48e8662f3547e9e483d67cc4af83e67d355ba664
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580416"
---
# <a name="configure-a-report-server-for-remote-administration"></a>リモート管理用のレポート サーバーの構成
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、レポート サーバー インスタンスをローカルでもリモートでも構成できます。 リモートのレポート サーバー インスタンスを構成するには、Reporting Services 構成ツールを使用するか、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI (Windows Management Instrumentation) プロバイダーを利用するカスタム コードを作成します。 Reporting Services 構成ツールには WMI プロバイダーのグラフィカル インターフェイスが用意されているので、コードを記述しなくてもレポート サーバーの構成を行えます。 このツールを起動する際に、接続先のリモート サーバーを指定できます。  
  
 ツールを使用してリモートのレポート サーバーを構成するには、このトピックの説明に従って Windows ファイアウォールでポートを有効にし、リモート接続とリモート WMI 要求も有効にしておく必要があります。  
  
 適切な構成を行うと、次のエラーを回避できます。  
  
 `The machine could not be found.`  
  
 `"The RPC server is unavailable. (Exception from HRESULT: 0x800706BA)".`  
  
## <a name="prerequisites"></a>Prerequisites  
 ファイアウォールの設定を変更するには、ローカルの Administrators グループのメンバーとして、ローカルでログオンする必要があります。 リモート接続を経由してリモート コンピューターの Windows のファイアウォール設定を変更することはできません。  
  
 管理者以外のユーザーがリモート管理を実行できるようにするには、DCOM (Distributed Component Object Model) の "リモートからのアクティブ化" アクセス許可をアカウントに与える必要があります。 管理者以外のユーザーがアクセスできるようにサーバーを構成する手順は、このトピックで説明します。  
  
 組織によっては、特定のオペレーティング システムまたはユーザーに対して、リモート サーバー管理を禁じるグループ ポリシーが定められている場合があります。 ファイアウォールの設定を変更する前に、リモート管理に対する制限があるかどうかをネットワーク管理者に確認してください。  
  
 詳細については、MSDN のプラットフォーム SDK ドキュメントの「 [Windows ファイアウォールを使用した接続](https://go.microsoft.com/fwlink/?LinkId=63615) 」を参照してください。  
  
## <a name="tasks"></a>処理手順  
 リモートのレポート サーバー構成を有効にするタスクは次のとおりです。  
  
-   Windows ファイアウォールでポートを有効にし、レポート サーバーおよび SQL Server データベース エンジン インスタンスによって使用されるポートで要求が許可されるようにします。  「 [レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 」および「 [データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)」を参照してください。  
  
-   レポート サーバー データベースをホストするデータベース エンジン インスタンスへのリモート接続を有効にします。 リモート接続は、レポート サーバー データベース接続の構成と暗号化キーの管理のために必要です。  
  
-   リモート WMI 要求が [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ファイアウォールを通過できるようにします。  
  
-   管理者以外のユーザーが管理を実行できるようにリモートのレポート サーバーを構成するには、DCOM 権限の設定で、標準 Windows ユーザー アカウントに対してリモート WMI アクセスを有効にする必要があります。 WMI ではリモート呼び出しのトランスポートとして DCOM を使用するため、ローカル管理者としてログオンしていないユーザーがサーバーを構成できるようにするには、DCOM 権限を設定する必要があります。  
  
-   管理者以外のユーザーが管理を実行できるようにリモートのレポート サーバーを構成するには、レポート サーバーの WMI 名前空間に対する WMI 権限も設定する必要があります。 既定では、ローカルの Administrator グループの全メンバーがレポート サーバーの WMI 名前空間にアクセスできます。 管理者以外のユーザーにアクセスを許可するには、アクセス許可を設定する必要があります。  
  
 このトピックでは、これらのタスクを実行する方法について説明します。  
  
### <a name="to-configure-remote-connections-to-the-report-server-database"></a>レポート サーバー データベースへのリモート接続を構成するには  
  
1.  **[スタート]** ボタンをクリックし、 **[プログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  左側のペインで、 **[SQL Server ネットワークの構成]** を展開し、 **のインスタンスの** [プロトコル] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をクリックします。  
  
3.  詳細ペインで TCP/IP プロトコルおよび名前付きパイプ プロトコルを有効にし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再起動します。  
  
### <a name="to-enable-remote-administration-in-windows-firewall"></a>Windows ファイアウォールでリモート管理を有効にするには  
  
1.  リモート管理を有効にするコンピューターに、ローカル管理者としてログオンします。  
  
2.  管理者特権を使用してコマンド プロンプトを開きます。  
  
3.  次のコマンドを実行します。  
  
    ```  
    netsh.exe firewall set service type=REMOTEADMIN mode=ENABLE scope=ALL  
    ```  
  
     スコープには他のオプションも指定できます。 詳細については、Windows ファイアウォールのマニュアルを参照してください。  
  
4.  リモート管理が有効になったかどうかを確認します。 次のコマンドを実行して、状態を表示します。  
  
    ```  
    netsh.exe firewall show state  
    ```  
  
5.  コンピューターを再起動します。  
  
### <a name="to-set-dcom-permissions-to-enable-remote-wmi-access-for-non-administrators"></a>DCOM 権限を設定して管理者以外のユーザーによるリモート WMI アクセスを有効にするには  
  
1.  [スタート] メニューで、 **[管理ツール]** をポイントし、 **[コンポーネント サービス]** をクリックします。  
  
     Windows Vista の場合は、[スタート] メニューの **[すべてのプログラム]** 、 **[ファイル名を指定して実行]** の順にクリックし、「 **mmc comexp.msc**」と入力します。  
  
2.  [コンポーネント サービス] フォルダーを開きます。  
  
3.  [コンピューター] フォルダーを開きます。  
  
4.  [マイ コンピューター] を選択します。  
  
5.  **[操作]** メニューの **[プロパティ]** を選択します。  
  
6.  **[COM セキュリティ]** をクリックします。  
  
7.  **[起動とアクティブ化のアクセス許可]** で、 **[制限の編集]** をクリックします。  
  
8.  **[起動許可]** に自分の名前が表示されない場合は、 **[追加]** をクリックします。  
  
9. 自分のアカウントの名前を入力して、 **[OK]** をクリックします。  
  
10. **[\<ユーザーまたはグループ のアクセス許可>]** で、 **[許可]** 列の **[リモートからの起動]** と **[リモートからのアクティブ化]** をオンにして、 **[OK]** をクリックします。  
  
### <a name="to-set-permissions-on-the-report-server-wmi-namespace-for-non-administrators"></a>管理者以外のユーザーにレポート サーバーの WMI 名前空間に対する権限を設定するには  
  
1.  [スタート] メニューで、 **[管理ツール]** をポイントし、 **[コンピューターの管理]** をクリックします。  
  
2.  [サービスとアプリケーション] フォルダーを開きます。  
  
3.  **[WMI コントロール]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[セキュリティ]** をクリックします。  
  
5.  Root フォルダーを開きます。  
  
6.  Microsoft フォルダーを開きます。  
  
7.  SQLServer フォルダーを開きます。  
  
8.  ReportServer フォルダーを開きます。  
  
9. インスタンス フォルダーを開きます。 既定のインスタンスをインストールした場合、フォルダーは MSSQLSERVER です。  
  
10. v10 フォルダーを開きます。  
  
11. Admin フォルダーを選択し、 **[セキュリティ]** をクリックします。  
  
12. **[追加]** をクリックして、サーバーを管理するために使用するユーザー アカウントを入力します。  
  
13. **[許可]** 列の **[アカウントの有効化]** 、 **[リモートの有効化]** 、 **[セキュリティの読み取り]** をオンにして、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
  
