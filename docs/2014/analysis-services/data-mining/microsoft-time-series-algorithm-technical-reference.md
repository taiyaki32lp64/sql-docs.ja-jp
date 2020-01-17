---
title: Microsoft タイム シリーズ アルゴリズム テクニカル リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ARTXP
- HISTORICAL_MODEL_GAP parameter
- AUTO_DETECT_PERIODICITY parameter
- time series algorithms [Analysis Services]
- ARIMA
- INSTABILITY_SENSITIVITY parameter
- PERIODICITY_HINT parameter
- MAXIMUM_SERIES_VALUE parameter
- time series [Analysis Services]
- MINIMUM_SUPPORT parameter
- HISTORIC_MODEL_COUNT parameter
- FORECAST_METHOD parameter
- MISSING_VALUE_SUBSTITUTION parameter
- MINIMUM_SERIES_VALUE parameter
- COMPLEXITY_PENALTY parameter
- PREDICTION_SMOOTHING parameter
ms.assetid: 7ab203fa-b044-47e8-b485-c8e59c091271
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c5ffde59f990602964ac178e629a9967d6304d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083761"
---
# <a name="microsoft-time-series-algorithm-technical-reference"></a>Microsoft Time Series アルゴリズム テクニカル リファレンス
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムには、時系列を分析するための 2 つの異なるアルゴリズムが含まれています。  
  
-   ARTXP アルゴリズム。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]で導入されたアルゴリズムで、系列内で最も近い値の予測に適しています。  
  
-   ARIMA アルゴリズム。長期的な予測の精度を向上させるために [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] で追加されたアルゴリズムです。  
  
 既定では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は各アルゴリズムを別々に使用してモデルのトレーニングを行い、その結果を統合して、さまざまな数の予測に対して最適な予測を出力します。 使用するデータや予測の要件に基づいて、一方のアルゴリズムのみを使用するように選択することもできます。 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]では、予測時のアルゴリズムの組み合わせを制御するカットオフ ポイントをカスタマイズすることもできます。  
  
 このトピックでは、各アルゴリズムがどのように実装されているのかについての追加情報を紹介し、パラメーターを設定してアルゴリズムをカスタマイズすることによって分析や予測の結果を微調整する方法を説明します。  
  
## <a name="implementation-of-the-microsoft-time-series-algorithm"></a>Microsoft Time Series アルゴリズムの実装  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Research は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムに基づいた実装で、SQL Server 2005 で使用されていた最初の ARTXP アルゴリズムを開発しました。 そのため、ARTXP アルゴリズムは周期的な時系列データを表す自己回帰ツリー モデルとして説明できます。 このアルゴリズムでは、さまざまな数の過去のアイテムが、予測する現在の各アイテムに関連付けられます。 ARTXP という名前は、過去の不明な状態が複数ある場合に ART アルゴリズム (自己回帰ツリー法) が適用されることに由来しています。 ARTXP アルゴリズムの詳細については、「 [時系列分析の自動回帰ツリー モデル](https://go.microsoft.com/fwlink/?LinkId=45966)」を参照してください。  
  
 ARIMA アルゴリズムは、長期的な予測の精度を向上させるために SQL Server 2008 で Microsoft Time Series アルゴリズムに追加されたアルゴリズムです。 このアルゴリズムには、Box と Jenkins によって説明された自己回帰和分移動平均を計算するためのプロセスが実装されています。 ARIMA 法では、時間的に連続して行われる観測の依存関係を特定することが可能であり、モデルの一部としてランダム ショックを組み込むこともできます。 ARIMA 法はまた増殖性の周期もサポートします。 ARIMA アルゴリズムについて詳しく理解するには、Box と Jenkins による著書を読むことをお勧めします。このセクションは、Microsoft Time Series アルゴリズムに ARIMA 法がどのように実装されているかという点について、具体的に説明することを目的としています。  
  
 既定では、Microsoft Time Series アルゴリズムは、ARTXP と ARIMA の両方の方法を使用し、その結果を組み合わせて予測精度を向上させます。 特定の方法のみを使用する場合は、アルゴリズム パラメーターの設定によって、ARTXP のみまたは ARIMA のみを使用することも、アルゴリズムの結果を組み合わせる方法を制御することもできます。 ARTXP アルゴリズムではクロス予測がサポートされていますが、ARIMA アルゴリズムではサポートされていないことに注意してください。 したがって、クロス予測は、両方のアルゴリズムを組み合わせて使用する場合や、ARTXP のみを使用するようにモデルを構成する場合にのみ使用できます。  
  
