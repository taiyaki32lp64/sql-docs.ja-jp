---
title: Analysis Services Multiidimensional | のグローバリゼーションのシナリオMicrosoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multiple language support [Analysis Services]
- languages [Analysis Services]
- SSAS, international considerations
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- SQL Server Analysis Services, international considerations
- Analysis Services, international considerations
ms.assetid: e8af85ff-ef33-4659-a003-bb34578eb2a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7b0d6e4d99c08556cefb31c33deb5238f33c636
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75225385"
---
# <a name="globalization-scenarios-for-analysis-services-multiidimensional"></a>Analysis Services 多次元のグローバル化のシナリオ
  
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、多言語のデータおよびメタデータを、表形式モデルと多次元データ モデルのどちらにも格納して操作できます。 データは Unicode (UTF-16) で格納され、Unicode エンコードの文字セットを使用します。 データ モデルに ANSI データを読み込むと、文字は Unicode の等価なコード ポイントを使用して格納されます。  
  
 Unicode をサポートしているということは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] が、Windows のクライアント/サーバー オペレーティング システムによってサポートされている任意の言語でデータを格納できることを意味します。Windows コンピューターで使用されるどの文字セットでも読み取り、書き込み、並べ替え、およびデータ比較が可能です。 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データを使用する BI クライアント アプリケーションは、その言語でモデル内にデータが存在すれば、ユーザーの選択した任意の言語でデータを表現できます。  
  
 言語のサポートは、ユーザーの立場に応じてさまざまな意味を持ちます。 Analysis Services での言語サポートに関連するいくつかの一般的な事項を以下で説明します。  
  
-   既に説明したとおり、データは、Windows クライアント オペレーティング システムにあるどの Unicode エンコードの文字セットでも格納できます。  
  
-   メタデータ (オブジェクトの名前、識別子、説明など) も、どの Unicode 言語およびスクリプトでも使用できます。 これは、ツールや環境が別の言語の場合にも当てはまります。 たとえば、スタック全体で英語およびラテン文字の照合順序を使用する開発環境で、名前にキリル文字を使用したオブジェクトをモデルに含めることができます。  
  
     多次元モデルの場合にのみ、キャプションと属性メンバーを翻訳で表現できます。 1 つまたは複数の翻訳を定義し、クライアントに返される翻訳をロケール識別子で決定できます。 詳細については、以下の[機能](#bkmk_features)を参照してください。  
  
-   
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] エンジン (msmdsrv) から返されるエラー、警告、および情報メッセージは、Office および Office 365 でサポートされる 43 の言語にローカライズされています。 特定の言語でメッセージを取得するために、特別な構成は必要ありません。 クライアント アプリケーションのロケールにより、どの言語で文字列が返されるかが決まります。  
  
-   構成ファイル (msmdsrv.ini) および AMO PowerShell は英語のみです。  
  
-   Analysis Services が実行される Windows サーバーに言語パックをインストールした場合、ログ ファイルには英語とローカライズされたメッセージが混在します。  
  
-   ドキュメントとツール ( [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 、 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]など) は、中国語 (簡体字)、中国語 (繁体字)、フランス語、ドイツ語、イタリア語、日本語、韓国語、ポルトガル語 (ブラジル)、ロシア語、およびスペイン語に翻訳されます。 言語固有のバージョンのツールを使用するには、言語固有のバージョンの SQL Server をインストールします (たとえば、SQL Server のドイツ語版をインストールし、ドイツ語で Management Studio を取得します)。または、 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]の対象言語でスタンドアロンのセットアップを実行します。  
  
 Analysis Services では、言語、照合順序、および翻訳をオブジェクト階層全体で独立して設定できます。  
  
 言語、照合順序、および翻訳を使用すると、たとえば、次のようなシナリオが可能になります。  
  
-   1 つのデータ モデルで複数の翻訳されたキャプションを提供することにより、ユーザーが選択した言語でフィールド名や値が表示されるようにできます。 カナダ、ベルギー、スイスなどのバイリンガル国で事業を行う企業では、クライアント/サーバー アプリケーション全体で複数の言語をサポートすることが標準的なコーディング要件になっています。 このシナリオは、翻訳と通貨換算によって可能になります。 詳細と参考資料のリンクは、この後の「 [機能](#bkmk_features) 」を参照してください。  
  
-   開発および運用環境を、地理的にさまざまな国に分散して設置できます。 ある国で開発したソリューションを別の国に配置するというシナリオは、ますます一般化しています。 1 つの言語で開発したソリューションを、別の言語パックを使用するサーバーに配置できるように準備するには、言語および照合順序のプロパティを設定する方法についての知識が不可欠です。 これらのプロパティを適切に設定すると、元のホスト システムから取得する継承された既定値をオーバーライドすることができます。 詳細については、この後の [言語および照合順序 &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md) 」をご覧ください。  
  
##  <a name="bkmk_features"></a>グローバル化多次元ソリューションを構築するための機能  
 
  [!INCLUDE[applies](../includes/applies-md.md)] 多次元データ モデルの場合のみ  
  
 クライアント レベルでは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] の多次元データを使用または操作するグローバル化されたアプリケーションで、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]の複数言語機能および複数カルチャ機能を使用できます。  
  
-   [翻訳 &#40;Analysis Services&#41;](translations-analysis-services.md)は、1つのオブジェクトに対して複数のキャプションを埋め込むために使用されます。翻訳された各文字列は、他の翻訳と共に存在できます。 
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用して、キューブ、メジャー、ディメンション、および属性のキャプション、説明、およびアカウントの種類に翻訳を定義できます。 翻訳が自動的に定義された [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトのデータおよびメタデータは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスへの接続時にロケール識別子を指定することによって取得できます。  
  
     この機能を使用する方法のレッスンは、 [チュートリアルの「](lesson-9-defining-perspectives-and-translations.md) レッスン 9 : パースペクティブと翻訳の定義 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 」をご覧ください。  
  
-   [Analysis Services&#41;&#40;通貨](currency-conversions-analysis-services.md)換算は、通貨データを含むメジャーを変換する特殊な MDX スクリプトによって行われます。 
  [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] のビジネス インテリジェンス ウィザードを使用すると、属性、メジャー グループのデータおよびメタデータの組み合わせを使用して通貨データを含むメジャーを換算する MDX スクリプトディメンションを生成できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[言語と照合順序 &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)|
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスに対して既定の言語と Windows 照合順序を指定します。 選択内容に応じて、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]によって管理されるデータおよびメタデータに影響が及びます。|  
|[翻訳 &#40;Analysis Services&#41;](translations-analysis-services.md)|
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースと、データベースに含まれるオブジェクトに対して翻訳を定義します。 このトピックでは、クライアント アプリケーションからの翻訳済みデータおよびメタデータの要求を [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] が解決する方法について説明しています。|  
|[通貨換算 &#40;Analysis Services&#41;](currency-conversions-analysis-services.md)|ビジネス インテリジェンス ウィザードを使用して通貨換算を定義します。|  
|[グローバリゼーションのヒントとベストプラクティス &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)|多言語データに関連した問題を回避するために役立ついくつかの設計およびコーディング手法について説明しています。|  
  
## <a name="see-also"></a>参照  
 [Windows アプリケーションの国際化](/windows/desktop/Intl/international-support)   
 [Microsoft のグローバリゼーションドキュメント](/globalization/)   
 [ロケールベースのアダプティブデザインを使用した Windows ストアアプリの作成](https://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [C# および XAML を使用したユニバーサル Windows アプリの開発](https://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
