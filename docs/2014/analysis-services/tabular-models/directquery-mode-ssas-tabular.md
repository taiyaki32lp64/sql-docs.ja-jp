---
title: DirectQuery モード (SSAS テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.realtime.f1
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a9c1510030f61896f686b49f4bc134a7dfcb42b
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284871"
---
# <a name="directquery-mode-ssas-tabular"></a>DirectQuery モード (SSAS テーブル)
  Analysis Services では、データを取得し、リレーショナル データベース システムから直接データと集計を取得することによって、表形式モデルからレポートを作成できます。 を使用して*DirectQuery モード*します。 ここでは、メモリにのみ存在する標準テーブル モデルと、リレーショナル データ ソースにクエリを実行できるテーブル モデルの違いを紹介し、DirectQuery モードで使用するモデルを作成および配置する方法について説明します。  
  
 このトピックのセクション:  
  
-   [DirectQuery モードの利点](#bkmk_Benefits)  
  
-   [DirectQuery モードで使用するためのモデルの作成](#bkmk_Design)  
  
    -   [DirectQuery モデルのデータ ソース](directquery-mode-ssas-tabular.md#bkmk_DataSources)  
  
    -   [検証と DirectQuery モードの設計上の制限](#bkmk_Validation)  
  
    -   [DirectQuery モデルの数式の互換性](#bkmk_FormulaCompat)  
  
    -   [DirectQuery モードでのセキュリティ](#bkmk_Security)  
  
    -   [DirectQuery モードでのセキュリティ](#bkmk_Security)  
  
-   [DirectQuery プロパティ](#bkmk_PropertyList)  
  
-   [関連トピックとタスク](#bkmk_related_tasks)  
  
##  <a name="bkmk_Benefits"></a> DirectQuery モードの利点  
 既定では、テーブル モデルでは、インメモリ キャッシュを使用してデータを格納およびデータにクエリを実行します。 テーブル モデルではメモリ内のデータを使用するため、複雑なクエリでも非常に高速に実行できます。 ただし、キャッシュされたデータの使用にはいくつかの欠点があります。  
  
-   ソース データが変更された場合、データは更新されません。 データを更新するには、モデルを処理する必要があります。  
  
-   モデルをホストするコンピューターの電源をオフにすると、キャッシュがディスクに保存され、モデルの読み込み時または PowerPivot ファイルを開くときに再び開かれます。 保存と読み込みの操作は時間がかかる場合があります。  
  
 対照的に、DirectQuery モードでは、SQLServer データベースに格納されているデータを使用します。  一般には、モデルの作成時にすべてのデータまたはデータの小さなサンプルをキャッシュにインポートし、モデルの配置時に、モデルに対するクエリのデータ ソースをキャッシュされたデータではなく SQL Server にする必要があることを指定します。 データに対する DAX クエリは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって、指定したリレーショナル データ ソースに対する同等の SQL ステートメントに変換されます。  
  
 DirectQuery モードを使用したモデルの配置には、かなりの利点があります。  
  
-   大きすぎて Analysis Services サーバーのメモリに収まらないデータ セットのモデルを作成できます。  
  
-   データが最新であることが保証され、データの別のコピーを維持するための追加の管理オーバーヘッドがありません。 基になるソース データに対する変更は、データ モデルに対するクエリに即時に反映できます。  
  
-   DirectQuery では、xVelocity メモリによって最適化された列インデックスで提供されるアクセラレーションなど、プロバイダー側のクエリ アクセラレーションを利用できます。  
  
-   バックエンド データベースによって適用されるセキュリティは、行レベル セキュリティを使用して適用されることが保証されます。 対照的に、キャッシュされたデータを使用する場合は、サーバー上とまったく同様にキャッシュが保護されることを保証するのが困難な場合があります。  
  
-   複数のクエリを必要とする可能性のある複雑な数式がモデルに含まれる場合、Analysis Services は最適化を実行して、バックエンド データベースに対して実行されるクエリのクエリ プランができるだけ効率的になることを保証できます。  
  
##  <a name="bkmk_Design"></a> DirectQuery モードで使用するためのモデルの作成  
 テーブル モデルは、モデル デザイナー [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を使用して作成されます。 モデル デザイナーはすべてのモデルをメモリに作成します。これは、モデリング時にデータが大きすぎてメモリに収まらない場合に、ワークスペース データベースで使用するキャッシュにデータのサブセットのみをインポートする必要があることを意味します。  
  
 DirectQuery モードに切り替える準備ができたら、DirectQuery モードを有効にするプロパティを変更できます。 詳細については、次を参照してください。 [DirectQuery デザイン モードを有効にする&#40;SSAS 表形式&#41;](enable-directquery-mode-in-ssdt.md)します。  
  
 この操作を行うと、モデル デザイナーは、キャッシュされたデータの操作を継続できるハイブリッド モードで実行するようにワークスペース データベースを自動的に構成します。 モデル デザイナーによって、モデル内の DirectQuery モードと互換性がない機能も通知されます。 考慮する必要のある主な要件を次の一覧にまとめます。  
  
-   **データ ソース:** DirectQuery モデルでは、1 つの SQL Server データ ソースからのみデータを使用できます。 モデルに対して DirectQuery モードがオンになると、コピーと貼り付け操作によって追加されたテーブルなど他の種類のデータをモデル デザイナーで使用できなくなります。 他のすべてのインポート オプションが無効になります。 クエリに含まれるテーブルは、SQL Server データ ソースに属している必要があります。 参照してください[DirectQuery モデルのデータ ソース](directquery-mode-ssas-tabular.md#bkmk_DataSources)詳細についてはします。  
  
-   **計算列のサポート:** 計算列は、DirectQuery モデルではサポートされません。 ただし、データ セットを操作するメジャーと KPI を作成できます。 参照してください[検証](#bkmk_Validation)詳細についてはします。  
  
-   **DAX 関数の使用を制限します。** 一部の DAX 関数は、他の関数で置き換えるか、データ ソースで派生列を使用して値を作成する必要がありますので、DirectQuery モードでは使用できません。 モデル デザイナーには、DirectQuery モードと互換性のない数式を作成したときに発生するエラーのデザイン時検証が用意されています。 詳細については、次のセクションを参照してください。[検証](#bkmk_Validation)です。  
  
-   **数式の互換性:** 特定の既知のケースでは、同じ数式で返される結果が、キャッシュ モデルまたはハイブリッド モデルと、リレーショナル データ ストアのみを使用する DirectQuery モデルとで異なる場合があります。 これらの相違は、xVelocity メモリ内分析 (VertiPaq) エンジンと SQL Server 間のセマンティックの相違によるものです。 これらの相違の詳細については、[数式の互換性](#bkmk_FormulaCompat)します。  
  
-   **セキュリティ:** さまざまな方法を使用して、モデルのデプロイ方法に応じてを保護することができます。 テーブル モデルのキャッシュされたデータは、Analysis Services インスタンスのセキュリティ モデルを使用して保護されます。 DirectQuery モデルはロールを使用して保護することもできますが、リレーショナル データ ストアに定義されているセキュリティも使用できます。 DirectQuery のみのモデルに基づいてレポートを開くユーザーは、SQL Server のアクセス許可で許可されているデータのみ表示できるようにモデルを構成できます。 詳細については、このセクションを参照してください。[セキュリティ](#bkmk_Security)します。  
  
-   **クライアントの制限:** モデルが DirectQuery モードでは、ときに、DAX を使用してのみ照会できます。 MDX を使用してクエリを作成することはできません。 つまり、Excel では MDX を使用するため Excel PivotClient を使用できません。  
  
     ただしでの DirectQuery モデルに対するクエリを作成できます[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]詳細については、XMLA Execute ステートメントの一部として DAX テーブル クエリを使用する場合は、[DAX クエリ構文のリファレンス] を参照してください (/dax dax の構文のリファレンス
  
 デザインの問題をすべて解決し、モデルをテストすると、配置の準備ができます。 この時点では、モデルに対するクエリに応答するための推奨される方法を設定できます。 ユーザーがキャッシュにアクセスできるようにしますか。または常にリレーショナル データ ソースのみ使用するようにしますか。  
  
 モデルをデプロイする場合、*ハイブリッド モード*キャッシュは引き続き使用できますし、クエリに使用できます。 ハイブリッド モードには、多くのオプションが用意されています。  
  
-   キャッシュとリレーショナル データ ソースの両方が使用可能な場合は、優先される接続方法を設定できますが、最終的には、クライアントが DirectQueryMode 接続文字列プロパティを使用して、使用されるソースを制御します。  
  
-   DirectQuery モードに使用されるプライマリ パーティションが処理されず、常にリレーショナル ソースが参照されるような方法で、キャッシュにパーティションを構成することもできます。 モデル デザインとレポート環境を最適化するために、多くの方法でパーティションを使用できます。 詳細については、次を参照してください。[パーティションと DirectQuery モード&#40;SSAS 表形式&#41;](define-partitions-in-directquery-models-ssas-tabular.md)します。  
  
-   モデルが配置された後、優先される接続方法を変更できます。 たとえば、テストにはハイブリッド モードを使用し、モデルを使用するレポートまたはクエリを完全にテストした後でのみ **DirectQuery のみ** のモードに切り替えることができます。 詳しくは、「 [DirectQuery の優先接続方法の設定または変更](../set-or-change-the-preferred-connection-method-for-directquery.md)」をご覧ください。  
  
###  <a name="bkmk_DataSources"></a> DirectQuery モデルのデータ ソース  
 デザイン環境を変更して DirectQuery モードを有効にするとすぐに、ワークスペース データベースのデータ ソースが検証されて、データ ソースが単一の SQL Server データ ソースから取得されたことが確認されます。 コピー貼り付けデータなど他のソースからのデータは、DirectQuery モデルでは許可されていません。  
  
 DirectQuery モードでモデルを使用する場合は、レポートに必要なすべてのデータが指定した SQL Server データベースに格納されていることを確認する必要があります。 モデリングに必要なデータがそのソースで使用可能でない場合は、Integration Services またはその他のデータ ウェアハウジング ツールを使用して、DirectQuery データ ソースとして使用する SQL Server データベースにデータをインポートすることを検討してください。  
  
###  <a name="bkmk_Validation"></a> 検証と DirectQuery モードの設計上の制限  
 DirectQuery モードで使用するモデルを作成する場合は、最初にデータの一部をキャッシュに読み込む必要があります。 最終的に使用するデータが大きすぎてメモリに収まらない場合は使用できます、**プレビューとフィルター**データを取得する、データのサブセットを選択するか、SQL スクリプトを作成するには、テーブルのインポート ウィザードのオプション。  
  
> [!WARNING]  
>  DirectQuery モードでは計算列の使用がサポートされないため、結合またはその他の操作を実行する列がある場合は、事前に計画し、データ インポート クエリまたはスクリプトの一部として列定義を作成する必要があります。  
  
 検証エラーを表示して解決するには、 **の** [エラー一覧] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]を開きます。 DirectQuery モードの使用を妨げる重大なエラーが **[エラー]** タブに表示されます。DirectQuery モードに変更する前にこれらのエラーを修正する必要があります。 解決が難しい検証エラーは、通常、DirectQuery モードではサポートされない数式に関連します。 このセクションを参照してください[数式の互換性](#bkmk_FormulaCompat)、数式および計算列に関連するエラーの概要についてはします。  
  
 DirectQuery アクセス用のモデルの作成時に考慮するその他の事項を次の一覧で説明します。  
  
-   *DirectQuery のみ* のモードでは、レポートの結果は結果を表示するユーザーのセキュリティ コンテキストによって異なる可能性があります。 ユーザーが期待どおりの結果を得られるように、さまざまな資格情報でモデルをテストする必要があります。  
  
-   ハイブリッド モードで動作するようにモデルを構成して、SQL Server のキャッシュまたはデータを使用できるようにするには、各ソースに接続するクライアントが異なる結果を参照する可能性がある (接続文字列に指定されたモードによって異なる) ことを認識する必要があります。 レポートを表示するユーザーに SQL Server のデータのみ表示されるようにする必要がある場合は、キャッシュをクリアするかモデルを DirectQueryOnly に変更する必要があります。  
  
###  <a name="bkmk_FormulaCompat"></a> DirectQuery モデルの数式の互換性  
 一部のモデルには DirectQuery モードではサポートされない数式が含まれており、検証エラーを防ぐためにモデルを再デザインする必要があります。 DirectQuery モードでサポートされている数式の制限を次に示します。  
  
-   計算列は、ハイブリッド モデルの場合でも、DirectQuery モードが有効になっているテーブル モデルではサポートされません。 モデルに計算列が必要な場合は、インポート定義で Transact-SQL を使用して派生列に変換することを検討してください。  
  
-   DirectQuery モデルでは、メジャーで使用する DAX 数式の使用がサポートされます。これらの数式は、リレーショナル データ ストアに対するセットベースの操作に変換されます。 暗黙的なメジャーを使用して作成するすべてのメジャーがサポートされます。  
  
-   すべての関数がサポートされるわけではありません。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、DirectQuery モデルにクエリを実行するときにすべての DAX 数式およびメジャー定義を SQL ステートメントに変換するため、Transact-SQL に変換できない要素を含む数式はモデルで検証エラーをトリガーします。 たとえば、タイム インテリジェンス関数はサポートされていません。 統計関数などのサポートされている関数も、動作が異なる可能性があります。 互換性の問題の完全な一覧を参照してください。[数式と DirectQuery モードでの互換性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)します。  
  
-   モデル内の一部の数式は、モデルを DirectQuery モードに切り替えるときに検証できますが、キャッシュとリレーショナル データ ストアに対して実行したときに異なる結果を返します。 これは、キャッシュに対する計算では Excel の動作をエミュレートすることを意図した多くの機能を含む xVelocity メモリ内分析 (VertiPaq) エンジンのセマンティクスが使用され、リレーショナル データ ストアに格納されているデータに対するクエリでは SQL Server のセマンティクスを使用する必要があるためです。 返す可能性のある別の結果、モデルの配置時にリアルタイムに DAX 関数の一覧は、次を参照してください。[数式と DirectQuery モードでの互換性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)します。  
  
###  <a name="bkmk_Connecting"></a> DirectQuery モデルに接続します。  
 クエリ言語として MDX を使用するクライアントは、DirectQuery モードを使用するモデルに接続できません。 たとえば、DirectQuery モデルに対して MDX クエリを作成しようとした場合は、キューブが見つからない、または処理されていないことを示すエラーが発生します。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、DAX 数式、または XMLA クエリを使用して、DirectQuery モデルに対するクエリを作成できます。 表形式モデルに対するアドホック クエリを実行する方法の詳細については、次を参照してください。[表形式モデルのデータ アクセス](tabular-model-data-access.md)します。  
  
 ハイブリッド モデルを使用している場合は、接続文字列プロパティ DirectQueryMode を指定して、ユーザーがキャッシュに接続するか、それとも DirectQuery データを使用するかを指定できます。  
  
###  <a name="bkmk_Security"></a> DirectQuery モードでのセキュリティ  
 モデル作成時に、ソース データの取得に使用するアクセス許可を指定します。 これは、多くの場合、自分の資格情報か、開発に使用されるアカウントになります。 ただし、DirectQuery モードを使用するようにモデルを切り替えると、セキュリティ コンテキストはより複雑になります。  
  
-   ユーザーに、リレーショナル データ ストアのデータに必要なアクセス レベルがあるかどうかを検討します。  
  
-   同じモデルまたはレポートを表示するユーザーには、ユーザーのセキュリティ コンテキストによっては、さまざまなデータを表示があります。  
  
-   モデル キャッシュが保持されている場合、キャッシュは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] セキュリティ モデル (ロール) を使用して保護されます。 キャッシュには、モデル デザイナーが表示権限を持ち、ユーザーが表示権限を持たないデータが含まれている場合があります。 モデルおよびレポート デザイナーでキャッシュをクリアするか、ロールによってアクセスを制御することでこのデータを保護する必要があります。  
  
-   キャッシュからクエリに応答するモデルは、データ ソースに接続するときに現在のユーザーの権限を借用できません。 データ ソースに接続するときに現在のユーザーの権限を借用する場合には、DirectQuery モードを使用する必要があります。  
  
-   レポート モデルにセキュリティが必要な場合は、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ロールを使用するか、またはデータ ソースに行レベルのアクセス許可を設定するという、2 つのオプションがあります。 テーブルへのアクセスの制御にはリレーショナル データ ソースのセキュリティが使用され、列レベルのセキュリティはサポートされていません。 したがって、1 つの地域のユーザーが異なる地域の売上金額を表示する権限を持たない場合、Sales テーブルに基づくメジャーを含むレポートでは空白またはエラーが返されます。  
  
 DirectQuery のみのモデルでも、DirectQuery を使用してクエリに応答するハイブリッド モデルでも、権限借用設定プロパティによって、DirectQuery を使用してモデルに接続するときに使用される資格情報が指定されます。 プロパティの値は次のとおりです。  
  
 **Default**  
 インポート ウィザードで指定した資格情報を使用して、データ ソースに接続します。 これには、特定の Windows ユーザーまたはサービス アカウントを指定できます。  
  
 `ImpersonateCurrentUser`  
 現在のユーザーの資格情報を使用して、データ ソースに接続します。  
  
 これらのプロパティを設定する方法については、次を参照してください。 [DirectQuery の配置シナリオ&#40;SSAS 表形式&#41;](../directquery-deployment-scenarios-ssas-tabular.md)します。  
  
##  <a name="bkmk_PropertyList"></a> DirectQuery プロパティ  
 DirectQuery を有効にし、モデルに対するクエリに使用されるデータのソースを制御するために [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] および [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で設定できるプロパティの一覧を次の表に示します。  
  
|プロパティ名|説明|  
|-------------------|-----------------|  
|**DirectQueryMode プロパティ**|このプロパティにより、モデル デザイナーで DirectQuery モードを使用できるようになります。 他の DirectQuery プロパティを変更するには、このプロパティを `On` に設定する必要があります。<br /><br /> 詳細については、次を参照してください。 [DirectQuery デザイン モードを有効にする&#40;SSAS 表形式&#41;](enable-directquery-mode-in-ssdt.md)します。|  
|**QueryMode プロパティ**|このプロパティでは、DirectQuery モデルの既定のクエリ メソッドを指定します。このプロパティは、モデルの配置時にモデル デザイナーで設定しますが、後でオーバーライドできます。 プロパティの値は次のとおりです。<br /><br /> **DirectQuery** -この設定は、モデルに対するすべてのクエリがリレーショナル データ ソースのみを使用する必要がありますを指定します。<br /><br /> **[DirectQuery (およびインメモリ)]** - クライアントから接続文字列で特に指定されていない限り、既定ではリレーショナル ソースを使用してクエリに応答する必要があることを指定します。<br /><br /> **[インメモリ]** - キャッシュのみを使用してクエリに応答する必要があることを指定します。<br /><br /> **[インメモリ (および DirectQuery)]** - 既定で次のように指定します。 クライアントから接続文字列で指定されていない限り、キャッシュを使用してクエリに応答する必要があります。<br /><br /> <br /><br /> 詳しくは、「 [DirectQuery の優先接続方法の設定または変更](../set-or-change-the-preferred-connection-method-for-directquery.md)」をご覧ください。|  
|**DirectQueryMode プロパティ**|モデルが配置された後、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でこのプロパティを変更して、DirectQuery モデルで優先されるクエリ データ ソースを変更できます。<br /><br /> 前のプロパティと同様に、このプロパティではモデルの既定のデータ ソースを指定します。値は次のとおりです。<br /><br /> **InMemory**:クエリでは、キャッシュのみを使用できます。<br /><br /> **DirectQuerywithInMemory**:クライアントから接続文字列で特に指定されていない限り、既定ではクエリでリレーショナル データ ソースが使用されます。<br /><br /> **InMemorywithDirectQuery**:クライアントから接続文字列で指定されていない限り、既定ではクエリでキャッシュが使用されます。<br /><br /> (**DirectQuery**:クエリでは、リレーショナル データ ソースのみ使用します。<br /><br /> <br /><br /> 詳しくは、「 [DirectQuery の優先接続方法の設定または変更](../set-or-change-the-preferred-connection-method-for-directquery.md)」をご覧ください。|  
|**権限借用設定プロパティ**|このプロパティでは、クエリ時に SQL Server データ ソースへの接続に使用される資格情報を定義します。 このプロパティはモデル デザイナーで設定でき、モデルの配置後に値を変更できます。<br /><br /> これらの資格情報は、リレーショナル データ ストアに対するクエリの応答にのみ使用されます。これらはハイブリッド モデルのキャッシュの処理に使用される資格情報と同じではありません。<br /><br /> モデルをメモリ内でのみ使用する場合は、権限借用を使用できません。 モデルで DirectQuery モードを使用していない限り、`ImpersonateCurrentUser` 設定は無効です。|  
  
 また、モデルにパーティションが含まれる場合は、DirectQuery モードでクエリのソースとして使用するパーティションを 1 つ選択する必要があります。 詳細については、次を参照してください。[パーティションと DirectQuery モード&#40;SSAS 表形式&#41;](define-partitions-in-directquery-models-ssas-tabular.md)します。  
  
##  <a name="bkmk_related_tasks"></a> 関連トピックとタスク  
  
|トピック|説明|  
|-----------|-----------------|  
|[パーティションと DirectQuery モード&#40;SSAS 表形式&#41;](define-partitions-in-directquery-models-ssas-tabular.md)|DirectQuery モード用に構成されたモデルでのパーティションの使用方法について説明します。|  
|[DirectQuery モードでの DAX 数式の互換性](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|DirectQuery モード用に構成されたモデルで使用できる数式の制限と互換性の要件について説明します。|  
|[DirectQuery デザイン モードを有効にする&#40;SSAS 表形式&#41;](enable-directquery-mode-in-ssdt.md)|DirectQuery モードの使用をサポートするように、デザイン時の環境を変更する方法について説明します。|  
|[DirectQuery パーティションを変更する&#40;SSAS 表形式&#41;](../change-the-directquery-partition-ssas-tabular.md)|DirectQuery パーティションを変更する方法について説明します。|  
|[DirectQuery の優先接続方法の設定または変更](../set-or-change-the-preferred-connection-method-for-directquery.md)|DirectQuery 用に構成されたモデルの接続方法の設定または変更方法について説明します。|  
|[DirectQuery の配置シナリオ&#40;SSAS 表形式&#41;](../directquery-deployment-scenarios-ssas-tabular.md)|DirectQuery の配置シナリオについて説明します。|  
|[テーブル モデルのデータベースの In-Memory または DirectQuery アクセスの構成](enable-directquery-mode-in-ssms.md)|DirectQuery 構成について|  
|[Analysis Services キャッシュのクリア](../instances/clear-the-analysis-services-caches.md)|テーブル モデルのキャッシュのクリア|  
  
## <a name="see-also"></a>参照  
 [パーティション (SSAS テーブル)](partitions-ssas-tabular.md)   
 [テーブル モデル プロジェクト (SSAS テーブル)](tabular-model-projects-ssas-tabular.md)   
 [Excel で分析 &#40;SSAS テーブル&#41;](analyze-in-excel-ssas-tabular.md)  
