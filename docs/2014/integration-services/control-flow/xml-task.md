---
title: XML タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e89f4835b95b1fe497df32ad9f773be84ccb161b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232725"
---
# <a name="xml-task"></a>XML タスク
  XML タスクは、XML データの処理に使用します。 このタスクを使用すると、パッケージは、XML ドキュメントの取得、Extensible Stylesheet Language Transformations (XSLT) スタイル シートや XPath 式の使用によるドキュメントへの操作の適用、複数ドキュメントのマージ、または更新したドキュメントの検証、比較、およびファイルや変数への保存を行うことができます。  
  
 このタスクを使用すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、XML ドキュメントを実行時に動的に変更できます。 XML タスクは、次の目的で使用できます。  
  
-   XML ドキュメントを再フォーマットする。 たとえば、このタスクは、XML ファイル内に存在するレポートにアクセスし、XSLT スタイル シートを動的に適用してドキュメントの表示形式をカスタマイズできます。  
  
-   XML ドキュメントのセクションを選択する。 たとえば、このタスクは、XML ファイル内に存在するレポートにアクセスし、XPath 式を動的に適用してドキュメントのセクションを選択できます。 この操作により、ドキュメント内の値を取得して処理することもできます。  
  
-   多くの変換元からドキュメントをマージする。 たとえば、このタスクは複数の変換元からレポートをダウンロードし、1 つの包括的な XML ドキュメントに動的にマージできます。  
  
-   XML ドキュメントを検証し、必要に応じて詳細なエラー出力を取得します。 詳細については、「 [Validate XML with the XML Task](xml-task.md)」を参照してください。  
  
 XML ソースを使用して XML ドキュメントの値を抽出し、データ フロー内に XML データを含めることができます。 詳細については、「 [XML ソース](../data-flow/xml-source.md)」を参照してください。  
  
## <a name="xml-operations"></a>XML 操作  
 XML タスクが実行する最初のアクションは、特定の XML ドキュメントの取得です。 このアクションは XML タスクに組み込まれており、自動的に発生します。 取得した XML ドキュメントは、XML タスクが実行する操作においてデータの変換元として使用されます。  
  
 XML 操作である Diff、Merge、および Patch には、2 つのオペランドが必要です。 最初のオペランドは、XML ソース ドキュメントを指定します。 2 番目のオペランドも XML ドキュメントを指定しますが、その内容は操作の必要条件に応じて変化します。 たとえば、Diff 操作では 2 つのドキュメントを比較します。したがって、2 番目のオペランドは、XML ソース ドキュメントの比較対象となる、類似した別の XML ドキュメントを指定します。  
  
 XML タスクは、変数またはファイル接続マネージャーをその変換元として使用できます。または、XML データをタスクのプロパティに含めることができます。  
  
 変換元が変数の場合、指定した変数には、XML ドキュメントのパスが含まれます。  
  
 変換元がファイル接続マネージャーの場合、指定したファイル接続マネージャーは変換元の情報を提供します。 ファイル接続マネージャーは、XML タスクとは別に構成され、XML タスク内で参照されます。 ファイル接続マネージャーの接続文字列は、XML ファイルのパスを指定します。 詳細については、「 [File Connection Manager](../connection-manager/file-connection-manager.md)」を参照してください。  
  
 XML タスクは、操作の結果を変数またはファイルに保存するように構成できます。 ファイルに保存する場合、XML タスクはファイル接続マネージャーを使用して、そのファイルにアクセスします。 また、Diff 操作によって生成された DiffGram の結果を、ファイルや変数に保存することもできます。  
  
## <a name="predefined-xml-operations"></a>定義済み XML 操作  
 XML タスクには、XML ドキュメントを処理するための定義済み操作のセットが含まれています。 次の表では、これらの操作について説明します。  
  
|Operation|説明|  
|---------------|-----------------|  
|[Diff]|2 つの XML ドキュメントを比較します。 XML ソース ドキュメントを基本ドキュメントとして使用し、Diff 操作は、そのドキュメントを 2 番目の XML ドキュメントと比較し、それらの違いを検出して XML DiffGram ドキュメントに書き込みます。 この操作には、比較をカスタマイズするためのプロパティが含まれています。|  
|［結合］|2 つの XML ドキュメントをマージします。 マージ操作は、XML ソース ドキュメントを基本ドキュメントとして使用し、2 番目のドキュメントの内容を基本ドキュメントに追加します。 この操作では、基本ドキュメント内のマージ場所を指定できます。|  
|修正プログラム|DiffGram ドキュメントと呼ばれる Diff 操作の出力を XML ドキュメントに適用し、DiffGram ドキュメントの内容を含む新しい親ドキュメントを作成します。|  
|[検証]|文書型定義 (DTD) または XML スキーマ定義 (XSD) スキーマに対して XML ドキュメントを検証します。|  
|XPath|XPath クエリと評価を実行します。|  
|XSLT (XSLT)|XML ドキュメントに対して XSL 変換を実行します。|  
  
