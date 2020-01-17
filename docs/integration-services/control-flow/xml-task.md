---
title: XML タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.xmltask.f1
- sql13.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca59166f994a0bd982c2f00c5c60c39207e9e02a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293662"
---
# <a name="xml-task"></a>XML タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  XML タスクは、XML データの処理に使用します。 このタスクを使用すると、パッケージは、XML ドキュメントの取得、Extensible Stylesheet Language Transformations (XSLT) スタイル シートや XPath 式の使用によるドキュメントへの操作の適用、複数ドキュメントのマージ、または更新したドキュメントの検証、比較、およびファイルや変数への保存を行うことができます。  
  
 このタスクを使用すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、XML ドキュメントを実行時に動的に変更できます。 XML タスクは、次の目的で使用できます。  
  
-   XML ドキュメントを再フォーマットする。 たとえば、このタスクは、XML ファイル内に存在するレポートにアクセスし、XSLT スタイル シートを動的に適用してドキュメントの表示形式をカスタマイズできます。  
  
-   XML ドキュメントのセクションを選択する。 たとえば、このタスクは、XML ファイル内に存在するレポートにアクセスし、XPath 式を動的に適用してドキュメントのセクションを選択できます。 この操作により、ドキュメント内の値を取得して処理することもできます。  
  
-   多くの変換元からドキュメントをマージする。 たとえば、このタスクは複数の変換元からレポートをダウンロードし、1 つの包括的な XML ドキュメントに動的にマージできます。  
  
-   XML ドキュメントを検証し、必要に応じて詳細なエラー出力を取得します。 詳細については、「 [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)」を参照してください。  
  
 XML ソースを使用して XML ドキュメントの値を抽出し、データ フロー内に XML データを含めることができます。 詳細については、「 [XML ソース](../../integration-services/data-flow/xml-source.md)」を参照してください。  
  
## <a name="xml-operations"></a>XML 操作  
 XML タスクが実行する最初のアクションは、特定の XML ドキュメントの取得です。 このアクションは XML タスクに組み込まれており、自動的に発生します。 取得した XML ドキュメントは、XML タスクが実行する操作においてデータの変換元として使用されます。  
  
 XML 操作である Diff、Merge、および Patch には、2 つのオペランドが必要です。 最初のオペランドは、XML ソース ドキュメントを指定します。 2 番目のオペランドも XML ドキュメントを指定しますが、その内容は操作の必要条件に応じて変化します。 たとえば、Diff 操作では 2 つのドキュメントを比較します。したがって、2 番目のオペランドは、XML ソース ドキュメントの比較対象となる、類似した別の XML ドキュメントを指定します。  
  
 XML タスクは、変数またはファイル接続マネージャーをその変換元として使用できます。または、XML データをタスクのプロパティに含めることができます。  
  
 変換元が変数の場合、指定した変数には、XML ドキュメントのパスが含まれます。  
  
 変換元がファイル接続マネージャーの場合、指定したファイル接続マネージャーは変換元の情報を提供します。 ファイル接続マネージャーは、XML タスクとは別に構成され、XML タスク内で参照されます。 ファイル接続マネージャーの接続文字列は、XML ファイルのパスを指定します。 詳しくは「 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)」をご覧ください。  
  
 XML タスクは、操作の結果を変数またはファイルに保存するように構成できます。 ファイルに保存する場合、XML タスクはファイル接続マネージャーを使用して、そのファイルにアクセスします。 また、Diff 操作によって生成された DiffGram の結果を、ファイルや変数に保存することもできます。  
  
## <a name="predefined-xml-operations"></a>定義済み XML 操作  
 XML タスクには、XML ドキュメントを処理するための定義済み操作のセットが含まれています。 次の表では、これらの操作について説明します。  
  
