---
title: DirectQuery の配置シナリオ (SSAS テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2aaf5cb8-294b-4031-94b3-fe605d7fc4c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a62a05c8908391b9ce925ecfe08ae30540b8fa29
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081651"
---
# <a name="directquery-deployment-scenarios-ssas-tabular"></a>DirectQuery の配置シナリオ (SSAS テーブル)
  このトピックでは、DirectQuery モデルのデザインと展開プロセスを紹介します。 DirectQuery をリレーショナル データのみ使用するように構成するか (DirectQuery のみ)、キャッシュ データのみの使用とリレーショナル データのみの使用を切り替えるようにモデルを構成できます (ハイブリッド モード)。 ここでは、両方のモードの実装プロセスについて説明し、モードとセキュリティ構成に応じたクエリ結果の差異について説明します。  
  
 [設計と展開の手順](#bkmk_DQProcedure)  
  
 [DirectQuery 構成の比較](#bkmk_Configurations)  
  
##  <a name="bkmk_DQProcedure"></a> 設計と展開の手順  
 **手順 1 です。ソリューションを作成します。**  
  
 使用するモードにかかわらず、DirectQuery モデルで使用できるデータに関する制限を説明する情報を確認する必要があります。 たとえば、モデルとレポートで使用されるすべてのデータは単一の SQL Server データベースから取得する必要があります。 詳しくは、「[DirectQuery モード &#40;SSAS テーブル&#41;](tabular-models/directquery-mode-ssas-tabular.md)」をご覧ください。  
  
 また、メジャーと計算列に関する制限を確認し、使用する式が DirectQuery モードと互換性があるかどうかを判断します。 次の要素を削除または変更することが必要な場合があります。  
  
-   計算列はサポートされていません。  
  
-   コピーして貼り付けられたデータは使用できません。 PowerPivot モデルをインポートしてソリューションを簡単に開始する場合は、ソリューションをインポートする前にリンク テーブルを削除してください。このデータは削除できず、DirectQuery 検証をブロックするためです。  
  
 **手順 2 です。モデル デザイナーで DirectQuery モードを有効にします。**  
  
 既定では、DirectQuery は無効になっています。 したがって、デザイン環境が DirectQuery モードをサポートするように構成する必要があります。  
  
 右クリックし、 **Model.bim**ソリューション エクスプ ローラーと、プロパティ セット内のノード**DirectQuery モード**を`On`します。  
  
 いつでも DirectQuery をオンにすることができます。ただし、DirectQuery モードと互換性のない列や数式を作成しないようにするために、最初から DirectQuery モードを有効にすることをお勧めします。  
  
 最初は、DirectQuery モデルが常にメモリに作成されます。 ワークスペース データベースの既定のクエリ モードも **[DirectQuery (In-Memory あり)]** に設定されます。 このハイブリッド動作モードでは、モデルが DirectQuery 要件を満たすことを検証しながら、インポートされたデータのキャッシュを使用してモデル デザイン プロセス中のパフォーマンスを向上させることができます。  
  
 **手順 3 です。検証エラーを解決するには**  
  
 DirectQuery をオンにしたとき、または新しいデータや数式を追加したときに検証エラーが発生する場合は、Visual Studio の **[エラー一覧]** を開き、必要な操作を実行します。  
  
-   エラー メッセージの説明に従って、DirectQuery モードに必要なプロパティ設定を変更します。  
  
-   計算列を削除します。 使用して列の作成は常に特定のメジャーの計算列が必要な場合、[リレーショナル クエリ デザイナー &#40;SSAS&#41; ](relational-query-designer-ssas.md)テーブルのインポート ウィザードで指定します。  
  
-   DirectQuery モードと互換性のない数式を変更または削除します。 計算で特定の関数が必要な場合は、Transact-SQL を使用して同等の関数を提供する方法を検討します。  
  
-   必要に応じてデータを追加します。  コピーして貼り付けたデータまたは SQL Server 以外のプロバイダーからのデータを以前にモデルで使用していた場合は、既存の接続に新しいビューと派生列を作成するか、分散クエリを使用できます。  DirectQuery モデルで使用されるすべてのデータは、単一の SQL Server データ ソースを介してアクセスできる必要があります。  
  
 **手順 4 です。推奨される方法、モデルに対するクエリの応答の設定します。**  
  
|||  
|-|-|  
|**DirectQuery のみ**|プロパティを **[DirectQuery]** に設定します。|  
|**ハイブリッド モード**|プロパティを **[In-Memory (DirectQuery あり)]** または **[DirectQuery (In-Memory あり)]** に設定します。<br /><br /> この値を後で変更して、別の設定を使用できます。<br /><br /> クライアントは接続文字列で優先メソッドをオーバーライドできます。|  
  
 **手順 5 です。DirectQuery パーティションを指定します。**  
  
|||  
|-|-|  
|**DirectQuery のみ**|任意。 DirectQuery のみのモデルには、パーティションは必要ありません。<br /><br /> ただし、デザイン フェーズ中にモデルにパーティションを作成した場合は、1 つのパーティションだけをデータ ソースとして使用できることに注意してください。 既定では、最初に作成したパーティションが DirectQuery パーティションとして使用されます。<br /><br /> モデルに必要なすべてのデータが DirectQuery パーティションにあることを確認するには、DirectQuery パーティションを選択し、SQL ステートメントを編集してデータ セット全体を取得します。|  
|**ハイブリッド モード**|モデル内のいずれかのテーブルに複数のパーティションがある場合は、1 つのパーティションを *DirectQuery パーティション*として選択する必要があります。 パーティションを割り当てない場合、既定では、最初に作成されたパーティションが DirectQuery パーティションとして使用されます。<br /><br /> DirectQuery 以外のすべてのパーティションの処理オプションを設定します。 通常、データはリレーショナル ソースから渡されるため、DirectQuery パーティションは処理されません。<br /><br /> 詳細については、次を参照してください。[パーティションと DirectQuery モード&#40;SSAS 表形式&#41;](tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)します。|  
  
 **手順 6 です。権限借用を構成します。**  
  
 権限借用は、DirectQuery モデルでのみサポートされます。 権限借用オプション **[権限借用設定]** では、指定した SQL Server データ ソースのデータを表示するときに使用する資格情報を定義します。  
  
|||  
|-|-|  
|**DirectQuery のみ**|**権限借用設定** プロパティには、SQL Server データ ソースへの接続に使用するアカウントを指定します。<br /><br /> **ImpersonateCurrentUser**値を使用する場合、モデルをホストする [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスは、モデルの現在のユーザーの資格情報を SQL Server データベースに渡します。|  
|**ハイブリッド モード**|**権限借用設定** プロパティには、SQL Server データ ソース内のデータへのアクセスに使用するアカウントを指定します。<br /><br /> この設定は、モデルで使用するキャッシュの処理に使用される資格情報には影響しません。|  
  
 **手順 7 です。モデルをデプロイします。**  
  
 モデルをデプロイする準備ができたら、開く、**プロジェクト**クリックし、Visual Studio のメニュー**プロパティ**します。 **QueryMode** プロパティを、次の表で説明する値のいずれかに設定します。  
  
 詳細については、次を参照してください。[デプロイから SQL Server Data Tools &#40;SSAS 表形式&#41;](tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md)します。  
  
|||  
|-|-|  
|**DirectQuery のみ**|**DirectQueryOnly**<br /><br /> DirectQuery のみを指定したため、モデルのメタデータはサーバーに配置されますが、モデルは処理されません。<br /><br /> ワークスペース データベースで使用されていたキャッシュは自動的には削除されません。 ユーザーがキャッシュされたデータを表示できないようにするには、デザイン時のキャッシュをクリアします。 詳細については、次を参照してください。 [Analysis Services のキャッシュをクリア](instances/clear-the-analysis-services-caches.md)します。|  
|**ハイブリッド モード**|**DirectQuery (インメモリあり)**<br /><br /> **インメモリと DirectQuery**<br /><br /> どちらの値でも、必要に応じてキャッシュまたはリレーショナル データ ソースを使用できます。 順序によって、モデルに対するクエリへの応答時に既定で使用されるデータ ソースが定義されます。<br /><br /> ハイブリッド モードでは、モデルのメタデータがサーバーに配置されると同時にキャッシュを処理する必要があります。<br /><br /> この設定は配置後に変更できます。|  
  
 **手順 8 です。配置済みモデルを確認します。**  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] で、モデルを配置した [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスを開きます。 データベースの名前を右クリックし、 **[プロパティ]** を選択します。  
  
-   **DirectQueryMode**プロパティは、配置のプロパティを定義したときに設定しました。  
  
-   **データ ソースの権限借用情報**プロパティは、ユーザーの権限借用オプションを定義したときに設定しました。 詳細については、「[権限借用オプションの設定 &#40;SSAS - 多次元&#41;](multidimensional-models/set-impersonation-options-ssas-multidimensional.md)」を参照してください。  
  
-   これらのプロパティは、モデルが配置された後、いつでも変更できます。  
  
##  <a name="bkmk_Configurations"></a> DirectQuery オプションの比較  
 **DirectQuery のみ**  
 このオプションは、データのソースが単一であることを保証する場合、またはデータが大きすぎてメモリに収まらない場合に推奨されます。 非常に大きなリレーショナル データ ソースを操作する場合は、デザイン時にデータのサブセットを使用してモデルを作成できます。 モデルを DirectQuery のみのモードで配置する場合は、データ ソース定義を編集して必要なすべてのデータを含めることができます。  
  
 このオプションは、リレーショナル データ ソースが提供しているセキュリティを使用してユーザーのデータ アクセスを制御する場合にも推奨されます。 キャッシュされたテーブル モデルでは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ロールを使用してデータ アクセスを制御することもできますが、キャッシュに格納されているデータも保護する必要があります。 セキュリティ コンテキストによってデータをキャッシュしないことが要求される場合は、常にこのオプションを使用する必要があります。  
  
 次の表で、DirectQuery のみのモードで可能な展開結果について説明します。  
  
|||  
|-|-|  
|**キャッシュなしの DirectQuery**|キャッシュにデータは読み込まれません。 モデルは処理できません。<br /><br /> モデルは、DAX クエリをサポートするクライアントを使用してクエリのみ行うことができます。 クエリ結果は、常に元のデータ ソースから返されます。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **[[QueryMode]]**  =  **[DirectQuery]**|  
|**キャッシュのみに対するクエリと DirectQuery**|配置が失敗します。 この構成はサポートされていません。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **[[QueryMode]]**  = **In-Memory**|  
  
 **ハイブリッド モード**  
 モデルをハイブリッド モードで配置すると多くの利点があります。必要に応じて SQL Server データ ソースから最新データを取得できますが、キャッシュを保持すると、レポートのデザインまたはモデルのテスト時にメモリ内のデータをより高いパフォーマンスで操作できます。  
  
 DirectQuery ハイブリッド モードは、モデルが非常に大きい場合にも役立ちます。 ユーザーが古いデータを取得したりキャッシュが処理される間モデルが使用不能になったりする代わりに、処理の進行中にモデルを DirectQuery モードに切り替えることができます。 パフォーマンスはわずかに低下する可能性がありますが、ユーザーはリレーショナル ストアからデータを直接取得できるため、結果が最新であることが保証されます。  
  
 次の表で、DirectQuery オプションの組み合わせにおける配置結果を比較します。  
  
|||  
|-|-|  
|**キャッシュ優先のハイブリッド モード**|モデルを処理することができ、データをキャッシュに読み込むことができます。 クエリでは、既定でキャッシュが使用されます。  クライアントで DirectQuery ソースを使用する場合は、接続文字列にパラメーターを挿入する必要があります。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **[[QueryMode]]**  = **In-Memory with DirectQuery**|  
|**DirectQuery 優先のハイブリッド モード**|モデルは処理され、データをキャッシュに読み込むことができます。 ただし、既定ではクエリで DirectQuery が使用されます。 クライアントでキャッシュ データを使用する場合は、接続文字列にパラメーターを挿入する必要があります。 モデル内のテーブルがパーティション分割されている場合は、キャッシュのプリンシパル パーティションも **[In-Memory (DirectQuery あり)]** に設定されます。<br /><br /> **DirectQueryMode** = `On`<br /><br /> **[[QueryMode]]**  =  **[DirectQuery (In-Memory あり)]**|  
  
## <a name="see-also"></a>参照  
 [DirectQuery モード &#40;SSAS テーブル&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [テーブル モデル データ アクセス](tabular-models/tabular-model-data-access.md)  
  
  