## <a name="understanding-arima-difference-order"></a>ARIMA の差分の次数について  
 このセクションでは、ARIMA モデルを理解するための用語を紹介し、Microsoft Time Series アルゴリズムの *差分* の具体的な実装について説明します。 これらの用語の詳しい説明については、Box と Jenkins による著書を読むことをお勧めします。  
  
-   項は数式の要素です。 たとえば、多項式の項では、変数と定数を組み合わせることができます。  
  
-   Microsoft Time Series アルゴリズムに含まれる ARIMA 式は、 *自己回帰* と *移動平均* の両方の項を使用します。  
  
-   タイム シリーズ モデルには、 *定常* モデルと *非定常*モデルがあります。 *定常モデル* とは、周期性が存在する場合があっても平均レベルに復帰するモデルです。一方、 *非定常モデル* の場合は、平衡のポイントがなく、 *ショック*(外部変数) の影響による変動や変化が大きくなりやすいことが特徴です。  
  
-   *差分* の目的は、時系列を安定化させ、定常化させることです。  
  
-   *差分の次数* は、時系列用に値の差分が計算される回数を表します。  
  
 Microsoft Time Series アルゴリズムでは、時系列内の値を取得し、そのデータを一定のパターンに近づけようとする処理が行われます。 データ系列がまだ定常化されていない場合、アルゴリズムは差分の次数を使用します。 差分の次数が増加するたびに、タイム シリーズがより定常化します。  
  
 たとえば、タイム シリーズ (z1、z2、…、zn) がある相違点の 1 つの順序を使用して計算を実行して場合、ここに新しい系列 (y1, y2,..., yn-1) を入手するに*イ語 = zi + 1 zi*します。 差分の次数が 2 の場合、アルゴリズムが別の系列 (x1、x2、…、xn-2)、1 次方程式から派生した y 系列に基づいて生成されます。 正しい差分の量はデータによって異なります。 差分の次数 1 は、傾向が一定のモデルで非常によく使われます。差分の次数 2 は、時間と共に変化する傾向を示すことができます。  
  
 既定では、Microsoft Time Series アルゴリズムで使用される差分の次数は -1 です。つまり、最適な差分の次数がアルゴリズムによって自動的に検出されます。 通常、(差分が必要な場合の) 最適な値は 1 ですが、状況によってはアルゴリズムが最大 2 までこの値を増やします。  
  
 Microsoft Time Series アルゴリズムでは、自動回帰の値を使用して最適な ARIMA 差分の次数を決定します。 アルゴリズムは AR 値を調べ、AR 項の次数を示す非表示パラメーターである ARIMA_AR_ORDER を設定します。 非表示パラメーター ARIMA_AR_ORDER の有効値は -1 ～ 8 です。 既定値の -1 では、適切な差分次数がアルゴリズムによって自動的に選択されます。  
  
 ARIMA_AR_ORDER の値が 1 を超える場合、アルゴリズムは時系列に多項式の項を乗算します。 多項式の 1 つの項が 1 または 1 に近い値のルートに解決された場合、アルゴリズムはこの項を削除し、差分の次数を 1 増やして、モデルの安定性を維持しようとします。 差分の次数が既に最大の場合、項が削除され、差分の次数は変化しません。  
  
 たとえば場合、AR の値 = 2、AR 多項式のようになります。1-1.4B + .45B ^2 = (1-.9B) (1 - 0.5B)。 用語 (1-.9B) 約 0.9 のルートに注意してください。 アルゴリズムはこの項を多項式から除外しますが、差分の次数が既に 2 であるため、差分の次数を 1 つ上げることができません。  
  
 ここで、差分の次数を **強制的に** 変更するための唯一の方法が、サポートされていないパラメーターである ARIMA_DIFFERENCE_ORDER の使用であることは重要です。 この非表示のパラメーターは、時系列上でアルゴリズムが差分を実行する回数を制御し、カスタムのアルゴリズム パラメーターを入力して設定できます。 ただし、適切な値が見つかるまで何度か値を調整する準備があり、必要な計算を熟知している場合を除いて、この値を変更することはお勧めできません。 また、差分次数が増加するしきい値を制御できるようなメカニズムは、非表示パラメーターも含めて、現時点では存在しない点に注意してください。  
  
 最後に、上で説明した式は、周期性のヒントが提供されていない簡易なケースであることに注意してください。 周期性のヒントが提供されている場合は、1 つの周期性のヒントごとに個別の AR 多項式の項が方程式の左側に追加されたうえで、同じ方法を使用して、差分計算済みの系列を不安定にする可能性がある項が除外されます。  
  