|操作|[説明]|  
|---------------|-----------------|  
|[Diff]|2 つの XML ドキュメントを比較します。 XML ソース ドキュメントを基本ドキュメントとして使用し、Diff 操作は、そのドキュメントを 2 番目の XML ドキュメントと比較し、それらの違いを検出して XML DiffGram ドキュメントに書き込みます。 この操作には、比較をカスタマイズするためのプロパティが含まれています。|  
|Merge|2 つの XML ドキュメントをマージします。 マージ操作は、XML ソース ドキュメントを基本ドキュメントとして使用し、2 番目のドキュメントの内容を基本ドキュメントに追加します。 この操作では、基本ドキュメント内のマージ場所を指定できます。|  
|[Patch]|DiffGram ドキュメントと呼ばれる Diff 操作の出力を XML ドキュメントに適用し、DiffGram ドキュメントの内容を含む新しい親ドキュメントを作成します。|  
|[検証]|文書型定義 (DTD) または XML スキーマ定義 (XSD) スキーマに対して XML ドキュメントを検証します。|  
|XPath|XPath クエリと評価を実行します。|  
|XSLT (XSLT)|XML ドキュメントに対して XSL 変換を実行します。|  
  
### <a name="diff-operation"></a>Diff 操作  
 Diff 操作は、比較を高速で行うか詳細に行うかに応じて、異なる比較アルゴリズムを使用するように構成できます。 また、比較するドキュメントのサイズに基づいて、高速比較を行うか詳細比較を行うかを自動的に選択するように、構成することもできます。  
  
 Diff 操作には、XML 比較をカスタマイズするオプションのセットが含まれています。 次の表では、このオプションについて説明します。  
  
|オプション|[説明]|  
|------------|-----------------|  
|**[IgnoreComments]**|この値で、コメント ノードを比較するかどうかを指定します。|  
|**[IgnoreNamespaces]**|この値で、要素名および属性名の名前空間の Uniform Resource Identifier (URI) を比較するかどうかを指定します。 このオプションを **true**に設定した場合、ローカル名が同じで、異なる名前空間を持つ 2 つの要素は、同一と見なされます。|  
|**[IgnorePrefixes]**|この値で、要素名および属性名のプレフィックスを比較するかどうかを指定します。 このオプションを **true,** に設定した場合、ローカル名が同じで、異なる名前空間 URI とプレフィックスを持つ 2 つの要素は、同一と見なされます。|  
|**[IgnoreXMLDeclaration]**|この値で、XML 宣言を比較するかどうかを指定します。|  
|**IgnoreOrderOfChildElements**|この値で、子要素の順序を比較するかどうかを指定します。 このオプションを **true**に設定した場合、兄弟の一覧での位置だけが異なる子要素は同一と見なされます。|  
|**IgnoreWhiteSpaces**|この値で、空白を比較するかどうかを指定します。|  
|**[IgnoreProcessingInstructions]**|この値で、処理命令を比較するかどうかを指定します。|  
|**[IgnoreDTD]**|この値で、DTD を無視するかどうかを指定します。|  
  
### <a name="merge-operation"></a>マージ操作  
 XPath ステートメントを使用してソース ドキュメント内でのマージ場所を特定すると、このステートメントによって 1 つのノードが返されます。 ステートメントによって複数のノードが返された場合は、最初のノードだけが使用されます。 2 番目のドキュメントの内容は、XPath クエリによって返される最初のノードでマージされます。  
  
### <a name="xpath-operation"></a>XPath 操作  
 XPath 操作は、XPath のさまざまな種類の機能を使用するように構成できます。  
  
-   **[評価]** オプションを選択すると、sum() などの XPath 関数を実装できます。  
  
-   **[ノード リスト]** オプションを選択すると、XML フラグメントとして選択したノードを返すことができます。  
  
-   **[値]** オプションを選択すると、文字列に連結されたノードのうち、選択したすべてのノードの内部のテキスト値を返すことができます。  
  
### <a name="validation-operation"></a>検証操作  
 検証操作は、文書型定義 (DTD) または XML スキーマ定義 (XSD) スキーマのどちらかを使用するように構成できます。  
  
 **ValidationDetails** を有効にして、詳細なエラー出力を取得します。 詳細については、「 [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)」を参照してください。  
  
## <a name="xml-document-encoding"></a>XML ドキュメントのエンコード  
 XML タスクでは、Unicode ドキュメントのマージのみがサポートされています。 つまり、このタスクによりマージ操作を適用できるのは、エンコードが Unicode のドキュメントのみです。 他のエンコードを使用すると、XML タスクが失敗する原因になります。  
  
