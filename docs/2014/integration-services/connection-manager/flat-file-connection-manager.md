---
title: フラット ファイル接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4466ebd24647520c7cbba2bf0baa93a0f60a72bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833818"
---
# <a name="flat-file-connection-manager"></a>フラット ファイル接続マネージャー
  フラット ファイル接続マネージャーを使用すると、パッケージはフラット ファイルのデータにアクセスできます。 たとえば、フラット ファイルの変換元と変換先は、フラット ファイル接続マネージャーを使用して、データの抽出および読み込みを行うことができます。  
  
 フラット ファイル接続マネージャーがアクセスできるファイルは、1 つだけです。 複数のファイルを参照するには、フラット ファイル接続マネージャーではなく、複数フラット ファイル接続マネージャーを使用します。 詳細については、「 [複数フラット ファイル接続マネージャー](multiple-flat-files-connection-manager.md)」を参照してください。  
  
## <a name="column-length"></a>列の長さ  
 フラット ファイル接続マネージャーでは、文字列型の列の長さが既定で 50 文字に設定されています。 **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスでは、サンプル データを評価し、これらの列の長さを自動的に変更して、データが切り捨てられたり、列の幅が広すぎたりしないようにできます。 また、その後にフラット ファイル ソースまたは変換で列の長さを変更しない限り、データ フロー全体をとおして文字列型の列の長さは一定です。 これらの文字列型の列が、変換先として幅の狭い列にマップされた場合、ユーザー インターフェイスに警告が表示されます。 さらに、実行時にデータの切り捨てによるエラーが発生する場合があります。 エラーや切り捨てが発生しないように、フラット ファイル接続マネージャー、フラット ファイル ソース、または変換で、変換先列に合うように列のサイズを変更することができます。 出力列の長さを変更するには設定、`Length`上の出力列のプロパティ、**入力と出力プロパティ** タブで、**高度なエディター**  ダイアログ ボックス。  
  
 接続マネージャーを使用するフラット ファイル ソースを追加および構成した後に、フラット ファイル接続マネージャーで列の長さを変更した場合は、フラット ファイル ソースの出力列のサイズを手動で変更する必要はありません。 **[フラット ファイル ソース]** ダイアログ ボックスを開くと、列のメタデータを同期するためのオプションがフラット ファイル ソースによって提供されます。  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>フラット ファイル接続マネージャーの構成  
 フラット ファイル接続マネージャーをパッケージに追加すると[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]接続マネージャーを作成実行時にフラット ファイル接続を解決する、フラット ファイル接続プロパティを設定し、フラット ファイル接続マネージャーを追加します、`Connections`パッケージのコレクション。  
  
 接続マネージャーの `ConnectionManagerType` プロパティは、`FLATFILE` に設定されます。  
  
 既定では、フラット ファイル接続マネージャーは、引用符で囲まれていないデータの行区切り記号を常に確認し、行区切り記号が見つかると新しい行を開始します。 これにより、接続マネージャーは列フィールドがない行を含むファイルを正しく解析できます。  
  
 場合によっては、この機能を無効にすると、パッケージのパフォーマンスが向上します。 フラット ファイル接続マネージャーのプロパティを設定してこの機能を無効にできます**AlwaysCheckForRowDelimiters**を`False`します。  
  
 フラット ファイル接続マネージャーは、次の方法で構成できます。  
  
-   使用するファイル、ロケール、およびコード ページを指定します。 ロケールは、日付など、ロケール依存型のデータの解釈に使用されます。コード ページは、文字列データを Unicode に変換するために使用されます。  
  
-   ファイル形式を指定します。 区切られた形式、固定幅形式、または幅合わせしない形式が使用できます。  
  
-   ヘッダー行、データ行、および列の区切り記号を指定します。 列の区切り記号は、ファイル レベルで設定し、列レベルで上書きできます。  
  
-   ファイルの最初の行に列の名前が含まれるかどうかを示します。  
  
-   テキスト修飾子文字を指定します。 各列は、テキスト修飾子を認識するように構成できます。  
  
     修飾子文字を使用して、修飾される文字列に修飾子文字を埋め込むことができるようになりました。 テキスト修飾子の二重インスタンスは、1 つのリテラル、つまりその文字列の 1 つのインスタンスとして解釈されます。 たとえば、テキスト修飾子が単一引用符で、入力データが 'abc'、'def'、'g'hi' の場合、出力データは abc、def、g'hi になります。  
  
-   各列の名前、データ型、最大幅などのプロパティを設定します。  
  
 フラット ファイル接続マネージャーの ConnectionString プロパティは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の [プロパティ] ウィンドウで式を指定することで設定できます。 検証エラーを回避するには、次の操作を行います。  
  
-   式を使用してファイルを指定する場合は、 **[フラット ファイル接続マネージャー エディター]** の **[ファイル名]** ボックスにファイル パスを追加します。  
  
-   フラット ファイル接続マネージャーの **DelayValidation** プロパティを **True**に設定します。  
  
 フラット ファイルの変換先に対してフラット ファイル接続マネージャーを使用することにより、実行時に式を使用してファイル名を作成できます。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[フラット ファイル接続マネージャー エディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [[フラット ファイル接続マネージャー エディター] &#40;[列] ページ&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
-   [[フラット ファイル接続マネージャー エディター] &#40;[詳細設定] ページ&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
-   [[フラット ファイル接続マネージャー エディター] ([プレビュー] ページ)](../flat-file-connection-manager-editor-preview-page.md)  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
  
