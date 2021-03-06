---
title: OLAP マイニング構造を作成する |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 21cbdc9d-d33c-4026-b9ef-1be2bd92b3b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1864bd14a3822269594773afa8b01fe36723f6a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2018
ms.locfileid: "52392005"
---
# <a name="create-an-olap-mining-structure"></a>Create an OLAP Mining Structure
  OLAP キューブまたはその他の多次元データ ストアに基づいてデータ マイニング モデルを作成することには、多くの利点があります。 OLAP ソリューションには、適切に整理、クリーンアップ、および書式設定された大量のデータが既に含まれています。ただし、データが複雑なため、アドホック探索でユーザーが有意なパターンを見つけることは困難です。 データ マイニングは、新しい相関関係を発見し、実用的な洞察力を得るための手段を提供します。  
  
 このトピックでは、既存の多次元ソリューションのディメンションおよび関連メジャーに基づいて OLAP マイニング構造を作成する方法について説明します。  
  
 [必要条件](#bkmk_Reqs)  
  
 [OLAP データ マイニング プロセスの概要](#bkmk_Overview)  
  
 [OLAP ソリューションでのデータ マイニングの使用に関するシナリオ](#bkmk_OLAP_Scenarios)  
  
 [フィルター](#bkmk_Filters)  
  
 [入れ子になったテーブルの使用](#bkmk_Nested)  
  
 [データ マイニング ディメンション](#bkmk_DMDimension)  
  
##  <a name="bkmk_Reqs"></a> OLAP マイニング構造およびモデルの要件  
 OLAP マイニング モデルをデザインしている場合、データ ソースは、キューブを作成するために使用したデータベース内に既に存在しています。 リモート キューブに接続してデータ マイニング オブジェクトを作成することはできません。キューブ オブジェクトは、データベースと同じソリューション内で作成対象のマイニング構造として使用可能である必要があります。  
  
 元のプロジェクト ファイルがない場合、または元のプロジェクト ファイルを変更したくない場合は、Visual Studio の **[サーバーからインポート (多次元またはデータ マイニング)]** オプションを使用して、メタデータおよびソリューション オブジェクトのコピーを取得します。 これにより、既存のオブジェクトに影響を与えることなく、配置ターゲットの変更、データ ソースの編集、およびキューブ オブジェクトの操作を行うことができます。  
  
 詳細については、「 [Analysis Services インポート ウィザードを使用したデータ マイニング プロジェクトのインポート](import-a-data-mining-project-using-the-analysis-services-import-wizard.md)」を参照してください。  
  
##  <a name="bkmk_Overview"></a> OLAP データ マイニング プロセスの概要  
 ソリューション エクスプローラーで **[マイニング構造]** ノードを右クリックし、  **[新しいマイニング構造]** をクリックして、データ マイニング ウィザードを起動します。 ウィザードに従って次の手順を実行して、新しい構造およびモデルの構造を作成します。  
  
1.  **定義方法の選択**:ここでは、データを選択して、ソースの種類、**既存のキューブから**します。  
  
    > [!NOTE]  
    >  既に説明したように、ソースとして使用する OLAP キューブは、マイニング構造と同じデータベース内に存在する必要があります。 さらに、PowerPivot for Excel アドインによって作成されたキューブは、データ マイニング用のソースとして使用できません。  
  
2.  **データ マイニング構造の作成**:構造と共にマイニング モデルまたは構造体だけを作成するかどうかを決定します。  
  
     さらに、データ分析用に適切なアルゴリズムを選択する必要があります。 特定のタスクに関して最適なアルゴリズムを判別するためのガイダンスについては、ハイパーリンクの「データ マイニング アルゴリズム (Analysis Services - データ マイニング)」(ms help://SQL111033/as_1devconc/html/ed1fc83b-b98c-437e-bf53-4ff001b92d64.htm) をご覧ください。  
  
3.  **ソース キューブ ディメンションの選択**:この手順では、データ ソースを選択すると同じです。 モデルのトレーニングに使用される最も重要なデータを含む 1 つのディメンションを選択する必要があります。 後で他のディメンションからデータを追加したり、ディメンションをフィルター処理したりできます。  
  
4.  **ケース キーの選択**:選択したディメンション内で、ケース データの一意識別子として機能する属性 (列) を選択します。  
  
     通常は 1 つの列が自動的に選択されますが、複数のキーがある場合は列を変更できます。  
  
5.  **ケース レベル列を選択すると**:ここで、選択したディメンションと、分析に関連する、関連するメジャーから属性を選択します。 この手順は、テーブルから列を選択する手順と同じです。  
  
     選択したディメンションの属性を使用して作成されたすべてのメジャーが自動的に選択されるので、選択内容を確認してください。  
  
     たとえば、キューブには、顧客の地理的な場所に基づいて運送費を計算するメジャーが含まれている、モデリングのメイン データ ソースとして、Customer ディメンションを選択した場合は、メジャーが提案されます候補として、モデルに追加するため。 既に属性に直接基づいているメジャーを追加しすぎないように注意してください。メジャー式に定義されているように、列の間には既に 1 つの暗黙的リレーションシップが存在しています。この (期待される) 相関関係の強度により、検出できた可能性がある他のリレーションシップがわかりにくくなることがあります。  
  
6.  **マイニング モデル列の使用法の指定**:属性または構造に追加するメジャーごとに、属性を予測に使用するか、入力として使用されるかどうかを指定する必要があります。 これらのオプションを選択しない場合、データは処理されますが分析には使用されません。ただし、後でドリルスルーを有効にした場合はバックグラウンド データとして使用できます。  
  
7.  **入れ子になったテーブルの追加**:関連するテーブルを追加する をクリックします。 **[メジャー グループ ディメンションの選択]** ダイアログ ボックスでは、現在のディメンションに関連するディメンションの中から 1 つだけディメンションを選択できます。  
  
     次に、 **[入れ子になったテーブル キーの選択]** ダイアログ ボックスを使用して、ケース データを含むディメンションに新しいディメンションをどのように関連付けるかを定義します。  
  
     **[入れ子になったテーブル列の選択]** ダイアログ ボックスを使用して、新しいディメンションから分析に使用する属性およびメジャーを選択します。 さらに、入れ子になった属性を予測に使用するかどうかを指定する必要があります。  
  
     必要な入れ子になった属性をすべて追加したら、 **[マイニング モデル列の使用法の指定]** ページに戻り、 **[次へ]** をクリックします。  
  
8.  **列のコンテンツおよびデータ型を指定**:この時点で、すべてのデータを分析に使用して、指定する必要があります追加されて、*データ型*と*コンテンツの種類*属性ごとにします。  
  
     OLAP モデルの場合、データ型を自動的に検出するオプションはありません。これは、データ型が既に多次元ソリューションで定義されていて、変更することができないためです。 キーも自動的に識別されます。 詳細については、「[データ型 (データ マイニング)](data-types-data-mining.md)」をご覧ください。  
  
     モデルで使用するそれぞれの列に対して選択した *コンテンツの種類* により、アルゴリズムにおけるデータの処理方法が決まります。 詳細については、「[コンテンツの種類 (データ マイニング)](content-types-data-mining.md)」をご覧ください。  
  
9. **ソース キューブのスライス**:ここでデータのサブセットのみを選択し、複数の対象となるモデルをトレーニングするには、キューブにフィルターを定義できます。  
  
     キューブをフィルター処理するには、フィルター処理するディメンションを選択します。次に、使用する条件を含む階層レベルを選択し、フィルターとして使用する条件を入力します。  
  
10. **テスト セットの作成**:このページで、わかりますウィザード データの量は、モデルのテストで使用するため確保する必要があります。 データで複数のモデルがサポートされている場合は、同じデータに対してすべてのモデルをテストできるように予約データセットを作成することをお勧めします。  
  
     詳細については、「 [テストおよび検証 (データ マイニング)](testing-and-validation-data-mining.md)" テンプレートを使用して、データ マイニング プロジェクトを作成します。  
  
11. **ウィザードの完了**:このページで、新しいマイニング構造と関連マイニング モデルに名前を指定し、構造とモデルを保存します。  
  
     さらにこのページでは、次のオプションを設定できます。  
  
    -   **[ドリルスルーを許可する]**  
  
    -   **[マイニング モデル ディメンションを作成する]**  
  
    -   **[マイニング モデル ディメンションを使用してキューブを作成する]**  
  
     これらのオプションの詳細については、このトピックの後半の「 [データ マイニング ディメンションおよびドリルスルーについて](#bkmk_DMDimension)」を参照してください。  
  
 この段階で、マイニング構造とそのモデルは単なるメタデータです。結果を得るには、これらの両方を処理する必要があります。  
  
##  <a name="bkmk_OLAP_Scenarios"></a> データ マイニングと OLAP データの使用に関するシナリオ  
 OLAP キューブには多数のメンバーおよびディメンションが含まれていることが多く、データ マイニングをどこから始めたらよいか判断するのが難しい場合があります。 キューブ内のパターンを手動で識別しやすくするには、通常、目的のディメンションを 1 つ特定してから、そのディメンションに関連するパターンを調べます。 次の表は、一般的な OLAP データ マイニング タスクの一覧で、各タスクを適用できるサンプル シナリオの説明、各タスクに使用するデータ マイニング アルゴリズムを示しています。  
  
|タスク|サンプル シナリオ|アルゴリズム|  
|----------|---------------------|---------------|  
|クラスターへのメンバーのグループ化|顧客メンバーのプロパティ、顧客が購入する製品、顧客が費やす金額に基づいて顧客ディメンションを分割します。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] クラスタリング アルゴリズム|  
|興味深いメンバーまたは異常なメンバーの検索|売上、利益、店舗の場所、店舗の規模に基づいて、Store ディメンション内の興味深い店舗または異常な店舗を識別します。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズム|  
|興味深いセルまたは異常なセルの検索|一般的な傾向に反している店舗売上を識別します。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズム|  
|相関関係の検索|地域、コンピューターの種類、OS、購入日など、サーバーのダウンタイムに関連する要因を識別します。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Naïve Bayes アルゴリズム|  
  
##  <a name="bkmk_Filters"></a> キューブのスライスとします。モデルのフィルター処理  
 モデルを作成しているときにキューブをスライスすることは、リレーショナル マイニング モデルにフィルターを作成することと似ています。 リレーショナル モデルでは、データ ソースのフィルターは、SQL ステートメントの WHERE 句として定義されます。キューブでは、エディターを使用して、MDX を使用するフィルター ステートメントを作成します。  
  
 たとえば、全世界における製品の売上に関する情報が含まれているキューブがある一方で、マーケティング キャンペーン用にイギリス在住の 31 歳以上の女性客を対象とする分析に基づいてモデルを作成したい場合があります。  
  
 このシナリオでは、2 つのフィルターを作成します。  
  
-   最初のフィルターは、Geography ディメンションを選択、Region の階層を選択して使用して、、**フィルター式**一覧を指定できる値から United Kingdom を選択します。  
  
-   2 番目のフィルターには、現在の Customer ディメンションの選択し、Gender 属性を選択属性値の一覧から [Female] を選択します。  
  
 マイニング構造を作成した後は、キューブ データとフィルター条件の両方の定義を変更できます。 詳しくは、「 [マイニング構造のソース キューブのフィルター選択](../filter-the-source-cube-for-a-mining-structure.md)」をご覧ください。  
  
 **[マイニング構造]** タブと **[マイニング モデル]** タブのどちらでも、 **[キューブ スライスの定義]** をクリックして既存のマイニング構造にフィルターを追加できます。 **[キューブのスライス]** ダイアログ ボックスでは、ドロップダウン リストから値を選択して有効な MDX フィルター式を作成できます。  
  
> [!WARNING]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ではキューブをデザインおよび参照するためのインターフェイスが変更されている点に注意してください。 詳細については、「 [キューブ内のデータおよびメタデータの参照](../multidimensional-models/browse-data-and-metadata-in-cube.md)」を参照してください。  
  
 キューブには、マイニング モデルに必要なデータを返すために必要な数のフィルターを追加できます。 また、個々のキューブ スライスでスライスを定義することもできます。 たとえば、製品に基づいている 2 つの入れ子になったテーブルが構造に含まれている場合は、2004 年 3 月で 1 つのテーブルをスライスし、2004 年 4 月で別のテーブルをスライスできます。 結果として得られるモデルは、3 月の購入に基づいて 4 月に購入を予測するために使用できます。  
  
##  <a name="bkmk_Nested"></a> OLAP マイニング モデルでの入れ子になったテーブルの使用  
 データ マイニング ウィザードを使用してキューブ データに基づくモデルを作成する場合、入れ子になったテーブルを追加できます。そのためには、関連するディメンションの名前を指定し、モデルに追加する属性またはメジャーを選択します。  
  
 たとえば、ケース データに使用するメイン ディメンションが Customer の場合、過去に顧客によって複数の製品が注文されていることが考えられ、キューブでは既に注文ファクト テーブルを介して各顧客が多くの製品にリンクされているため、Products ディメンションを関連ディメンションとして追加します。  
  
 入れ子になっているテーブルを追加するには、ウィザードの **[マイニング モデル列の使用法の指定]** ページで **[入れ子になっているテーブルの追加]** をクリックします。 関連するディメンションとメジャーを選択するためのダイアログ ボックスが開きます。 ケースおよび入れ子になったディメンションは、外部キーを使用して関連付ける必要があります。メジャーには、ケースまたは入れ子になったテーブルに既に含まれているいずれかの属性を使用する必要があります。 残念ながら、これらの制限事項あまりをモデリングに有用な属性のみを選択する必要があるため、スコープを絞り込みます。  
  
 入れ子になったテーブルに追加するそれぞれの属性またはメジャーに対して、 **[入れ子になったテーブル列の選択]** ダイアログ ボックスで **[予測可能]** または **[入力]** を選択して、入れ子になった属性を予測に使用するかどうかを指定する必要があります。 これらのオプションを選択しない場合、データはマイニング構造に追加されますが、分析には使用されません。  
  
 さらに、それぞれの属性およびメジャーに対して、属性が連続属性、不連続属性、または分離属性かどうかを指定する必要があります。 ウィザードでは属性のデータ型に基づいて既定値が自動的に選択されますが、アルゴリズム要件によってはこれらの既定値を変更する必要があります。 選択したアルゴリズムと互換性がないコンテンツの種類を選択する場合 (たとえばを使用する継続的な数値型、単純ベイズ モデルと)、モデルを処理しようとするまでは、エラー メッセージを表示しません。  
  
 これらのオプションの設定が完了すると、ウィザードによって入れ子になったテーブルがケース テーブルに追加されます。 入れ子になったテーブルの既定の名前は、入れ子になったディメンション名ですが、入れ子になったテーブルとその列は名前を変更できます。 この操作を繰り返すことにより、複数の入れ子になったテーブルをマイニング構造に追加できます。  
  
 このような入れ子になったテーブル データを使用する能力は、SQL Server データ マイニングで提供される非常に強力な機能の 1 つです。キューブにおいては、関連するデータのサブセットの使用に関して無限の可能性があります。  
  
##  <a name="bkmk_DMDimension"></a> データ マイニング ディメンションおよびドリルスルーについて  
 **[ドリルスルーを許可する]** オプションを使用すると、モデルを参照している間に基になるキューブ データに対するクエリを実行できます。 データは新しいデータ マイニング ディメンションに含まれていませんが、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースはデータ バインディングを使用してソース キューブから情報を取得できます。  
  
 **[マイニング モデル ディメンションを作成する]** オプションを使用すると、既存のキューブ内にアルゴリズムによって検出されたパターンを格納する新しいディメンションを生成できます。 新しいディメンション内の階層は、主にモデルの種類によって決まります。 たとえば、クラスタリング モデルの表現は非常にフラットで、階層の最上位に [(すべて)] ノードがあり、各クラスターはその次のレベルにあります。 これに対し、デシジョン ツリー モデルに対して作成されたディメンションは、ツリーの分岐を表す非常に深い階層を持つ場合があります。  
  
 **[マイニング モデル ディメンションを使用してキューブを作成する]** オプションを使用すると、新しいデータ マイニング ディメンションを新しいキューブにエクスポートできます。 データ マイニング ディメンションでのドリルスルーに必要なすべてのオブジェクトが自動的に含められます。  
  
> [!WARNING]  
>  データ マイニング ディメンションの作成をサポートするモデルは、Microsoft クラスタリング アルゴリズム、Microsoft デシジョン ツリー アルゴリズム、または Microsoft アソシエーション アルゴリズムに基づくモデルのみです。  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング構造列](mining-structure-columns.md)   
 [マイニング モデル列](mining-model-columns.md)   
 [マイニング モデルのプロパティ](mining-model-properties.md)   
 [マイニング構造と構造列のプロパティ](properties-for-mining-structure-and-structure-columns.md)  
  
  