> [!NOTE]  
>  Diff および Patch 操作には、2 番目のオペランドの XML データ内の XML 宣言を無視するオプションが含まれています。このオプションを使用すると、これらの操作で別のエンコードを持つドキュメントを使用できるようになります。  
  
 XML ドキュメントが使用できることを検証するには、XML 宣言を確認します。 この宣言では、エンコードが 8 ビット Unicode であることを示す UTF-8 が、明示的に指定されている必要があります。  
  
 次のタグは、エンコードが Unicode 8 ビットであることを示します。  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>XML タスクで使用できるカスタム ログ メッセージ  
 次の表では、XML タスクのカスタム ログ エントリを説明します。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**XMLOperation**|タスクで実行される操作に関する情報を提供します。|  
  
## <a name="configuration-of-the-xml-task"></a>XML タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [XML タスクを使った XML の検証](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>プログラムによる XML タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="xml-task-editor-general-page"></a>XML Task Editor (General Page)
  **[XML タスク エディター]** ダイアログ ボックスの **[全般]** ノードを使用すると、操作の種類を指定したり構成したりできます。  
  
 このタスクの詳細については、「[XML タスクを使った XML の検証](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)」をご覧ください。 XML ドキュメントとデータの操作の詳細については、MSDN ライブラリの「[.NET Framework における XML の使用](https://go.microsoft.com/fwlink/?LinkId=56214)」を参照してください。  
  
### <a name="static-options"></a>静的オプション  
 **[OperationType]**  
 一覧から操作の種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[検証]**|文書型定義 (DTD) または XML スキーマ定義 (XSD) スキーマに対して XML ドキュメントを検証します。 このオプションを選択すると、 **[Validate]** セクションに動的オプションが表示されます。|  
|**XSLT (XSLT)**|XML ドキュメントに対して XSL 変換を実行します。 このオプションを選択すると、 **[XSLT]** セクションに動的オプションが表示されます。|  
|**[XPath]**|XPath クエリと評価を実行します。 このオプションを選択すると、 **[Xpath]** セクションに動的オプションが表示されます。|  
|**Merge**|2 つの XML ドキュメントをマージします。 このオプションを選択すると、 **[Merge]** セクションに動的オプションが表示されます。|  
|**[Diff]**|2 つの XML ドキュメントを比較します。 このオプションを選択すると、 **[Diff]** セクションに動的オプションが表示されます。|  
|**[Patch]**|Diff 操作からの出力を適用して、新しいドキュメントを作成します。 このオプションを選択すると、 **[Patch]** セクションに動的オプションが表示されます。|  
  
 **[SourceType]**  
 XML ドキュメントのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **ソース**  
 **[ソース]** が **[直接入力]** に設定されている場合は、XML コードを指定するか、省略記号ボタン **[...]** をクリックしてから **[ドキュメント ソース エディター]** ダイアログ ボックスを使用して XML を指定します。  
  
 **[ソース]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[ソース]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[ **\<新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
### <a name="operationtype-dynamic-options"></a>[OperationType] の動的オプション  
  
#### <a name="operationtype--validate"></a>[OperationType] = [Validate]  
 Validate 操作用のオプションを指定します。  
  
 **[SaveOperationResult]**  
 XML タスクが Validate 操作の出力を保存するかどうかを指定します。  
  
 **[OverwriteDestination]**  
 対象となるファイルまたは変数を上書きするかどうかを指定します。  
  
 **変換先**  
 既存のファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[DestinationType]**  
 XML ドキュメントの対象となる種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[ValidationType]**  
 検証の種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[DTD]**|文書型定義 (DTD) を使用します。|  
|**[XSD]**|XML スキーマ定義 (XSD) スキーマを使用します。 このオプションを選択すると、 **[ValidationType]** セクションに動的オプションが表示されます。|  
  
 **[FailOnValidationFail]**  
 ドキュメントの検証に失敗した場合に、操作が失敗するかどうかを指定します。  
  
 **[ValidationDetails]**  
 このプロパティの値が true の場合は、詳細なエラー出力を表示します。 詳細については、「 [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)」を参照してください。  
  
### <a name="validationtype-dynamic-options"></a>[ValidationType] の動的オプション  
  
#### <a name="validationtype--xsd"></a>[ValidationType] = [XSD]  
 **[SecondOperandType]**  
 2 番目の XML ドキュメントのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperand]**  
 **[SecondOperandType]** が **[直接入力]** に設定されている場合は、XML コードを指定するか、省略記号ボタン **[...]** をクリックしてから **[ソース エディター]** ダイアログ ボックスを使用して XML を指定します。  
  
 **[SecondOperandType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[XPathStringSourceType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
#### <a name="operationtype--xslt"></a>[OperationType] = [XSLT]  
 XSLT 操作用のオプションを指定します。  
  
 **[SaveOperationResult]**  
 XML タスクが XSLT 操作の出力を保存するかどうかを指定します。  
  
 **[OverwriteDestination]**  
 対象となるファイルまたは変数を上書きするかどうかを指定します。  
  
 **変換先**  
 **[DestinationType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[DestinationType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
 **[DestinationType]**  
 XML ドキュメントの対象となる種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperandType]**  
 2 番目の XML ドキュメントのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperand]**  
 **[SecondOperandType]** が **[直接入力]** に設定されている場合は、XML コードを指定するか、省略記号ボタン **[...]** をクリックしてから **[ソース エディター]** ダイアログ ボックスを使用して XML を指定します。  
  
 **[SecondOperandType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[XPathStringSourceType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
#### <a name="operationtype--xpath"></a>[OperationType] = [XPath]  
 XPath 操作用のオプションを指定します。  
  
 **[SaveOperationResult]**  
 XML タスクが XPath 操作の出力を保存するかどうかを指定します。  
  
 **[OverwriteDestination]**  
 対象となるファイルまたは変数を上書きするかどうかを指定します。  
  
 **変換先**  
 **[DestinationType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[DestinationType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
 **[DestinationType]**  
 XML ドキュメントの対象となる種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperandType]**  
 2 番目の XML ドキュメントのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperand]**  
 **[SecondOperandType]** が **[直接入力]** に設定されている場合は、XML コードを指定するか、省略記号ボタン **[...]** をクリックしてから **[ソース エディター]** ダイアログ ボックスを使用して XML を指定します。  
  
 **[SecondOperandType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[XPathStringSourceType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
 **[PutResultInOneNode]**  
 結果を 1 つのノードに記述するかどうかを指定します。  
  
 **[XPathOperation]**  
 XPath の結果の種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**Evaluation**|XPath 関数の結果を返します。|  
|**[ノード リスト]**|選択されたノードを XML フラグメントとして返します。|  
|**値**|文字列に連結された、選択されたすべてのノードの内部テキスト値を返します。|  
  
#### <a name="operationtype--merge"></a>[OperationType] = [Merge]  
 Merge 操作用のオプションを指定します。  
  
 **[XPathStringSourceType]**  
 XML ドキュメントのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[XPathStringSource]**  
 **[XPathStringSourceType]** が **[直接入力]** に設定されている場合は、XML コードを指定するか、省略記号ボタン **[...]** をクリックしてから **[ドキュメント ソース エディター]** ダイアログ ボックスを使用して XML を指定します。  
  
 **[XPathStringSourceType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[XPathStringSourceType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 XPath ステートメントを使用してソース ドキュメント内でのマージ場所を特定すると、このステートメントによって 1 つのノードが返されます。 ステートメントによって複数のノードが返された場合は、最初のノードだけが使用されます。 2 番目のドキュメントの内容は、XPath クエリによって返される最初のノードでマージされます。  
  
 **[SaveOperationResult]**  
 XML タスクが Merge 操作の出力を保存するかどうかを指定します。  
  
 **[OverwriteDestination]**  
 対象となるファイルまたは変数を上書きするかどうかを指定します。  
  
 **変換先**  
 **[DestinationType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[DestinationType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
 **[DestinationType]**  
 XML ドキュメントの対象となる種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperandType]**  
 2 番目の XML ドキュメントの対象となる種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperand]**  
 **[SecondOperandType]** が **[直接入力]** に設定されている場合は、XML コードを指定するか、省略記号ボタン **[...]** をクリックしてから **[ドキュメント ソース エディター]** ダイアログ ボックスを使用して XML を指定します。  
  
 **[SecondOperandType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[SecondOperandType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--diff"></a>[OperationType] = [Diff]  
 Diff 操作用のオプションを指定します。  
  
 **[DiffAlgorithm]**  
 Diff アルゴリズムを選択して、文書を比較する場合に使用します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**Auto**|XML タスクに、高速アルゴリズムを使用するか、詳細アルゴリズムを使用するかを決定します。|  
|**[高速]**|高速ではあるが詳細ではない Diff アルゴリズムを使用します。|  
|**[詳細]**|詳細な Diff アルゴリズムを使用します。|  
  
 **[DiffOptions]**  
 Diff 操作に適用するための Diff オプションを設定します。 次の表に示すオプションがあります。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**[IgnoreXMLDeclaration]**|XML 宣言を比較するかどうかを指定します。|  
|**[IgnoreDTD]**|文書型定義 (DTD) を無視するかどうかを指定します。|  
|**[IgnoreWhiteSpaces]**|ドキュメントを比較するときに空白の量の違いを無視するかどうかを指定します。|  
|**[IgnoreNamespaces]**|要素名および属性名の名前空間の URI (Uniform Resource Identifier) を比較するかどうかを指定します。<br /><br /> 注:このオプションが **True** に設定されている場合、ローカル名が同じで、名前空間が異なる 2 つの要素は同一と見なされます。|  
|**[IgnoreProcessingInstructions]**|処理命令を比較するかどうかを指定します。|  
|**[IgnoreOrderOfChildElements]**|子の要素の順序を比較するかどうかを指定します。<br /><br /> 注:このオプションが **True** に設定されている場合、兄弟の一覧で位置のみが異なる子要素は同一と見なされます。|  
|**[IgnoreComments]**|コメント ノードを比較するかどうかを指定します。|  
|**[IgnorePrefixes]**|要素名および属性名のプレフィックスを比較するかどうかを指定します。<br /><br /> 注:このオプションが **True** に設定されている場合、ローカル名が同じで、名前空間 URI とプレフィックスが異なる 2 つの要素は同一と見なされます。|  
  
 **[FailOnDifference]**  
 Diff 操作が失敗した場合に、タスクが失敗するかどうかを指定します。  
  
 **[SaveDiffGram]**  
 比較結果である DiffGram ドキュメントを保存するかどうかを指定します。  
  
 **[SaveOperationResult]**  
 XML タスクが Diff 操作の出力を保存するかどうかを指定します。  
  
 **[OverwriteDestination]**  
 対象となるファイルまたは変数を上書きするかどうかを指定します。  
  
 **変換先**  
 **[DestinationType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[DestinationType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
 **[DestinationType]**  
 XML ドキュメントの対象となる種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperandType]**  
 XML ドキュメントの対象となる種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperand]**  
 **[SecondOperandType]** が **[直接入力]** に設定されている場合は、XML コードを指定するか、省略記号ボタン **[...]** をクリックしてから **[ドキュメント ソース エディター]** ダイアログ ボックスを使用して XML を指定します。  
  
 **[SecondOperandType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[SecondOperandType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--patch"></a>[OperationType] = [Patch]  
 Patch 操作用のオプションを指定します。  
  
 **[SaveOperationResult]**  
 XML タスクが Patch 操作の出力を保存するかどうかを指定します。  
  
 **[OverwriteDestination]**  
 対象となるファイルまたは変数を上書きするかどうかを指定します。  
  
 **変換先**  
 **[DestinationType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[DestinationType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
 **[DestinationType]**  
 XML ドキュメントの対象となる種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperandType]**  
 XML ドキュメントの対象となる種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[SecondOperand]**  
 **[SecondOperandType]** が **[直接入力]** に設定されている場合は、XML コードを指定するか、省略記号ボタン **[...]** をクリックしてから **[ドキュメント ソース エディター]** ダイアログ ボックスを使用して XML を指定します。  
  
 **[SecondOperandType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **[SecondOperandType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>関連コンテンツ  

-   [www.codeplex.com](www.codeplex.com) に掲載されている CodePlex サンプル「 [Process XML Data パッケージ サンプル](https://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples)」  
  
  
