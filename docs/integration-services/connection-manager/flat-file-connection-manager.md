---
title: "フラット ファイル接続マネージャー |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.ffileconnection.general.f1
- sql13.dts.designer.ffileconnection.columns.f1
- sql13.dts.designer.ffileconnection.columnproperties.f1
- sql13.dts.designer.ffileconnection.preview.f1
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 2b3f4c303b1d60cbbe23c639c36a6336ca07447f
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="flat-file-connection-manager"></a>フラット ファイル接続マネージャー
  フラット ファイル接続マネージャーを使用すると、パッケージはフラット ファイルのデータにアクセスできます。 たとえば、フラット ファイルの変換元と変換先は、フラット ファイル接続マネージャーを使用して、データの抽出および読み込みを行うことができます。  
  
 フラット ファイル接続マネージャーがアクセスできるファイルは、1 つだけです。 複数のファイルを参照するには、フラット ファイル接続マネージャーではなく、複数フラット ファイル接続マネージャーを使用します。 詳細については、「 [複数フラット ファイル接続マネージャー](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)」を参照してください。  
  
## <a name="column-length"></a>列の長さ  
 フラット ファイル接続マネージャーでは、文字列型の列の長さが既定で 50 文字に設定されています。 **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスでは、サンプル データを評価し、これらの列の長さを自動的に変更して、データが切り捨てられたり、列の幅が広すぎたりしないようにできます。 また、その後にフラット ファイル ソースまたは変換で列の長さを変更しない限り、データ フロー全体をとおして文字列型の列の長さは一定です。 これらの文字列型の列が、変換先として幅の狭い列にマップされた場合、ユーザー インターフェイスに警告が表示されます。 さらに、実行時にデータの切り捨てによるエラーが発生する場合があります。 エラーや切り捨てが発生しないように、フラット ファイル接続マネージャー、フラット ファイル ソース、または変換で、変換先列に合うように列のサイズを変更することができます。 出力列の長さを変更するには、 **[詳細エディター]** ダイアログ ボックスの **[入力プロパティと出力プロパティ]** タブで、出力列の **Length** プロパティを設定します。  
  
 接続マネージャーを使用するフラット ファイル ソースを追加および構成した後に、フラット ファイル接続マネージャーで列の長さを変更した場合は、フラット ファイル ソースの出力列のサイズを手動で変更する必要はありません。 **[フラット ファイル ソース]** ダイアログ ボックスを開くと、列のメタデータを同期するためのオプションがフラット ファイル ソースによって提供されます。  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>フラット ファイル接続マネージャーの構成  
 フラット ファイル接続マネージャーをパッケージに追加すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、実行時にフラット ファイル接続を解決する接続マネージャーを作成し、フラット ファイル接続プロパティを設定して、フラット ファイル接続マネージャーをパッケージの **Connections** コレクションに追加します。  
  
 接続マネージャーの **ConnectionManagerType** プロパティは、 **FLATFILE**に設定されます。  
  
 既定では、フラット ファイル接続マネージャーは、引用符で囲まれていないデータの行区切り記号を常に確認し、行区切り記号が見つかると新しい行を開始します。 これにより、接続マネージャーは列フィールドがない行を含むファイルを正しく解析できます。  
  
 場合によっては、この機能を無効にすると、パッケージのパフォーマンスが向上します。 この機能を無効にするには、フラット ファイル接続マネージャーのプロパティである **AlwaysCheckForRowDelimiters**を **False**に設定します。  
  
 フラット ファイル接続マネージャーは、次の方法で構成できます。  
  
-   使用するファイル、ロケール、およびコード ページを指定します。 ロケールは、日付など、ロケール依存型のデータの解釈に使用されます。コード ページは、文字列データを Unicode に変換するために使用されます。  
  
-   ファイル形式を指定します。 区切られた形式、固定幅形式、または幅合わせしない形式が使用できます。  
  
