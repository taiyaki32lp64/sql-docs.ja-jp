---
title: レプリケーション管理オブジェクトの概念 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- replication [SQL Server], RMO
- programming interfaces [SQL Server replication]
- replication [SQL Server], how-to topics
- RMO [SQL Server]
- Replication Management Objects
- programming [SQL Server replication], RMO
ms.assetid: 37476d50-fb47-49e3-9504-3b163ac381d8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2cbc3571aa26728fa94957bb0c2f207ff769f4c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721794"
---
# <a name="replication-management-objects-concepts"></a>Replication Management Objects Concepts
  レプリケーション管理オブジェクト (RMO) は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のレプリケーション機能をカプセル化するマネージド コード アセンブリです。 RMO は <xref:Microsoft.SqlServer.Replication> 名前空間により実装されます。  
  
 以下のセクションのトピックでは、レプリケーション タスクをプログラムから制御する場合の RMO の使用方法について説明します。  
  
 [[ディストリビューションの構成]](../configure-distribution.md)  
 このセクションのトピックでは、RMO を使用してパブリッシングおよびディストリビューションを構成する方法について説明します。  
  
 [パブリケーションの作成](../publish/create-a-publication.md)  
 このセクションのトピックでは、RMO を使用してパブリケーションおよびアーティクルを作成、削除、および変更する方法について説明します。  
  
 [パブリケーションのサブスクライブ](../subscribe-to-publications.md)  
 このセクションのトピックでは、RMO を使用してサブスクリプションを作成、削除、および変更する方法について説明します。  
  
 [レプリケーション トポロジのセキュリティ保護](../security/view-and-modify-replication-security-settings.md)  
 このセクションのトピックでは、RMO を使用してセキュリティ設定を表示および変更する方法について説明します。  
  
 [サブスクリプションの同期 &#40;レプリケーション&#41;](../synchronize-data.md)  
 ここでは、サブスクリプションを同期する方法を説明します。  
  
 [レプリケーションの監視](../monitoring-replication.md)  
 ここでは、プログラムからレプリケーション トポロジを監視する方法を説明します。  
  
## <a name="introduction-to-rmo-programming"></a>RMO プログラミングの概要  
 RMO は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーションのすべての機能をプログラミングできるように設計されています。 RMO の名前空間は <xref:Microsoft.SqlServer.Replication> です。これは [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework アセンブリである Microsoft.SqlServer.Rmo.dll により実装されます。 同様に <xref:Microsoft.SqlServer.Replication> 名前空間に属している Microsoft.SqlServer.Replication.dll アセンブリにより、さまざまなレプリケーション エージェント (スナップショット エージェント、ディストリビューション エージェント、マージ エージェント) のプログラミングのためのマネージド コード インターフェイスが実装されます。 そのクラスには RMO からアクセスしてサブスクリプションを同期できます。 Microsoft.SqlServer.Replication.BusinessLogicSupport.dll アセンブリにより実装される、<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 名前空間のクラスを使用して、マージ レプリケーション用のカスタム ビジネス ロジックを作成できます。 このアセンブリは RMO から独立しています。  
  
## <a name="deploying-applications-based-on-rmo"></a>RMO に基づくアプリケーションの配置  
 RMO は、SQL Server Compact を除く [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のすべてのバージョンに含まれるレプリケーション コンポーネントとクライアント接続コンポーネントに依存しています。 RMO に基づいてアプリケーションを配置するには、アプリケーションを実行するコンピューターに、レプリケーション コンポーネントとクライアント接続コンポーネントを含むバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールする必要があります。  
  
## <a name="getting-started-with-rmo"></a>RMO の概要  
 ここでは、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio を使用して単純な RMO プロジェクトを開始する方法を説明します。  
  
#### <a name="to-create-a-new-microsoft-visual-c-project"></a>新しい Microsoft Visual C# プロジェクトを作成するには  
  
1.  Visual Studio を起動します。  
  
2.  **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3.  **[プロジェクトの種類]** ダイアログ ボックスで **[Visual C# プロジェクト]** を選択します。 **[テンプレート]** ウィンドウで **[Windows アプリケーション]** を選択します。  
  
4.  (省略可) **[名前]** に、新しいアプリケーションの名前を入力します。  
  
5.  **[OK]** をクリックして、Visual C# Windows テンプレートを読み込みます。  
  
6.  **[プロジェクト]** メニューの **[参照の追加]** 項目を選択します。 **[参照の追加]** ダイアログ ボックスが表示されます。  
  
7.  **[.NET]** タブの一覧から、次のアセンブリを選択して **[OK]** をクリックします。  
  
    -   Microsoft.SqlServer.Replication .NET プログラミング インターフェイス  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   レプリケーション エージェント ライブラリ  
  
    > [!NOTE]  
    >  複数のファイルを選択するには、&lt;localizedText&gt;Ctrl&lt;/localizedText&gt; キーを押しながら各ファイルをクリックします。  
  
8.  (省略可) 手順 6. を繰り返します。 **[参照]** タブをクリックして [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM に移動し、Microsoft.SqlServer.Replication.BusinessLogicSupport.dll を選択した後、 **[OK]** をクリックします。  
  
9. **[表示]** メニューの **[コード]** をクリックします。  
  
10. コード内で、名前空間のステートメントの前に次の `using` ステートメントを入力し、RMO 名前空間内の型を修飾します。  
  
    ```  
    // These namespaces are required.  
    using Microsoft.SqlServer.Replication;  
    using Microsoft.SqlServer.Management.Common;  
    // This namespace is only used when creating custom business  
    // logic for merge replication.  
    using Microsoft.SqlServer.Replication.BusinessLogicSupport;   
    ```  
  
#### <a name="to-create-a-new-microsoft-visual-basic-net-project"></a>新しい Microsoft Visual Basic .NET プロジェクトを作成するには  
  
1.  Visual Studio を起動します。  
  
2.  **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3.  [プロジェクトの種類] ウィンドウで **[Visual Basic]** を選択します。 [テンプレート] ウィンドウで **[Windows アプリケーション]** を選択します。  
  
4.  (省略可) **[名前]** ボックスに、新しいアプリケーションの名前を入力します。  
  
5.  **[OK]** をクリックして、Visual Basic Windows テンプレートを読み込みます。  
  
6.  **[プロジェクト]** メニューの **[参照の追加]** を選択します。 **[参照の追加]** ダイアログ ボックスが表示されます。  
  
7.  **[.NET]** タブの一覧から、次のアセンブリを選択して **[OK]** をクリックします。  
  
    -   Microsoft.SqlServer.Replication .NET プログラミング インターフェイス  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   レプリケーション エージェント ライブラリ  
  
    > [!NOTE]  
    >  複数のファイルを選択するには、&lt;localizedText&gt;Ctrl&lt;/localizedText&gt; キーを押しながら各ファイルをクリックします。  
  
8.  (省略可) 手順 6. を繰り返します。 **[参照]** タブをクリックして [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM に移動し、Microsoft.SqlServer.Replication.BusinessLogicSupport.dll を選択した後、 **[OK]** をクリックします。  
  
9. **[表示]** メニューの **[コード]** をクリックします。  
  
10. コード内で、すべての宣言の前に次の `Imports` ステートメントを入力し、RMO 名前空間内の型を修飾します。  
  
    ```  
    ' These namespaces are required.  
    Imports Microsoft.SqlServer.Replication  
    Imports Microsoft.SqlServer.Management.Common  
    ' This namespace is only used when creating custom business  
    ' logic for merge replication.  
    Imports Microsoft.SqlServer.Replication.BusinessLogicSupport   
    ```  
  
## <a name="connecting-to-a-replication-server"></a>レプリケーション サーバーへの接続  
 RMO プログラミング オブジェクトでは、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスのインスタンスを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの接続を作成する必要があります。 サーバーへの接続は、RMO プログラミング オブジェクトとは別に作成されます。 接続はインスタンスの作成中に RMO オブジェクトに渡されるか、オブジェクトの <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに割り当てることで渡されます。 この方法では、RMO プログラミング オブジェクトおよび接続オブジェクト インスタンスを別々に作成および管理することが可能となり、単一の接続オブジェクトを複数の RMO プログラミング オブジェクトと共に再利用することができます。 レプリケーション サーバーへの接続には、次の規則が適用されます。  
  
-   指定された <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトに、すべての接続プロパティを定義します。  
  
-   各 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに対する接続に、それぞれ独自の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトが含まれている必要があります。  
  
-   <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトが、サーバー上で作成またはアクセスされる RMO プログラミング オブジェクトの <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに割り当てられます。  
  
-   <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> メソッドにより、サーバーへの接続が開かれます。 接続を使用してサーバー上の RMO プログラミング オブジェクトにアクセスするメソッドを呼び出す前に、このメソッドを呼び出しておく必要があります。  
  
-   RMO でも SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト) でも、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] への接続には <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用するため、RMO オブジェクトと SMO オブジェクトの両方で同じ接続を使用できます。 詳細については、「[SQL Server のインスタンスへの接続](../../server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)」を参照してください。  
  
-   接続を作成し、サーバーに正常にログオンするための認証情報はすべて <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトで指定されます。  
  
-   既定は Windows 認証です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用するには、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> を `false` に設定し、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> および <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> に有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインおよびパスワードを設定する必要があります。 セキュリティ資格情報は常にセキュリティ保護された状態で保存し、処理する必要があります。可能な限り、実行時に入力するようにします。  
  
-   マルチスレッド化されたアプリケーションの場合、各スレッドで別々の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを使用します。  
  
 RMO オブジェクトで使用された、アクティブなサーバー接続を閉じるには、<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> オブジェクトに対して <xref:Microsoft.SqlServer.Management.Common.ServerConnection> メソッドを呼び出します。  
  
## <a name="setting-rmo-properties"></a>RMO プロパティの設定  
 RMO プログラミング オブジェクトのプロパティは、サーバー上のこれらのレプリケーション オブジェクトのプロパティを表します。 サーバー上に新しいレプリケーション オブジェクトを作成するとき、RMO プロパティを使用してこれらのオブジェクトを定義します。 既存のオブジェクトの場合、RMO プロパティは既存のオブジェクトのプロパティを表しますが、変更できるのは書き込み可能または設定可能なプロパティのみです。 プロパティは、新しいオブジェクトまたは既存のオブジェクトに設定できます。  
  
### <a name="setting-properties-for-new-replication-objects"></a>新しいレプリケーション オブジェクトのプロパティの設定  
 サーバーに新しいレプリケーション オブジェクトを作成する際、必要なプロパティをすべて指定した後で、オブジェクトの `Create` メソッドを呼び出す必要があります。 新しいレプリケーション オブジェクトのプロパティの設定の詳細については、「[Configure Publishing and Distribution](../configure-publishing-and-distribution.md)」 (パブリッシングとディストリビューションの構成) を参照してください。  
  
### <a name="setting-properties-for-existing-replication-objects"></a>既存のレプリケーション オブジェクトのプロパティの設定  
 サーバー上に存在するレプリケーション オブジェクトの場合、RMO ではオブジェクトの種類に応じて、プロパティの一部またはすべてを変更することがサポートされます。 書き込み可能または設定可能なプロパティのみを変更できます。 プロパティを変更するには、`Load` または <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、サーバーから現在のプロパティを取得しておく必要があります。 これらのメソッドを呼び出すことは、既存のオブジェクトが変更されることを表します。  
  
 既定では、オブジェクトのプロパティを変更するときに、使用される <xref:Microsoft.SqlServer.Management.Common.ServerConnection> の実行モードに基づいてこれらの変更がサーバーにコミットされます。 オブジェクトのプロパティを取得または変更する前に、<xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> メソッドを使用して、そのオブジェクトがサーバー上に存在するかどうかを確認できます。 レプリケーション オブジェクトのプロパティの変更方法の詳細については、「[ディストリビューターとパブリッシャーのプロパティの表示および変更](../view-and-modify-distributor-and-publisher-properties.md)」を参照してください。  
  
> [!NOTE]  
>  複数の RMO クライアントまたは複数の RMO プログラミング オブジェクト インスタンスが、サーバー上の同じレプリケーション オブジェクトにアクセスする場合、RMO オブジェクトの `Refresh` メソッドを呼び出して、サーバー上のオブジェクトの現在の状態に基づいてプロパティを更新できます。  
  
### <a name="caching-property-changes"></a>プロパティの変更のキャッシュ  
 <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> プロパティが <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes.CaptureSql> に設定されている場合、RMO により生成されるすべての [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントがキャプチャされ、いずれかの実行メソッドを使用して 1 つのバッチで手動で実行できます。 RMO を使用するとプロパティの変更をキャッシュでき、オブジェクトの <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを使用して 1 つのバッチでまとめてコミットできます。 プロパティの変更をキャッシュするには、オブジェクトの <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> プロパティを `true` に設定する必要があります。 RMO におけるプロパティの変更がキャッシュされる場合でも、変更がいつサーバーに送られるのかは <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトによって制御されます。 レプリケーション オブジェクトのプロパティのキャッシュの詳細については、「[ディストリビューターとパブリッシャーのプロパティの表示および変更](../view-and-modify-distributor-and-publisher-properties.md)」を参照してください。  
  
> [!IMPORTANT]  
>  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスでは、プロパティを設定するときに明示的なトランザクションの宣言がサポートされますが、そのようなトランザクションでは内部的なレプリケーション トランザクションに干渉する場合があるため、予期しない結果が生じる可能性があります。RMO では使用しないでください。  
  
## <a name="example"></a>例  
 この例では、プロパティ変更のキャッシュを示します。 トランザクション パブリケーションの属性に加えられた変更は、明示的にサーバーに送られるまでキャッシュされます。  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_ChangeTranPub_cached)]  
  
## <a name="see-also"></a>参照  
 [Replication System Stored Procedures Concepts](replication-system-stored-procedures-concepts.md)   
 [レプリケーションのプログラミング概念](replication-programming-concepts.md)  
  
  
