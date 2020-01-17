---
title: スクリプト コンポーネント | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scriptcomponentdetails.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d9a601a710531aa6905f35a2fe5ca7f02a9177f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770681"
---
# <a name="script-component"></a>スクリプト コンポーネント
  スクリプト コンポーネントはスクリプトをホストします。これにより、パッケージにカスタム スクリプト コードを含めて実行できます。 スクリプト コンポーネントは、パッケージ内で次の目的に使用できます。  
  
-   複数の変換をデータ フロー内で使用する代わりに、複数の変換をデータに適用します。 たとえば、スクリプトによって 2 つの列に値を追加し、その合計の平均を計算できます。  
  
-   既存の .NET アセンブリのビジネス ルールにアクセスします。 たとえば、スクリプトによって `Income` 列で有効な値の範囲を指定するビジネス ルールを適用できます。  
  
-   [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 式の文法で定められた関数や演算子以外のカスタム式とカスタム関数を使用します。 たとえば、LUHN 式を使用して、クレジット カード番号を検証します。  
  
-   列データを検証し、無効なデータを含むレコードをスキップします。 たとえば、スクリプトを使用すると、郵送料が妥当かどうかを査定して、極端に高い場合や極端に安い場合にレコードをスキップできます。  
  
 スクリプト コンポーネントを使用すると、カスタム関数をデータ フローへ簡単、迅速に含めることができます。 ただし、複数のパッケージでスクリプト コードを再利用する場合、スクリプト コンポーネントを使用するのではなく、カスタム コンポーネントをプログラムすることをお勧めします。 詳細については、「 [カスタム データ フロー コンポーネントの開発](../../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」を参照してください。  
  
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
 スクリプト コンポーネントでは、スクリプトを記述する環境として [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) を使用します。 **スクリプト変換エディター**から VSTA にアクセスします。 詳細については、「 [スクリプト変換エディター ([スクリプト] ページ)](../../script-transformation-editor-script-page.md)」を参照してください。  
  
 スクリプト コンポーネントでは、コンポーネントのメタデータを表す、ScriptMain という名前の自動生成クラスが含まれる VSTA プロジェクトが用意されています。 たとえば、スクリプト コンポーネントを 3 つの出力を持つ変換として使用する場合、ScriptMain には各出力のメソッドが含まれます。 ScriptMain は、スクリプトに対するエントリ ポイントです。  
  
 VSTA には、色分け表示が可能な [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] エディター、IntelliSense、オブジェクト ブラウザーなど、 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 環境での標準機能がすべて含まれています。 スクリプト コンポーネントが使用するスクリプトは、パッケージ定義に格納されます。 パッケージをデザインする際、スクリプト コードは一時的にプロジェクト ファイルに書き込まれます。  
  
 VSTA では、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# と [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic の両方のプログラミング言語がサポートされます。  
  
 スクリプト コンポーネントのプログラミング方法の詳細については、「 [スクリプト コンポーネントによるデータ フローの拡張](script-component.md)」を参照してください。 スクリプト コンポーネントを変換元、変換、または変換先として構成する方法の詳細については、「 [特定の種類のスクリプト コンポーネントの開発](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)」を参照してください。 ODBC 変換先など、スクリプト コンポーネントの使用法を示すその他の例については、「 [その他のスクリプト コンポーネントの例](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)」を参照してください。  
  
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
 **[スクリプト変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [スクリプト変換エディター ([入力列] ページ)](../../script-transformation-editor-input-columns-page.md)  
  
-   [スクリプト変換エディター ([入力および出力] ページ)](../../script-transformation-editor-inputs-and-outputs-page.md)  
  
-   [スクリプト変換エディター ([スクリプト] ページ)](../../script-transformation-editor-script-page.md)  
  
-   [スクリプト変換エディター ([接続マネージャー] ページ)](../../script-transformation-editor-connection-managers-page.md)  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>プログラムによるスクリプト コンポーネントの構成  
 **[プロパティ]** ウィンドウまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [Integration Services の変換](integration-services-transformations.md)  
  
 [スクリプト コンポーネントによるデータ フローの拡張](script-component.md)  
  
  