-   ヘッダー行、データ行、および列の区切り記号を指定します。 列の区切り記号は、ファイル レベルで設定し、列レベルで上書きできます。  
  
-   ファイルの最初の行に列の名前が含まれるかどうかを示します。  
  
-   テキスト修飾子文字を指定します。 各列は、テキスト修飾子を認識するように構成できます。  
  
     フラット ファイル接続マネージャーでは、修飾子文字を使用して、修飾される文字列に修飾子文字を埋め込むことができます。 テキスト修飾子の二重インスタンスは、1 つのリテラル、つまりその文字列の 1 つのインスタンスとして解釈されます。 たとえば、テキスト修飾子が単一引用符で、入力データが 'abc'、'def'、'g'hi' の場合、出力データは abc、def、g'hi になります。 ただし、修飾文字列に埋め込まれた修飾子のインスタンスが原因で、フラット ファイル ソースは DTS_E_PRIMEOUTPUTFAILED エラーで失敗します。
  
-   各列の名前、データ型、最大幅などのプロパティを設定します。  
  
 フラット ファイル接続マネージャーの ConnectionString プロパティは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の [プロパティ] ウィンドウで式を指定することで設定できます。 検証エラーを回避するには、次の操作を行います。  
  
-   式を使用してファイルを指定する場合は、 **[フラット ファイル接続マネージャー エディター]** の **[ファイル名]**ボックスにファイル パスを追加します。  
  
-   フラット ファイル接続マネージャーの **DelayValidation** プロパティを **True**に設定します。  
  
 フラット ファイルの変換先に対してフラット ファイル接続マネージャーを使用することにより、実行時に式を使用してファイル名を作成できます。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="flat-file-connection-manager-editor-general-page"></a>[フラット ファイル接続マネージャー エディター] ([全般] ページ)
  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、ファイルおよびデータ形式を選択できます。 フラット ファイル接続により、パッケージをテキスト ファイルに接続できるようになります。  
  
 フラット ファイル接続マネージャーの詳細については、「 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[接続マネージャー名]**  
 ワークフローにおけるフラット ファイル接続の一意な名前を指定します。 指定された名前は、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **Description**  
 接続の説明を記述します。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、接続の目的について記述することをお勧めします。  
  
 **ファイル名**  
 フラット ファイル接続で使用するパスおよびファイル名を入力します。  
  
 **参照**  
 フラット ファイル接続で使用するファイル名を探します。  
  
 **ロケール**  
 ロケールを指定して、順序付けおよび日時の形式に関する言語固有の情報を提供します。  
  
 **Unicode**  
 Unicode を使用するかどうかを示します。 Unicode を使用する場合は、コード ページを指定できません。  
  
 **コード ページ**  
 非 Unicode テキストのコード ページを指定します。  
  
 **Format**  
 区切り記号形式、固定幅形式、または幅合わせしない形式をファイルで使用するかどうかを示します。  
  
|値|Description|  
|-----------|-----------------|  
|[区切り記号]|列は、 **[列]** ページで指定した区切り記号で区切られます。|  
|[固定幅]|列は固定幅を持ちます。|  
|[幅合わせしない]|幅合わせしない形式のファイルとは、最後の列を除くすべての列が固定幅のファイルです。 最後の列は、行区切り記号で区切られます。|  
  
 **テキスト修飾子**  
 使用するテキスト修飾子を指定します。 たとえば、テキスト フィールドを引用符で囲むことを指定できます。  
  
> [!NOTE]  
>  テキスト修飾子を選択した後で、 **[なし]** オプションを再度選択することはできません。 テキスト修飾子の選択を解除するには、「 **なし** 」と入力します。  
  
 **[ヘッダー行区切り記号]**  
 ヘッダー行の区切り記号の一覧から選択するか、区切り記号テキストを入力します。  
  
