---
title: Kerberos の制約付き委任用に Analysis Services の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6d751477-6bf1-48b4-8833-5a631bbe7650
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cfceb6b2314f9e57d6d383312d9f9373f7df1621
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67832921"
---
# <a name="configure-analysis-services-for-kerberos-constrained-delegation"></a>Kerberos の制約付き委任のための Analysis Services の構成
  Kerberos 認証用に Analysis Services を構成する際は、通常、データを照会するときに Analysis Services でユーザー ID の権限を借用すること、Analysis Services でユーザー ID を下位レベル サービスに委任すること、またはその両方を実現することが重要になります。 これらのシナリオで求められる構成要件はそれぞれ異なります。 どちらのシナリオでも、構成が正しく行われたことを確認するための検証が必要になります。  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と Kerberos に関する接続性の問題のトラブルシューティングに役立つ診断ツールです。 Kerberos 認証の詳細については、「 [Microsoft® Kerberos Configuration Manager for SQL Server®](https://www.microsoft.com/download/details.aspx?id=39046)」をご覧ください。  
  
 このトピックには、次のセクションが含まれます。  
  
-   [Analysis Services によるユーザー ID の権限の借用](#bkmk_impersonate)  
  
-   [信頼された委任のための Analysis Services の構成](#bkmk_delegate)  
  
-   [権限が借用された ID または委任された ID のテスト](#bkmk_test)  
  
> [!NOTE]  
>  Analysis Services への接続がシングル ホップである場合や、SharePoint Secure Store Service または Reporting Services によって提供された保存された資格情報をソリューションで使用する場合、委任は必要ありません。 すべての接続が Excel から Analysis Services データベースに対する直接接続である場合、または保存された資格情報に基づいている場合、Kerberos (または NTLM) を使用するのに制約付き委任を構成する必要はありません。  
>   
>  ユーザー id を複数のコンピューター接続 (「ダブルホップ」と呼ばれます) に渡す場合、Kerberos の制約付き委任が必要です。 Analysis Services データ アクセスがユーザー ID に基づき、接続要求が委任サービスから発信される場合は、次のセクションのチェック リストを使用して、Analysis Services が元の呼び出し元の権限を借用できることを確認します。 Analysis Services の認証フローの詳細については、「 [Microsoft BI 認証と ID 委任](https://go.microsoft.com/fwlink/?LinkID=286576)」をご覧ください。  
>   
>  セキュリティ上、Microsoft は常に制約なし委任よりも制約付き委任をお勧めします。 制約なし委任では、サービス ID が *あらゆる* ダウンストリーム コンピューター、サービスまたはアプリケーションで別のユーザーを偽装できるようになるため、大きなセキュリティ リスクとなります (一方、制約付き委任ではこれらのサービスが明示的に定義されます)。  
  
##  <a name="bkmk_impersonate"></a> Analysis Services によるユーザー ID の権限の借用  
 Reporting Services、IIS、SharePoint などの上位レベル サービスに Analysis Services 上のユーザー ID の権限を借用することを許可するには、これらのサービスに対して Kerberos の制約付き委任を構成する必要があります。 このシナリオでは、Analysis Services は、委任サービスで提供された ID を使用して現在のユーザーの権限を借用し、そのユーザー ID のロールのメンバーシップに基づく結果を返します。  
  
|タスク|説明|  
|----------|-----------------|  
|手順 1:アカウントが委任に適していることを確認する|サービスの実行に使用されるアカウントの適切なプロパティが Active Directory にあることを確認します。 Active Directory のサービス アカウントは、機微なアカウントとしてマークされていてはならず、委任シナリオから明確に除外されている必要があります。 詳細については、「 [ユーザー アカウントとは](https://go.microsoft.com/fwlink/?LinkId=235818)」をご覧ください。<br /><br /> **\*\* 重要な\* \*** 一般に、すべてのアカウントおよびサーバーする必要がありますかに属している同じ Active Directory ドメインと同じフォレストの信頼されるドメイン。 ただし、Windows Server 2012 はドメインの境界を越えた委任をサポートしているので、ドメインの機能レベルが Windows Server 2012 である場合、ドメインの境界を越えた Kerberos の制約付き委任を構成できます。 また、Analysis Services を HTTP アクセス用に構成し、クライアント接続で IIS の認証方法を使用することもできます。 詳細については、「 [インターネット インフォメーション サービス &#40;IIS&#41; 8.0 上の Analysis Services への HTTP アクセスの構成](configure-http-access-to-analysis-services-on-iis-8-0.md)」をご覧ください。|  
|手順 2:SPN を登録する|制約付き委任をセットアップする前に、Analysis Services インスタンス用に SPN (Service Principle Name) を登録する必要があります。 中間層サービスの Kerberos の制約付き委任を構成するときに Analysis Services SPN が必要となります。 手順については、「 [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md) 」をご覧ください。<br /><br /> SPN (Service Principle Name) は、Kerberos 認証用に構成されたドメイン内のサービスの一意の ID を指定します。 通常、統合セキュリティを使用するクライアント接続は、SSPI 認証の一部として SPN を要求します。 この要求は、Active Directory ドメイン コントローラー (DC) に転送されます。その際、クライアントによって示された SPN に対応する SPN が Active Directory 内に登録されている場合は、KDC によりチケットが提供されます。|  
|手順 3:制約付き委任を構成する|まず、使用するアカウントを検証し、そのアカウントの SPN を登録します。次に、上位レベル サービス (IIS、Reporting Services、SharePoint Web サービスなど) を制約付き委任用に構成し、委任が許可される特定のサービスとして Analysis Services SPN を指定します。<br /><br /> SharePoint で実行されるサービス (たとえば、Excel Services、SharePoint モードの Reporting Services) は、通常、Analysis Services の多次元データまたはテーブル データを使用するブックやレポートをホストします。 これらのサービスに対して制約付き委任を構成することは一般的な構成タスクであり、Excel Services からのデータの更新をサポートするために必要です。 SharePoint サービスに加え、Analysis Services データに対するダウンストリーム データ接続要求を表す可能性のあるその他のサービスの手順については、次のリンクをご覧ください。<br /><br /> 「[Excel Services の ID 委任 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299826) 」または「 [How to configure Excel Services in SharePoint Server 2010 f」または「 Kerberos authentication](https://support.microsoft.com/kb/2466519)」<br /><br /> [PerformancePoint Services の ID 委任 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299827)<br /><br /> [SQL Server Reporting Services の場合の ID 委任 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299828)<br /><br /> IIS 7.0 の詳細については、「 [Windows 認証を設定する (IIS 7.0)](https://technet.microsoft.com/library/cc754628\(v=ws.10\).aspx) 」または「 [Kerberos 認証を使用するように SQL Server 2008 Analysis Services および SQL Server 2005 Analysis Services を構成する方法](https://support.microsoft.com/kb/917409)」を参照してください。|  
|手順 4:接続のテスト|テスト中、異なる ID でリモート コンピューターから接続し、ビジネス ユーザーと同じアプリケーションを使用して Analysis Services をクエリします。 SQL Server Profiler を使用すると接続を監視できます。 要求にあるユーザー ID を確認する必要があります。 詳細については、このセクションの「 [権限が借用された ID または委任された ID のテスト](#bkmk_test) 」をご覧ください。|  
  
##  <a name="bkmk_delegate"></a> 信頼された委任のための Analysis Services の構成  
 Kerberos の制約付き委任用に Analysis Services を構成すると、サービスは、下位レベル サービス (リレーショナル データベース エンジンなど) のクライアント ID の権限を借用して、クライアントが直接接続されているかのようにデータを照会できます。  
  
 Analysis Services の委任シナリオは、`DirectQuery` 用に構成されたテーブル モデルに限られます。 これは、委任された資格情報を Analysis Services が別のサービスに渡すことができる唯一のシナリオです。 前のセクションで説明された SharePoint のシナリオなど、他のすべてのシナリオでは、Analysis Services は委任チェーンの受信側です。 DirectQuery の詳細については、「[DirectQuery モード (SSAS テーブル)](../tabular-models/directquery-mode-ssas-tabular.md)」を参照してください。  
  
> [!NOTE]  
>  共通する誤りは、ROLAP ストレージ、処理操作、またはリモート パーティションへのアクセスによって制約付き委任が要求されてしまうことです。 この場合は当てはまりません。 これらすべての操作は、代わりにサービス アカウント (処理アカウントとも呼ばれます) によって直接実行されます。 このような操作の権限が直接サービス アカウントに付与されているため (例えば、リレーショナル データベースに db_datareader 権限を付与することにより、サービスがデータを処理できるようにします)、Analysis Services におけるこれらの操作に委任は必要ありません。 サーバー操作と権限の詳細については、「[サービス アカウントの構成 (Analysis Services)](configure-service-accounts-analysis-services.md)」を参照してください。  
  
 このセクションでは、信頼された委任用に Analysis Services を設定する方法について説明します。 このタスクを完了すると、Analysis Services で委任された資格情報を SQL Server に渡すことができます。これは、テーブル ソリューションで使用される DirectQuery モードをサポートします。  
  
 開始前の準備:  
  
-   Analysis Services が開始されていることを確認します。  
  
-   Analysis Services に対して登録されている SPN が有効であることを確認します。 手順については、「 [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md)」をご覧ください。  
  
 両方の前提条件が満たされたら、次の手順を実行します。 制約付き委任を設定するには、ドメイン管理者である必要があります。  
  
1.  [Active Directory ユーザーとコンピューター] で、Analysis Services サービスが実行されているサービス アカウントを見つけます。 サービス アカウントを右クリックし、 **[プロパティ]** を選択します。  
  
     わかりやすくするために、以降のスクリーン ショットでは、OlapSvc と SQLSvc を使用して Analysis Services と SQL Server をそれぞれ表しています。  
  
     OlapSvc は、SQLSvc への制約付き委任用に構成されるアカウントです。 このタスクを完了すると、データを要求するときに元の呼び出し元の権限を借用して、サービス チケットの委任された資格情報を SQLSvc に渡す権限が OlapSvc に与えられます。  
  
2.  [委任] タブで、 **[指定されたサービスへの委任でのみこのユーザーを信頼する]** を選択し、 **[Kerberos のみを使う]** を選択します。 Analysis Services による資格情報の委任を許可するサービスを指定するために、 **[追加]** をクリックします。  
  
     [委任] タブは、ユーザー アカウント (OlapSvc) がサービス (Analysis Services) に割り当てられ、このサービスの SPN が登録されている場合にのみ表示されます。 SPN を登録するには、このサービスが実行されている必要があります。  
  
     ![SSAS_Kerberos_1_AccountProperties](../media/ssas-kerberos-1-accountproperties.gif "SSAS_Kerberos_1_AccountProperties")  
  
3.  [サービスの追加] ページで、 **[ユーザーまたはコンピューター]** をクリックします。  
  
     ![SSAS_Kerberos_2_](../media/ssas-kerberos-2.gif "SSAS_Kerberos_2_")  
  
4.  [ユーザーまたはコンピューターの選択] ページで、Analysis Services のテーブル モデル データベースにデータを提供する SQL Server インスタンスを実行するために使用するアカウントを入力します。 **[OK]** をクリックして、サービス アカウントを受け入れます。  
  
     目的のアカウントを選択できない場合は、SQL Server が実行されていて、そのアカウント用に SPN が登録されていることを確認します。 データベース エンジンの SPN の詳細については、「 [Kerberos 接続用のサービス プリンシパル名の登録](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)」をご覧ください。  
  
     ![SSAS_Kerberos_3_SelectUsers](../media/ssas-kerberos-3-selectusers.gif "SSAS_Kerberos_3_SelectUsers")  
  
5.  SQL Server インスタンスが [サービスの追加] に表示されます。 このアカウントを使用している他のサービスも一覧に表示されます。 使用する SQL Server インスタンスを選択します。 **[OK]** をクリックして、インスタンスを受け入れます。  
  
     ![SSAS_Kerberos_4_](../media/ssas-kerberos-4.gif "SSAS_Kerberos_4_")  
  
6.  次のスクリーン ショットに示すような Analysis Services サービス アカウントのプロパティ ページが表示されます。 **[OK]** をクリックして変更を保存します。  
  
     ![SSAS_Kerberos_5_Finished](../media/ssas-kerberos-5-finished.gif "SSAS_Kerberos_5_Finished")  
  
7.  異なる ID を使用してリモート クライアント コンピューターから接続して委任が成功するかどうかをテストし、テーブル モデルに対してクエリを実行します。 要求のユーザー ID は、SQL Server Profiler で確認できます。  
  
##  <a name="bkmk_test"></a> 権限が借用された ID または委任された ID のテスト  
 データを照会しているユーザーの ID を監視するには、SQL Server Profiler を使用します。  
  
1.  Analysis Services インスタンスで **SQL Server Profiler** を開始し、新しいトレースを開始します。  
  
2.  [イベントの選択] で、[Security Audit] セクションの [`Audit Login`] および [`Audit Logout`] のチェック ボックスがオンになっていることを確認します。  
  
3.  リモート クライアント コンピューターから、アプリケーション サービス (SharePoint、Reporting Services など) を介して Analysis Services に接続します。 Audit Login イベントに、Analysis Services に接続しているユーザーの ID が表示されます。  
  
 徹底的なテストを行うには、ネットワーク上の Kerberos 要求と応答を取得できるネットワーク監視ツールを使用する必要があります。 このタスクには、Kerberos 用にフィルター処理されたネットワーク モニター ユーティリティ (netmon.exe) を使用できます。 Netmon 3.4 などのツールを使用して、Kerberos 認証をテストの詳細については、次を参照してください。 [Kerberos 認証を構成します。コア構成 (SharePoint Server 2010)](https://technet.microsoft.com/library/gg502602\(v=office.14\).aspx)します。  
  
 また、Active Directory オブジェクトの [プロパティ] ダイアログ ボックスにある [委任] タブの各オプションの詳細な説明については、「 [Active Directory 内で最も紛らわしいダイアログ ボックス](https://www.itprotoday.com/active-directory/most-confusing-dialog-box-active-directory) 」をご覧ください。 この記事ではまた、LDP を使ってテストし、テスト結果を解釈する方法を説明します。  
  
## <a name="see-also"></a>参照  
 [Microsoft BI 認証と ID 委任](https://go.microsoft.com/fwlink/?LinkID=286576)   
 [Kerberos を使用した相互認証](https://go.microsoft.com/fwlink/?LinkId=299283)   
 [Analysis Services への接続](connect-to-analysis-services.md)   
 [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md)   
 [接続文字列プロパティ (Analysis Services)](connection-string-properties-analysis-services.md)  
  
  
