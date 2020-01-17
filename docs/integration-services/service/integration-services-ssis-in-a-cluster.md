---
title: クラスターにおける Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f9203423267f68137e11203be60ffa4d0e0c3e41
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296896"
---
# <a name="integration-services-ssis-in-a-cluster"></a>クラスターにおける Integration Services (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をクラスター化することはお勧めしません。[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、クラスター化されるサービスまたはクラスター対応サービスではなく、クラスター ノード間のフェールオーバーはサポートしません。 したがって、クラスター環境では、クラスターの各ノードで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールし、スタンドアロン サービスとして起動する必要があります。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスはクラスター化されるサービスではありませんが、クラスターの各ノードに個別に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールした後、クラスター リソースとして動作するように手動で構成することができます。  
  
 ただし、クラスター化されたハードウェア環境を構築する目的が高可用性を実現することにある場合は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成しなくても、この目的を達成できます。  クラスター内の他のノードからクラスター内の任意のノード上でパッケージを管理するには、クラスター内の各ノードで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルを変更します。 パッケージが格納されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の使用可能なすべてのインスタンスを指し示すように、それぞれの構成ファイルを変更します。 この方法を使用すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成したときに発生する可能性のある問題を回避できるうえ、ほとんどの顧客から求められる高可用性を実現できます。 構成ファイルの変更方法の詳細については、「[Integration Services サービス &#40;SSIS サービス&#41;](../../integration-services/service/integration-services-service-ssis-service.md)」を参照してください。  
  
 クラスター環境でサービスをどのように構成するかに関して詳しい情報に基づく決断を行うには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの役割を理解することがきわめて重要です。 詳細については、「[Integration Services サービス (SSIS サービス)](../../integration-services/service/integration-services-service-ssis-service.md)」を参照してください。  
  
## <a name="disadvantages"></a>欠点
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成する場合、次のような潜在的な欠点があります。  
  
-   **フェールオーバーが発生したときに、実行中のパッケージが再起動されません。**
    
    チェックポイントからパッケージを再開することで、パッケージのエラーから回復できます。 サービスをクラスター リソースとして構成しなくても、チェックポイントからパッケージを再開できます。 詳細については、「 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)」を参照してください。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] とは異なるリソース グループに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービスを構成した場合、クライアント コンピューターから [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して msdb データベースに格納されているパッケージを管理することはできません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、このダブルホップ シナリオで資格情報を委任することはできません。  
  
-   クラスター内に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを含む複数の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] リソース グループがある場合、フェールオーバーにより予期しない結果が生じる可能性があります。 次のシナリオについて考えてみます。 グループ 1 は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを含み、ノード A 上で実行されています。グループ 2 は、同様に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを含み、ノード B 上で実行されています。次に、グループ 2 からノード A へのフェールオーバーが発生します。ここで、ノード A 上で [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの別のインスタンスを起動しようとした場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは単一インスタンス サービスなので、その試みは失敗します。 ノード A へのフェールオーバーを試行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが同様に失敗するかどうかは、グループ 2 における [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成に依存します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスがリソース グループ内の他のサービスに影響を与えるように構成されている場合、フェールオーバーを試行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスは失敗します。なぜなら、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが失敗しているからです。 サービスがリソース グループ内の他のサービスに影響を与えないように構成されている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスはノード A にフェールオーバーできます。リソース グループ内の他のサービスに影響を与えないようにグループ 2 の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが構成されていない限り、フェールオーバーを試行している [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが失敗すると、フェールオーバーを試行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスも失敗する可能性があります。  

## <a name="configure-the-service-as-a-cluster-resource"></a>サービスをクラスター リソースとして構成する
このセクションでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成する利点が欠点を上回ると判断したユーザー向けに、必要な構成手順を説明します。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成することをお勧めしません。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成するには、次のタスクを完了する必要があります。  
  
-   クラスターに [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールします。  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をクラスターにインストールするには、クラスター内の各ノードに [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールする必要があります。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をクラスター リソースとして構成します。  
  
     Integration Services がクラスターの各ノードにインストールされている状態で、Integration Services をクラスター リソースとして構成する必要があります。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成する場合、サービスを [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]と同じリソース グループに追加することも、異なるグループに追加することもできます。 次の表に、リソース グループの選択に関連する利点と欠点を示します。  
  
    |Integration Services と SQL Server が同じリソース グループに属する場合|Integration Services と SQL Server が異なるリソース グループに属する場合|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] と [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サービスが同じ仮想サーバー上で実行されるので、クライアント コンピューターは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を使用して、msdb データベースに格納されているパッケージを管理できます。 この構成では、ダブルホップ シナリオの委任の問題を回避できます。|クライアント コンピューターは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、msdb データベースに格納されているパッケージを管理することができません。 クライアント コンピューターは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが実行されている仮想サーバーに接続できます。 ただし、当該コンピューターは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されている仮想サーバーにユーザーの資格情報を委任することはできません。 これは、ダブルホップ シナリオと呼ばれます。|  
    |[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、CPU およびその他のコンピューター リソースの利用に関して他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスと競合します。|異なるリソース グループは異なるノードに構成されているので、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、CPU およびその他のコンピューター リソースの利用に関して他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスと競合しません。|  
    |両方のサービスが同じコンピューター上で実行されているので、msdb データベースへのパッケージの読み込みと保存をより高速に行うことができ、生成されるネットワーク トラフィックも少なくて済みます。|msdb データベースへのパッケージの読み込みと保存に時間がかかる可能性があり、生成されるネットワーク トラフィックが多くなります。|  
    |両方のサービスは同時にオンラインまたはオフラインになります。|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスがオンラインのときに [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] がオフラインの場合があります。 その場合、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の msdb データベースに格納されているパッケージを利用できなくなります。|  
    |必要に応じて [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをすばやく別のノードに移動できません。|必要に応じて [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをすばやく別のノードに移動できます。|  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]をどちらのリソース グループに追加するかを決定した後、当該グループのクラスターとして [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を構成する必要があります。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスおよびパッケージ ストアを構成します。  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をクラスター リソースとして構成した後は、クラスター内の各ノード上で [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルの場所および内容を変更する必要があります。 これは、フェールオーバーが発生した場合にすべてのノードで構成ファイルとパッケージ ストアを使用可能にするための変更です。 構成ファイルの場所および内容を変更した後、サービスをオンラインにする必要があります。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとしてオンラインにします。  
  
 クラスターまたは任意のサーバー上で [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを構成した後は、クライアント コンピューターからサービスに接続できるように DCOM 権限を構成しなければならない場合があります。 詳細については、「[Integration Services サービス (SSIS サービス)](../../integration-services/service/integration-services-service-ssis-service.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、資格情報を委任できません。 したがって、次の条件に一致するときは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して msdb データベースに格納されているパッケージを管理することはできません。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が別個のサーバーまたは仮想サーバー上で実行されている。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を実行しているクライアントが 3 台目のコンピューターである。  
  
 クライアント コンピューターは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが実行されている仮想サーバーに接続できます。 ただし、当該コンピューターは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されている仮想サーバーにユーザーの資格情報を委任することはできません。 これは、ダブルホップ シナリオと呼ばれます。  
  
### <a name="to-install-integration-services-on-a-cluster"></a>クラスターに Integration Services をインストールするには  
  
1.  1 つ以上のノードのクラスターをインストールして構成します。  
  
2.  (省略可能) [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]などのクラスター化サービスをインストールします。  
  
3.  クラスターの各ノードに [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールします。  
  
### <a name="to-configure-integration-services-as-a-cluster-resource"></a>Integration Services をクラスター リソースとして構成するには  
  
1.  **クラスター アドミニストレーター**を開きます。  
  
2.  コンソール ツリーで、[グループ] フォルダーを選択します。  
  
3.  結果ペインで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を追加するグループを選択します。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と同じリソース グループに Integration Services をクラスター リソースとして追加するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が属しているグループを選択します。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]とは異なるグループに Integration Services をクラスター リソースとして追加するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が属している以外のグループを選択します。  
  
4.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[リソース]** をクリックします。  
  
5.  リソース ウィザードの **[新しいリソース]** ページで、名前を入力し、 **[サービスの種類]** として **[汎用サービス]** を選択します。 **[グループ]** の値は変更せずに、 **[次へ]** をクリックします。  
  
6.  **[実行可能な所有者]** ページで、リソースの実行可能な所有者として、クラスターのノードを追加または削除し、 **[次へ]** をクリックします。  
  
7.  依存関係を追加するには、 **[依存関係]** ページで **[利用できるリソース]** からリソースを選択し、 **[追加]** をクリックします。 フェールオーバーが発生した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がオンラインになる前に、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージが保存されている共有ディスクの両方がオンラインになる必要があります。 依存関係を選択したら、 **[次へ]** をクリックします。  
  
     詳細については、「 [Add Dependencies to a SQL Server Resource](../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md)」を参照してください。  
  
8.  **[汎用サービス パラメーター]** ページで、サービスの名前に「 **MsDtsServer** 」と入力し、 **[次へ]** をクリックします。  
  
9. **[レジストリ レプリケーション]** ページで、 **[追加]** をクリックし、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルの場所を示すレジストリ キーを追加します。 このファイルは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスと同じリソース グループに属している共有ディスクに配置されている必要があります。  
  
10. **[レジストリ キー]** ダイアログ ボックスで、「 **SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile**」と入力します。 **[OK]** をクリックし、 **[完了]** をクリックします。  
  
     これで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスがクラスター リソースとして追加されました。  
  
### <a name="to-configure-the-integration-services-service-and-package-store"></a>Integration Services サービスおよびパッケージ ストアを構成するには  
  
1.  構成ファイル %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml を探し、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを追加したグループの共有ディスクにコピーします。  
  
2.  共有ディスク上で、パッケージ ストアとして使用するために **Packages** という名前のフォルダーを新規作成します。 このフォルダーに対するフォルダー一覧表示権限と書き込み権限を、適切なユーザーおよびグループに許可します。  
  
3.  共有ディスク上で、テキスト エディターまたは XML エディターを使用して構成ファイルを開き、 **ServerName** 要素の値を、同じリソース グループ内の仮想 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前に変更します。  
  
4.  **StorePath** 要素の値を、共有ディスク上の、前の手順で作成した **Packages** フォルダーの完全修飾パスに変更します。  
  
5.  レジストリ内の **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** の値を共有ディスク上のサービス構成ファイルの完全修飾パスとファイル名に更新します。  
  
### <a name="to-bring-the-integration-services-service-online"></a>Integration Services サービスをオンラインにするには  
  
-   これには、 **クラスター アドミニストレーター**で、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを選択して右クリックし、ポップアップ メニューの **[オンラインにする]** をクリックします。 これで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスがクラスター リソースとしてオンラインになります。  
  
  