### <a name="diff-operation"></a>Diff 操作  
 Diff 操作は、比較を高速で行うか詳細に行うかに応じて、異なる比較アルゴリズムを使用するように構成できます。 また、比較するドキュメントのサイズに基づいて、高速比較を行うか詳細比較を行うかを自動的に選択するように、構成することもできます。  
  
 Diff 操作には、XML 比較をカスタマイズするオプションのセットが含まれています。 次の表では、このオプションについて説明します。  
  
|オプション|説明|  
|------------|-----------------|  
|**IgnoreComments**|この値で、コメント ノードを比較するかどうかを指定します。|  
|**IgnoreNamespaces**|この値で、要素名および属性名の名前空間の Uniform Resource Identifier (URI) を比較するかどうかを指定します。 このオプションを `true` に設定した場合、ローカル名が同じで、異なる名前空間を持つ 2 つの要素は、同一と見なされます。|  
|**IgnorePrefixes**|この値で、要素名および属性名のプレフィックスを比較するかどうかを指定します。 このオプションを `true,` に設定した場合、ローカル名が同じで、異なる名前空間 URI とプレフィックスを持つ 2 つの要素は、同一と見なされます。|  
|**IgnoreXMLDeclaration**|この値で、XML 宣言を比較するかどうかを指定します。|  
|**IgnoreOrderOfChildElements**|この値で、子要素の順序を比較するかどうかを指定します。 このオプションを `true` に設定した場合、兄弟の一覧での位置だけが異なる子要素は同一と見なされます。|  
|**IgnoreWhiteSpaces 文字**|この値で、空白を比較するかどうかを指定します。|  
|**IgnoreProcessingInstructions**|この値で、処理命令を比較するかどうかを指定します。|  
|**IgnoreDTD**|この値で、DTD を無視するかどうかを指定します。|  
  
### <a name="merge-operation"></a>マージ操作  
 XPath ステートメントを使用してソース ドキュメント内でのマージ場所を特定すると、このステートメントによって 1 つのノードが返されます。 ステートメントによって複数のノードが返された場合は、最初のノードだけが使用されます。 2 番目のドキュメントの内容は、XPath クエリによって返される最初のノードでマージされます。  
  
### <a name="xpath-operation"></a>XPath 操作  
 XPath 操作は、XPath のさまざまな種類の機能を使用するように構成できます。  
  
-   
  **[評価]** オプションを選択すると、sum() などの XPath 関数を実装できます。  
  
-   
  **[ノード リスト]** オプションを選択すると、XML フラグメントとして選択したノードを返すことができます。  
  
-   
  **[値]** オプションを選択すると、文字列に連結されたノードのうち、選択したすべてのノードの内部のテキスト値を返すことができます。  
  
### <a name="validation-operation"></a>検証操作  
 検証操作は、文書型定義 (DTD) または XML スキーマ定義 (XSD) スキーマのどちらかを使用するように構成できます。  
  
 
  `ValidationDetails` を有効にして、詳細なエラー出力を取得します。 詳細については、「 [Validate XML with the XML Task](xml-task.md)」を参照してください。  
  
## <a name="xml-document-encoding"></a>XML ドキュメントのエンコード  
 XML タスクでは、Unicode ドキュメントのマージのみがサポートされています。 つまり、このタスクによりマージ操作を適用できるのは、エンコードが Unicode のドキュメントのみです。 他のエンコードを使用すると、XML タスクが失敗する原因になります。  
  
> [!NOTE]  
>  Diff および Patch 操作には、2 番目のオペランドの XML データ内の XML 宣言を無視するオプションが含まれています。このオプションを使用すると、これらの操作で別のエンコードを持つドキュメントを使用できるようになります。  
  
 XML ドキュメントが使用できることを検証するには、XML 宣言を確認します。 この宣言では、エンコードが 8 ビット Unicode であることを示す UTF-8 が、明示的に指定されている必要があります。  
  
 次のタグは、エンコードが Unicode 8 ビットであることを示します。  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>XML タスクで使用できるカスタム ログ メッセージ  
 次の表では、XML タスクのカスタム ログ エントリを説明します。 詳細については、「[Integration Services (SSIS) のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」を参照してください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`XMLOperation`|タスクで実行される操作に関する情報を提供します。|  
  
## <a name="configuration-of-the-xml-task"></a>XML タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[XML タスクエディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [XML タスクを使用した XML の検証](xml-task.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>プログラムによる XML タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   agilebi.com のブログ「 [XML 変換先スクリプト コンポーネント](http://agilebi.com/jwelch/2007/06/02/xml-destination-script-component/)」  
  
-   [www.codeplex.com](www.codeplex.com) に掲載されている CodePlex サンプル「 [Process XML Data パッケージ サンプル](https://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples)」  
  
