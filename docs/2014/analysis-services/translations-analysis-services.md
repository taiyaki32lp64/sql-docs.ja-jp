---
title: 翻訳 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e97c9ba15aab664e9f0c77f9eb84152f75c3e3d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065882"
---
# <a name="translations-analysis-services"></a>翻訳 (Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]**  多次元のみ  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] の多次元データ モデルでは、キャプションに複数の翻訳を埋め込み、LCID に基づいてロケール固有の文字列を提供することができます。 データベース名、キューブ オブジェクト、およびデータベース ディメンション オブジェクトに翻訳を追加できます。  
  
 翻訳を定義するには、メタデータと翻訳されたキャプションをモデル内に作成します。しかし、クライアント アプリケーションでローカライズされた文字列をレンダリングするには、`Language` プロパティをオブジェクトに設定するか、または接続文字列で `Locale Identifier` パラメーターを渡す (たとえば、`LocaleIdentifier=1036` を設定するとフランス語の文字列が返されます) 必要があります。 同じオブジェクトでさまざまな言語の翻訳を同時にサポートする場合は、`Locale Identifier` を使用するように計画してください。 `Language` プロパティを設定する方法でも機能しますが、処理やクエリにも影響が出るため、意図しない結果になる恐れがあります。 `Locale Identifier` は翻訳した文字列を返すためにのみ使用されるため、それを設定する方が適切です。  
  
 翻訳は、ロケール識別子 (LCID)、オブジェクトの翻訳されたキャプション (たとえば、ディメンションまたは属性の名前)、およびオプションとして対象言語でのデータ値を提供する列へのバインドで構成されます。 複数の翻訳を保持できますが、特定の接続で使用できる翻訳は 1 つのみです。 モデルに埋め込むことができる翻訳の数に理論上の制限はありませんが、翻訳を 1 つ追加するごとにテストの複雑さが増すことと、すべての翻訳で同じ照合順序を共有する必要があることから、ソリューションを設計する際にはこれらの当然の制約に注意してください。  
  
> [!TIP]  
>  Excel、Management Studio、 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] などのクライアント アプリケーションを使用して、翻訳した文字列を返すことができます。 詳細については、「 [Globalization Tips and Best Practices &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) 」をご覧ください。  
  
## <a name="setting-up-a-model-to-support-translated-members"></a>翻訳されたメンバーをサポートするモデルの設定  
 多言語ソリューションで使用するデータ モデルには、単にラベル (フィールド名と説明) を翻訳する以上の処置が必要になります。 また、さまざまな言語スクリプトで表記したデータ値を提供する必要もあります。 多言語ソリューションを実現するには、個々の属性に外部データベース内の列をバインドし、データを取得する必要があります。  
  
 Adventure Works サンプル データベース (多次元かつリレーショナルなデータ ウェアハウス) は、翻訳機能の例を示しています。 このサンプル モデルには、翻訳されたキャプションと説明が含まれています。 サンプルのリレーショナル データ ウェアハウスに含まれる翻訳した値の列が、モデル内のローカライズされた属性メンバーを提供します。  
  
 モデルで使用できる翻訳されたデータ値を表示するには、次の手順を実行します。  
  
1.  デザイナーで、Adventure Works 多次元モデルを開きます。  
  
2.  ソリューション エクスプ ローラーでデータ ソース ビューを開くし、Adventure Works DW をダブルクリックして\<バージョン > .dsv します。  
  
3.  dimDate、dimProduct、dimProductCategory、または dimProductSubcateogry を検索します。 これらのすべてのディメンションには、月、曜日、製品名、カテゴリ名などの、翻訳されたメンバーの属性が含まれています。  
  
