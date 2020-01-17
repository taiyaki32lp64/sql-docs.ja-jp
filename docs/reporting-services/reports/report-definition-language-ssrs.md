---
title: レポート定義言語 (SSRS) | Microsoft Docs
ms.date: 01/24/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Reporting Services, RDL
- Reporting Services, RDL
- RDL [Reporting Services], about Report Definition Language
- SSRS, RDL
- Report Definition Language, about Report Definition Language
- Report Definition Language
- RDL [Reporting Services]
- reports [Reporting Services], definitions
ms.assetid: b18b025e-f4bd-4744-8f86-0ac9fb967548
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25a6872cd74faae521f9687d20d54541ef1798a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579998"
---
# <a name="report-definition-language-ssrs"></a>レポート定義言語 (SSRS)
  レポート定義言語 (RDL) は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート定義の XML 表現です。 レポート定義には、レポートのデータ取得とレイアウトの情報が含まれます。 RDL は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]用に作成された XML 文法に準拠する XML 要素で構成されます。 レポート定義ファイル内のコード アセンブリにアクセスすることによって、レポート アイテムの値、スタイル、および書式設定を制御するために独自のカスタム機能を追加できます。  
  
 RDL は、レポート定義の交換を可能にする共通スキーマを定義することで、商用レポート製品の相互運用性を促進します。 XML で使用できるプロトコルまたはプログラム インターフェイスは RDL で使用できます。 RDL は次のように定義できます。  
  
-   レポート定義の XML スキーマ  
  
-   ビジネスおよびサード パーティ用の交換形式  
  
-   追加の名前空間とカスタム要素をサポートする拡張可能で開放型のスキーマ  
  