## <a name="customizing-the-microsoft-time-series-algorithm"></a>Microsoft Time Series アルゴリズムのカスタマイズ  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムでは、結果として得られるマイニング モデルの動作、パフォーマンス、および精度に影響を与える次のパラメーターがサポートされています。  
  
> [!NOTE]  
>  Microsoft Time Series アルゴリズムは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで利用できます。ただし、いくつかの高度な機能 (時系列分析をカスタマイズするためのパラメーターなど) は、特定のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]だけでサポートされています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2012 の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)」を参照してください。  
  
### <a name="detection-of-seasonality"></a>周期性の検出  
 周期性の検出は、ARIMA と ARTXP の両方のアルゴリズムでサポートされています。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、高速フーリエ変換を使用してトレーニングの前に周期性を検出します。 ただし、アルゴリズム パラメーターを設定することで、周期性の検出や時系列分析の結果に影響を与えることができます。  
  
-   *AUTODETECT_SEASONALITY*の値を変更すると、生成される可能な時間単位の数に影響を与えることができます。  
  
-   *PERIODICITY_HINT*に 1 つまたは複数の値を設定して、データの予測されるサイクルに関する情報をアルゴリズムに提供すると、検出の精度を高めることができる場合があります。  
  
> [!NOTE]  
>  周期性のヒントは、ARTXP アルゴリズムと ARIMA アルゴリズムの両方に大きく影響します。 したがって、不適切なヒントを指定すると、結果に悪影響を与える可能性があります。  
  
### <a name="choosing-an-algorithm-and-specifying-the-blend-of-algorithms"></a>アルゴリズムの選択と、アルゴリズムの組み合わせの指定  
 既定では (または MIXED オプションをオンにした場合は)、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって両方のアルゴリズムが同じ重み付けで組み合わされます。 しかし、[!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] では、特定のアルゴリズムを指定したり、各アルゴリズムの結果における割合をカスタマイズすることもできます。そのためには、結果に短期と長期の予測に対する重み付けを行うパラメーターを設定します。 *FORECAST_METHOD* パラメーターは、既定では MIXED に設定されています。この場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は両方のアルゴリズムを使用して、各アルゴリズムの強みを最大限に活かすようにそれぞれの値に重みを付けます。  
  
-   アルゴリズムの選択を制御するには、 *FORECAST_METHOD* パラメーターを設定します。  
  
-   クロス予測を使用する場合は、ARTXP または MIXED オプションを使用する必要があります。ARIMA はクロス予測をサポートしていません。  
  
-   短期予測を重視する場合は、 *FORECAST_METHOD* を ARTXP に設定します。  
  
-   長期予測の精度を高める場合は、 *FORECAST_METHOD* を ARIMA に設定します。  
  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で ARIMA アルゴリズムと ARTXP アルゴリズムをどのように組み合わせるかをカスタマイズすることもできます。 *PREDICTION_SMOOTHING* パラメーターを設定することにより、組み合わせの開始点と変化率の両方を制御できます。  
  
-   *PREDICTION_SMOOTHING* を 0 に設定すると、モデルは ARTXP だけを使用します。  
  
-   *PREDICTION_SMOOTHING* を 1 に設定すると、モデルは ARIMA だけを使用します。  
  
-   *PREDICTION_SMOOTHING* を 0 と 1 の間の値に設定すると、ARTXP アルゴリズムが予測期間の "指数的に減少する関数" として重み付けされ、 ARIMA アルゴリズムが ARTXP の重みの 1 の補数として重み付けされます。 モデルでは、曲線を滑らかにするために正規化および安定化定数が使用されます。  
  
 一般に、予測するタイム スライスが 5 以下であれば、ほとんどの場合、ARTXP の方が適しています。 予測するタイム スライスが増えるにつれて、ARIMA を使用した方がより良い結果が得られるようになります。  
  
 次の図は、 *PREDICTION_SMOOTHING* を既定値の 0.5 に設定した場合にモデルで 2 つのアルゴリズムがどのように組み合わされるのかを示しています。 最初は ARIMA と ARTXP の重みが均等ですが、予測期間の値が増えるにつれて ARIMA の重みが増加しています。  
  
 ![タイム シリーズ アルゴリズムの組み合わせの既定曲線](../media/time-series-mixing-default.gif "タイム シリーズ アルゴリズムの組み合わせの既定曲線")  
  
 一方、次の図は、 *PREDICTION_SMOOTHING* を 0.2 に設定した場合のアルゴリズムの組み合わせを示しています。 期間 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]では、ARIMA の重みが 0.2、ARTXP の重みが 0.8 です。 その後、ARIMA の重みが指数関数的に増加し、ARTXP の重みも同じように減少します。  
  
 ![タイム シリーズ モデルの組み合わせの減衰曲線](../media/time-series-blending-curve.gif "タイム シリーズ モデルの組み合わせの減衰曲線")  
  
