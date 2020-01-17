---
title: XML ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsource.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 28e7a7395c02e44e52469992f3738f0d873e227f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62899945"
---
# <a name="xml-source"></a>XML ソース
  XML ソースは XML データ ファイルを読み取り、ソース出力の列にデータを設定します。  
  
 XML ファイルのデータには、多くの場合、階層リレーションシップが含まれます。 たとえば、XML データ ファイルはカタログおよびカタログ内のアイテムを表す場合があります。 データ フローにデータを入力できるようにするためには、XML データ ファイルの要素のリレーションシップを特定し、ファイル内部の各要素に対して出力を生成する必要があります。  
  
## <a name="schemas"></a>スキーマ  
 XML ソースは、スキーマを使用して XML データを解釈します。 XML ソースでは、XML スキーマ定義 (XSD) ファイルまたはインライン スキーマを使用して、XML データを表形式に変換できます。 **[XML ソース エディター]** ダイアログ ボックスを使用して XML ソースを構成する場合、ユーザー インターフェイスにより、指定した XML データ ファイルから XSD を生成できます。  
  
> [!NOTE]  
>  DTD はサポートされていません。  
  
 スキーマでは、単一の名前空間のみがサポートされます。スキーマ コレクションはサポートされません。  
  
> [!NOTE]  
>  XML ソースは、XML ファイルのデータを XSD に対して検証しません。  
  
## <a name="xml-source-editor"></a>[XML ソース エディター]  
 XML ファイルのデータには、多くの場合、階層リレーションシップが含まれます。 **[XML ソース エディター]** ダイアログ ボックスでは、指定したスキーマを使用して XML ソース出力を生成します。 XSD ファイルの指定、インライン スキーマの使用、または、指定した XML データ ファイルからの XSD の生成を行うことができます。 スキーマは、デザイン時に使用できる必要があります。  
  
 XML ソースは、XML ファイル内の別の要素が含まれる各要素の出力を作成し、XML データから表形式構造を生成します。 たとえば、XML データがカタログおよびカタログ内のアイテムを表している場合、XML ソースはカタログの出力、および、カタログに含まれる各種類のアイテムに対する出力を作成します。 各アイテムの出力には、そのアイテムの属性に対する出力列が含まれます。  
  
 出力内のデータの階層リレーションシップに関する情報を提供するため、XML ソースは、各子要素に対する親要素を識別する列を出力に追加します。 異なる種類のアイテムを持つカタログの場合、各アイテムは、アイテムが属するカタログを識別する列の値を持つことになります。  
  
 XML ソースは各要素に対して出力を作成しますが、すべての出力を使用する必要はありません。 使用しない出力を削除したり、下流コンポーネントに出力を連結しないようにできます。  
  
 また、XML ソースは、明確な名前を持つ出力名を生成します。 これらの名前は、長すぎて、出力を識別するには役に立たない場合があります。 出力名は、一意である限り変更できます。 また、出力列のデータ型や長さも変更できます。  
  
 各出力に対し、XML ソースはエラー出力を追加します。 既定では、エラー出力の列は、長さ 255 文字の Unicode 文字列データ型 (DT_WSTR) です。ただし、データ型と長さを変更して、エラー出力の列を構成できます。  
  
 XML データ ファイルに、XSD に存在しない要素が含まれる場合、これらの要素は無視され、出力が生成されません。 これに対し、XML データ ファイルに XSD で表されている要素がない場合、出力には NULL 値の列が含まれます。  
  
 データが XML データ ファイルから抽出されると、そのデータは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型に変換されます。 ただし、XML ソースは XML データを DT_TIME2 データ型または DT_DBTIMESTAMP2 データ型に変換することはできません。これらのデータ型をサポートしていないためです。 詳細については、「 [Integration Services Data Types](integration-services-data-types.md)」を参照してください。  
  
 XSD またはインライン スキーマで要素のデータ型を指定することもできますが、指定しない場合は **[XML ソース エディター]** ダイアログ ボックスで出力の要素が含まれる列に Unicode 文字列データ型 (DT_WSTR) が割り当てられ、その列の長さが 255 文字に設定されます。  
  
 スキーマで要素の最大長を指定する場合、出力列の長さはこの値に設定されます。 最大長が、要素の変換後の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型でサポートされている長さよりも大きい場合、データはデータ型の最大長に切り捨てられます。 たとえば、長さ 5,000 の文字列の場合、DT_WSTR データ型の最大長は 4,000 文字であるため、4,000 文字に切り捨てられます。同様に、バイト データは DT_BYTES データ型の最大長である 8,000 文字に切り捨てられます。 スキーマで最大長を指定しない場合、どのデータ型でも列の既定の長さは 255 に設定されます。 XML ソースのデータの切り捨ては、他のデータ フロー コンポーネントでの切り捨てと同様に処理されます。 詳細については、「 [データのエラー処理](error-handling-in-data.md)」を参照してください。  
  
 データ型と列の長さは変更できます。 詳細については、「 [Integration Services Data Types](integration-services-data-types.md)」を参照してください。  
  
## <a name="configuration-of-the-xml-source"></a>XML ソースの構成  
 XML ソースでは、3 つの異なるデータ アクセス モードがサポートされています。 XML データ ファイルのファイルの場所、ファイルの場所を含む変数、または XML データを含む変数を指定できます。  
  
 XML ソースには、パッケージの読み込み時にプロパティ式で更新できる、`XMLData` カスタム プロパティと `XMLSchemaDefinition` カスタム プロパティがあります。 詳細については、「[Integration Services (SSIS) の式](../expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../expressions/use-property-expressions-in-packages.md)」、および「[XML 入力元のカスタム プロパティ](xml-source-custom-properties.md)」を参照してください。  
  
 XML ソースでは、複数の標準出力と複数のエラー出力がサポートされています。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、XML ソースを構成するための **[XML ソース エディター]** ダイアログ ボックスがあります。 このダイアログ ボックスは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから利用できます。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[XML ソース エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[XML ソース エディター] &#40;[接続マネージャー] ページ&#41;](../xml-source-editor-connection-manager-page.md)  
  
-   [[XML ソース エディター] &#40;[列] ページ&#41;](../xml-source-editor-columns-page.md)  
  
-   [XML ソース エディター &#40;[エラー出力] ページ&#41;](../xml-source-editor-error-output-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [XML 入力元のカスタム プロパティ](xml-source-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [XML ソースを使用してデータを抽出する](xml-source.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 技術記事「 [XML ファイルを使用して、SSIS パッケージを構成する](https://www.sqlshack.com/using-xml-file-configure-ssis-package/)します。  
  
  
