---
title: マスター データ サービスのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: da78f21c6346281dc23332f40e8e6f46ff07aa06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774660"
---
# <a name="upgrade-master-data-services"></a>マスター データ サービスのアップグレード
  Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  CTP2 へのアップグレード シナリオは 4 つあります。 状況に適したシナリオを選択してください。  
  
-   [データベース エンジンのアップグレードを伴わないアップグレード](#noengine)  
  
-   [データベース エンジンのアップグレードを伴うアップグレード](#engine)  
  
-   [2 台のコンピューターのシナリオでのアップグレード](#twocomputer)  
  
-   [アップグレードおよびバックアップからのデータベースの復元](#restore)  
  
> [!IMPORTANT]
>  -   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1 リリースから CTP2 リリースへのアップグレードはサポートされていません。  
> -   アップグレードを実行する前にデータベースをバックアップしてください。  
> -   アップグレード プロセスでは、ストアド プロシージャを再作成し、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]で使用されるテーブルをアップグレードします。 これらのコンポーネントのいずれかに加えたカスタマイズは失われる場合があります。  
> -   モデル配置パッケージは作成されたエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のみで使用できます。 作成されたモデル配置パッケージを展開することはできません[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]に[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]します。  
> -   マスター データ サービスおよび Data Quality Services を [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] CTP2 にアップグレードした後も、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 バージョンの Excel 用マスター データ サービス アドインを使用し続けることができます。 ただし、SQL Server 2014 CTP2 にアップグレードした後、以前のバージョンの Excel 用マスター データ サービス アドインは機能しません。 ダウンロードすることができます、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 バージョンのマスター データ サービス アドインを使用して Excel の[ここ](https://go.microsoft.com/fwlink/?LinkId=328664)します。  
  
##  <a name="noengine"></a> データベース エンジンのアップグレードを伴わないアップグレード  
 このシナリオと見なす、サイド バイ サイドでインストールのため両方[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]と[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]同じコンピューターまたは別のコンピューターに同時にインストールされます。  
  
 このシナリオでは、引き続き [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] を使用して、MDS データベースをホストします。 ただし、MDS データベースのスキーマをアップグレードしてから、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを作成して MDS データベースにアクセスする必要があります。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Web アプリケーションからは、MDS データベースにアクセスできなくなります。  
  
 インストールを選択する場合[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]と SQL Server の以前のバージョン ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]/[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) と同じコンピューターでは、これを行う別の場所にファイルがインストールされているためです。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、既定で、ファイルが *drive*:\Program Files\Microsoft SQL Server\120\Master Data Services にインストールされます。  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]では、既定で、ファイルが *drive*:\Program Files\Microsoft SQL Server\110\Master Data Services にインストールされます。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]では、既定で、ファイルが *drive*:\Program Files\Microsoft SQL Server\Master Data Services にインストールされます。  
  
 この作業を実行するには、次の手順を実行します。  
  
1.  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] とその他の必要な機能をインストールします。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップ ウィザードを開きます。  
  
    2.  左ペインで、 **[インストール]** をクリックします。  
  
    3.  右ペインで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加]** をクリックします。  
  
    4.  **[機能の選択]** ページで、 **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** とその他にインストールする機能を選択します。  
  
    5.  ウィザードを完了します。  
  