### <a name="setting-algorithm-parameters"></a>アルゴリズム パラメーターの設定  
 次の表は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムで使用できるパラメーターを示しています。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*AUTO_DETECT_PERIODICITY*|周期性を検出する [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] から 1 までの数値を指定します。 既定値は 0.6 です。<br /><br /> より [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]に近い値を設定すると、非常に周期的なデータのみを対象にして周期性が検出されます。<br /><br /> 1 に近い値を設定すると、多くのほぼ周期的なパターンの検出と、周期性のヒントの自動生成が行われます。<br /><br /> 注:多くの周期性のヒントを扱うは、モデルのトレーニング時間が大幅に長くより正確なモデルに可能性があります。|  
|*COMPLEXITY_PENALTY*|デシジョン ツリーの拡大を制御します。 既定値は 0.1 です。<br /><br /> 値を小さくすると、分割の可能性が増加します。 値を大きくすると、分割の可能性が減少します。<br /><br /> 注:このパラメーターは、一部のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] だけで使用できます。|  
|*FORECAST_METHOD*|分析および予測に使用するアルゴリズムを指定します。 指定できる値は、ARTXP、ARIMA、および MIXED です。 既定値は MIXED です。|  
|*HISTORIC_MODEL_COUNT*|作成する履歴モデルの数を指定します。 既定値は 1 です。<br /><br /> 注:このパラメーターは、一部のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] だけで使用できます。|  
|*HISTORICAL_MODEL_GAP*|2 つの連続した履歴モデル間のタイム ラグを指定します。 既定値は、10 です。 この値は、モデルによって定義される時間単位の数を表します。<br /><br /> たとえば、この値を g に設定すると、g、2*g、3\*g などの間隔でタイム スライスによって切り捨てられるデータに対して履歴モデルが作成されます。<br /><br /> 注:このパラメーターは、一部のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] だけで使用できます。|  
|*INSTABILITY_SENSITIVITY*|予測の分散が特定のしきい値を超えて ARTXP アルゴリズムの予測が中止されるポイントを制御します。 既定値は 1 です。<br /><br /> 注:このパラメーターは、ARIMA のみを使用するモデルには適用されません。<br /><br /> 既定値の 1 では、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]と同じ動作になります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、各予測の正規化された標準偏差を監視します。 この値がいずれかの予測のしきい値を超えると、タイム シリーズ アルゴリズムが NULL を返して予測処理が中止されます。<br /><br /> 値を [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] にすると、不安定性の検出が中止されます。 この場合は、偏差に関係なく予測を無制限に作成できます。<br /><br /> 注:このパラメーターは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise でのみ変更できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には既定値の 1 のみが使用されます。|  
|*MAXIMUM_SERIES_VALUE*|予測に使用する最大値を指定します。 このパラメーターを *MINIMUM_SERIES_VALUE*と共に使用すると、予測が所定の範囲内に制約されます。 たとえば、日次の予測販売数量が製品の在庫数を超えないように指定することができます。<br /><br /> 注:このパラメーターは、一部のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] だけで使用できます。|  
|*MINIMUM_SERIES_VALUE*|予測できる最小値を指定します。 このパラメーターを *MAXIMUM_SERIES_VALUE*と共に使用すると、予測が所定の範囲内に制約されます。 たとえば、販売数量の予測が負の値にならないように指定できます。<br /><br /> 注:このパラメーターは、一部のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] だけで使用できます。|  
|*MINIMUM_SUPPORT*|各タイム シリーズ ツリーで分割を生成するために必要なタイム スライスの最小数を指定します。 既定値は 10 です。|  
|*MISSING_VALUE_SUBSTITUTION*|履歴データのギャップを埋める方法を指定します。 既定では、データ内のギャップは許可されません。 データに複数のシリーズが含まれている場合は、シリーズの端を揃える必要もあります。 つまり、すべてのシリーズの開始点と終了点が同じである必要があります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] はこのパラメーターの値を、タイム シリーズ モデルで `PREDICTION JOIN` を実行する際に新しいデータのギャップを埋めるためにも使用します。 このパラメーターに指定できる値の一覧を次の表に示します。<br /><br /> None:既定値です。 トレーニング済みモデルの曲線に沿ってプロットされた値で不足値を置き換えます。<br /><br /> 先の：前のタイム スライスの値を繰り返します。<br /><br /> 平均:トレーニングに使用されたタイム スライスの移動平均を使用します。<br /><br /> 数値定数は:指定した数値を使用してすべての不足値を置き換えます。|  
|*PERIODICITY_HINT*|データの周期性に関して、アルゴリズムにヒントを提供します。 たとえば、売上が年ごとに異なり、シリーズの単位が月である場合、周期性は 12 です。 このパラメーターの形式は {n [, n]} です。ここで、n には正の値を指定します。<br /><br /> 角かっこ ([]) 内の n は省略可能で、必要なだけ繰り返すことができます。 たとえば、毎月提供されるデータに対して複数の周期性のヒントを指定して、年、四半期、および月のパターンを検出するには、「{12, 3, 1}」と入力します。 ただし、周期性はモデルの品質に大きな影響を与えるので注意してください。 指定したヒントが実際の周期性と異なると、結果が悪影響を受けることがあります。<br /><br /> 既定値は {1} です。<br /><br /> 注:中かっこが必要です。 また、このパラメーターは文字列データ型です。 したがって、このパラメーターをデータ マイニング拡張機能 (DMX) ステートメントの一部として入力する場合は、数字と中かっこを引用符で囲む必要があります。|  
|*PREDICTION_SMOOTHING*|予測を最適化するためにモデルを組み合わせる方法を指定します。 このパラメーターは、一部のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] だけで使用できます。 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] ～ 1 の任意の値を入力するか、次のいずれかの値を使用します。<br /><br /> [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] :予測に ARTXP のみを使用するように指定します。 少数の予測に最適化されます。<br /><br /> 0.5:(既定値)予測の両方のアルゴリズムを使用して、結果のブレンドを指定します。<br /><br /> 1:予測に ARIMA のみを使用するように指定します。 多数の予測に最適化されます。<br /><br /> <br /><br /> 注:使用して、 *FORECAST_METHOD*パラメーター トレーニングを制御します。|  
  
