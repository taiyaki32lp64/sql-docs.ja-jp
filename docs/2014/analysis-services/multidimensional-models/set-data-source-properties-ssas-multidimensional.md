---
title: データ ソースのプロパティ (SSAS 多次元) の設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.datasourceproperties.f1
helpviewer_keywords:
- Data Source Properties dialog box
ms.assetid: bf8b600f-5b99-4f7d-908b-8a391721e9dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 76d25aabd5b24cdbcc72d3c356168a040a83081a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073050"
---
# <a name="set-data-source-properties-ssas-multidimensional"></a>データ ソースのプロパティの設定 (SSAS 多次元)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、データ ソース オブジェクトによって、多次元モデルにデータを提供する外部データ ウェアハウスまたはリレーショナル データベースへの接続を指定します。 データ ソースのプロパティにより、接続文字列、タイムアウト間隔、最大接続数、およびトランザクション分離レベルが決定されます。  
  
## <a name="set-data-source-properties-in-sql-server-data-tools"></a>SQL Server Data Tools でのデータ ソース プロパティの設定  
  
1.  ソリューション エクスプローラーでデータ ソースをダブルクリックして、データ ソース デザイナーを開きます。  
  
2.  データ ソース デザイナーの **[権限借用情報]** タブをクリックします。 詳細については、「 [データ ソースの作成 &#40;SSAS 多次元&#41;](create-a-data-source-ssas-multidimensional.md)」を参照してください。  
  
## <a name="set-data-source-properties-in-management-studio"></a>Management Studio でのデータ ソース プロパティの設定  
  
1.  データベース フォルダーを展開し、データベース名の下の **[データ ソース]** フォルダーを開き、 **オブジェクト エクスプローラー** でデータ ソースを右クリックして **[プロパティ]** をクリックします。  
  
2.  必要に応じて、名前、説明、または権限借用オプションを変更します。 詳細については、「[権限借用オプションの設定 &#40;SSAS - 多次元&#41;](set-impersonation-options-ssas-multidimensional.md)」を参照してください。  
  
## <a name="data-source-properties"></a>データ ソースのプロパティ  
  
|項目|定義|  
|----------|----------------|  
|**[名前]、[ID]、[説明]**|[名前]、[ID]、および [説明] は、多次元モデルのデータ ソース オブジェクトの識別と説明に使用します。<br /><br /> 名前と説明は、ソリューションを配置または処理した後に、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] または [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で指定できます。<br /><br /> ID は、オブジェクトの作成時に生成されます。 名前と説明は簡単に変更できますが、ID は読み取り専用であり、変更することはできません。 固定オブジェクト ID により、モデル全体でオブジェクトの依存関係と参照が維持されます。|  
|**[タイムスタンプの作成]**|この読み取り専用プロパティは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]に表示されます。 データ ソースが作成された日時を表示します。|  
|**[スキーマの最終更新]**|この読み取り専用プロパティは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]に表示されます。 データ ソースのメタデータが最後に更新された日時を表示します。 この値はソリューションを配置したときに更新されます。|  
|**[クエリ タイムアウト]**|接続要求を破棄するまでの試行時間を指定します。<br /><br /> 次の形式でクエリ タイムアウトを入力します。<br /><br /> *\<時間 >*:*\<分 >*:*\<(秒) >*<br /><br /> このプロパティは、`DatabaseConnectionPoolTimeoutConnection` サーバー プロパティによって却下できます。 値が **[クエリ タイムアウト]** の値未満の場合、このサーバー プロパティが使用されます。<br /><br /> 詳細については、**クエリ タイムアウト**プロパティを参照してください<xref:Microsoft.AnalysisServices.DataSource.Timeout%2A>します。 サーバー プロパティの詳細については、「 [OLAP のプロパティ](../server-properties/olap-properties.md)」を参照してください。|  
|**接続文字列**|多次元モデルにデータを提供するデータベースの物理的な場所と、接続に使用するデータ プロバイダーを指定します。 この情報は、接続要求を行うクライアント ライブラリに提供されます。 プロバイダーによって、接続文字列に設定できるプロパティが決まります。<br /><br /> 接続文字列は、 **[接続マネージャー]** ダイアログ ボックスで指定した情報を使用して作成されます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のデータ ソースのプロパティ ページで、接続文字列を表示および編集することもできます。<br /><br /> SQL Server データベースでは、`user ID` を含む接続文字列はデータベース認証を示し、`Integrated Security=SSPI` を含む接続は Windows 認証を示します。<br /><br /> データベースを新しい場所に移動した場合は、サーバー名またはデータベース名を変更できます。 現在接続に指定されている資格情報がデータベース ログインにマップされていることを必ず確認してください。|  
|**[接続の最大数]**|データ ソースに接続するときに、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で許可される最大接続数を指定します。 指定した接続数よりも多くの接続が必要な場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は接続が使用できるようになるまで待機します。 既定値は 10 です。 接続数を制限することにより、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の要求によって外部データ ソースが過負荷になるのを防ぐことができます。|  
|**分離性**|リレーショナル データベースへの接続で発行される SQL コマンドのロックおよび行のバージョン管理の動作を指定します。 有効な値は、ReadCommitted または Snapshot です。 既定値は ReadCommitted です。これは、ダーティ リードを防ぐために、データが読み取られる前にデータをコミットする必要があることを示します。 Snapshot は、以前にコミットされたデータのスナップショットから読み取ることを示します。 SQL Server での分離レベルについての詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)」を参照してください。|  
|**マネージド プロバイダー**|データ ソースがマネージド プロバイダーを使用している場合、System.Data.SqlClient や System.Data.OracleClient などのマネージド プロバイダーの名前を表示します。<br /><br /> データ ソースがマネージド プロバイダーを使用していない場合、このプロパティには空の文字列が表示されます。<br /><br /> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]では、このプロパティは読み取り専用となります。 接続で使用するプロバイダーを変更するには、接続文字列を編集します。|  
|**[権限借用情報]**|Windows 認証を使用するデータ ソースへの接続時に [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の実行に使用する Windows ID を指定します。 オプションとして、一連の定義済み Windows 資格情報の使用、サービス アカウントの使用、現在のユーザーの ID の使用、モデルに複数のデータ ソース オブジェクトが含まれている場合に役立つ継承オプションがあります。 詳細については、「[権限借用オプションの設定 &#40;SSAS - 多次元&#41;](set-impersonation-options-ssas-multidimensional.md)」を参照してください。<br /><br /> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、有効な値の一覧に次の値が含まれています。<br /><br /> **ImpersonateAccount** (特定の Windows ユーザー名とパスワードを使用して、データ ソースに接続します)。<br /><br /> **ImpersonateServiceAccount** (サービス アカウントのセキュリティ ID を使用して、データ ソースに接続します)。 これが既定値です。<br /><br /> **ImpersonateCurrentUser** (現在のユーザーのセキュリティ ID を使用して、データ ソースに接続します)。 このオプションは、外部のデータ ウェアハウスまたはデータベースからデータを取得するデータ マイニング クエリでのみ有効です。データ接続を多次元データベースでの処理、読み込み、または書き戻しに使用する場合は、このオプションを選択しないでください。<br /><br /> **Inherit** または **default** (このデータ ソース オブジェクトを含む [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの権限借用設定を使用します)。 データベースのプロパティには、権限借用のオプションが含まれます。|  
  
## <a name="see-also"></a>参照  
 [多次元モデルのデータ ソース](data-sources-in-multidimensional-models.md)   
 [データ ソースの作成 &#40;SSAS 多次元&#41;](create-a-data-source-ssas-multidimensional.md)  
  
  
