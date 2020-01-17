---
title: スクリプト コンポーネント | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.scriptcomponentdetails.f1
- sql13.dts.designer.scriptcomponent.f1
- sql13.dts.designer.scriptcomponent.connections.f1
- sql13.dts.designer.scriptcomponent.inputcolumn.f1
- sql13.dts.designer.scriptcomponent.columnproperties.f1
- sql13.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a40336899e804ee634cf586078ec7c219f31c486
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297877"
---
# <a name="script-component"></a>スクリプト コンポーネント

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  スクリプト コンポーネントはスクリプトをホストします。これにより、パッケージにカスタム スクリプト コードを含めて実行できます。 スクリプト コンポーネントは、パッケージ内で次の目的に使用できます。  
  
-   複数の変換をデータ フロー内で使用する代わりに、複数の変換をデータに適用します。 たとえば、スクリプトによって 2 つの列に値を追加し、その合計の平均を計算できます。  
  
-   既存の .NET アセンブリのビジネス ルールにアクセスします。 たとえば、スクリプトによって **Income** 列で有効な値の範囲を指定するビジネス ルールを適用できます。  
  
-   [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 式の文法で定められた関数や演算子以外のカスタム式とカスタム関数を使用します。 たとえば、LUHN 式を使用して、クレジット カード番号を検証します。  
  
-   列データを検証し、無効なデータを含むレコードをスキップします。 たとえば、スクリプトを使用すると、郵送料が妥当かどうかを査定して、極端に高い場合や極端に安い場合にレコードをスキップできます。  
  
 スクリプト コンポーネントを使用すると、カスタム関数をデータ フローへ簡単、迅速に含めることができます。 ただし、複数のパッケージでスクリプト コードを再利用する場合、スクリプト コンポーネントを使用するのではなく、カスタム コンポーネントをプログラムすることをお勧めします。 詳細については、「 [カスタム データ フロー コンポーネントの開発](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」を参照してください。  
  
> [!NOTE]  
>  スクリプト コンポーネントに値が NULL である列の読み取りを試みるスクリプトが含まれる場合は、パッケージを実行すると、スクリプト コンポーネントが失敗します。 スクリプトでは <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.IsNull%2A> メソッドを使用して、列の値の読み取りを試みる前に列が NULL かどうかを判断することをお勧めします。  
  
 スクリプト コンポーネントは、変換元、変換、または変換先として使用できます。 このコンポーネントは、1 つの入力と複数の出力をサポートします。 コンポーネントの使用方法に応じて、入力または出力のどちらか、またはその両方がサポートされます。 スクリプトは、入力または出力の列ごとに起動します。  
  
-   スクリプト コンポーネントを変換元として使用する場合、複数の出力がサポートされます。  
  
-   スクリプト コンポーネントを変換として使用する場合、1 つの入力と複数の出力がサポートされます。  
  
-   スクリプト コンポーネントを変換先として使用する場合、1 つの入力がサポートされます。  
  
 スクリプト コンポーネントでは、エラー出力はサポートされていません。  
  
 スクリプト コンポーネントがパッケージにとって適切な選択である場合、入力と出力を構成し、コンポーネントが使用するスクリプトを開発して、コンポーネント自体を構成する必要があります。  
  
## <a name="understanding-the-script-component-modes"></a>スクリプト コンポーネントのモードについて  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでは、スクリプト コンポーネントにメタデータ デザイン モードとコード デザイン モードの 2 つのモードがあります。 メタデータ デザイン モードでは、スクリプト コンポーネントの入力と出力を追加および変更できますが、コードは記述できません。 すべての入力と出力を構成した後に、コード デザイン モードに切り替え、スクリプトを記述します。 スクリプト コンポーネントは、入力と出力のメタデータから、基本コードを自動的に生成します。 スクリプト コンポーネントで基本コードを生成した後にメタデータを変更すると、更新された基本コードと互換性がない可能性があるため、記述したコードをコンパイルできないことがあります。  
  
## <a name="writing-the-script-that-the-component-uses"></a>コンポーネントが使用するスクリプトの記述  
 スクリプト コンポーネントでは、スクリプトを記述する環境として [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) を使用します。 **スクリプト変換エディター**から VSTA にアクセスします。 詳細については、「 [スクリプト変換エディター ([スクリプト] ページ)](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)」を参照してください。  
  
 スクリプト コンポーネントでは、コンポーネントのメタデータを表す、ScriptMain という名前の自動生成クラスが含まれる VSTA プロジェクトが用意されています。 たとえば、スクリプト コンポーネントを 3 つの出力を持つ変換として使用する場合、ScriptMain には各出力のメソッドが含まれます。 ScriptMain は、スクリプトに対するエントリ ポイントです。  
  
 VSTA には、色分け表示が可能な [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] エディター、IntelliSense、オブジェクト ブラウザーなど、 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 環境での標準機能がすべて含まれています。 スクリプト コンポーネントが使用するスクリプトは、パッケージ定義に格納されます。 パッケージをデザインする際、スクリプト コードは一時的にプロジェクト ファイルに書き込まれます。  
  
 VSTA では、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# と [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic の両方のプログラミング言語がサポートされます。  
  
 スクリプト コンポーネントのプログラミング方法の詳細については、「 [スクリプト コンポーネントによるデータ フローの拡張](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。 スクリプト コンポーネントを変換元、変換、または変換先として構成する方法の詳細については、「 [特定の種類のスクリプト コンポーネントの開発](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)」を参照してください。 ODBC 変換先など、スクリプト コンポーネントの使用法を示すその他の例については、「 [その他のスクリプト コンポーネントの例](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)」を参照してください。  
  
> [!NOTE]  
>  スクリプトをプリコンパイルするかどうかを指定できた以前のバージョンとは異なり、 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 以降のバージョンではすべてのスクリプトがプリコンパイルされます。 スクリプトがプリコンパイルされると、実行時に言語エンジンを読み込まないため、パッケージの実行速度が向上します。 ただし、コンパイル済みのバイナリ ファイルは多量のディスク領域を使用します。  
  
## <a name="configuring-the-script-component"></a>スクリプト コンポーネントの構成  
 スクリプト コンポーネントは、次の方法で構成できます。  
  
-   参照する入力列を選択します。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーを使用する場合、入力は 1 つのみ構成できます。  
  
-   コンポーネントが実行するスクリプトを指定します。  
  
-   スクリプト言語を指定します。  
  
-   読み取り専用変数と読み取り/書き込み変数を、コンマで区切られた一覧にして指定します。  
  
-   出力を追加し、スクリプトが値を割り当てる出力列を追加します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
### <a name="configuring-the-script-component-in-the-designer"></a>デザイナーでのスクリプト コンポーネントの構成  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>プログラムによるスクリプト コンポーネントの構成  
 **[プロパティ]** ウィンドウまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="select-script-component-type"></a>[スクリプト コンポーネントの種類を選択]
  **[スクリプト コンポーネントの種類を選択]** ダイアログ ボックスを使用すると、変換元、変換、または変換先として構成済みのスクリプト変換を作成するかどうかを指定できます。  
  
 スクリプト コンポーネントの詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)」を参照してください。 スクリプト コンポーネントのプログラミングの詳細については、「 [スクリプト コンポーネントによるデータ フローの拡張](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。  
  
### <a name="options"></a>および  
 **[変換元]** 、 **[変換先]** 、または **[変換]** のどれを選択するかに応じて、スクリプト変換の構成とスクリプト変換エディターのページが変わります。  
  
## <a name="script-transformation-editor-connection-managers-page"></a>[スクリプト変換エディター] ([接続マネージャー] ページ)
  **[スクリプト変換エディター]** の **[接続マネージャー]** ページを使用すると、スクリプトで使用される接続を指定できます。  
  
 スクリプト コンポーネントの詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)」を参照してください。 スクリプト コンポーネントのプログラミングの詳細については、「 [スクリプト コンポーネントによるデータ フローの拡張](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。  
  
### <a name="options"></a>および  
 **Connection managers**  
 スクリプトで使用できる接続の一覧を表示します。  
  
 **名前**  
 接続を表す一意な名前を入力します。  
  
 **接続マネージャー**  
 使用できる接続マネージャーの一覧から選択するか、[ **\<新しい接続>** ] を選択して **[SSIS 接続マネージャーの追加]** ダイアログ ボックスを開きます。  
  
 **[説明]**  
 接続の説明を入力します。  
  
 **[追加]**  
 **[接続マネージャー]** の一覧に、他の接続を追加します。  
  
 **[削除]**  
 **[接続マネージャー]** の一覧から、選択した接続を削除します。  
  
## <a name="script-transformation-editor-input-columns-page"></a>[スクリプト変換エディター] ([入力列] ページ)
  **[スクリプト変換エディター]** ダイアログ ボックスの **[入力列]** ページを使用すると、入力列のプロパティを設定できます。  
  
> [!NOTE]  
>  ソース コンポーネントでは、出力はあっても入力はないため、 **[入力列]** ページはソース コンポーネントには表示されません。  
  
 スクリプト コンポーネントの詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)」を参照してください。 スクリプト コンポーネントのプログラミングの詳細については、「 [スクリプト コンポーネントによるデータ フローの拡張](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。  
  
### <a name="options"></a>および  
 **[入力名]**  
 使用できる入力の一覧から選択します。  
  
 **使用できる入力列**  
 チェック ボックスを使用して、スクリプト変換に使用する列を指定します。  
  
 **入力列**  
 各行に対して使用できる入力列の一覧から選択します。 選択内容が **[使用できる入力列]** テーブルのチェック ボックスに反映されます。  
  
 **[出力の別名]**  
 各出力列の別名を入力します。 既定は入力列の名前です。一意のわかりやすい名前を付けることもできます。  
  
 **[使用法の種類]**  
 スクリプト変換で各列を **ReadOnly** または **ReadWrite**として扱うかどうかを指定します。  
  
## <a name="script-transformation-editor-inputs-and-outputs-page"></a>[スクリプト変換エディター] ([入力および出力] ページ)
  **[スクリプト変換エディター]** ダイアログ ボックスの **[入力および出力]** ページを使用すると、スクリプト変換の入力および出力を追加、削除、構成できます。  
  
> [!NOTE]  
>  基になるコンポーネントには出力はありますが、入力はありません。変換先のコンポーネントには入力はありますが、出力はありません。 変換には入力と出力の両方があります。  
  
 スクリプト コンポーネントの詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)」を参照してください。 スクリプト コンポーネントのプログラミングの詳細については、「 [スクリプト コンポーネントによるデータ フローの拡張](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。  
  
### <a name="options"></a>および  
 **Inputs and outputs**  
 左側で入力または出力を選択すると、右側の表にプロパティが表示されます。 編集に使用できるプロパティは、選択内容によって異なります。 表示されるプロパティの多くは読み取り専用です。 各プロパティの詳細については、次のトピックを参照してください。  
  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 **[出力の追加]**  
 追加の出力を一覧に追加します。  
  
 **[列の追加]**  
 新しい出力列を格納するフォルダーを選択して **[列の追加]** をクリックすると、列が追加されます。  
  
 **[出力の削除]**  
 出力を選択した後、 **[出力の削除]** をクリックするとその出力が削除されます。  
  
 **[列の削除]**  
 列を選択した後、 **[列の削除]** をクリックするとその列が削除されます。  
  
## <a name="script-transformation-editor-script-page"></a>[スクリプト変換エディター] ([スクリプト] ページ)
  **[スクリプト変換エディター]** ダイアログ ボックスの **[スクリプト]** タブを使用すると、スクリプトおよび関連プロパティを指定できます。  
  
 スクリプト コンポーネントの詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)」を参照してください。 スクリプト コンポーネントのプログラミングの詳細については、「 [スクリプト コンポーネントによるデータ フローの拡張](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。  
  
### <a name="options"></a>および  
 **[プロパティ]**  
 スクリプト変換のプロパティを表示および変更します。 表示されるプロパティの多くは読み取り専用です。 以下のプロパティを変更できます。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**[説明]**|スクリプト変換の目的を記述します。|  
|**LocaleID**|ロケールを指定して、順序付けおよび日時の変換に関する地域固有の情報を提供します。|  
|**名前**|わかりやすいコンポーネント名を入力します。|  
|**[ValidateExternalMetadata]**|スクリプト変換において、デザイン時に外部データ ソースに対して列のメタデータを検証するかどうかを示します。 値 **false** を設定した場合、検証は実行時まで延期されます。|  
|**[ReadOnlyVariables]**|スクリプト変換が読み取り専用でアクセスする変数の、コンマ区切りの一覧を入力します。<br /><br /> 注:変数名の大文字と小文字は区別されます。|  
|**[ReadWriteVariables]**|スクリプト変換が読み取り/書き込み用にアクセスする変数の、コンマ区切りの一覧を入力します。<br /><br /> 注:変数名の大文字と小文字は区別されます。|  
|**[ScriptLanguage]**|スクリプト コンポーネントが使用するスクリプト言語を選択します。<br /><br /> スクリプト コンポーネントとスクリプト タスクの既定のスクリプト言語を設定するには、 **[オプション]** ダイアログ ボックスの **[全般]** ページにある **[スクリプト言語]** オプションを使用します。|  
|**[UserComponentTypeName]**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インフラストラクチャをサポートする <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> クラスと **Microsoft.SqlServer.TxScript** アセンブリを指定します。|  
  
 **[スクリプトの編集]**  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) を使用して、スクリプトを作成または変更します。  
  
## <a name="related-content"></a>関連コンテンツ  
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
 [スクリプト コンポーネントによるデータ フローの拡張](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
  
  
