---
title: XML ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.xmlsource.f1
- sql13.dts.designer.xmlsourceadapter.connectionmanager.f1
- sql13.dts.designer.xmlsourceadapter.columns.f1
- sql13.dts.designer.xmlsourceadapter.erroroutput.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d766d6a36dbe8f91f2c2fd42433093b298935b48
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290840"
---
# <a name="xml-source"></a>XML ソース

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
 データが XML データ ファイルから抽出されると、そのデータは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型に変換されます。 ただし、XML ソースは XML データを DT_TIME2 データ型または DT_DBTIMESTAMP2 データ型に変換することはできません。これらのデータ型をサポートしていないためです。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 XSD またはインライン スキーマで要素のデータ型を指定することもできますが、指定しない場合は **[XML ソース エディター]** ダイアログ ボックスで出力の要素が含まれる列に Unicode 文字列データ型 (DT_WSTR) が割り当てられ、その列の長さが 255 文字に設定されます。  
  
 スキーマで要素の最大長を指定する場合、出力列の長さはこの値に設定されます。 最大長が、要素の変換後の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型でサポートされている長さよりも大きい場合、データはデータ型の最大長に切り捨てられます。 たとえば、長さ 5,000 の文字列の場合、DT_WSTR データ型の最大長は 4,000 文字であるため、4,000 文字に切り捨てられます。同様に、バイト データは DT_BYTES データ型の最大長である 8,000 文字に切り捨てられます。 スキーマで最大長を指定しない場合、どのデータ型でも列の既定の長さは 255 に設定されます。 XML ソースのデータの切り捨ては、他のデータ フロー コンポーネントでの切り捨てと同様に処理されます。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。  
  
 データ型と列の長さは変更できます。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="configuration-of-the-xml-source"></a>XML ソースの構成  
 XML ソースでは、3 つの異なるデータ アクセス モードがサポートされています。 XML データ ファイルのファイルの場所、ファイルの場所を含む変数、または XML データを含む変数を指定できます。  
  
 XML ソースには、パッケージの読み込み時にプロパティ式で更新できる、**XMLData** カスタム プロパティと **XMLSchemaDefinition** カスタム プロパティがあります。 詳細については、「[Integration Services (SSIS) の式](../../integration-services/expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../integration-services/expressions/use-property-expressions-in-packages.md)」、および「[XML 入力元のカスタム プロパティ](../../integration-services/data-flow/xml-source-custom-properties.md)」を参照してください。  
  
 XML ソースでは、複数の標準出力と複数のエラー出力がサポートされています。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、XML ソースを構成するための **[XML ソース エディター]** ダイアログ ボックスがあります。 このダイアログ ボックスは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから利用できます。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [XML 入力元のカスタム プロパティ](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="xml-source-editor-connection-manager-page"></a>[XML ソース エディター] ([接続マネージャー] ページ)
  **[XML ソース エディター]** の **[接続マネージャー]** ページを使用すると、XML ファイルと、XML データを変換する XSD を指定できます。  
  
### <a name="static-options"></a>静的オプション  
 **[データ アクセス モード]**  
 ソースからデータを選択する方法を指定します。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|[XML ファイルの場所]|XML ファイルからデータを取得します。|  
|[変数からの XML ファイル]|XML ファイルの名前を変数で指定します。<br /><br /> **関連情報**: [パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|[変数からの XML データ]|変数から XML データを取得します。|  
  
 **[インライン スキーマを使用する]**  
 XML ソース データ自体に、その構造とデータを定義して検証する XSD スキーマを含めるかどうかを指定します。  
  
 **[XSD の場所]**  
 XSD スキーマ ファイルのパスと名前を入力するか、 **[参照]** をクリックしてファイルを指定します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、XSD スキーマ ファイルを指定します。  
  
 **[XSD の生成]**  
 **[名前を付けて保存]** ダイアログ ボックスを使用して、XSD スキーマ ファイルが自動生成される場所を選択します。 スキーマは XML データの構造から推測されます。  
  
### <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
  
#### <a name="data-access-mode--xml-file-location"></a>[データ アクセス モード] が [XML ファイルの場所] の場合  
 **[XML の場所]**  
 XML データ ファイルのパスと名前を入力するか、 **[参照]** をクリックしてファイルを指定します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、XML データ ファイルを指定します。  
  
#### <a name="data-access-mode--xml-file-from-variable"></a>[データ アクセス モード] が [変数からの XML ファイル] の場合  
 **[変数名]**  
 XML ファイルのパスとファイル名を含む変数を選択します。  
  
#### <a name="data-access-mode--xml-data-from-variable"></a>[データ アクセス モード] が [変数からの XML データ] の場合  
 **[変数名]**  
 XML データを含む変数を選択します。  
  
## <a name="xml-source-editor-columns-page"></a>[XML ソース エディター] ([列] ページ)
  **[XML ソース エディター]** ダイアログ ボックスの **[列]** ノードを使用して、出力列を外部 (変換元) 列にマップします。  
  
### <a name="options"></a>オプション  
 **使用できる外部列**  
 データ ソース内の使用できる外部列の一覧を表示します。 このテーブルを使用して列を追加または削除することはできません。  
  
 **[外部列]**  
 タスクで外部 (変換元) 列を読み取る順序を表示します。 この順序を変更するには、最初にエディターに表示されているテーブル内で選択されている列を選択解除してから、一覧から外部列を別の順で選択します。  
  
 **出力列**  
 各出力列の一意な名前を表示します。 既定では選択された外部 (変換元) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。 指定された名前は、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに表示されます。  
  
## <a name="xml-source-editor-error-output-page"></a>[XML ソース エディター] ([エラー出力] ページ)
  **[XML ソース エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択したり、エラー出力列のプロパティを設定したりできます。  
  
### <a name="options"></a>オプション  
 **[入力または出力]**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[XML ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで選択した外部 (ソース) 列を表示します。  
  
 **Error**  
 エラーが発生した場合に、障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **関連項目:** [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **切り捨て**  
 切り捨てが発生したときの処理方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を指定します。  
  
 **[説明]**  
 エラーの説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="related-tasks"></a>Related Tasks  
 [XML ソースを使用してデータを抽出する](../../integration-services/data-flow/extract-data-by-using-the-xml-source.md)  