##  <a name="bkmk_RDL_Specifications"></a> RDL の仕様  
 特定のスキーマ バージョンの仕様をダウンロードするには、「 [レポート定義言語の仕様](https://go.microsoft.com/fwlink/?linkid=116865)」を参照してください。  
  
##  <a name="bkmk_RDL_XML_Schema_Definition"></a> RDL XML スキーマ定義  
 A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のレポート定義言語 (RDL) ファイルは、XML スキーマ定義 (XSD) ファイルを使用して検証されます。 スキーマでは、.rdl ファイル内で RDL 要素を使用できる場所に関する規則を定義しています。 要素には、データ型とカーディナリティ (要素を使用できる回数) が含まれます。 要素には、単純なものも複雑なものもあります。 単純な要素には、子要素または属性がありません。 複雑な要素には、子要素のほか、必要に応じて属性を指定できます。  
  
 たとえば、スキーマには、 **ReportParametersType**複合型の RDL 要素 **ReportParameters**が含まれます。 通常、要素の複合型の名前は、要素名の後に **Type**という単語が続きます。 **ReportParameters** 要素は、 **Report** 要素 (複合型) に含めることができ、 **ReportParameter** 要素を含むことができます。 **ReportParameterType** は単純型で、 **Boolean**、 **DateTime**、 **Integer**、 **Float**、または **String**のいずれかの値のみを指定できます。 XML スキーマ データ型の詳細については、「 [XML スキーマ第 2 部: データ型 (第 2 版)](https://go.microsoft.com/fwlink/?linkid=4871)」を参照してください。  
  
 RDL XSD は、ReportDefinition.xsd ファイルから入手できます。このファイルは製品 CD-ROM の Extras フォルダーにあります。 また、次の URL からレポート サーバーで入手することもできます: `https://servername/reportserver/reportdefinition.xsd`  
  
##  <a name="bkmk_Creating_RDL"></a> RDL の作成  
 RDL は開放型で拡張可能な性質を持つため、XML スキーマに基づき RDL を生成するさまざまなツールとアプリケーションを作成できます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、RDL ファイルを作成するための複数のツールが用意されています。 詳細については、「 [Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)」を参照してください。  
  
 アプリケーションから RDL を生成する最も簡単な方法の 1 つは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 名前空間と <xref:System.Xml> 名前空間の <xref:System.Linq> クラスを使用することです。 特に、 **XmlTextWriter** クラスは RDL の記述に使用できます。 **XmlTextWriter**を使用すると、任意の [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] アプリケーションで完全なレポート定義を最初から最後まで生成できます。 開発者は、カスタム プロパティを持つカスタム レポート アイテムを追加して、RDL を拡張することもできます。 **XmlTextWriter** クラスおよび <xref:System.Xml> 名前空間の詳細については、『[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 開発者ガイド』を参照してください。 言語統合クエリ (LINQ) の詳細については、MSDN で「LINQ to XML」を検索してください。  
  
 レポート定義の標準的なファイル拡張子は .rdl です。 .rdlc という拡張子のクライアント レポート定義ファイルを作成することもできます。 どちらの拡張子の場合も、MIME の種類は text/xml です。 レポートの詳細については、「[Reporting Services レポート &#40;SSRS&#41;](../../reporting-services/reports/reporting-services-reports-ssrs.md)」を参照してください。  
  
##  <a name="bkmk_RDL_Types"></a> RDL 型  
 次の表に、RDL 要素および属性で使用される型を示します。  
  
|Type|[説明]|  
|----------|-----------------|  
|**Binary**|base-64 でエンコードされたバイナリ値を持つプロパティです。|  
|**Boolean**|オブジェクトの値として **true** または **false** を持つプロパティです。 特に指定しない限り、オプションのブール値オブジェクトを省略した場合の値は **False**です。|  
|**Date**|ISO8601 の日付形式 (YYYY-MM-DD[THH:MM[:SS[.S]]]) で指定した、完全指定の日付または datetime の値を持つプロパティです。|  
|**Enum**|文字列テキストの値を持つプロパティです。値は指定値の一覧のうちのいずれかである必要があります。|  
|**Float**|浮動小数点数値を持つプロパティです。 オプションの 10 進区切り記号として、ピリオド (.) が使用されます。|  
|**Integer**|整数 (int32) 値を持つプロパティです。|  
|**言語**|米国英語を表す "en-us" などの言語文化コードを含むテキスト値を持つプロパティです。 値は、特定の言語か、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]で既定の言語が定義されたニュートラル言語である必要があります。|  
|**[名前]**|文字列テキストの値を持つプロパティです。 名前は、アイテムの名前空間内で一意である必要があります。 指定しない場合、名前を持つ最も内側のオブジェクトが、アイテムの名前空間となります。|  
|**NormalizedString**|正規化された文字列テキストの値を持つプロパティです。|  
|**[サイズ]**|サイズ要素には、数値が含まれている必要があります (小数点としてピリオドを使用)。 数値の後には、cm、mm、in、pt、pc など、CSS 長さ単位の指定子を入力する必要があります。 数値と指定子の間のスペースは省略可能です。 サイズ指定子の詳細については、「[CSS Values and Units Reference (CSS の値と単位のリファレンス)](/previous-versions//ms537660(v=vs.85))」を参照してください。<br /><br /> RDL では、 **Size** の最大値は 160 インチで、 最小サイズは 0 インチです。|  
|**String**|文字列テキストの値を持つプロパティです。|  
|**UnsignedInt**|符号なし整数 (uint32) 値を持つプロパティです。|  
|**Variant**|任意の単純な XML 型を持つプロパティです。|  
  
##  <a name="bkmk_RDL_Data_Types"></a> RDL データ型  
 DataType 列挙は、RDL で属性、式、またはパラメーターのデータ型を定義します。 次の表に、共通言語ランタイム (CLR) データ型と RDL データ型の対応を示します。  
  
|**CLR 型**|**対応するデータ型**|  
|-----------------------|---------------------------------|  
|Boolean|Boolean|  
|DateTime、DateTimeOffset|DateTime|  
|Int16、Int32、UInt16、Byte、SByte|Integer|  
|Single、Double|float|  
|String、Char、GUID、Timespan|String|  
  
## <a name="see-also"></a>参照  
 [レポート定義スキーマのバージョンを確認する &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)   
 [レポートでのカスタム アセンブリの使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [カスタム レポート アイテム](../../reporting-services/custom-report-items/custom-report-items.md)  
  
  
