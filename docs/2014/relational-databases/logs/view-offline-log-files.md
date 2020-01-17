---
title: オフライン ログ ファイルの表示 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer, viewing offline logs
- offline log files
ms.assetid: 9223e474-f224-4907-a4f2-081e11db58f5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5547d5fb1c2b083a51837df5d9cacb1be393f555
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144598"
---
# <a name="view-offline-log-files"></a>オフライン ログ ファイルの表示
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降では、対象となるインスタンスがオフラインの場合または開始できない場合に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ ファイルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカルまたはリモート インスタンスから表示できます。  
  
 登録済みサーバーから、またはプログラムにより WMI および WQL (WMI Query Language) クエリを通じて、オフラインのログ ファイルにアクセスできます。  
  
> [!NOTE]  
>  これらの方法によってオンラインのインスタンスに接続することもできますが、ある理由により、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続で接続することはできません。  
  
## <a name="before-you-begin"></a>作業を開始する準備  
 オフライン ログ ファイルに接続するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが、オフライン ログ ファイルの表示に使用するコンピューターと、表示するログ ファイルが置かれているコンピューターにインストールされている必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが両方のコンピューターにインストールされている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス、およびどちらかのコンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンを実行しているインスタンスのオフライン ファイルを表示できます。  
  
 登録済みサーバーを使用している場合は、接続するインスタンスが **[ローカル サーバー グループ]** または **[中央管理サーバー]** で登録されている必要があります。 (インスタンスは自身に登録するか、またはサーバー グループのメンバーにすることができます)。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを登録済みサーバーに追加する方法の詳細については、次のトピックを参照してください。  
  
