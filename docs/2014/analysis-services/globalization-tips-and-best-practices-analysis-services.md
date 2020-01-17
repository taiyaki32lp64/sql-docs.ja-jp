---
title: グローバリゼーションのヒントとベストプラクティス (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- translations [Analysis Services], client applications
- date comparisons
- day-of-week comparisons [Analysis Services]
- time [Analysis Services]
- month comparisons [Analysis Services]
ms.assetid: 71a8c438-1370-4c69-961e-d067ee4e47c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d8d98d2a45ff50c60a37ee04e576567db7f96e26
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874415"
---
# <a name="globalization-tips-and-best-practices-analysis-services"></a>グローバリゼーションのヒントとベスト プラクティス (Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]**  多次元のみ  
  
 以下のヒントとガイドラインは、ビジネス インテリジェンス ソリューションの移植性を増すのに役立つと同時に、言語と照合順序の設定に直接関連するエラーを回避できます。  
  
-   [スタック全体における類似した照合順序の使用](#bkmk_sameColl)  
  
-   [照合順序に関する一般的な推奨事項](#bkmk_recos)  
  
-   [オブジェクト ID の大文字小文字の区別](#bkmk_objid)  
  
-   [Excel と SQL Server Profiler を使用したロケールのテスト](#bkmk_test)  
  
-   [翻訳が含まれるソリューションにおける MDX クエリの作成](#bkmk_mdx)  
  
-   [日付値と時刻値が含まれる MDX クエリの作成](#bkmk_datetime)  
  
##  <a name="bkmk_sameColl"></a> スタック全体における類似した照合順序の使用  
 可能な場合には、データベース エンジンに対して使用する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 内の照合順序設定を、文字幅の区別、大文字小文字の区別、アクセントの区別ができるだけ同じ、類似した設定にしてください。  
  
 各サービスには独自の照合順序設定があり、データベース エンジンは既定で SQL_Latin1_General_CP1_CI_AS に、Analysis Services は Latin1_General_AS にそれぞれ設定されています。 これらの既定値は、大文字小文字、文字幅、アクセントの区別に関しては互換性があります。 いずれかの照合順序の設定を変える場合、照合順序プロパティが基本的な仕方で異なると、問題が生じる恐れがあります。  
  
 照合順序設定が機能的に同じである場合でも、文字列内のいずれかの場所にある空白がサービスごとに異なって解釈されるという特殊なケースに陥ることがあります。  
  
 空白文字は「特殊ケース」です。Unicode では、単一バイト (SBCS) とダブル バイト文字セット (DBCS) のどちらでも表せるからです。 リレーショナル エンジンでは、スペース (1 つは SBCS、もう 1 つは DBCS) で区切られた 2 つの複合文字列は同じであると見なされます。 Analysis Services では、処理中、同じ 2 つの複合文字列は同一ではなく、2 つ目のインスタンスは重複としてフラグが立てられます。  
  
 詳細および提案されている回避策については、「 [Unicode 文字列にブランクがある場合、照合順序に基づいて処理結果が異なる](https://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx)」をご覧ください。  
  
##  <a name="bkmk_recos"></a> 照合順序に関する一般的な推奨事項  
 Analysis Services は、常にすべての使用可能な言語および照合順序の一覧を提示します。ユーザーが選択した言語に基づいて照合順序がフィルター処理されることはありません。 必ず、実行可能な組み合わせを選択してください。  
  
 一般的に使用される照合順序には、次の一覧にあるものが含まれます。  
  
 この一覧は、その他の選択肢を除外する明確な推奨事項ではなく、詳しい調査の開始点と見なしてください。 この一覧で特に推奨されていない照合順序が、対象となるデータに最適なものであることもあります。 データ値が適切に並べ替えられ、適切に比較されるかどうか確認する唯一の方法は、徹底的にテストすることです。 照合順序をテストする際には、いつものように、処理とクエリの両方のワークロードを実行してください。  
  
-   Latin1_General_100_AS は、 [ISO 基本ラテン アルファベット](http://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet)の 26 文字を使用するアプリケーションによく使用されます。  
  
-   スカンジナビア語の文字 (ø など) 含む北ヨーロッパ言語では、Finnish_Swedish_100 を使用できます。  
  
-   ロシア語などの東ヨーロッパ言語では、多くの場合、Cyrillic_General_100 を使用します。  
  
-   中国語の言語および照合順序は地域によって異なりますが、一般に簡体中国語または繁体中国語のいずれかです。  
  
     中華人民共和国およびシンガポールでは、Microsoft サポートの観察によると、ピンイン付きの簡体字国語の並べ替え順序がよく使用されています。 推奨される照合順序は、Chinese_PRC (SQL Server 2000 の場合)、Chinese_PRC_90 (SQL Server 2005 の場合)、または Chinese_Simplified_Pinyin_100 (SQL Server 2008 以降の場合) です。  
  
     台湾では、繁体字中国語のほうが一般的で、お勧めする並べ替え順序は画数に基づく次のものです。Chinese_Taiwan_Stroke (SQL Server 2000 の場合)、Chinese_Taiwan_Stroke_90 (SQL Server 2005 の場合)、Chinese_Traditional_Stroke_Count_100 (SQL Server 2008 以降の場合)。  
  
     その他の地域 (香港やマカオなど) でも、繁体字中国語が使用されます。 香港では、照合順序に Chinese_Hong_Kong_Stroke_90 (SQL Server 2005 上) が使用されることも珍しくありません。 マカオでは、Chinese_Traditional_Stroke_Count_100 (SQL Server 2008 以降) が非常に頻繁に使用されています。  
  
-   日本語では、最もよく使用される照合順序は Japanese_CI_AS です。 [JIS2004](http://en.wikipedia.org/wiki/JIS_X_0213)をサポートするシステムでは、Japanese_XJIS_100 が使用されます。 Japanese_BIN2 は、通常、Windows 以外のプラットフォームからのデータ、または SQL Server リレーショナル データベース エンジン以外のデータ ソースからのデータを移行するプロジェクトで使用されるのが一般的です。  
  
     Japanese_Bushu_Kakusu_100 が、Analysis Services のワークロードを実行するサーバーで使用されることはまれです。  
  
-   韓国では、Korean_100 が推奨されます。 Korean_Wansung_Unicode も使用可能なリストにまだ含まれていますが、これは非推奨になりました。  
  
##  <a name="bkmk_objid"></a> オブジェクト ID の大文字小文字の区別  
 SQL Server 2012 SP2 以降、オブジェクト ID の大文字小文字は照合順序に関係なく区別されるようになりましたが、言語ごとに次のように動作が異なります。  
  
|言語セット|大文字と小文字の区別|  
|---------------------|----------------------|  
|**基本的なラテン アルファベット**|ラテン文字 (任意の 26 個の英語大文字小文字) で表されるオブジェクト ID は、照合順序に関係なく、大文字小文字の区別なしで処理されます。 たとえば、次のオブジェクト ID は同じであると見なされます。54321**abcdef**、54321**ABCDEF**、54321**AbCdEf**。 Analysis Services はこうした文字列内の文字を内部的には大文字として処理し、言語に関係なく単純なバイト比較を実行します。<br /><br /> 26 文字だけが影響を受けることに注意してください。 言語が西ヨーロッパ言語で、スカンジナビア語の文字を使用している場合、追加の文字は大文字に変換されません。|  
|**キリル語、ギリシャ語、コプト語、アルメニア語**|キリル語など、ラテン語以外の大文字小文字の区別がある言語のオブジェクト ID では、常に大文字小文字が区別されます。 たとえば、Измерение と измерение の違いは最初の文字の大文字小文字だけですが、この場合も 2 つの異なる値であると見なされます。|  
  
 **オブジェクト ID の大文字小文字の区別の影響**  
  
 この表で説明されている大文字小文字の動作に関連するのは、オブジェクト名ではなく、オブジェクト ID のみです。 ご使用のソリューションの動作方法に変化がある場合 (比較の前後、つまり SQL Server 2012 SP2 以降のインストール後)、処理上の問題が生じる可能性が高くなります。 クエリは、オブジェクト ID によって影響を受けません。 (DAX と MDX の) どちらのクエリ言語の場合であっても、数式エンジンは (ID ではなく) オブジェクト名を使用します。  
  
> [!NOTE]  
>  大文字小文字の区別に関連するコードの変更は、一部のアプリケーションの互換性に影響を与える変更です。 詳細については、「 [SQL Server 2014 の Analysis Services 機能における重大な変更」を](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)参照してください。  
  
##  <a name="bkmk_test"></a> Excel、SQL Server Profiler、SQL Server Management Studio を使用したロケール テスト  
 翻訳をテストする場合、接続で対象の翻訳の LCID を指定する必要があります。 「 [SSAS から Excel への各種言語の取得](http://extremeexperts.com/sql/Tips/ExcelDiffLocale.aspx)」に記されているように、Excel を使用して翻訳をテストできます。  
  
 このためには、.odc ファイルを手動で編集し、ロケール ID 接続文字列プロパティを含めます。 これを、Adventure Works サンプル多次元データベースを使用して試してください。  
  
-   既存の .odc ファイルを探します。 Adventure Works 多次元用のファイルが見つかったら、右クリックしてメモ帳で開きます。  
  
-   接続文字列に `Locale Identifier=1036` を追加します。 ファイルを保存して閉じます。  
  
-   Excel で、 **[データ]**  |  **[既存の接続]** の順に開きます。 リストをフィルター処理し、対象のコンピューター上の接続ファイルのみにします。 Adventure Works 用の接続を検索します (名前を注意深く探します。複数ある場合もあります)。 接続を開きます。  
  
     Adventure Works サンプル データベースのフランス語翻訳が表示されるはずです。  
  
     フランス語翻訳を![使用した Excel ピボットテーブル]と(media/ssas-localetest-excel.png "フランス語翻訳")  
  
 その後、SQL Server Profiler を使用してロケールを確認できます。 `Session Initialize` イベントをクリックし、下に表示されるテキスト領域のプロパティ リストを探して `<localeidentifier>1036</localeidentifier>`を見つけます。  
  
 Management Studio で、サーバー接続のロケール ID を指定できます。  
  
-   オブジェクト エクスプローラーで、 **[接続]**  |  **[Analysis Services]**  |  **[オプション]** の順に移動し、 **[追加の接続パラメーター]** タブをクリックします。  
  
-   `Local Identifier=1036` と入力し、 **[接続]** をクリックします。  
  
-   Adventure Works データベースに対して、MDX クエリを実行します。 クエリ結果は、フランス語翻訳になるはずです。  
  
     Ssms での![フランス語翻訳による mdx クエリ](media/ssas-localetest-ssms.png "Ssms でのフランス語翻訳を使用した mdx クエリ")  
  
##  <a name="bkmk_mdx"></a> 翻訳が含まれるソリューションにおける MDX クエリの作成  
 翻訳では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトの名前の表示情報が提供されますが、同じオブジェクトの識別子は翻訳されません。 可能であれば必ず、翻訳されたキャプションと名前ではなく、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトの識別子とキーを使用してください。 たとえば、多次元式 (MDX) ステートメントおよびスクリプトのメンバー名ではなく、メンバー キーを使用して、複数の言語間での移植性を確保します。  
  
> [!NOTE]  
>  表形式のオブジェクト名は、照合順序に関係なく、いつでも大文字小文字の区別がないことに注意してください。 一方、多次元オブジェクト名の場合、照合の大文字小文字の区別の設定に従います。 多次元オブジェクト名のみが大文字小文字の区別があるため、多次元オブジェクトを参照するすべての MDX クエリの大文字小文字が正しいことを必ずご確認ください。  
  
##  <a name="bkmk_datetime"></a> 日付値と時刻値が含まれる MDX クエリの作成  
 日付と時刻を MDX に基づくクエリとすることで、異なる言語間での移植性を向上させるための提案を以下に記します。  
  
1.  **比較と操作に対する数値部分の使用**  
  
     月と曜日の比較および操作を実行する場合は、文字列相当値ではなく、日付と時刻の数値部分を使用します (たとえば、MonthName ではなく MonthNumberofYear を使用します)。 数値は、言語翻訳の違いによってほとんど影響を受けません。  
  
2.  **結果セットにおける文字列相当値の使用**  
  
     エンド ユーザーに表示する結果セットを作成する際、(MonthName などの) 文字列を使用し、提供した翻訳を複数言語の読者が利用できるようにすることを考慮してください。  
  
3.  **ユニバーサルの日時情報に対する ISO 日付形式の使用**  
  
     1 人の [Analysis Services の専門家](http://geekswithblogs.net/darrengosbell/Default.aspx) は次のように勧めています。「SQL または MDX でクエリに渡す日付文字列には ISO 日付形式 yyyy-mm-dd を必ず使います。この形式にはあいまいさがなく、クライアントまたはサーバーの地域設定に関係なく作動するためです。 サーバーでは、あいまいな日付形式を解析する場合にこの地域設定に従う必要があるとは思いますが、どのような場合であってもそれが最善の選択肢であると考える必要はないとも思います」。  
  
4.  `Use the Format function to enforce a specific format, regardless of regional language settings`  
  
     フォーラム投稿から借用している以下の MDX クエリは、基礎となる地域設定とは無関係に、特定の形式で日付を返すための Format の使用法を示しています。  
  
     元々の投稿内容については、「 [SSAS 2012 によって生成される無効な日付 (Network Steve でのフォーラム投稿)](http://www.networksteve.com/forum/topic.php/SSAS_2012_generates_invalid_dates/?TopicId=40504&Posts=2) 」をご覧ください。  
  
    ```  
    WITH MEMBER [LinkTimeAdd11Date_Manual] as Format(dateadd("d",15,"2014-12-11"), "mm/dd/yyyy")  
    member [LinkTimeAdd15Date_Manual] as Format(dateadd("d",11,"2014-12-13"), "mm/dd/yyyy")  
    SELECT  
    { [LinkTimeAdd11Date_Manual]  
    ,[LinkTimeAdd15Date_Manual]  
    }  
    ON COLUMNS   
    FROM [Adventure Works]  
  
    ```  
  
## <a name="see-also"></a>参照  
 [Analysis Services Multiidimensional  のグローバリゼーションのシナリオ](globalization-scenarios-for-analysis-services-multiidimensional.md)  
 [国際化に対応した Transact-SQL ステートメントの記述](../relational-databases/collations/write-international-transact-sql-statements.md)  
  
  
