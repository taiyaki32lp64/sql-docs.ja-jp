---
title: データ フロー コンポーネントのプロパティを設定する | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 10b397e4fdabefe333854fe04ab37c4bdd92cf38
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291841"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>データ フロー コンポーネントのプロパティを設定する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  変換元、変換先、変換などを含むデータ フロー コンポーネントのプロパティを設定するには、次の機能のいずれかを使用します。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が提供するコンポーネント エディター。 これらのエディターには、各データ フロー コンポーネントのカスタム プロパティのみ含まれます。  
  
-   **[プロパティ]** ウィンドウでは、各要素のコンポーネントレベルのカスタム プロパティ、およびすべてのデータ フロー要素との共通プロパティの一覧が表示されます。  
  
-   **[詳細エディター]** ダイアログ ボックスでは、各コンポーネントのカスタム プロパティにアクセスできます。 また、 **[詳細エディター]** ダイアログ ボックスを使用すると、すべてのデータ フロー コンポーネントの共通プロパティである、入力、出力、エラー出力、列、および外部列のプロパティにもアクセスできます。  
  
## <a name="set-the-properties-of-a-data-flow-component-with-a-component-editor"></a>コンポーネント エディターを使用してデータ フロー コンポーネントのプロパティを設定する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックし、プロパティを表示して変更するコンポーネントのあるデータ フローが含まれる、データ フロー タスクをダブルクリックします。  
  
4.  データ フロー コンポーネントをダブルクリックします。  
  
5.  コンポーネント エディターで、プロパティ値を表示または変更し、エディターを閉じます。  
  
6.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="set-the-properties-of-a-data-flow-component-in-the-properties-window"></a>[プロパティ] ウィンドウでデータ フロー コンポーネントのプロパティを設定する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックし、プロパティを表示して変更するコンポーネントが含まれているデータ フロー タスクをダブルクリックします。  
  
4.  データ フロー コンポーネントを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  プロパティ値を表示または変更し、 **[プロパティ]** ウィンドウを閉じます。  
  
    > [!NOTE]  
    >  プロパティの多くは読み取り専用であり、変更できません。  
  
6.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="set-the-properties-of-a-data-flow-component-with-the-advanced-editor"></a>詳細エディターを使用してデータ フロー コンポーネントのプロパティを設定する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックし、表示または変更するコンポーネントが含まれているデータ フロー タスクをダブルクリックします。  
  
4.  データ フロー デザイナーで、データ フロー コンポーネントを右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、複数の入力をサポートするデータ フロー コンポーネントで **[詳細エディター]** を使用できません。  
  
5.  **[詳細エディター]** ダイアログ ボックスで、次のいずれかの手順を実行します。  
  
    -   コンポーネントで使用する接続を表示および指定するには、 **[接続マネージャー]** タブをクリックします。  
  
        > [!NOTE]  
        >  **[接続マネージャー]** タブは、接続マネージャーを使用してファイルやデータベースなどのデータ ソースに接続するデータ フロー コンポーネントのみで使用できます。  
  
    -   コンポーネント レベルのプロパティを表示および変更するには、 **[コンポーネントのプロパティ]** タブをクリックします。  
  
    -   外部列と使用できる出力との間のマッピングを表示および変更するには、 **[列マッピング]** タブをクリックします。  
  
        > [!NOTE]  
        >  **[列マッピング]** タブは、変換元または変換先を表示または編集するときにのみ使用できます。  
  
    -   使用できる入力列の一覧を表示して、出力列の名前を更新するには、 **[入力列]** タブをクリックします。  
  
        > [!NOTE]  
        >  [入力列] タブは、変換または変換先を使用した作業でのみ使用できます。 詳細については、「 [Integration Services の変換](../../integration-services/data-flow/transformations/integration-services-transformations.md)」を参照してください。  
  
    -   入力、出力、およびエラー出力のプロパティや、列自体のプロパティを表示および変更するには、 **[入力プロパティと出力プロパティ]** タブをクリックします。  
  
        > [!NOTE]  
        >  変換元には入力はありません。 変換先には出力はありません。ただし、オプションのエラー出力がある場合があります。  
  
6.  プロパティ値を表示または変更します。  
  
7.  **[OK]** をクリックします。  
  
8.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