4.  任意のフィールドを右クリックし、 **[データの探索]** を選択します。 各メンバーの英語、スペイン語、およびフランス語の翻訳が表示されます。  
  
 日付、時刻、通貨の形式は、翻訳を通じては実装されません。 クライアントのロケールに基づいてカルチャに固有の形式を動的に提供するには、通貨変換ウィザードと `FormatString` プロパティを使用します。 「[通貨換算 (Analysis Services)](currency-conversions-analysis-services.md)」および「[FormatString 要素 (ASSL)](https://docs.microsoft.com/bi-reference/assl/properties/formatstring-element-assl)」をご覧ください。  
  
 [レッスン 9:パースペクティブと翻訳の定義](lesson-9-defining-perspectives-and-translations.md)Analysis Services チュートリアルでは手順については説明、作成すると、翻訳をテストします。  
  
## <a name="defining-translations"></a>翻訳の定義  
 翻訳を定義するには、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベース、ディメンション、またはキューブ オブジェクトの子として `Translation` オブジェクトを作成します。 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] を使用してソリューションを開き、翻訳を定義します。  
  
### <a name="add-translations-to-a-cube"></a>キューブに翻訳を追加する  
 翻訳は、キューブ、メジャー グループ、メジャー、キューブ ディメンション、パースペクティブ、KPI、アクション、名前付きセット、および計算されるメンバーに追加できます。  
  
1.  ソリューション エクスプローラーで、キューブ名をダブルクリックして、キューブ デザイナーを開きます。  
  
2.  **[翻訳]** タブをクリックします。翻訳をサポートするすべてのオブジェクトが、このページに表示されます。  
  
3.  各オブジェクトについて、対象言語 (内部で LCID に解決される)、キャプションの翻訳、および説明の翻訳を指定します。 Management Studio でサーバーの言語を設定したとしても、1 つの属性に対して翻訳のオーバーライドを追加したとしても、言語の一覧は Analysis Services 全体で一貫性が保たれます。  
  
     照合順序は変更できないことに注意してください。 キャプションの翻訳によって複数の言語をサポートしている場合でも、1 つのキューブは基本的に 1 つの照合順序を使用します (この後説明するとおり、ディメンションの属性は例外)。 照合順序を共有している場合に言語が正しく並べ替えられない場合は、照合順序の要件に対応するためにキューブのコピーを作成する必要があるかもしれません。  
  
4.  プロジェクトをビルドし、配置します。  
  
5.  Excel などのクライアント アプリケーションを使用してデータベースに接続し、ロケール識別子を使用するように接続文字列を変更します。 詳細については、「 [グローバリゼーションのヒントとベスト プラクティス (Analysis Services)](globalization-tips-and-best-practices-analysis-services.md) 」をご覧ください。  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>ディメンションおよび属性に翻訳を追加する  
 翻訳は、データベース ディメンション、属性、階層、および階層内のレベルに追加できます。  
  
 翻訳されたキャプションは、キーボードまたはコピー/貼り付けを使用して手動でモデルに追加しますが、ディメンションの属性メンバーについては、翻訳された値を外部データベースから取得できます。 具体的には、属性の `CaptionColumn` プロパティをデータ ソース ビューの列にバインドできます。  
  
 照合順序の設定は、属性レベルでオーバーライドできます。たとえば、特定の属性について文字幅の区別で調整したり、バイナリ並べ替えを使用したりできます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]では、データ バインドが定義されている場所で照合順序が公開されます。 ディメンション属性の翻訳は DSV 内の別のソース列にバインドするので、ソース列で使用する照合順序を指定できるように、照合順序の設定が可能になっています。 リレーショナル データベース内の列の照合順序について詳しくは、「 [Set or Change the Column Collation](../relational-databases/collations/set-or-change-the-column-collation.md) 」を参照してください。  
  
1.  ソリューション エクスプローラーで、ディメンション名をダブルクリックして、ディメンション デザイナーを開きます。  
  
2.  **[翻訳]** タブをクリックします。翻訳をサポートするすべてのディメンション オブジェクトが、このページに表示されます。  
  
     各オブジェクトについて、対象言語 (LCID に解決される)、キャプションの翻訳、および説明の翻訳を指定します。 Management Studio でサーバーの言語を設定したとしても、1 つの属性に対して翻訳のオーバーライドを追加したとしても、言語の一覧は Analysis Services 全体で一貫性が保たれます。  
  
