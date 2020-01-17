---
title: テーブル モデル データベースへの BI セマンティック モデル接続の作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 69b306f6-ee8a-44d2-8f51-0cad2c0bc135
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f058516059c0cadf92b9d558a47990af0a54725f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071659"
---
# <a name="create-a-bi-semantic-model-connection-to-a-tabular-model-database"></a>テーブル モデル データベースへの BI セマンティック モデル接続の作成
  このトピックでは、SharePoint ファーム外の Analysis Services インスタンスで実行しているテーブル モデル データベースにリダイレクトする BI セマンティック モデル接続を設定する方法について説明します。  
  
 BI セマンティック モデル接続を作成して SharePoint 権限および Analysis Services 権限を構成したら、その接続を Excel または [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] レポートのデータ ソースとして使用できます。  
  
 このトピックのセクションは次のとおりです。 各タスクは、所定の順序で実行してください。  
  
 [前提条件の確認](#bkmk_prereq)  
  
 [共有サービス アプリケーションへの Analysis Services 管理権限の付与](#bkmk_ssas)  
  
 [テーブル モデル データベースの読み取り権限の付与](#bkmk_BISM)  
  
 [テーブル モデル データベースへの BI セマンティック モデル接続の作成](#bkmk_connect)  
  
 [BI セマンティック モデル接続への SharePoint 権限の構成](#bkmk_permissions)  
  
 [次の手順](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> 前提条件の確認  
 BI セマンティック モデル接続ファイルを作成するには、投稿権限以上の権限が必要です。  
  
 BI セマンティック モデル接続のコンテンツ タイプをサポートしているライブラリが必要です。 詳細については、次を参照してください。 [BI セマンティック モデル接続のコンテンツ タイプをライブラリに追加&#40;PowerPivot for SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)します。  
  
 BI セマンティック モデル接続を設定するサーバーおよびデータベース名を確認しておく必要があります。 Analysis Services は、テーブル モード用に構成する必要があります。 サーバーで実行しているデータベースは、テーブル モデル データベースである必要があります。 サーバー モードを確認する方法については、「 [Analysis Services インスタンスのサーバー モードの決定](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)」を参照してください。  
  
 特定のシナリオでは、SharePoint 環境の共有サービスが、Analysis Services インスタンスに対する管理権限を持っている必要があります。 管理権限が必要なサービスは、PowerPivot サービス アプリケーション、Reporting Services サービス アプリケーション、PerformancePoint サービス アプリケーションなどです。 管理権限を付与する前に、これらのサービス アプリケーションの ID を知っておく必要があります。 ID を確認するには、サーバーの全体管理を使用できます。  
  
 サーバーの全体管理でセキュリティ情報を表示するには、SharePoint サービス管理者である必要があります。  
  
 Management Studio で管理者権限を付与するには、Analysis Services のシステム管理者である必要があります。  
  
 PowerPivot for SharePoint は、クラシック モード認証を使用する Web アプリケーションからアクセスする必要があります。 外部データ ソースへの BI セマンティック モデル接続は、クラシック モード サインインに依存します。 詳細については、次を参照してください。 [PowerPivot Authentication and Authorization](power-pivot-authentication-and-authorization.md)します。  
  
 接続シーケンスに参加しているすべてのコンピューターとユーザーは、同じドメインまたは信頼されたドメイン (双方向の信頼関係) に属している必要があります。  
  
##  <a name="bkmk_ssas"></a> 共有サービス アプリケーションへの Analysis Services 管理権限の付与  
 SharePoint から Analysis Services サーバー上のテーブル モデル データベースへの接続は、データを要求するユーザーに代わって、共有サービスによって行われることがあります。 要求を行うサービスは、通常、PowerPivot サービス アプリケーション、Reporting Services サービス アプリケーション、または PerformancePoint サービス アプリケーションです。 接続が成功するために、このサービスには Analysis Services サーバーに対する管理権限が必要です。 Analysis Services では、別のユーザーの権限を借用して接続できるのは管理者のみです。  
  
 次の条件の下で接続が使用される場合は、管理権限が必要です。  
  
-   BI セマンティック モデル接続ファイルの構成中に接続情報を確認するとき。  
  
-   BI セマンティック モデル接続を使用して、Power View レポートを開始するとき。  
  
-   BI セマンティック モデル接続を使用して、PerformancePoint Web パーツを設定するとき。  
  
 これらの動作が期待どおりに行われるようにするには、各サービス ID に Analysis Services インスタンスに対する管理権限を付与します。 次の手順に従って、必要な権限を付与します。  
  
 **サーバー管理者ロールへのサービス ID の追加**  
  
1.  SQL Server Management Studio で Analysis Services インスタンスに接続します。  
  
2.  サーバー名を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[セキュリティ]** をクリックして、 **[追加]** をクリックします。 サービス アプリケーションを実行する Windows ユーザー アカウントを入力します。  
  
     ID を確認するには、サーバーの全体管理を使用できます。 [セキュリティ] セクションの **[サービス アカウントの構成]** を開き、各アプリケーションで使用されるサービス アプリケーション プールにどの Windows アカウントが関連付けられているかどうかを確認します。次に、このトピックの手順に従って、アカウントに管理権限を付与します。  
  
##  <a name="bkmk_BISM"></a> テーブル モデル データベースの読み取り権限の付与  
 データベースがファームの外部にあるサーバーで実行しているため、接続の設定の一環として、バックエンドの Analysis Services サーバーに対するデータベース ユーザー権限を付与します。 Analysis Services はロールベースの権限モデルを使用します。 model データベースに接続するユーザーは、メンバーに読み取りアクセスを付与するロールを介して、読み取り権限以上の権限を使用して接続する必要があります。  
  
 ロール (および場合によってはロール メンバーシップ) が定義されるのは、モデルが [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で作成されるときです。 SQL Server Management Studio ではロールを作成することはできませんが、定義済みのロールにメンバーを追加することはできます。 ロールの作成の詳細については、「[ロールの作成および管理 (SSAS テーブル)](../tabular-models/roles-ssas-tabular.md)」を参照してください。  
  
#### <a name="assign-role-membership"></a>ロールのメンバーシップの割り当て  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続し、オブジェクト エクスプローラーでデータベースを展開し、さらに **[ロール]** を展開します。 既に定義されているロールが表示されます。 ロールが存在しない場合は、モデルの作成者に連絡してロールの追加を依頼します。 Management Studio でロールを表示するには、モデルを再配置する必要があります。  
  
2.  ロールを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  [メンバーシップ] ページで、アクセスする必要がある Windows グループ アカウントおよびユーザー アカウントを追加します。  
  
##  <a name="bkmk_connect"></a> テーブル モデル データベースへの BI セマンティック モデル接続の作成  
 Analysis Services で権限を設定した後で、SharePoint に戻り、BI セマンティック モデル接続を作成できます。  
  
1.  BI セマンティック モデル接続の格納先となるライブラリで、SharePoint リボンの **[ドキュメント]** をクリックします。  
  
2.  [新しいドキュメント] の下矢印をクリックし、 **[BI セマンティック モデル接続ファイル]** を選択して、[新しい BI セマンティック モデル接続] ページを開きます。  
  
3.  **[サーバー]** プロパティと **[データベース]** プロパティの両方を設定します。 データベース名がわからない場合は、SQL Server Management Studio を使用して、サーバーに配置されているデータベースの一覧を表示します。  
  
     **[サーバー名]** には、サーバーのネットワーク名、IP アドレス、または完全修飾ドメイン名 (myserver.mydomain.corp.adventure-works.com など) を指定します。 サーバーが名前付きインスタンスとしてインストールされている場合は、computername\instancename の形式でサーバー名を入力します。  
  
     **[データベース]** には、サーバーで現在使用可能なテーブル データベースを指定する必要があります。 他の BI セマンティック モデル接続ファイル、Office Data Connection (.odc) ファイル、Analysis Services OLAP データベース、または PowerPivot ブックを指定しないでください。 データベース名を取得するには、Management Studio を使用してサーバーに接続して、使用可能なデータベースの一覧を表示します。 データベースのプロパティ ページを使用して、名前が正しいことを確認します。  
  
4.  **[OK]** をクリックしてページを保存します。 この時点で、PowerPivot サービス アプリケーションが接続を検証します。  
  
     接続情報が正しく、PowerPivot サービス アプリケーションに管理権限が付与されていて、現在のユーザーとして Analysis Services に接続できるようになっていれば、検証は成功します。  
  
     接続情報が間違っているか、サービス アプリケーションに権限がない場合、検証は失敗します。 ファイルを保存するかどうかを確認するメッセージがページに表示されます。 接続が有効であることがわかっている場合、エラーの原因は無効な接続情報ではなく、権限がないことであるため、ファイルを保存します。  
  
     Excel または Power View でテーブル モデル データベースに接続してみることで、接続を検証できます。 データ ソース接続が成功した場合は、検証による警告が発生していても、接続は有効です。  
  
##  <a name="bkmk_permissions"></a> BI セマンティック モデル接続への SharePoint 権限の構成  
 BI セマンティック モデル接続を Excel ブックまたは Reporting Services レポートのデータ ソースとして使用するには、SharePoint ライブラリ内の BI セマンティック モデル接続アイテムに対する **読み取り** 権限が必要です。 読み取り権限レベルには、BI セマンティック モデル接続情報を Excel デスクトップ アプリケーションにダウンロードできるようにする **"アイテムを開く"** 権限が含まれます。  
  
 SharePoint で権限を付与するには、いくつかの方法があります。 次の手順では、 **読み取り** 権限レベルを持つ、 **BISM ユーザー** という名前の新しいグループを作成する方法について説明します。  
  
 権限を変更するには、サイト所有者である必要があります。  
  
1.  [サイトの操作] の **[サイトの権限]** をクリックします。  
  
2.  **[グループの作成]** をクリックして、新しいグループの名前を「 **BISM ユーザー**」と指定します。  
  
3.  **[読み取り]** 権限レベルを選択し、 **[作成]** をクリックします。  
  
4.  [ユーザーとグループ] の **[BISM ユーザー]** を選択します。  
  
5.  [新規作成] をポイントして **[ユーザーの追加]** をクリックし、ユーザー アカウントまたはグループ アカウントを追加します。  
  
     これで、追加したユーザーおよびグループに、サイト レベルから権限を継承するすべてのライブラリとリストを含むサイト全体の読み取り権限が付与されます。 この権限レベルでは高すぎる場合は、必要に応じて特定のライブラリ、リスト、またはアイテムからこのグループを削除できます。  
  
 アイテム レベルで権限を選択的に削除するには、次の操作を行います。  
  
1.  ライブラリで、ドキュメントを選択します。 右側の下矢印をクリックし、 **[権限の管理]** をクリックします。  
  
2.  既定では、アイテムは権限を継承します。 このライブラリ内の個々のドキュメントの権限を変更するには、 **[権限の継承を中止]** をクリックします。  
  
3.  **[BISM ユーザー]** の横にあるチェック ボックスをオンにします。  
  
4.  **[ユーザー権限の削除]** をクリックします。  
  
##  <a name="bkmk_next"></a> 次の手順  
 BI セマンティック モデル接続を作成し、セキュリティで保護したら、データ ソースとして指定できます。 詳細については、「 [Excel または Reporting Services での BI セマンティック モデル接続の使用](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [PowerPivot BI セマンティック モデル接続&#40;.bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [PowerPivot ブックへの BI セマンティック モデル接続の作成](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
  