## <a name="common-properties-of-data-flow-components"></a>データ フロー コンポーネントの共通プロパティ
[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、データ フロー オブジェクトのコンポーネント、入力、出力、入力列、および出力列の各レベルに、共通プロパティとカスタム プロパティがあります。 多くのプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
 ここでは、データ フロー オブジェクトの共通プロパティを一覧で示し、それぞれについて説明します。  
  
-   [コンポーネント](#components)  
  
-   [入力](#inputs)  
  
-   [Input columns](#inputcolumns)  
  
-   [出力](#outputs)  
  
-   [出力列](#outputcolumns)  
  
 
###  <a name="components"></a> Component properties  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、データ フロー内のコンポーネントに <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントのプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|[説明]|  
|--------------|---------------|-----------------|  
|ComponentClassID|String|コンポーネントの CLSID。|  
|ContactInfo|String|コンポーネント開発者の連絡先情報。|  
|[説明]|String|データ フロー コンポーネントの説明。 このプロパティの既定値は、データ フロー コンポーネントの名前です。|  
|ID|Integer|コンポーネントのこのインスタンスを一意に識別する値。|  
|[IdentificationString]|String|コンポーネントを識別します。|  
|IsDefaultLocale|Boolean|コンポーネントが、それ自体が属するデータ フロー タスクのロケールを使用するかどうかを示します。|  
|LocaleID|Integer|パッケージを実行する際、データ フロー コンポーネントが使用するロケール。 データ フロー コンポーネントでは、すべての Windows ロケールが使用できます。|  
|[オブジェクト名]|String|データ フロー コンポーネントの名前。|  
|PipelineVersion|Integer|コンポーネントを実行するように設計されたデータ フロー タスクのバージョン。|  
|UsesDispositions|Boolean|コンポーネントにエラー出力があるかどうかを示します。|  
|[ValidateExternalMetadata]|Boolean|外部列のメタデータを検証するかどうかを示します。 このプロパティの既定値は **True**です。|  
|Version|Integer|コンポーネントのバージョン。|  
  
###  <a name="inputs"></a> 入力プロパティ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、変換および変換先には入力があります。 データ フロー内のコンポーネントの入力は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの入力のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|[説明]|  
|--------------|---------------|-----------------|  
|[説明]|String|入力の説明。|  
|ErrorOrTruncationOperation|String|行の処理中にエラーや切り捨てが発生する可能性がある場合、その種類を指定するオプションの文字列。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|エラーの処理方法を指定する値。 値は **Fail component**、 **Ignore failure**、 **Redirect row**|  
|HasSideEffects|Boolean|コンポーネントが下流コンポーネントにアタッチされていない場合や、 **RunInOptimizedMode** が **true**の場合に、データ フローの実行プランからコンポーネントを削除できるかどうかを示します。|  
|ID|Integer|入力を一意に識別する値。|  
|[IdentificationString]|String|入力を識別する文字列。|  
|IsSorted|Boolean|入力のデータを並べ替えるかどうかを示します。|  
|[オブジェクト名]|String|入力の名前。|  
|SourceLocale|Integer|入力データのロケール ID (LCID)。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|行の処理中に発生した切り捨てを処理する方法を指定する値。 です。 値は **Fail component**、 **Ignore failure**、 **Redirect row**|  
  
 変換先および一部の変換では、エラー出力がサポートされず、これらのコンポーネントの ErrorRowDisposition プロパティおよび TruncationRowDisposition プロパティは読み取り専用です。  
  
###  <a name="inputcolumns"></a> 入力列プロパティ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、入力には入力列のコレクションが含まれています。 データ フロー内のコンポーネントの入力列は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの入力列のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|[説明]|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|文字データ型を持つ列の比較を示すフラグの組。 詳しくは、「 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)」をご覧ください。|  
|[説明]|String|入力列を説明します。|  
|ErrorOrTruncationOperation|String|行の処理中にエラーや切り捨てが発生する可能性がある場合、その種類を指定するオプションの文字列。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|エラーの処理方法を指定する値。 値は **Fail component**、 **Ignore failure**、 **Redirect row**|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|出力列に割り当てられた外部メタデータ列の ID。|  
|ID|Integer|入力列を一意に識別する値。|  
|[IdentificationString]|String|入力列を識別する文字列。|  
|LineageID|Integer|上流列の ID。|  
|LineageIdentificationString|String|上流列の名前を含む識別文字列。|  
|[オブジェクト名]|String|入力列の名前。|  
|SortKeyPosition|Integer|列を並べ替えるかどうか、並べ替える場合はその並べ替え順、および複数の列の並べ替えの順序を示す値。 値 **0** は、その列が並べ替えられないことを示します。  詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|行の処理中に発生した切り捨てを処理する方法を指定する値。 値は **Fail component**、 **Ignore failure**、 **Redirect row**|  
|UpstreamComponentName|String|上流コンポーネントの名前。|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|コンポーネントが入力列を使用する方法を指定する値。|  
  
 入力列には、後の「データ型プロパティ」で説明するデータ型プロパティもあります。  
  
###  <a name="outputs"></a> 出力プロパティ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、変換元および変換には出力があります。 データ フロー内のコンポーネントの出力は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの出力のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|[説明]|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|Boolean|出力がパスに接続されていない場合に、データ フロー エンジンが出力を削除するかどうかを指定する値。|  
|[説明]|String|出力を説明します。|  
|ErrorOrTruncationOperation|String|行の処理中にエラーや切り捨てが発生する可能性がある場合、その種類を指定するオプションの文字列。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|エラーの処理方法を指定する値。 値は **Fail component**、 **Ignore failure**、 **Redirect row**|  
|ExclusionGroup|Integer|相互排他的な出力のグループを識別する値。|  
|HasSideEffects|Boolean|コンポーネントが上流コンポーネントにアタッチされていない場合や、 **RunInOptimizedMode** が **true**の場合に、データ フローの実行プランからコンポーネントを削除できるかどうかを示します。|  
|ID|Integer|出力を一意に識別する値。|  
|[IdentificationString]|String|出力を識別する文字列。|  
|IsErrorOut|Boolean|出力がエラー出力かどうかを示します。|  
|IsSorted|Boolean|出力を並べ替えるかどうかを示します。 既定値は **False**です。<br /><br /> **\*\* 重要 \*\*** **IsSorted** プロパティの値を **True** に設定しても、データは並べ替えられません。 このプロパティでは、データが既に並べ替えられている下流コンポーネントにヒントのみを提供します。 詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。|  
|[オブジェクト名]|String|出力の名前。|  
|SynchronousInputID|Integer|出力に同期する入力の ID。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|行の処理中に発生した切り捨てを処理する方法を指定する値。 値は **Fail component**、 **Ignore failure**、 **Redirect row**|  
  
###  <a name="outputcolumns"></a> 出力列プロパティ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、出力に出力列のコレクションが含まれています。 データ フロー内のコンポーネントの出力列は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの出力列のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|[説明]|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|文字データ型を持つ列の比較を示すフラグの組。 詳しくは、「 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)」をご覧ください。|  
|[説明]|String|出力列を説明します。|  
|ErrorOrTruncationOperation|String|行の処理中にエラーや切り捨てが発生する可能性がある場合、その種類を指定するオプションの文字列。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|エラーの処理方法を指定する値。 値は **Fail component**、 **Ignore failure**、 **Redirect row** 既定値は **Fail component**です。|  
|ExternalMetadataColumnID|Integer|出力列に割り当てられた外部メタデータ列の ID。|  
|ID|Integer|出力列を一意に識別する値。|  
|[IdentificationString]|String|出力列を識別する文字列。|  
|LineageID|Integer|出力列の ID。 下流コンポーネントは、この値を使用して列を参照します。|  
|LineageIdentificationString|String|列の名前を含む識別文字列。|  
|[オブジェクト名]|String|出力列の名前。|  
|SortKeyPosition|Integer|列を並べ替えるかどうか、並べ替える場合はその並べ替え順、および複数の列の並べ替えの順序を示す値。 値 **0** は、その列が並べ替えられないことを示します。 詳細については、「 [Sort Data for the Merge and Merge Join Transformations](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」(マージ変換およびマージ結合変換用にデータを並べ替える方法) を参照してください。|  
|SpecialFlags|Integer|出力列の特殊なフラグを含む値。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|行の処理中に発生した切り捨てを処理する方法を指定する値。 値は **Fail component**、 **Ignore failure**、 **Redirect row** 既定値は **Fail component**です。|  
  
 出力列には、データ型プロパティの組も含まれています。  
  
### <a name="external-metadata-column-properties"></a>外部メタデータ列のプロパティ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、入力および出力に外部メタデータ列のコレクションを含めることができます。 データ フロー内のコンポーネントの外部メタデータ列は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの外部メタデータ列のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|[説明]|  
|--------------|---------------|-----------------|  
|[説明]|String|外部列を説明します。|  
|ID|Integer|列を一意に識別する値。|  
|[IdentificationString]|String|列を識別する文字列。|  
|[オブジェクト名]|String|外部列の名前。|  
  
 外部メタデータ列には、データ型プロパティの組も含まれています。  
  
### <a name="data-type-properties"></a>データ型プロパティ  
 出力列および外部メタデータ列には、データ型プロパティの組が含まれています。 列のデータ型に応じて、プロパティは読み取り/書き込み可能または読み取り専用の場合があります。  
  
 次の表は、出力列および外部メタデータ列のデータ型プロパティを示しています。  
  
|プロパティ|データ型|[説明]|  
|--------------|---------------|-----------------|  
|CodePage|Integer|Unicode でない文字列データのコード ページを指定します。|  
|DataType|Integer (列挙)|列の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。|  
|長さ|Integer|列の長さ (文字数単位)。|  
|有効桁数|Integer|数値列の有効桁数。|  
|Scale|Integer|数値列の小数点以下桁数。|  

## <a name="custom-properties-of-data-flow-components"></a>データ フロー コンポーネントのカスタム プロパティ
カスタム プロパティの詳細については、次のトピックを参照してください。  
  
-   [ADO NET カスタム プロパティ](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
-   [CDC 制御タスクのカスタム プロパティ](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
-   [CDC ソースのカスタム プロパティ](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [データ マイニング モデル トレーニング変換先のカスタム プロパティ](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [DataReader 変換先のカスタム プロパティ](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
-   [ディメンション処理変換先のカスタム プロパティ](../../integration-services/data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Excel のカスタム プロパティ](../../integration-services/data-flow/excel-custom-properties.md)  
  
-   [フラット ファイルのカスタム プロパティ](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
-   [ODBC 変換先のカスタム プロパティ](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
-   [ODBC 変換元のカスタム プロパティ](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB のカスタム プロパティ](../../integration-services/data-flow/ole-db-custom-properties.md)OLE DB のカスタム プロパティ  
  
-   [パーティション処理変換先のカスタム プロパティ](../../integration-services/data-flow/partition-processing-destination-custom-properties.md)  
  
-   [RAW ファイルのカスタム プロパティ](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
-   [レコードセット変換先のカスタム プロパティ](../../integration-services/data-flow/recordset-destination-custom-properties.md)  
  
-   [SQL Server Compact Edition 変換先のカスタム プロパティ](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [SQL Server 変換先のカスタム プロパティ](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
-   [変換のカスタム プロパティ](../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
-   [XML 入力元のカスタム プロパティ](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
## <a name="use-an-expression-in-a-data-flow-component"></a>データ フロー コンポーネントで式を使用する
この手順では、条件分割変換または派生列変換に式を追加する方法について説明します。 条件分割変換では、式を使用して、変換出力にデータ行を出力する条件を定義します。また、派生列変換では、式を使用して、列に割り当てる値を定義します。  
  
 変換に式を実装するには、あらかじめパッケージに少なくとも 1 つのデータ フロー タスクとソースが含まれている必要があります。 
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[制御フロー]** タブをクリックし、式を実装するデータ フローを含むデータ フロー タスクをクリックします。  
  
4.  **[データ フロー]** タブをクリックし、 **[ツールボックス]** からデザイン画面に条件分割変換または派生列変換のいずれかをドラッグします。  
  
5.  緑色のコネクタをソースまたは変換から条件分割変換または派生列変換にドラッグします。  
  
6.  変換をダブルクリックして、変換のダイアログ ボックスを開きます。  
  
7.  左側のペインで **[変数]** を展開し、システム変数およびユーザー定義変数を表示します。また、 **[列]** を展開して、変換の入力列を表示します。  
  
8.  右側のペインで **[数学関数]** 、 **[文字列関数]** 、 **[日付/時刻関数]** 、 **[NULL 関数]** 、 **[型キャスト]** 、および **[演算子]** を展開して、式の文法で用意されている関数、キャスト、および演算子にアクセスします。  
  
9. 変換に応じて、次のいずれかの操作を実行し、式を作成します。  
  
    -   **[条件分割変換エディター]** ダイアログ ボックスで、変数、列、関数、演算子、およびキャストを **[条件]** 列にドラッグします。 ドラッグする代わりに、 **[条件]** 列に式を直接入力することもできます。  
  
    -   **[派生列変換エディター]** ダイアログ ボックスで、変数、列、関数、演算子、およびキャストを **[式]** 列にドラッグします。 ドラッグする代わりに、 **[式]** 列に式を直接入力することもできます。  
  
        > [!NOTE]  
        >  **[条件]** 列または **[式]** 列からフォーカスを外したときに、式テキストが強調表示された場合、式の文法が間違っていることを示します。  
  
10. **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
    > [!NOTE]  
    >  式が有効でない場合、式に文法エラーがあることを示す警告が表示されます。  

## <a name="data-flow-properties-that-you-can-set-with-an-expression"></a>式で設定できるデータ フロー プロパティ
データ フロー タスク コンテナーで使用できるプロパティ式を使用して、データ フロー オブジェクトの特定のプロパティの値を指定できます。  
  
 プロパティ式の使用の詳細については、「 [パッケージでプロパティ式を使用する](../../integration-services/expressions/use-property-expressions-in-packages.md)」を参照してください。  
  
 プロパティ式を使用して、パッケージを配置するインスタンスごとに構成をカスタマイズできます。 また、コマンド プロンプト ユーティリティ **dtexec** に **/set** オプションを付けて使用すると、プロパティ式を使用してパッケージの実行時制約を指定することもできます。 たとえば、並べ替え変換で使用される **MaximumThreads** 、または、あいまいグループ化変換およびあいまい参照変換の **MaxMemoryUsage** を制約できます。 制約を行わないと、これらの変換により大容量のデータがメモリ内にキャッシュされる場合があります。  
  
 このトピックに示すデータ フロー オブジェクトのプロパティの 1 つに対するプロパティ式を指定するには、デザイナーの **[制御フロー]** 画面でデータ フロー タスクを選択するか、コンポーネントやパスを個別に選択せずにデザイナーの **[データ フロー]** タブを選択して、データ フロー タスクの **[プロパティ]** ウィンドウを表示します。 **[式]** プロパティを選択し、省略記号 (...) をクリックして、 **[プロパティ式エディター]** ダイアログ ボックスを表示します。 **[プロパティ]** の一覧からプロパティを選択し、 **[式]** テキスト ボックスに式を入力するか、省略記号 (...) をクリックして **[式ビルダー]** ダイアログ ボックスを表示します。  
  
 **[プロパティ]** の一覧には、現在、デザイナーの **[データ フロー]** 画面に配置されているデータ フロー オブジェクトで使用できるプロパティのみが表示されます。 したがって、 **[プロパティ]** の一覧では、プロパティ式をサポートするデータ フロー オブジェクトのすべてのプロパティを表示することはできません。 たとえば、デザイナー画面に ADO NET ソースを配置した場合、 **[プロパティ]** の一覧には **[ADO NET Source].[SqlCommand]** プロパティのエントリが表示されます。 この一覧には、データ フロー タスク自体の多数のプロパティも表示されます。  
 
 次の一覧にあるプロパティの値は、プロパティ式を使用して指定できます。  
  
### <a name="data-flow-sources"></a>データ フローの変換元  
  
|データ フロー オブジェクト|[プロパティ]|  
|----------------------|--------------|  
|ADO NET ソース|TableOrViewName プロパティ<br /><br /> SqlCommand プロパティ|  
|XML ソース|XMLData プロパティ<br /><br /> XMLSchemaDefinition プロパティ|  
  
### <a name="data-flow-transformations"></a>データ フロー変換  
 これらのカスタム プロパティの詳細については、「 [変換のカスタム プロパティ](../../integration-services/data-flow/transformations/transformation-custom-properties.md)」を参照してください。  
  
|データ フロー オブジェクト|プロパティ|  
|----------------------|--------------|  
|条件分割変換|FriendlyExpression プロパティ|  
|派生列変換|FriendlyExpression プロパティ|  
|あいまいグループ化変換|MaxMemoryUsage プロパティ|  
|あいまい参照変換|MaxMemoryUsage プロパティ|  
|参照変換|SqlCommand プロパティ<br /><br /> SqlCommandParam プロパティ|  
|OLE DB コマンド変換|SqlCommand プロパティ|  
|比率サンプリング変換|SamplingValue プロパティ|  
|ピボット変換|PivotKeyValue プロパティ|  
|行サンプリング変換|SamplingValue プロパティ|  
|並べ替え変換|MaximumThreads プロパティ|  
|ピボット解除変換|PivotKeyValue プロパティ|  
  
### <a name="data-flow-destinations"></a>データ フローの変換先  
  
|データ フロー オブジェクト|プロパティ|  
|----------------------|--------------|  
|ADO NET 変換先|TableOrViewName プロパティ<br /><br /> BatchSize プロパティ<br /><br /> CommandTimeOut プロパティ|  
|フラット ファイル変換先|Header プロパティ|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先|TableName プロパティ|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先|BulkInsertTableName プロパティ<br /><br /> BulkInsertFirstRow プロパティ<br /><br /> BulkInsertLastRow プロパティ<br /><br /> BulkInsertOrder プロパティ<br /><br /> Timeout プロパティ|  