-   [サーバー グループの作成または編集 &#40;SQL Server Management Studio&#41;](../../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [接続済みのサーバーの登録 &#40;SQL Server Management Studio&#41;](../../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)  
  
-   [中央管理サーバーとサーバー グループの作成 &#40;SQL Server Management Studio&#41;](../../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
 プログラムにより WMI および WQL クエリでオフライン ログ ファイルを表示する方法の詳細については、次のトピックを参照してください。  
  
-   [SqlErrorLogEvent Class](../wmi-provider-configuration-classes/sqlerrorlogevent-class.md) (このトピックでは、特定のログ ファイルで記録されたイベントの値を取得する方法について説明しています。)  
  
-   [SqlErrorLogFile Class](../wmi-provider-configuration-classes/sqlerrorlogfile-class.md) (このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の指定されたインスタンス上のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログ ファイルに関する情報を取得する方法について説明しています。)  
  
##  <a name="BeforeYouBegin"></a> Permissions  
 オフラインのログ ファイルに接続するには、ローカルおよびリモートの両方のコンピューターで次の権限が必要です。  
  
-   **Root\Microsoft\SqlServer\ComputerManagement12** WMI 名前空間への読み取りアクセス。 既定では、すべてのユーザーがアカウントの有効化権限による読み取りアクセスを持ちます。 詳細については、このセクションで後述する「WMI 権限を確認するには」を参照してください。  
  
-   エラー ログ ファイルを含むフォルダーへの読み取り権限。 既定では、エラー ログ ファイルは、次のパスにあります (\<*Drive>* は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール先ドライブ、\<*InstanceName*> は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス名です)。  
  
     **\<Drive>:\Program Files\Microsoft SQL Server\MSSQL12.\<InstanceName>\MSSQL\Log**  
  
 WMI 名前空間のセキュリティ設定を確認するには、WMI コントロール スナップインを使用します。  
  
#### <a name="to-verify-wmi-permissions"></a>WMI 権限を確認するには  
  
1.  WMI コントロール スナップインを開きます。 これを行うには、次のいずれかの操作を実行します (オペレーティング システムによって異なります)。  
  
    -   クリックして**開始**、型`wmimgmt.msc`で、**検索の開始**ボックス、および ENTER キーを押します。  
  
    -   クリックして**開始**、 をクリックして**実行**、型`wmimgmt.msc`、し、ENTER キーを押します。  
  
2.  既定では、WMI コントロール スナップインはローカル コンピューターを管理します。  
  
     リモート コンピューターに接続する場合は、次の手順を実行します。  
  
    1.  **[WMI コントロール (ローカル)]** を右クリックし、 **[別のコンピューターへ接続]** をクリックします。  
  
    2.  **[管理するコンピューターの変更]** ダイアログ ボックスで **[別のコンピューター]** をクリックします。  
  
    3.  リモート コンピューター名を入力し、 **[OK]** をクリックします。  
  
3.  **[WMI コントロール (ローカル)]** または **[WMI コントロール (***RemoteComputerName***)]** を右クリックして、 **[プロパティ]** をクリックします。  
  
4.  **[WMI コントロールのプロパティ]** ダイアログ ボックスで、 **[セキュリティ]** タブをクリックします。  
  
5.  名前空間ツリーで、次の名前空間を探してクリックします。  
  
     **Root\Microsoft\SqlServer\ComputerManagement10**  
  
6.  **[セキュリティ]** をクリックします。  
  
7.  使用するアカウントに **[アカウントの有効化]** 権限があることを確認します。 この権限により、WMI オブジェクトへの読み取りアクセスが許可されます。  
  
### <a name="view-log-files"></a>ログ ファイルの表示  
 次の手順は、登録済みサーバーを使用してオフラインのログ ファイルを表示する方法を示します。 この手順の前提条件は次のとおりです。  
  
 接続する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが登録済みサーバーに登録されていること。  
  
##### <a name="to-view-log-files-for-instances-that-are-offline"></a>オフラインのインスタンスのログ ファイルを表示するには  
  
1.  ローカル インスタンス上のオフライン ログ ファイルを表示するには、高度な権限で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を起動してください そのためには、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を起動するときに、 **[SQL Server Management Studio]** を右クリックして、 **[管理者として実行]** をクリックします。  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[表示]** メニューの **[登録済みサーバー]** をクリックします。  
  
3.  コンソール ツリーで、オフライン ファイルを表示するインスタンスを特定します。  
  
4.  次のいずれかの操作を行います。  
  
    -   インスタンスが **[ローカル サーバー グループ]** の下にある場合は、 **[ローカル サーバー グループ]** を展開し、サーバー グループを展開します (インスタンスがグループのメンバーである場合)。次に、インスタンスを右クリックして **[SQL Server ログの表示]** をクリックします。  
  
    -   インスタンスが中央管理サーバーである場合は、 **[中央管理サーバー]** を展開し、インスタンスを右クリックして **[中央管理サーバーのアクション]** をポイントし、 **[SQL Server ログの表示]** をクリックします。  
  
    -   インスタンスが **[中央管理サーバー]** の下にある場合は、 **[中央管理サーバー]** を展開し、中央管理サーバーを展開してインスタンスを右クリックし (またはサーバー グループを展開してインスタンスを右クリックし)、 **[SQL Server ログの表示]** をクリックします。  
  
5.  ローカル インスタンスに接続している場合は、現在のユーザー資格情報を使用して接続が行われます。  
  
     リモート インスタンスに接続している場合は、 **[ログ ファイルの表示 - 接続するユーザー]** ダイアログ ボックスで、次のいずれかの操作を行います。  
  
    -   現在のユーザーとして接続するには、 **[別のユーザーとして接続する]** チェック ボックスがオフになっていることを確認し、 **[OK]** をクリックします。  
  
    -   別のユーザーとして接続するには、 **[別のユーザーとして接続する]** チェック ボックスをオンにし、 **[ユーザーを設定]** をクリックします。 ユーザー資格情報を求められたら入力し (ユーザー名を *domain_name*\\*user_name*の形式で入力します)、 **[OK]** をクリックします。再度 **[OK]** をクリックして接続します。  
  
    > [!NOTE]  
    >  ログ ファイルの読み込みに時間がかかりすぎる場合は、[ログ ファイルの表示] ツール バーの **[停止]** をクリックできます。  
  
## <a name="see-also"></a>関連項目  
 [ログ ファイルの表示](log-file-viewer.md)  
  
  
