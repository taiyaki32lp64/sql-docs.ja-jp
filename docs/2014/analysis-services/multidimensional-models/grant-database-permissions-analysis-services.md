---
title: データベース アクセス許可 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], full control
- full control permissions [Analysis Services]
ms.assetid: be7e5f64-af43-47d6-84a5-c5c1c277d644
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 335fe6deeb3d89483f5f5adb040b0788891053cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074947"
---
# <a name="grant-database-permissions-analysis-services"></a>データベース権限の付与 (Analysis Services)
  リレーショナル データベースのバックグラウンドを持つ方が Analysis Services データベース管理を始める場合に、まず理解する必要があることは、データ アクセスの観点で、データベースは Analysis Services の主要なセキュリティ保護可能なオブジェクトではないということです。  
  
 Analysis Services の主要なクエリ構造はキューブ (または表形式モデル) であり、それらの特定のオブジェクトにユーザー権限が設定されます。 リレーショナル データベース エンジンではデータベース ログインおよびユーザー権限 (多くの場合 `db_datareader`) がデータベース自体に対して設定されるのとは対照的に、Analysis Services データベースは大部分がデータ モデルの主要なクエリ オブジェクトのコンテナーとなります。 キューブまたは表形式モデルに対するデータ アクセスを有効にすることがある場合は、ここでは、データベースの権限をバイパスし、このトピックに直接移動します。[キューブまたはモデル アクセス許可を付与&#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)します。  
  
 Analysis Services のデータベース権限によって、管理機能が使用できるようになります。フル コントロール データベース権限と概要は同じですが、処理操作を委任する場合の粒度が高くなるという特性があります。 Analysis Services データベースの権限レベルは、次の図と説明に示すように、 **[ロールの作成]** ダイアログ ボックスの **[全般]** ペインに指定されています。  
  
 Analysis Services にはログインがありません。 単にロールを作成し、 **[メンバーシップ]** ペインで Windows アカウントを割り当てるだけです。 管理者も含めてすべてのユーザーが、Windows アカウントを使用して Analysis Services に接続します。  
  
 ![ロールを作成するには、ダイアログが表示されたデータベースのアクセス許可](../media/ssas-permsdbrole.png "ロールを作成するには、ダイアログが表示されたデータベースのアクセス許可")  
  
 データベース レベルで指定される権限には、3 つの種類があります。  
  
 **フル コントロール (管理者)** : フル コントロールは、Analysis Services データベースに対して幅広い裁量を持つすべてを網羅した権限であり、たとえば、データベース内の任意のオブジェクトに対してクエリまたは処理を実行したり、ロールのセキュリティを管理したりできます。 フル コントロールは、データベース管理者ステータスと同義です。 `Full Control`を選択すると、`Process Database`権限および`Read Definition`権限も選択され、どちらも削除することはできません。  
  
> [!NOTE]  
>  サーバー管理者 (サーバー管理者ロールのメンバー) も、サーバー上のすべてのデータベースに対して、暗黙的にフル コントロールがあります。  
  
 `Process Database` それぞれがこのアクセス許可は、データベース レベルで処理を委任するために使用します。 管理者は、別のユーザーまたはサービスにデータベース内の任意のオブジェクトに対する処理操作の呼び出しを許可するロールを作成して、このタスクの負担を軽減できます。 また、特定のオブジェクトに対する処理を可能にするロールも作成できます。 詳細については、「 [処理権限の付与 &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md) 」を参照してください。  
  
 `Read Definition` このアクセス許可には、オブジェクトのメタデータを読み取る権限が付与されます。 それぞれ-関連付けられているデータを表示する機能。 通常、この権限は専用の処理用に作成されたロールで使用され、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] や [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] などのツールを使用してデータベースを対話的に処理できるようにします。 `Read Definition`がない場合、`Process Database`権限はスクリプト化されたシナリオでのみ有効になります。 SSIS や他のスケジューラなどで処理を自動化する場合は、`Process Database`があって`Read Definition`がないロールを作成することをお勧めします。 それ以外の場合は、2 つのプロパティを同じロールに結合することで、ユーザー インターフェイスにデータ モデルを視覚化する SQL Server ツールを使用して自動処理と対話型処理の両方をサポートすることを検討してください。  
  
## <a name="full-control-administrator-permissions"></a>フル コントロール (管理者) 権限  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] では、データベース管理者はフル コントロール (管理者) 権限が含まれているロールに割り当てられた Windows ユーザー ID です。 データベース管理者は、データベース内で次のようなタスクを実行できます。  
  
-   オブジェクトを処理します。  
  
-   キューブ、ディメンション、メジャー グループ、パースペクティブ、データ マイニング モデルなど、データベース内のすべてのオブジェクトのデータおよびメタデータを読み取ります。  
  
-   フル コントロール権限も持つロールにユーザーを追加するなどユーザーまたは権限を追加して、データベース ロールを作成または変更します。  
  
-   データベース ロールまたはロール メンバーシップを削除します。  
  
-   データベースのアセンブリ (またはストアド プロシージャ) を登録します。  
  
 データベース管理者は、サーバー上でデータベースを追加または削除したり、同じサーバー上の他のデータベースに管理者権限を付与したりすることはできません。 その特権は、サーバー管理者にのみ属します。 参照してください[サーバーの管理者アクセス許可の付与&#40;Analysis Services&#41; ](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)このアクセス許可レベルの詳細についてはします。  
  
 すべてのロールがユーザー定義であるため、この目的専用のロール (たとえば、"dbadmin" という名前のロール) を作成し、適切な Windows ユーザー アカウントおよびグループ アカウントを割り当てることをお勧めします。  
  
#### <a name="create-roles-in-ssms"></a>SSMS でのロールの作成  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]のインスタンスに接続[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]、オープン、**データベース**フォルダー、データベースを選択し、右クリック**ロール** | **新しいロール**.  
  
2.  **[全般]** ペインで、DBAdmin などのような名前を入力します。  
  
3.  キューブの **[フル コントロール (管理者)]** チェック ボックスをオンにします。 `Process Database`および`Read Definition`は、自動的にオンになります。 どちらの権限も、`Full Control`が含まれているロールに常に含まれています。  
  
4.  **[メンバーシップ]** ペインで、このロールを使用して Analysis Services に接続する Windows ユーザー アカウントおよびグループ アカウントを追加します。  
  
5.  **[OK]** をクリックして、ロールの作成を終了します。  
  
## <a name="process-database"></a>[データベースの処理]  
 データベースのアクセス許可を付与するロールを定義するときにスキップできます`Full Control`だけを選択および`Process Database`します。 この権限はデータベース レベルで設定され、データベース内のすべてのオブジェクトに対する処理を許可します。 「[処理権限の付与 &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)」を参照してください。  
  
## <a name="read-definition"></a>[定義の読み取り]  
 ような`Process Database`設定`Read Definition`データベース レベルのアクセス許可が、データベース内の他のオブジェクトに連鎖的に影響します。 よりきめ細かいレベルで定義の読み取り権限を設定する場合は、[全般] ペインでデータベース プロパティとして [定義の読み取り] をオフにする必要があります。 詳細については、「[オブジェクト メタデータに対する定義の読み取り権限の付与 &#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [サーバーの管理者アクセス許可の付与&#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [処理権限の付与 &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
  