3.  翻訳した値を提供する列に属性をバインドするには、次の手順を実行します。  
  
    1.  ディメンション デザイナーの **[翻訳]** タブを表示した状態のまま、新しい翻訳を追加します。 言語を選択します。 ページに新しい列が表示され、翻訳した値を入力できます。  
  
    2.  属性のいずれかに隣接する空のセルにカーソルを置きます。 属性をキーにすることはできませんが、その他のすべての属性は有効な選択肢です。 ドットが表示された小さいボタンが表示されているはずです。 そのボタンをクリックして、 **[属性データの翻訳]** ダイアログ ボックスを開きます。  
  
    3.  キャプションの翻訳を入力します。 これは、対象言語のデータのラベルとして使用されます。たとえば、ピボット テーブルのフィールド一覧のフィールド名です。  
  
    4.  属性メンバーの翻訳済みの値を提供するソース列を選択します。 ディメンションにバインドされたテーブルまたはクエリ内の既存の列のみ使用できます。 列が存在しない場合は、データ ソース ビュー、ディメンション、およびキューブを変更して列を選択する必要があります。  
  
    5.  該当する場合は、照合順序と並べ替えの順序を選択します。  
  
4.  プロジェクトをビルドし、配置します。  
  
5.  Excel などのクライアント アプリケーションを使用してデータベースに接続し、ロケール識別子を使用するように接続文字列を変更します。 詳細については、「[グローバリゼーションのヒントとベスト プラクティス (Analysis Services)](globalization-tips-and-best-practices-analysis-services.md)」をご覧ください。  
  
### <a name="add-a-translation-of-the-database-name"></a>データベース名の翻訳を追加する  
 データベース レベルでは、データベースの名前と説明に翻訳を追加できます。 翻訳されたデータベース名は、言語の LCID を指定するクライアント接続に表示されますが、ツールによっては表示されないことがあります。 たとえば、Management Studio でデータベースを表示する場合は、接続のロケール識別子を指定しても翻訳済みの名前は表示されません。 Management Studio で Analysis Services の接続に使用される API は、`Language` プロパティを読み取りません。  
  
1.  ソリューション エクスプローラーで、プロジェクト名を右クリックし、 **[データベースの編集]** を選択して、データベース デザイナーを開きます。  
  
2.  [翻訳] 内で、対象言語 (LCID に解決される)、キャプションの翻訳、および説明の翻訳を指定します。 Management Studio でサーバーの言語を設定したとしても、1 つの属性に対して翻訳のオーバーライドを追加したとしても、言語の一覧は Analysis Services 全体で一貫性が保たれます。  
  
3.  データベースの [プロパティ] ページで、翻訳に対して指定したのと同じ LCID を `Language` に設定します。 必要であれば、`Collation` にも値を設定します (既定値が意味をなさなくなった場合)。  
  
4.  データベースをビルドして配置します。  
  
## <a name="resolving-translations"></a>翻訳の解決  
 クライアント アプリケーションがロケール識別子を要求した場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトのデータおよびメタデータを最も近い一致する LCID に解決しようとします。 クライアント アプリケーションで既定の言語が指定されていない場合、ニュートラルなロケール識別子 (0) が指定されている場合、または既定の言語識別子 (1024) が処理される場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] はインスタンスの既定の言語を使用して [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトのデータおよびメタデータを返します。  
  
## <a name="see-also"></a>参照  
 [Analysis Services 多次元のグローバリゼーションのシナリオ](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [言語および照合順序 (Analysis Services)](languages-and-collations-analysis-services.md)   
 [列の照合順序の設定または変更](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [グローバリゼーションのヒントとベスト プラクティス (Analysis Services)](globalization-tips-and-best-practices-analysis-services.md)  
  
  