2.  インストールが完了したら、MDS データベース スキーマをアップグレードします。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
        > [!IMPORTANT]  
        >  MDS データベース スキーマをアップグレードするには、MDS データベースの作成時に指定した管理者アカウントでログインする必要があります。 MDS データベースの mdm.tblUser で、このユーザーは **1** の **ID**値を持ちます。 このユーザーの変更方法の詳細については、次を参照してください。[システム管理者アカウントを変更&#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)します。  
  
    2.  左ペインで **[データベース構成]** をクリックします。  
  
    3.  右側のウィンドウで次のようにクリックします。**データベースの選択**の情報を指定し、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]または[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]データベース インスタンス。  
  
    4.  **[データベースのアップグレード]** をクリックして、 **データベースのアップグレード ウィザード**を起動します。 詳細については、「[データベースのアップグレード ウィザード  &#40;Master Data Services 構成マネージャー&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)」を参照してください。  
  
3.  アップグレードが完了したら、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを作成します。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
    2.  左ペインで **[Web の構成]** をクリックします。  
  
    3.  右ペインで、 **[Web サイト]** ボックスの一覧から次のいずれかのオプションを選択します。  
  
        -   **[既定の Web サイト]**。その後、 **[アプリケーションの作成]** をクリックします。  
  
        -   **[新しいサイトの作成]**。 Web サイトを作成すると、新しい Web アプリケーションが自動的に作成されます。  
  
        > [!IMPORTANT]  
        >  以前のバージョンの SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) から取得した既存の MDS Web アプリケーションを、Master Data Services 構成マネージャーの SQL Server 2014 バージョンで選択できます。 既存の Web アプリケーションを選択することはできません。代わりに MDS に対応する [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを作成する必要があります。 それ以外の場合は、アップグレード後の MDS データベースに Web アプリケーションを関連付けようとすると、ページに関連付けられた構成データが無効であるため、要求したページにアクセスできないことを示すエラーが返されます。  
        >   
        >  既存の ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) Web アプリケーションとして同じ名前を、MDS Web アプリケーションの名前 (別名) として使用する場合は、まず Web アプリケーションおよびそれに関連付けられているアプリケーション プールを IIS から削除し、次に Master Data Services 構成マネージャーの SQL Server 2014 バージョンを使用して同じ名前の Web アプリケーションを作成します。 Web アプリケーションとアプリケーション プールを IIS から削除する方法については、「 [Remove an Application (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=323537) 」 (アプリケーションを削除する (IIS 7))、および「 [Remove an Application Pool (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=323538)」(アプリケーション プールを削除する (IIS 7)) を参照してください。  
  
4.  アップグレードされた MDS データベースと新しい web アプリケーションを関連付けるようになりました。  
  
    1.  **[アプリケーションとデータベースの関連付け]** セクションで、 **[選択]** をクリックします。  
  
    2.  MDS データベースを選択します。  
  
    3.  **[適用]** をクリックします。  
  
##  <a name="engine"></a> データベース エンジンのアップグレードを伴うアップグレード  
 このシナリオでは、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] または SQL Server 2012 のデータベース エンジンと [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] アプリケーションの両方を [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードします。  
  
 この作業を実行するには、次の手順を実行します。  
  
1.  **[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] の場合のみ**:**[コントロール パネル]** > **[プログラムと機能]** の順に開き、Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]をアンインストールします。  
  
2.  データベース エンジンを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードします。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップ ウィザードを開きます。  
  
    2.  左ペインで、 **[インストール]** をクリックします。  
  
    3.  右側のウィンドウで次のようにクリックします。 **SQL Server 2005、SQL Server 2008、SQL Server 2008 R2 または SQL Server 2012 からアップグレード**します。  
  
    4.  ウィザードを完了します。  
  
3.  **[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] の場合のみ**:アップグレードが完了したら、追加、 ** [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] **機能します。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップ ウィザードを開きます。  
  
    2.  左ペインで、 **[インストール]** をクリックします。  
  
    3.  右ペインで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加]** をクリックします。  
  
    4.  **インストールの種類**、ウィザードのページ、**既存のインスタンスに機能を追加**オプション、および MDS データベースがインストールされているインスタンスを選択します。  
  
    5.  **機能の選択**] ページ [**共有機能**を選択します** [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** します。  
  
    6.  ウィザードを完了します。  
  
4.  MDS データベース スキーマをアップグレードします。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
        > [!IMPORTANT]  
        >  MDS データベース スキーマをアップグレードするには、MDS データベースの作成時に指定した管理者アカウントでログインする必要があります。 MDS データベースの mdm.tblUser で、このユーザーは **1** の **ID**値を持ちます。 このユーザーの変更方法の詳細については、次を参照してください。[システム管理者アカウントを変更&#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)します。  
  
    2.  左ペインで **[データベース構成]** をクリックします。  
  
    3.  右側のウィンドウで次のようにクリックします。**データベースの選択**し、データベース インスタンスの情報を指定します。  
  
    4.  **[データベースのアップグレード]** をクリックして、 **データベースのアップグレード ウィザード**を起動します。 詳細については、「[データベースのアップグレード ウィザード  &#40;Master Data Services 構成マネージャー&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)」を参照してください。  
  
    5.  **[適用]** をクリックします。  
  
5.  アップグレードが完了したら、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを作成します。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
    2.  左ペインで **[Web の構成]** をクリックします。  
  
    3.  右ペインで、 **[Web サイト]** ボックスの一覧から次のいずれかのオプションを選択します。  
  
        -   **[既定の Web サイト]**。その後、 **[アプリケーションの作成]** をクリックします。  
  
        -   **[新しいサイトの作成]**。 Web サイトを作成すると、新しい Web アプリケーションが自動的に作成されます。  
  
        > [!IMPORTANT]  
        >  以前のバージョンの SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) から取得した既存の MDS Web アプリケーションを、Master Data Services 構成マネージャーの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンで選択できます。 既存の Web アプリケーションを選択することはできません。代わりに MDS に対応する [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを作成する必要があります。 それ以外の場合は、アップグレード後の MDS データベースに Web アプリケーションを関連付けようとすると、ページに関連付けられた構成データが無効であるため、要求したページにアクセスできないことを示すエラーが返されます。  
        >   
        >  既存の ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) Web アプリケーションとして同じ名前を、MDS Web アプリケーションの名前 (別名) として使用する場合は、まず Web アプリケーションおよびそれに関連付けられているアプリケーション プールを IIS から削除し、次に Master Data Services 構成マネージャーの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンを使用して同じ名前の Web アプリケーションを作成します。 Web アプリケーションとアプリケーション プールを IIS から削除する方法については、「 [Remove an Application (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=323537) 」 (アプリケーションを削除する (IIS 7))、および「 [Remove an Application Pool (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=323538)」(アプリケーション プールを削除する (IIS 7)) を参照してください。  
  
6.  アップグレードされた MDS データベースと新しい web アプリケーションを関連付けるようになりました。  
  
    1.  **[アプリケーションとデータベースの関連付け]** セクションで、 **[選択]** をクリックします。  
  
    2.  MDS データベースを選択します。  
  
    3.  **[適用]** をクリックします。  
  
##  <a name="twocomputer"></a> 2 台のコンピューターのシナリオでのアップグレード  
 このシナリオでは、SQL Server が 2 台のコンピューターにインストールされているシステムをアップグレードします。1 台は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、もう 1 台は SQL Server 2008 R2 または SQL Server 2012 がインストールされています。  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] がインストールされている場合は、引き続き [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] を使用して、1 台のコンピューターで MDS データベースをホストします。 ただし、MDS データベースのスキーマをアップグレードしてから、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを使用して MDS データベースにアクセスする必要があります。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Web アプリケーションからは、MDS データベースにアクセスできなくなります。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、既定で、ファイルが *drive*:\Program Files\Microsoft SQL Server\120\Master Data Services にインストールされます。  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]では、既定で、ファイルが *drive*:\Program Files\Microsoft SQL Server\110\Master Data Services にインストールされます。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]では、既定で、ファイルが *drive*:\Program Files\Microsoft SQL Server\Master Data Services にインストールされます。  
  
 この作業を実行するには、次の手順を実行します。  
  
1.  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] とその他の必要な機能をインストールします。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップ ウィザードを開きます。  
  
    2.  左ペインで、 **[インストール]** をクリックします。  
  
    3.  右ペインで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加]** をクリックします。  
  
    4.  **[機能の選択]** ページで、 **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** とその他にインストールする機能を選択します。  
  
    5.  ウィザードを完了します。  
  
