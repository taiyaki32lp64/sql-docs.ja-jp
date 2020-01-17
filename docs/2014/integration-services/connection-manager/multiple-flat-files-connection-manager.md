---
title: 複数フラット ファイル接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7235f5f333ac7bb4520a6244e103baafba343ea3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833703"
---
# <a name="multiple-flat-files-connection-manager"></a>複数フラット ファイル接続マネージャー
  複数フラット ファイル接続マネージャーを使用すると、パッケージで複数のフラット ファイルのデータにアクセスできます。 たとえば、データ フロー タスクが For ループ コンテナーなどのループ コンテナーの内部にある場合は、フラット ファイル ソースで複数フラット ファイル接続マネージャーを使用できます。 コンテナーの各ループで、フラット ファイル ソースは、複数フラット ファイル接続マネージャーが提供する次のファイル名からデータを読み込みます。  
  
 複数フラット ファイル接続マネージャーをパッケージに追加すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、実行時に複数のフラット ファイルの接続を解決する接続マネージャーを作成し、複数フラット ファイル接続マネージャーのプロパティを設定して、複数フラット ファイル接続マネージャーをパッケージの `Connections` コレクションに追加します。  
  
 接続マネージャーの `ConnectionManagerType` プロパティは、`MULTIFLATFILE` に設定されます。  
  
 複数フラット ファイル接続マネージャーは、次の方法で構成できます。  
  
-   使用するファイル、ロケール、およびコード ページを指定します。 ロケールは、日付など、ロケール依存型のデータの解釈に使用されます。コード ページは、文字列データを Unicode に変換するために使用されます。  
  
-   ファイル形式を指定します。 区切られた形式、固定幅形式、または幅合わせしない形式が使用できます。  
  
-   ヘッダー行、データ行、および列の区切り記号を指定します。 列の区切り記号は、ファイル レベルで設定し、列レベルで上書きできます。  
  
-   ファイルの最初の行に列の名前が含まれるかどうかを示します。  
  
-   テキスト修飾子文字を指定します。 各列は、テキスト修飾子を認識するように構成できます。  
  
-   各列の名前、データ型、最大幅などのプロパティを設定します。  
  
 複数フラット ファイル接続マネージャーが複数のファイルを参照する場合、ファイルのパスをパイプ (|) 文字で区切ります。 この接続マネージャーの `ConnectionString` プロパティの形式は、次のとおりです。  
  
 \<*パス*>|\<*パス*>  
  
 複数のファイルを指定する場合、ワイルドカード文字を使用することもできます。 たとえば、ドライブ C 上のすべてのテキスト ファイルの値の参照を`ConnectionString`プロパティは、c: に設定することができます\\*.txt します。  
  
 複数フラット ファイル接続マネージャーが複数のファイルを参照する場合、ファイルの形式はすべて同じである必要があります。  
  
 複数フラット ファイル接続マネージャーでは、文字列型の列の長さが既定で 50 文字に設定されています。 **[複数フラット ファイル接続マネージャー エディター]** ダイアログ ボックスでは、データが切り捨てられたり、列の幅が広くなりすぎないように、サンプル データを評価して、これらの列の長さを自動的に変更できます。 フラット ファイル ソースまたは変換で列の長さを変更しない限り、データ フローでの列の長さは一定です。 これらの列が幅の狭い変換先列にマップされると、ユーザー インターフェイスに警告が表示されます。また、実行時にデータの切り捨てによるエラーが発生する場合があります。 フラット ファイル接続マネージャー、フラット ファイル ソース、または変換では、変換先列に合うように列のサイズを変更できます。 出力列の長さを変更するには設定、`Length`上の出力列のプロパティ、**入力と出力プロパティ** タブで、**高度なエディター**  ダイアログ ボックス。  
  
 接続マネージャーを使用するフラット ファイル ソースを追加および構成した後に、複数フラット ファイル接続マネージャーで列の長さを変更しても、フラット ファイル ソースの出力列のサイズを手動で変更する必要はありません。 **[フラット ファイル ソース]** ダイアログ ボックスを開くと、列のメタデータを同期するためのオプションがフラット ファイル ソースによって提供されます。  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>複数フラット ファイル接続マネージャーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[複数フラット ファイル接続マネージャー エディター] ([全般] ページ)](../general-page-of-integration-services-designers-options.md)  
  
-   [[複数フラット ファイル接続マネージャー エディター] ([列] ページ)](../multiple-flat-files-connection-manager-editor-columns-page.md)  
  
-   [[複数フラット ファイル接続マネージャー エディター] ([詳細設定] ページ)](../multiple-flat-files-connection-manager-editor-advanced-page.md)  
  
-   [[複数フラット ファイル接続マネージャー エディター] ([プレビュー] ページ)](../multiple-flat-files-connection-manager-editor-preview-page.md)  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="see-also"></a>関連項目  
 [[フラット ファイル ソース]](../data-flow/flat-file-source.md)   
 [フラット ファイル変換先](../data-flow/flat-file-destination.md)   
 [Integration Services (SSIS) の接続](integration-services-ssis-connections.md)  
  
  
