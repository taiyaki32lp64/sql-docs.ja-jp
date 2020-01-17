---
title: 表形式モデル ソリューションの配置 (SSAS テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aff96558-e5e5-4b95-8ddf-ee0709c842fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0126337fb1f871a4d89354bd65cbfd11932bf5c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066365"
---
# <a name="tabular-model-solution-deployment-ssas-tabular"></a>テーブル モデル ソリューションの配置 (SSAS テーブル)
  テーブル モデル プロジェクトを作成した後、ユーザーがレポート クライアント アプリケーションを使用してモデルを参照できるように配置する必要があります。 このトピックでは、テーブル モデル ソリューションを環境に配置する際に使用できるさまざまなプロパティと方法について説明します。  
  
 このトピックのセクション:  
  
-   [利点](#bkmk_benefits)  
  
-   [SQL Server データ ツール (SSDT) からのテーブル モデルの配置](#bkmk_deploying_bism)  
  
-   [配置プロパティ](#bkmk_deploy_props)  
  
-   [配置方法](#bkmk_meth)  
  
-   [配置サーバーの構成と配置済みのモデルへの接続](#bkmk_connecting)  
  
-   [関連タスク](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> 利点  
 テーブル モデルを配置すると、テスト環境、ステージング環境、または実稼働環境に model データベースが作成されます。 これで、ユーザーは SharePoint で .bism 接続ファイルを使用するか、Microsoft Excel、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、カスタム アプリケーションなどのレポート クライアント アプリケーションから直接データ接続を使用して、配置済みモデルに接続できます。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の新しいテーブル モデル プロジェクトの作成時に作成され、モデルの作成に使用するモデル ワークスペース データベースは、ワークスペース サーバー インスタンス上に保持されるため、必要に応じてモデル プロジェクトに変更を加えてから、テスト環境、ステージング環境、または実稼働環境に再配置できます。  
  
##  <a name="bkmk_deploying_bism"></a> SQL Server データ ツール (SSDT) からのテーブル モデルの配置  
 配置は簡単なプロセスですが、モデルを適切な構成オプションで適切な Analysis Services インスタンスに配置するには、特定の手順に従う必要があります。  
  
 表形式のモデルは、いくつかの配置固有のプロパティで定義されます。 配置すると、 **[サーバー]** プロパティで指定された Analysis Services インスタンスへの接続が確立されます。 **[データベース]** プロパティで指定された名前の model データベースが存在しない場合、その名前の新しいデータベースがそのインスタンスに作成されます。 モデル プロジェクトの Model.bim ファイルからメタデータを使用して、展開サーバー上の model データベースでオブジェクトを構成します。 **[処理オプション]** では、モデル メタデータのみを配置するだけであるか、model データベースを作成するかを指定できます。または、 **[既定]** または **[完全]** が指定されている場合は、データ ソースへの接続に使用した権限借用の資格情報がメモリ内でモデル ワークスペース データベースから配置済みの model データベースに渡されます。 Analysis Services により、配置済みのモデルにデータを取り込む処理が実行されます。 配置プロセスが完了すると、クライアント アプリケーションでデータ接続を使用するか、または SharePoint で .bism 接続ファイルを使用して、model データベースに接続できます。  
  
##  <a name="bkmk_deploy_props"></a> 配置プロパティ  
 プロジェクトの [配置オプション] および [配置サーバー] のプロパティでは、モデルをステージング環境または運用環境の Analysis Services に配置する方法と場所を指定します。 すべてのモデル プロジェクトに対して既定のプロパティ設定が定義されていますが、固有の配置要件に応じて、プロジェクトごとにそれらのプロパティ設定を変更できます。 既定の配置プロパティの設定の詳細については、「[既定のデータ モデルと配置プロパティの構成 &#40;SSAS テーブル&#41;](properties-ssas-tabular.md)」を参照してください。  
  
### <a name="deployment-options-properties"></a>[配置オプション] のプロパティ  
 [配置オプション] のプロパティを以下に示します。  
  
|プロパティ|既定の設定|説明|  
|--------------|---------------------|-----------------|  
|**[処理オプション]**|**Default**|このプロパティでは、オブジェクトの変更を配置するときに必要な処理方法を指定します。 このプロパティには、次のオプションがあります。<br /><br /> **既定の**-この設定は、Analysis Services が必要な処理の種類を決定を指定します。 未処理のオブジェクトは処理され、必要に応じて、属性リレーションシップ、属性階層、ユーザー階層、および計算列が再計算されます。 通常は、[完全処理] オプションを使用するよりも、配置時間が高速になります。<br /><br /> **処理を行う**-この設定は、メタデータのみを配置を指定します。 配置後、配置済みのモデルに対して処理操作を実行してデータの更新および再計算を実行する必要がある場合があります。<br /><br /> **完全な**-この設定は、両方、メタデータが展開されているし、完全な処理操作の実行を指定します。 これにより、配置済みのモデルには、メタデータおよびデータの最新の更新が含まれます。|  
|**トランザクション配置**|**False**|このプロパティでは、配置がトランザクションかどうかを指定します。 既定では、すべてのオブジェクトまたは変更されたオブジェクトの配置は、それらを配置した後の処理とトランザクション関係がありません。 処理に失敗しても、配置は成功して持続できます。 これを変更して、配置と処理を 1 つのトランザクションに組み込むこともできます。|  
|**クエリ モード**|**In-Memory**|このプロパティでは、クエリ結果が返される元のソースが In-Memory (キャッシュ) モードと DirectQuery モードのどちらで実行されるかを指定します。 このプロパティには、次のオプションがあります。<br /><br /> **DirectQuery** -この設定は、モデルに対するすべてのクエリがリレーショナル データ ソースのみを使用する必要がありますを指定します。<br /><br /> **[DirectQuery (およびインメモリ)]** - クライアントから接続文字列で特に指定されていない限り、既定ではリレーショナル ソースを使用してクエリに応答する必要があることを指定します。<br /><br /> **[インメモリ]** - キャッシュのみを使用してクエリに応答する必要があることを指定します。<br /><br /> **[インメモリ (および DirectQuery)]** - 既定で次のように指定します。 クライアントから接続文字列で指定されていない限り、キャッシュを使用してクエリに応答する必要があります。<br /><br /> <br /><br /> 詳細については、「[DirectQuery モード &#40;SSAS テーブル&#41;](directquery-mode-ssas-tabular.md)」を参照してください。|  
  
### <a name="deployment-server-properties"></a>[配置サーバー] のプロパティ  
 [配置サーバー] のプロパティを以下に示します。  
  
|プロパティ|既定の設定|説明|  
|--------------|---------------------|-----------------|  
|**[サーバー]**<br /><br /> プロジェクトの作成時に設定します。|**localhost**|このプロパティは、プロジェクトの作成時に設定し、モデルを配置する Analysis Services インスタンスの名前を指定します。 既定では、モデルは、ローカル コンピューター上の Analysis Services の既定のインスタンスに配置されます。 ただし、この設定を変更して、ローカル コンピューター上の名前付きインスタンスや、Analysis Services オブジェクトを作成する権限のあるリモート コンピューター上の任意のインスタンスを指定できます。|  
|**のエディション**|ワークスペース サーバーがある場所のインスタンスと同じエディション。|このプロパティでは、モデルを配置する Analysis Services サーバーのエディションを指定します。 サーバー エディションにより、プロジェクトに組み込むことができるさまざまな機能が定義されます。 既定では、ローカルの Analysis Services サーバーのエディションになります。 Analysis Services の実稼働サーバーなど、別の Analysis Services サーバーを指定する場合は、その Analysis Services サーバーのエディションを指定する必要があります。|  
|**[データベース]**|**\<projectname>**|このプロパティでは、配置時にモデル オブジェクトがインスタンス化される Analysis Services データベースの名前を指定します。 この名前は、レポート クライアント データ接続や .bism データ接続ファイルにも指定されます。<br /><br /> この名前は、モデルの作成中にいつでも変更できます。 モデルを配置した後に名前を変更した場合、配置後に行った変更は既に配置されているモデルには反映されません。 たとえば、`TestDB` という名前のソリューションを開き、既定の model データベース名の Model という名前のソリューションを配置した後、ソリューションを変更して、model データベースの名前を `Sales` に変更すると、そのソリューションが配置された Analysis Services インスタンスには、Model という名前のデータベースと Sales という名前のデータベースが別々に表示されます。|  
|**[キューブ名]**|**[モデル]**|このプロパティでは、クライアント ツール (Excel など) および分析管理オブジェクト (AMO) に表示するキューブ名を指定します。|  
  
### <a name="directquery-options-properties"></a>[DirectQuery オプション] のプロパティ  
 [配置オプション] のプロパティを以下に示します。  
  
|プロパティ|既定の設定|説明|  
|--------------|---------------------|-----------------|  
|**権限借用設定**|**[既定]**|このプロパティでは、DirectQuery モードで実行されるモデルがデータ ソースに接続するときに使用される権限借用設定を指定します。 権限借用資格情報は、メモリ内キャッシュのクエリを実行するときには使用されません。 このプロパティの設定には、以下のオプションがあります。<br /><br /> **既定の**-この設定は、Analysis Services がデータ ソース接続がテーブルのインポート ウィザードを使用して作成されたときに、権限借用情報 ページで指定されたオプションを使用して指定します。<br /><br /> **ImpersonateCurrentUser** -この設定は、すべてのデータ ソースに接続するとき現在ログオンしているユーザーのユーザー アカウントが使用を指定します。|  
  
##  <a name="bkmk_meth"></a> 配置方法  
 テーブル モデル プロジェクトを配置する方法はいくつかあります。 多次元プロジェクトなど、他の Analysis Services プロジェクトに使用できる配置方法の多くは、テーブル モデル プロジェクトの配置にも使用できます。  
  
|方法|説明|リンク|  
|------------|-----------------|----------|  
|**SQLServer データ ツールの Deploy コマンド**|Deploy コマンドは、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 作成環境からテーブル モデル プロジェクトを配置する単純で直観的な方法です。<br /><br /> **\*\* 注意 \*\*** この方法は、運用サーバーへの配置には使用できません。 この方法を使用して、既存のモデル内の特定のプロパティを上書きできます。|[SQL Server データ ツールからの配置 &#40;SSAS テーブル&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|  
|**分析管理オブジェクト (AMO) オートメーション**|AMO を使用すると、ソリューションの配置に使用できるコマンドを含む、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の完全なコマンド セットのプログラム インターフェイスを利用できます。 ソリューション配置の方法として最も柔軟に使用できるのは、AMO オートメーションですが、この方法ではプログラミング作業も必要になります。  AMO を使用する主な利点は、AMO アプリケーションでは SQL Server エージェントを使用して、あらかじめ設定したスケジュールに従って配置を実行できることです。|[分析管理オブジェクト &#40;AMO&#41; による開発](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|**XMLA**|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、既存の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのメタデータの XMLA スクリプトを生成し、別のサーバーでそのスクリプトを実行して初期データベースを再作成します。 XMLA スクリプトは、配置プロセスを定義し、それをコード化して XMLA スクリプトに保存することにより、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で簡単に作成できます。 XMLA スクリプトをファイルに保存すると、簡単に、スケジュールに基づいてスクリプトを実行したり、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに直接接続しているアプリケーションにスクリプトを埋め込んだりすることができます。<br /><br /> SQL Server エージェントを使用すると、XMLA スクリプトもあらかじめ設定したスケジュールに従って実行できますが、XMLA スクリプトには AMO ほどの柔軟性はありません。 AMO では、さまざまなすべての管理コマンドをホストすることにより、広範にわたる機能を実現しています。|[XMLA を使用したモデル ソリューションの配置](../multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**配置ウィザード**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトによって生成された XMLA 出力ファイルを使用して、プロジェクトのメタデータを宛先サーバーに配置するには、配置ウィザードを使用します。 配置ウィザードを使用すると、プロジェクト ビルドの出力ディレクトリによって作成される [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ファイルからインスタンスを直接配置できます。<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の配置ウィザードを使用する主な利点は利便性です。 後で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で使用するために XMLA スクリプトを保存できるのと同様に、配置ウィザード スクリプトも保存できます。 配置ウィザードは、対話的に実行することも、配置ユーティリティを使用してコマンド プロンプトから実行することもできます。|[Deploy Model Solutions Using the Deployment Wizard](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**配置ユーティリティ**|配置ユーティリティを使用すると、コマンド プロンプトから Analysis Services の配置エンジンを起動することができます。|[配置ユーティリティを使用したモデル ソリューションの配置](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**データベースの同期ウィザード**|2 つの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース間でメタデータとデータを同期するには、データベースの同期ウィザードを使用します。<br /><br /> 同期ウィザードを使用すると、コピー元のサーバーからコピー先のサーバーにデータとメタデータをコピーできます。 配置するデータベースのコピーが、コピー先のサーバーにない場合、新しいデータベースがコピー先のサーバーにコピーされます。 コピー先のサーバーに同じデータベースのコピーが既にある場合、コピー先サーバー上のデータベースは、ソース データベースのメタデータとデータを使用するように更新されます。|[Analysis Services データベースの同期](../multidimensional-models/synchronize-analysis-services-databases.md)|  
|**バックアップと復元**|バックアップは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを転送する最も簡単な方法です。 **[バックアップ]** ダイアログ ボックスを使用すると、オプション構成を設定した後で、ダイアログ ボックスから直接バックアップを実行できます。 また、スクリプトを作成して保存し、必要なときに実行することもできます。<br /><br /> バックアップと復元は、他の配置方法ほど頻繁には使用されませんが、インフラストラクチャの要件を最小限に抑えながら配置をすばやく完了することができます。|[Analysis Services データベースのバックアップと復元](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_connecting"></a> 配置サーバーの構成と配置済みのモデルへの接続  
 model データベースを配置した後は、モデルのデータ アクセスのセキュリティ保護、バックアップ、および処理操作に関する追加の考慮事項があります。それらは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、Analysis Services サーバーで構成できます。 これらのプロパティおよび構成設定はこのトピックの対象外ですが、それでも配置済みの model データの安全性を保証し、最新の状態に保ち、組織内のユーザーに重要なデータ分析リソースを提供する際には非常に重要です。  
  
 モデルを配置し、サーバーのオプション設定を構成したら、レポート クライアント アプリケーションによって接続して、モデル メタデータの参照および分析に使用できます。 クライアント アプリケーションから配置済みの model データベースへの接続は、このトピックの対象外です。 クライアント アプリケーションから配置済みの model データベースに接続する方法の詳細については、「 [テーブル モデル データ アクセス](tabular-model-data-access.md)」を参照してください。  
  
##  <a name="bkmk_rt"></a> 関連タスク  
  
|タスク|説明|  
|----------|-----------------|  
|[SQL Server データ ツールからの配置 &#40;SSAS テーブル&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で Deploy コマンドを使用して、配置プロパティを構成し、テーブル モデル プロジェクトを配置する方法について説明します。|  
|[配置ウィザードを使用したモデル ソリューションの配置](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|このセクションの各トピックでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードを使用して、テーブル モデル ソリューションと多次元モデル ソリューションの両方を配置する方法について説明します。|  
|[配置ユーティリティを使用したモデル ソリューションの配置](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ユーティリティを使用して、テーブル モデル ソリューションと多次元モデル ソリューションを配置する方法について説明します。|  
|[XMLA を使用したモデル ソリューションの配置](../multidimensional-models/deploy-model-solutions-using-xmla.md)|XMLA を使用して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] テーブル ソリューションと多次元ソリューションを配置する方法について説明します。|  
|[Analysis Services データベースの同期](../multidimensional-models/synchronize-analysis-services-databases.md)|データベースの同期ウィザードを使用して、2 つの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] テーブル データベースと多次元データベース間でメタデータとデータを同期する方法について説明します。|  
  
## <a name="see-also"></a>参照  
 [テーブル モデル データベースへの接続 &#40;SSAS&#41;](connect-to-a-tabular-model-database-ssas.md)  
  
  