2.  インストールが完了したら、MDS データベース スキーマをアップグレードします。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
        > [!IMPORTANT]  
        >  MDS データベース スキーマをアップグレードするには、MDS データベースの作成時に指定した管理者アカウントでログインする必要があります。 MDS データベースの mdm.tblUser で、このユーザーは **1** の **ID**値を持ちます。 このユーザーの変更方法の詳細については、次を参照してください。[システム管理者アカウントを変更&#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)します。  
  
    2.  左ペインで **[データベース構成]** をクリックします。  
  
    3.  右側のウィンドウで次のようにクリックします。**データベースの選択**の情報を指定し、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]または[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]の場合は、その他のコンピューター上のインスタンスをデータベース[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]または[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]他のコンピューターにインストールされます。  
  
    4.  **[データベースのアップグレード]** をクリックして、 **データベースのアップグレード ウィザード**を起動します。 詳細については、「[データベースのアップグレード ウィザード  &#40;Master Data Services 構成マネージャー&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)」を参照してください。  
  
3.  アップグレードが完了したら、SQL Server 2014 Web アプリケーションを作成します。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
    2.  左ペインで **[Web の構成]** をクリックします。  
  
    3.  右ペインで、 **[Web サイト]** ボックスの一覧から次のいずれかのオプションを選択します。  
  
        -   **[既定の Web サイト]**。その後、 **[アプリケーションの作成]** をクリックします。  
  
        -   **[新しいサイトの作成]**。 Web サイトを作成すると、新しい Web アプリケーションが自動的に作成されます。  
  
        > [!IMPORTANT]  
        >  以前のバージョンの SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) から取得した既存の MDS Web アプリケーションを、Master Data Services 構成マネージャーの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンで選択できます。 既存の Web アプリケーションを選択することはできません。代わりに MDS に対応する [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを作成する必要があります。 それ以外の場合は、アップグレード後の MDS データベースに Web アプリケーションを関連付けようとすると、ページに関連付けられた構成データが無効であるため、要求したページにアクセスできないことを示すエラーが返されます。  
        >   
        >  既存の ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) Web アプリケーションとして同じ名前を、MDS Web アプリケーションの名前 (別名) として使用する場合は、まず Web アプリケーションおよびそれに関連付けられているアプリケーション プールを IIS から削除し、次に Master Data Services 構成マネージャーの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンを使用して同じ名前の Web アプリケーションを作成します。 Web アプリケーションとアプリケーション プールを IIS から削除する方法については、「 [Remove an Application (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=323537) 」 (アプリケーションを削除する (IIS 7))、および「 [Remove an Application Pool (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=323538)」(アプリケーション プールを削除する (IIS 7)) を参照してください。  
  
4.  Web アプリケーションをアップグレード後の MDS データベースに関連付けます。  
  
    1.  **[アプリケーションとデータベースの関連付け]** セクションで、 **[選択]** をクリックします。  
  
    2.  MDS データベースを選択します。  
  
    3.  **[適用]** をクリックします。  
  
##  <a name="restore"></a> アップグレードおよびバックアップからのデータベースの復元  
 このシナリオでは、1 台の同じコンピューターまたは 2 台の異なるコンピューターに、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] と、SQL Server 2008 R2 または SQL Server 2012 がインストールされています。 また、アップグレードの前に、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 リリースより前のバージョンでデータベースがバックアップされており、そのデータベースを復元する必要があります。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、既定で、ファイルが *drive*:\Program Files\Microsoft SQL Server\120\Master Data Services にインストールされます。  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]では、既定で、ファイルが *drive*:\Program Files\Microsoft SQL Server\110\Master Data Services にインストールされます。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]では、既定で、ファイルが *drive*:\Program Files\Microsoft SQL Server\Master Data Services にインストールされます。  
  
 この作業を実行するには、次の手順を実行します。  
  