### <a name="modeling-flags"></a>ModelingFlags  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムでは、次のモデリング フラグがサポートされています。 モデリング フラグは、マイニング構造やマイニング モデルを作成するときに定義し、分析時に各列の値をどのように処理するかを指定します。 詳細については、「[モデリング フラグ &#40;データ マイニング&#41;](modeling-flags-data-mining.md)」を参照してください。  
  
|モデリング フラグ|説明|  
|-------------------|-----------------|  
|NOT NULL|列に NULL を含めることはできないことを示します。 モデルのトレーニング中に NULL が検出された場合はエラーが発生します。<br /><br /> マイニング構造列に適用されます。|  
|MODEL_EXISTENCE_ONLY|列が、次の 2 つの可能な状態を持つ列として扱われることを示します。Missing および Existing。 NULL は Missing 値になります。<br /><br /> マイニング モデル列に適用されます。|  
  
## <a name="requirements"></a>必要条件  
 タイム シリーズ モデルには、一意の値を含む Key Time 列、入力列、および少なくとも 1 つの予測可能列が必要です。  
  
### <a name="input-and-predictable-columns"></a>入力列と予測可能列  
 次の表のように、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムでは、特定の入力列のコンテンツの種類、予測可能列のコンテンツの種類、およびモデリング フラグがサポートされています。  
  
|[列]|コンテンツの種類|  
|------------|-------------------|  
|入力属性|Continuous、Key、Key Time、Table|  
|予測可能な属性|Continuous、Table|  
  
> [!NOTE]  
>  コンテンツの種類 Cyclical および Ordered はサポートされますが、アルゴリズムはこれらを不連続の値として扱い、特別な処理は行いません。  
  
## <a name="see-also"></a>参照  
 [Microsoft タイム シリーズ アルゴリズム](microsoft-time-series-algorithm.md)   
 [タイム シリーズ モデルのクエリ例](time-series-model-query-examples.md)   
 [タイム シリーズ モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
