---
title: 共通プロパティ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- external metadata column properties [Integration Services]
- output properties [Integration Services]
- data types [Integration Services], properties
- input properties [Integration Services]
- component properties [Integration Services]
ms.assetid: 51973502-5cc6-4125-9fce-e60fa1b7b796
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5b20a0d2f47e89070712a4063acba4da0225b85d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060962"
---
# <a name="common-properties"></a>共通プロパティ
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、データ フロー オブジェクトのコンポーネント、入力、出力、入力列、および出力列の各レベルに、共通プロパティとカスタム プロパティがあります。 多くのプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
 ここでは、データ フロー オブジェクトの共通プロパティを一覧で示し、それぞれについて説明します。  
  
-   [Components](#components)  
  
-   [入力](#inputs)  
  
-   [Input columns](#inputcolumns)  
  
-   [出力](#outputs)  
  
-   [出力列](#outputcolumns)  
  
 カスタム プロパティの詳細については、次のトピックを参照してください。  
  
-   [ADO NET カスタム プロパティ](data-flow/ado-net-custom-properties.md)  
  
-   [CDC 制御タスクのカスタム プロパティ](control-flow/cdc-control-task-custom-properties.md)  
  
-   [CDC ソースのカスタム プロパティ](data-flow/cdc-source-custom-properties.md)  
  
-   [データ マイニング モデル トレーニング変換先のカスタム プロパティ](data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [DataReader 変換先のカスタム プロパティ](data-flow/datareader-destination-custom-properties.md)  
  
-   [ディメンション処理変換先のカスタム プロパティ](data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Excel のカスタム プロパティ](data-flow/excel-custom-properties.md)  
  
-   [フラット ファイルのカスタム プロパティ](data-flow/flat-file-custom-properties.md)  
  
-   [ODBC 変換先のカスタム プロパティ](data-flow/odbc-destination-custom-properties.md)  
  
-   [ODBC 変換元のカスタム プロパティ](data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB のカスタム プロパティ](data-flow/ole-db-custom-properties.md)OLE DB のカスタム プロパティ  
  
-   [パーティション処理変換先のカスタム プロパティ](data-flow/partition-processing-destination-custom-properties.md)  
  
-   [RAW ファイルのカスタム プロパティ](data-flow/raw-file-custom-properties.md)  
  
-   [レコードセット変換先のカスタム プロパティ](data-flow/recordset-destination-custom-properties.md)  
  
-   [SQL Server Compact Edition 変換先のカスタム プロパティ](data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [SQL Server 変換先のカスタム プロパティ](data-flow/sql-server-destination-custom-properties.md)  
  
-   [変換のカスタム プロパティ](data-flow/transformations/transformation-custom-properties.md)  
  
-   [XML 入力元のカスタム プロパティ](data-flow/xml-source-custom-properties.md)  
  
##  <a name="components"></a> コンポーネントのプロパティ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、データ フロー内のコンポーネントに <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントのプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|ComponentClassID|String|コンポーネントの CLSID。|  
|ContactInfo|String|コンポーネント開発者の連絡先情報。|  
|説明|String|データ フロー コンポーネントの説明。 このプロパティの既定値は、データ フロー コンポーネントの名前です。|  
|ID|Integer|コンポーネントのこのインスタンスを一意に識別する値。|  
|[IdentificationString]|String|コンポーネントを識別します。|  
|IsDefaultLocale|ブール値|コンポーネントが、それ自体が属するデータ フロー タスクのロケールを使用するかどうかを示します。|  
|LocaleID|Integer|パッケージを実行する際、データ フロー コンポーネントが使用するロケール。 データ フロー コンポーネントでは、すべての Windows ロケールが使用できます。|  
|名前|String|データ フロー コンポーネントの名前。|  
|PipelineVersion|Integer|コンポーネントを実行するように設計されたデータ フロー タスクのバージョン。|  
|UsesDispositions|ブール値|コンポーネントにエラー出力があるかどうかを示します。|  
|[ValidateExternalMetadata]|ブール値|外部列のメタデータを検証するかどうかを示します。 このプロパティの既定値は `True` です。|  
|バージョン|Integer|コンポーネントのバージョン。|  
  
##  <a name="inputs"></a> 入力プロパティ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、変換および変換先には入力があります。 データ フロー内のコンポーネントの入力は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの入力のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|説明|String|入力の説明。|  
|ErrorOrTruncationOperation|String|行の処理中にエラーや切り捨てが発生する可能性がある場合、その種類を指定するオプションの文字列。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|エラーの処理方法を指定する値。 値は、`Fail component`、`Ignore failure`、および `Redirect row` です。|  
|HasSideEffects|ブール値|下流コンポーネントにアタッチされていないとき、および、コンポーネントをデータ フローの実行プランから削除できるかどうかを示す`RunInOptimizedMode`は`true`します。|  
|ID|Integer|入力を一意に識別する値。|  
|[IdentificationString]|String|入力を識別する文字列。|  
|IsSorted|ブール値|入力のデータを並べ替えるかどうかを示します。|  
|名前|String|入力の名前。|  
|SourceLocale|Integer|入力データのロケール ID (LCID)。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|行の処理中に発生した切り捨てを処理する方法を指定する値。 . 値は、`Fail component`、`Ignore failure`、および `Redirect row` です。|  
  
 変換先および一部の変換では、エラー出力がサポートされず、これらのコンポーネントの ErrorRowDisposition プロパティおよび TruncationRowDisposition プロパティは読み取り専用です。  
  
###  <a name="inputcolumns"></a> 入力列プロパティ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、入力には入力列のコレクションが含まれています。 データ フロー内のコンポーネントの入力列は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの入力列のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|文字データ型を持つ列の比較を示すフラグの組。 詳しくは、「 [Comparing String Data](data-flow/comparing-string-data.md)」をご覧ください。|  
|説明|String|入力列を説明します。|  
|ErrorOrTruncationOperation|String|行の処理中にエラーや切り捨てが発生する可能性がある場合、その種類を指定するオプションの文字列。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|エラーの処理方法を指定する値。 値は、`Fail component`、`Ignore failure`、および `Redirect row` です。|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|出力列に割り当てられた外部メタデータ列の ID。|  
|ID|Integer|入力列を一意に識別する値。|  
|[IdentificationString]|String|入力列を識別する文字列。|  
|LineageID|Integer|上流列の ID。|  
|名前|String|入力列の名前。|  
|SortKeyPosition|Integer|列を並べ替えるかどうか、並べ替える場合はその並べ替え順、および複数の列の並べ替えの順序を示す値。 値 **0** は、その列が並べ替えられないことを示します。  詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|行の処理中に発生した切り捨てを処理する方法を指定する値。 値は、`Fail component`、`Ignore failure`、および `Redirect row` です。|  
|UpstreamComponentName|String|上流コンポーネントの名前。|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|コンポーネントが入力列を使用する方法を指定する値。|  
  
 入力列には、後の「データ型プロパティ」で説明するデータ型プロパティもあります。  
  
##  <a name="outputs"></a> 出力プロパティ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、変換元および変換には出力があります。 データ フロー内のコンポーネントの出力は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの出力のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|ブール値|出力がパスに接続されていない場合に、データ フロー エンジンが出力を削除するかどうかを指定する値。|  
|説明|String|出力を説明します。|  
|ErrorOrTruncationOperation|String|行の処理中にエラーや切り捨てが発生する可能性がある場合、その種類を指定するオプションの文字列。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|エラーの処理方法を指定する値。 値は、`Fail component`、`Ignore failure`、および `Redirect row` です。|  
|ExclusionGroup|Integer|相互排他的な出力のグループを識別する値。|  
|HasSideEffects|ブール値|コンポーネントが上流コンポーネントにアタッチされていない場合や、`RunInOptimizedMode` が `true` の場合に、データ フローの実行プランからコンポーネントを削除できるかどうかを示します。|  
|ID|Integer|出力を一意に識別する値。|  
|[IdentificationString]|String|出力を識別する文字列。|  
|IsErrorOut|ブール値|出力がエラー出力かどうかを示します。|  
|IsSorted|ブール値|出力を並べ替えるかどうかを示します。 既定値は `False` です。<br /><br /> **\*\* 重要な\* \*** の値を設定、`IsSorted`プロパティを`True`もデータは並べ替えられません。 このプロパティでは、データが既に並べ替えられている下流コンポーネントにヒントのみを提供します。 詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。|  
|名前|String|出力の名前。|  
|SynchronousInputID|Integer|出力に同期する入力の ID。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|行の処理中に発生した切り捨てを処理する方法を指定する値。 値は、`Fail component`、`Ignore failure`、および `Redirect row` です。|  
  
###  <a name="outputcolumns"></a> 出力列のプロパティ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、出力に出力列のコレクションが含まれています。 データ フロー内のコンポーネントの出力列は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの出力列のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|文字データ型を持つ列の比較を示すフラグの組。 詳しくは、「 [Comparing String Data](data-flow/comparing-string-data.md)」をご覧ください。|  
|説明|String|出力列を説明します。|  
|ErrorOrTruncationOperation|String|行の処理中にエラーや切り捨てが発生する可能性がある場合、その種類を指定するオプションの文字列。|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|エラーの処理方法を指定する値。 値は、`Fail component`、`Ignore failure`、および `Redirect row` です。 既定値は `Fail component` です。|  
|ExternalMetadataColumnID|Integer|出力列に割り当てられた外部メタデータ列の ID。|  
|ID|Integer|出力列を一意に識別する値。|  
|[IdentificationString]|String|出力列を識別する文字列。|  
|LineageID|Integer|出力列の ID。 下流コンポーネントは、この値を使用して列を参照します。|  
|名前|String|出力列の名前。|  
|SortKeyPosition|Integer|列を並べ替えるかどうか、並べ替える場合はその並べ替え順、および複数の列の並べ替えの順序を示す値。 値 **0** は、その列が並べ替えられないことを示します。 詳細については、「 [Sort Data for the Merge and Merge Join Transformations](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」(マージ変換およびマージ結合変換用にデータを並べ替える方法) を参照してください。|  
|SpecialFlags|Integer|出力列の特殊なフラグを含む値。|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|行の処理中に発生した切り捨てを処理する方法を指定する値。 値は、`Fail component`、`Ignore failure`、および `Redirect row` です。 既定値は `Fail component` です。|  
  
 出力列には、データ型プロパティの組も含まれています。  
  
## <a name="external-metadata-column-properties"></a>外部メタデータ列のプロパティ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、入力および出力に外部メタデータ列のコレクションを含めることができます。 データ フロー内のコンポーネントの外部メタデータ列は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のコンポーネントの外部メタデータ列のプロパティを示しています。 一部のプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|説明|String|外部列を説明します。|  
|ID|Integer|列を一意に識別する値。|  
|[IdentificationString]|String|列を識別する文字列。|  
|名前|String|外部列の名前。|  
  
 外部メタデータ列には、データ型プロパティの組も含まれています。  
  
## <a name="data-type-properties"></a>データ型プロパティ  
 出力列および外部メタデータ列には、データ型プロパティの組が含まれています。 列のデータ型に応じて、プロパティは読み取り/書き込み可能または読み取り専用の場合があります。  
  
 次の表は、出力列および外部メタデータ列のデータ型プロパティを示しています。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|CodePage|Integer|Unicode でない文字列データのコード ページを指定します。|  
|DataType|Integer (列挙)|列の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] データ型。 詳細については、「 [Integration Services Data Types](data-flow/integration-services-data-types.md)」を参照してください。|  
|長さ|Integer|列の長さ (文字数単位)。|  
|有効桁数|Integer|数値列の有効桁数。|  
|Scale|Integer|数値列の小数点以下桁数。|  
  
## <a name="see-also"></a>参照  
 [データ フロー](data-flow/data-flow.md)   
 [変換のカスタム プロパティ](data-flow/transformations/transformation-custom-properties.md)   
 [パスのプロパティ](../../2014/integration-services/path-properties.md)   
 [式を使って設定できるデータ フロー プロパティ](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