1.  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] とその他の必要な機能をインストールします。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップ ウィザードを開きます。  
  
    2.  左ペインで、 **[インストール]** をクリックします。  
  
    3.  右ペインで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加]** をクリックします。  
  
    4.  **[機能の選択]** ページで、 **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** とその他にインストールする機能を選択します。  
  
    5.  ウィザードを完了します。  
  
2.  バックアップされたデータベースを復元します。  
  
3.  インストールが完了したら、MDS データベース スキーマをアップグレードします。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
        > [!IMPORTANT]  
        >  MDS データベース スキーマをアップグレードするには、MDS データベースの作成時に指定した管理者アカウントでログインする必要があります。 MDS データベースの mdm.tblUser で、このユーザーは **1** の **ID**値を持ちます。 このユーザーの変更方法の詳細については、次を参照してください。[システム管理者アカウントを変更&#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)します。  
  
    2.  左ペインで **[データベース構成]** をクリックします。  
  
    3.  右側のウィンドウで次のようにクリックします。**データベースの選択**の情報を指定し、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]または[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]データベース インスタンス。  
  
    4.  **[データベースのアップグレード]** をクリックして、 **データベースのアップグレード ウィザード**を起動します。 詳細については、「[データベースのアップグレード ウィザード  &#40;Master Data Services 構成マネージャー&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)」を参照してください。  
  
4.  アップグレードが完了したら、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを作成します。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
    2.  左ペインで **[Web の構成]** をクリックします。  
  
    3.  右ペインで、 **[Web サイト]** ボックスの一覧から次のいずれかのオプションを選択します。  
  
        -   **[既定の Web サイト]**。その後、 **[アプリケーションの作成]** をクリックします。  
  
        -   **[新しいサイトの作成]**。 Web サイトを作成すると、新しい Web アプリケーションが自動的に作成されます。  
  
        > [!IMPORTANT]  
        >  以前のバージョンの SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) から取得した既存の MDS Web アプリケーションを、Master Data Services 構成マネージャーの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンで選択できます。 既存の Web アプリケーションを選択することはできません。代わりに MDS に対応する [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを作成する必要があります。 それ以外の場合は、アップグレード後の MDS データベースに Web アプリケーションを関連付けようとすると、ページに関連付けられた構成データが無効であるため、要求したページにアクセスできないことを示すエラーが返されます。  
        >   
        >  既存の ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) Web アプリケーションとして同じ名前を、MDS Web アプリケーションの名前 (別名) として使用する場合は、まず Web アプリケーションおよびそれに関連付けられているアプリケーション プールを IIS から削除し、次に Master Data Services 構成マネージャーの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンを使用して同じ名前の Web アプリケーションを作成します。 Web アプリケーションとアプリケーション プールを IIS から削除する方法については、「 [Remove an Application (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=323537) 」 (アプリケーションを削除する (IIS 7))、および「 [Remove an Application Pool (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=323538)」(アプリケーション プールを削除する (IIS 7)) を参照してください。  
  
5.  アップグレードされた MDS データベースと新しい web アプリケーションを関連付けるようになりました。  
  
    1.  **[アプリケーションとデータベースの関連付け]** セクションで、 **[選択]** をクリックします。  
  
    2.  MDS データベースを選択します。  
  
    3.  **[適用]** をクリックします。  
  
## <a name="troubleshooting"></a>トラブルシューティング  
 **問題点:** 開くと、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]または[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web アプリケーション、「クライアント バージョンには、データベースのバージョンと互換性がありません」エラー メッセージが表示されます。  
  
 **解決方法:** この問題が発生したときに、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]または[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]マスター データ マネージャー web アプリケーションをアップグレードされたデータベースにアクセスしようとする[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]マスター データ サービス。 代わりに、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web アプリケーションを使用する必要があります。  
  
 この問題はまた、MDS データベース スキーマをアップグレードするときに、IIS で **MDS アプリケーション プール** を停止および再起動しなかった場合にも発生する可能性があります。 その場合は、 **MDS アプリケーション プール** を再起動して問題を解決します。  
  
## <a name="see-also"></a>参照  
 [マスター データ サービスのインストール](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
