---
title: SQL Server ユーティリティのトラブルシューティング |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: f5f47c2a-38ea-40f8-9767-9bc138d14453
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d5203a0a613bcd8af4b247058f3cb594be5d4c3f
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797780"
---
# <a name="troubleshoot-the-sql-server-utility"></a>SQL Server ユーティリティのトラブルシューティング
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティのトラブルシューティングの項目としては、UCP を使用した SQL Server インスタンスの登録処理の失敗の解決、データ収集の失敗 (UCP のマネージド インスタンスのリスト ビューで灰色のアイコンが表示される) に対するトラブルシューティング、パフォーマンス ボトルネックの緩和、リソースの正常性に関する問題の解決などがあります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] UCP によって識別されるリソース正常性の問題の軽減の詳細については、「 [SQL Server Resource Health &#40;&#41;SQL Server ユーティリティのトラブルシューティング](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)」を参照してください。  
  
## <a name="failed-operation-to-enroll-an-instance-of-sql-server-into-a-sql-server-utility"></a>SQL Server インスタンスを SQL Server ユーティリティに登録する処理の失敗  
 登録する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用して接続し、UCP があるドメインとは異なる Active Directory ドメインに属するプロキシ アカウントを指定した場合、インスタンスの検証には成功しますが、次のエラー メッセージが表示されて登録処理に失敗します。  
  
 Transact-SQL ステートメントまたはバッチの実行中に例外が発生しました。 (Microsoft.SqlServer.ConnectionInfo)  
  
 追加情報: Windows NT グループまたはユーザー '\<ドメイン名\アカウント名>' に関する情報を取得できませんでした。エラー コード 0x5。 (Microsoft SQL Server、エラー: 15404)  
  
 この問題は、次のようなシナリオで発生します。  
  
1.  UCP は "Domain_1" のメンバーです。  
  
2.  一方向のドメイン信頼関係が存在します。つまり、"Domain_1" は "Domain_2" から信頼されていませんが、"Domain_2" は "Domain_1" から信頼されています。  
  
3.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティに登録する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスは、"Domain_1" のメンバーでもあります。  
  
4.  登録操作中に、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスに接続して、"sa" を使用して登録します。 "Domain_2" からのプロキシ アカウントを指定します。  
  
5.  検証に成功しますが、登録に失敗します。  
  
 上記の例を使用してこの問題の回避策として、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスに接続し、"sa" を使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティに登録し、"Domain_1" からプロキシアカウントを指定します。  
  
## <a name="failed-wmi-validation"></a>WMI 検証の失敗  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]インスタンスで WMI が正しく構成されていない場合は、UCP の作成操作とマネージド インスタンスの登録操作で警告が表示されますが、操作はブロックされません。 また、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントが目的の WMI クラスに対する権限を持たないように [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント アカウントの構成を変更した場合、影響を受ける [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスでデータ収集を行うと UCP へのアップロードに失敗します。 この結果、UCP に灰色のアイコンが表示されます。  
  
 データ収集が失敗した結果、影響を受ける [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンスの UCP リスト ビューに灰色の状態アイコンが表示されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスのジョブ履歴には、sysutility_mi_collect_and_upload がステップ 2 (PowerShell スクリプトから収集されたデータのステージング) で失敗したことが示されます。  
  
 エラー メッセージの要約は次のとおりです。  
  
 シェル変数 "ErrorActionPreference" が Stop に設定されているため、コマンドの実行が停止しました: アクセスが拒否されました。  
  
 エラー: \<の日付/時刻 (MM/DD/YYYY HH: MM: SS) >: cpu プロパティの収集中に例外が発生しました。  WMI クエリに失敗した可能性があります。  警告。  
  
 この問題を解決するには、次の構成設定を確認します。  
  
-   Windows Server 2003 上で、SQL Server エージェント サービスは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンスの Windows Performance Monitoring グループに属している必要があります。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンス上で、WMI サービスが有効になっており、構成されている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンス上で、WMI リポジトリが破損している可能性があります。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンス上で、パフォーマンス ライブラリが欠落または破損している可能性があります。  
  
 指定した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスが UCP にデータを報告するように正しく構成されていることを検証するには、指定した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]インスタンスで次のクラスが使用可能であり、SQL Server エージェント サービス アカウントからこれらのクラスにアクセスできるかどうかを確認します。  
  
-   Win32_MountPoint  
  
-   Win32_PerfRawData_PerfProc_Process  
  
-   Win32_PerfRawData_PerfOS_Processor  
  
-   Win32_Processor  
  
-   Win32_Volume  
  
-   Win32_LogicalDisk  
  
 各クラスで Get-WmiObject PowerShell コマンドレットを使用して、各クラスにアクセスできるかどうかを確認します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンスで、次のコマンドレットを実行します。  
  
```  
Get-WmiObject Win32_MountPoint -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_PerfRawData_PerfProc_Process -ErrorAction Stop| Out-Null  
Get-WmiObject Win32_PerfRawData_PerfOS_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Volume -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_LogicalDisk -ErrorAction Stop | Out-Null  
```  
  
 WMI のトラブルシューティングの詳細については、「 [wmi のトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=178250)」を参照してください。 SQL Server ユーティリティのこれらの操作におけるクエリはローカルで実行されるので、DCOM およびリモート トラブルシューティングの内容は適用されません。  
  
## <a name="failed-data-collection"></a>データ収集の失敗  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティのデータ収集イベントが失敗した場合は、次の可能性を検討してください。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンス上の "ユーティリティ情報" コレクション セットのプロパティは一切変更しないでください。また、データ コレクションはユーティリティ エージェント ジョブによって制御されるため、データ コレクションのオン/オフを手動で切り替えることも避けてください。  
  
-   WMI 検証に失敗したか、この機能がサポートされていません。 詳細については、このトピックの前半の「WMI 検証の失敗」を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティのビューポイントのデータは自動的に更新されないため、マネージド インスタンスのリスト ビューのデータを手動で更新してください。 データを更新するには、 **ユーティリティ エクスプローラー** のナビゲーション ウィンドウで **[マネージド インスタンス]** ノードを右クリックして **[更新]** をクリックするか、リスト ビューで [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス名を右クリックして **[更新]** をクリックします。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスが UCP に登録された後、ユーティリティ エクスプローラーのコンテンツ ウィンドウ内のダッシュボードとビューポイントに最初に表示されるまでに最大 30 分かかる場合があります。  
  
-   SQL Server 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスが実行されていることを確認します。  
  
-   データ コレクションまたはデータ アップロードがタイムアウトの問題で失敗する場合は、MSDB データベースの dbo.fn_sysutility_mi_get_collect_script() 関数を更新します。 具体的には、"Invoke-BulkCopyCommand()" 関数に次の行を追加します。  
  
    ```
    $bulkCopy.BulkCopyTimeout=180  
    ```  
  
     タイムアウトの既定値は 30 秒です。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスがクラスター化されていない場合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント サービスが実行されていることと、このサービスが UCP、および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンスで自動的に開始するように設定されていることを確認します。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンスでデータ収集を実行するために有効なアカウントが使用されていることを確認します。 たとえば、パスワードの有効期限が切れている可能性があります。 プロキシ パスワードの有効期限が切れている場合は、次のように、SSMS でパスワード資格情報を更新します。  
  
    1.  SSMS の **オブジェクト エクスプローラー**で、 **[セキュリティ]** ノードを展開し、 **[資格情報]** ノードを展開します。  
  
    2.  **UtilityAgentProxyCredential_\<GUID >** を右クリックし、 **[プロパティ]** を選択します。  
  
    3.  [資格情報のプロパティ] ダイアログボックスで、必要に応じて**UtilityAgentProxyCredential_\<GUID >** 資格情報を更新します。  
  
    4.  **[OK]** をクリックして変更を確認します。  
  
-   TCP/IP は、UCP と [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンスで有効にしておく必要があります。 TCP/IP は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを使用して有効にします。  
  
-   UCP の SQL Server Browser サービスを開始して、自動的に開始するように構成する必要があります。 組織の方針で SQL Server Browser サービスを使用できない場合は、次の手順を実行して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスから UCP に接続できるようにします。  
  
    1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージインスタンスの Windows タスクバーで、 **[スタート]** をクリックし、 **[実行]** をクリックします。  
  
    2.  該当するボックスに「cliconfg.exe」と入力し、 **[OK]** をクリックします。  
  
    3.  "SQL クライアント設定ユーティリティ EXE" の起動を許可するように求めるメッセージが表示されたら、 **[続行]** をクリックします。  
  
    4.  **[クライアントネットワークユーティリティの SQL Server]** ダイアログボックスで、 **[別名]** タブを選択し、 **[追加]** をクリックします。  
  
    5.  **[ネットワーク ライブラリ設定の追加]** ダイアログ ボックスで、次の操作を行います。  
  
    6.  ネットワーク ライブラリの一覧で、[TCP/IP] を指定します。  
  
    7.  **[サーバー別名]** ボックスに、UCP の ComputerName\InstanceName を指定します。  
  
    8.  **[サーバー名]** ボックスに、UCP の ComputerName を指定します。  
  
    9. **[ポートを動的に決定する]** チェック ボックスをオフにします。  
  
    10. **[ポート番号]** ボックスに、UCP がリッスンしているポート番号を指定します。  
  
    11. **[OK]** をクリックして変更を保存します。  
  
    12. SQL Server Browser サービスが無効になっている UCP に接続する、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスごとに、この手順を繰り返します。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスがネットワークに接続されていることを確認します。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のマネージド インスタンス上に、名前が同じでも大文字と小文字の区別に関する設定が異なるデータベースがある場合は、データベースとそのビューポイントが正しく識別されず、データ収集に失敗することがあります。 たとえば、"MYDATABASE" という名前のデータベースで、実際には "MyDatabase" という名前のデータベースの正常性状態が示される場合があります。 この場合、エラーにはなりません。 データ収集の失敗は、データベース ファイルやファイル グループの名前など、UCP に表示される他のオブジェクトの大文字と小文字の不一致から発生することもあります。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスが Windows Server 2003 コンピューター上でホストされている場合、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント サービス アカウントは、Performance Monitor Users セキュリティ グループまたはローカルの Administrators グループに属している必要があります。 属していない場合は、アクセス拒否エラーが発生してデータ収集が失敗します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント サービス アカウントを Performance Monitor Users セキュリティ グループに追加するには、次の手順を実行します。  
  
    1.  **[コンピューターの管理]** を開き、 **[ローカル ユーザーとグループ]** 、 **[グループ]** の順に展開します。  
  
    2.  **[Performance Monitor Users]** を右クリックし、 **[グループに追加]** をクリックします。  
  
    3.  **[追加]** をクリックします。  
  
    4.  SQL Server エージェント サービスを実行しているアカウントを入力し、 **[OK]** をクリックします。  
  
    5.  ユーザーをこのグループに追加する前に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスが既に UCP に登録されている場合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント サービスを再起動します。  
  
## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server のリソース正常性のトラブルシューティング &#40;SQL Server ユーティリティ&#41;](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)