|値|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|ヘッダー行は、復帰と改行の組み合わせで区切られます。|  
|**{CR}**|ヘッダー行は、復帰で区切られます。|  
|**{LF}**|ヘッダー行は、改行で区切られます。|  
|**[セミコロン {;}]**|ヘッダー行は、セミコロンで区切られます。|  
|**[コロン {:}]**|ヘッダー行は、コロンで区切られます。|  
|**[コンマ {,}]**|ヘッダー行は、コンマで区切られます。|  
|**[タブ {t}]**|ヘッダー行は、タブで区切られます。|  
|**[縦棒 {&#124;}]**|ヘッダー行は、縦棒で区切られます。|  
  
 **[スキップするヘッダー行数]**  
 必要に応じて、スキップするヘッダー行数または初期データ行数を指定します。  
  
 **[先頭データ行を列名として使用する]**  
 先頭データ行を列名として使用するか、ここに列名を指定するかを示します。  
## <a name="flat-file-connection-manager-editor-columns-page"></a>[フラット ファイル接続マネージャー エディター] ([列] ページ)
  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスの **[列]** ページを使用すると、行および列情報を指定したり、ファイルをプレビューしたりできます。  
  
 フラット ファイル接続マネージャーの詳細については、「 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)」を参照してください。  
  
### <a name="static-options"></a>静的オプション  
 **[接続マネージャー名]**  
 ワークフローにおけるフラット ファイル接続マネージャーの一意な名前を指定します。 指定された名前は、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **Description**  
 接続の説明を記述します。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、接続の目的について記述することをお勧めします。  
  
### <a name="flat-file-format-dynamic-options"></a>フラット ファイル形式の動的オプション  
  
#### <a name="format--delimited"></a>[形式] = [区切り記号]  
 **[行区切り記号]**  
 使用できる行区切り記号の一覧から選択するか、区切り記号テキストを入力します。  
  
|値|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|行は、復帰と改行の組み合わせで区切られます。|  
|**{CR}**|行は、復帰で区切られます。|  
|**{LF}**|行は、改行で区切られます。|  
|**[セミコロン {;}]**|行は、セミコロンで区切られます。|  
|**[コロン {:}]**|行は、コロンで区切られます。|  
|**[コンマ {,}]**|行は、コンマで区切られます。|  
|**[タブ {t}]**|行は、タブで区切られます。|  
|**[縦棒 {&#124;}]**|行は、縦棒で区切られます。|  
  
 **列区切り記号**  
 使用できる列区切り記号の一覧から選択するか、区切り記号テキストを入力します。  
  
|値|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|列は、復帰と改行の組み合わせで区切られます。|  
|**{CR}**|列は、復帰で区切られます。|  
|**{LF}**|列は、改行で区切られます。|  
|**[セミコロン {;}]**|列は、セミコロンで区切られます。|  
|**[コロン {:}]**|列は、コロンで区切られます。|  
|**[コンマ {,}]**|列は、コンマで区切られます。|  
|**[タブ {t}]**|列は、タブで区切られます。|  
|**[縦棒 {&#124;}]**|列は、縦棒で区切られます。|  
  
 **[更新]**  
 スキップする区切り記号を変更したときの効果を表示するには、 **[最新の情報に更新]**をクリックします。 このボタンは、他の接続オプションを変更した場合にのみ表示されます。  
  
 **[プレビュー]**  
 フラット ファイル内のサンプル データを、選択されたオプションに基づいて列と行に分割して表示します。  
  
 **[列のリセット]**  
 元の列以外のすべての列を削除するには、 **[列のリセット]**をクリックします。  
  
#### <a name="format--fixed-width"></a>[形式] = [固定幅]  
 **フォント**  
 プレビュー データの表示に使用するフォントを選択します。  
  
 **[変換元データ列]**  
 行の幅を調整するには、赤い垂直行マーカーをスライドさせます。列の幅を調整するには、プレビュー ウィンドウの最上部のルーラーをクリックします。  
  
 **[行幅]**  
 個々の列に対して区切り記号を追加する前に、行の長さを指定します。 または、プレビュー ウィンドウの赤い垂直線をドラッグして行の終わりをマークします。 行幅値は自動的に更新されます。  
  
 **[列のリセット]**  
 元の列以外のすべての列を削除するには、 **[列のリセット]**をクリックします。  
  
#### <a name="format--ragged-right"></a>[形式] = [幅合わせしない]  
  
> [!NOTE]  
>  幅合わせしない形式のファイルとは、最後の列を除くすべての列が固定幅のファイルです。 最後の列は、行区切り記号で区切られます。  
  
 **フォント**  
 プレビュー データの表示に使用するフォントを選択します。  
  
 **[変換元データ列]**  
 行の幅を調整するには、赤い垂直行マーカーをスライドさせます。列の幅を調整するには、プレビュー ウィンドウの最上部のルーラーをクリックします。  
  
 **[行区切り記号]**  
 使用できる行区切り記号の一覧から選択するか、区切り記号テキストを入力します。  
  
|値|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|行は、復帰と改行の組み合わせで区切られます。|  
|**{CR}**|行は、復帰で区切られます。|  
|**{LF}**|行は、改行で区切られます。|  
|**[セミコロン {;}]**|行は、セミコロンで区切られます。|  
|**[コロン {:}]**|行は、コロンで区切られます。|  
|**[コンマ {,}]**|行は、コンマで区切られます。|  
|**[タブ {t}]**|行は、タブで区切られます。|  
|**[縦棒 {&#124;}]**|行は、縦棒で区切られます。|  
  
 **[列のリセット]**  
 元の列以外のすべての列を削除するには、 **[列のリセット]**をクリックします。  
## <a name="flat-file-connection-manager-editor-advanced-page"></a>[フラット ファイル接続マネージャー エディター] ([詳細設定] ページ)
  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスの **[詳細設定]** ページでは、Integration Services で、フラット ファイルからデータをどのように読み取るか、フラット ファイルにデータをどのように書き込むかを指定するプロパティを設定できます。 フラット ファイル内の列名を変更し、ファイル内の各列にデータ型および区切り記号を指定するプロパティを設定できます。  
  
 既定では、文字列の列の長さは 50 文字です。 これらの列の長さを変更して、データが切り捨てられたり、列の幅が広くなりすぎないようにできます。 また、変換先列と互換性を持つように他のメタデータも更新できます。 たとえば、整数データのみを含む列のデータ型を、DT_I2 などの数値データ型に変更するなどの操作を行えます。 このような変更は手動で行えます。また、 **[型の選択]** ボタンをクリックし、 **[列の型の推測]** ダイアログ ボックスを使用して、サンプル データを評価し、自動的に変更することもできます。  
  
 フラット ファイル接続マネージャーの詳細については、「 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[接続マネージャー名]**  
 ワークフローにおけるフラット ファイル接続マネージャーの一意な名前を指定します。 指定された名前は、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **Description**  
 接続マネージャーの説明を記述します。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、接続マネージャーの目的について記述することをお勧めします。  
  
 **[各列のプロパティを構成します。]**  
 左側のペインで列を選択すると、そのプロパティが右側のペインに表示されます。 データ型プロパティの説明については、次の表を参照してください。 いくつかのプロパティは、一部のフラット ファイル形式でのみ設定できます。  
  
|プロパティ|Description|  
|--------------|-----------------|  
|**[列の型]**|列が区切り形式、固定幅形式、幅合わせしない形式のうちどれであるかを示します。 このプロパティは読み取り専用です。 幅合わせしない形式のファイルとは、最後の列を除くすべての列が固定幅のファイルです。 最後の列は、行区切り記号で区切られます。|  
|**[出力列の幅]**|格納する値をバイト数で指定します。Unicode ファイルの場合、この値は文字数に対応します。 データ フロー タスクでは、この値を使用してフラット ファイル ソースの出力列の幅を設定します。 オブジェクト モデルでは、このプロパティの名前は MaximumWidth です。|  
|**DataType**|使用できるデータ型を一覧から選択します。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。|  
|**[テキスト修飾子]**|テキスト データが引用符などのテキスト修飾子文字で囲まれているかどうかを示します。<br /><br /> True: フラット ファイルのテキスト データは修飾されます。 False: フラット ファイルのテキスト データは修飾されません。|  
|**名前**|わかりやすい列名を指定します。 名前を入力しないと、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって、列 1、列 2 などの形式で自動的に名前が作成されます。|  
|**[データ スケール]**|数値データの小数点以下の精度を指定します。 これは小数点以下の桁数を表します。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。|  
|**[列区切り記号]**|使用できる列区切り記号の一覧から、列区切り記号を選択します。 テキストに出現しないと思われる区切り記号を選択してください。 固定幅列の場合、この値は無視されます。<br /><br /> **{CR}{LF}**。 列は、復帰と改行の組み合わせで区切られます。<br /><br /> **{CR}**。 列は、復帰で区切られます。<br /><br /> **{LF}**。 列は、改行で区切られます。<br /><br /> **セミコロン {;}**。 列は、セミコロンで区切られます。<br /><br /> **コロン {:}**。 列は、コロンで区切られます。<br /><br /> **コンマ {,}**。 列は、コンマで区切られます。<br /><br /> **タブ {t}**。 列は、タブで区切られます。<br /><br /> **縦棒 {&#124;}**。 列は、縦棒で区切られます。|  
|**[データ精度]**|数値データの精度を指定します。 精度とは、桁数です。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。|  
|**[入力列の幅]**|格納する値をバイト数で指定します。Unicode ファイルの場合、これは文字数として表示されます。 区切られた列の場合、この値は無視されます。<br /><br /> **注** オブジェクト モデルでは、このプロパティの名前は ColumnWidth です。|  
  
 **新規**  
 **[新規作成]**をクリックして新しい列を追加します。 既定では、 **[新規作成]** ボタンをクリックすると、新しい列がリストの末尾に追加されます。 さらにこのボタンのドロップダウン リストには、次のオプションがあります。  
  
|値|Description|  
|-----------|-----------------|  
|**[列の追加]**|新しい列をリストの末尾に追加します。|  
|**[前に挿入]**|選択した列の前に新しい列を追加します。|  
|**[後に挿入]**|選択した列の後に新しい列を追加します。|  
  
 **Del**  
 列を選択して **[削除]**をクリックすると、列が削除されます。  
  
 **[型の推測]**  
 **[列の型の推測]** ダイアログ ボックスを使用して、ファイルのサンプル データを評価し、各列のデータ型と長さの推測を取得します。 詳細については、「 [[列の型の推測] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md)」を参照してください。  
## <a name="flat-file-connection-manager-editor-preview-page"></a>[フラット ファイル接続マネージャー エディター] ([プレビュー] ページ)
  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスの **[プレビュー]** ノードを使用すると、ソース ファイルの内容を表形式で表示できます。  
  
 フラット ファイル接続マネージャーの詳細については、「 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[接続マネージャー名]**  
 ワークフローにおけるフラット ファイル接続マネージャーの一意な名前を指定します。 指定された名前は、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **Description**  
 接続の説明を記述します。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、接続の目的について記述することをお勧めします。  
  
 **[スキップするデータ行数]**  
 フラット ファイルの冒頭でスキップする行数を指定します。  
  
 **[更新]**  
 **[最新の情報に更新]**をクリックすると、スキップする行数を変更した結果が表示されます。 このボタンは、他の接続オプションを変更した場合にのみ表示されます。  
  
 **[プレビュー]**  
 フラット ファイル内のサンプル データを、選択したオプションに基づいて列と行に分割して表示します。  
 