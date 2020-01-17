---
title: フラット ファイル ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfilesource.f1
- sql13.dts.designer.flatfilesourceadapter.connection.f1
- sql13.dts.designer.flatfilesourceadapter.columns.f1
- sql13.dts.designer.flatfilesourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5af33c29f1c013937cff99f8d357b0b538b9ffdb
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292481"
---
# <a name="flat-file-source"></a>フラット ファイル ソース

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  フラット ファイル ソースは、テキスト ファイルからデータを読み取ります。 テキスト ファイルには、Delimited 形式、FixedWidth 形式、または Mixed 形式を使用できます。  
  
-   Delimited 形式では、列区切り記号と行区切り記号を使用して、列と行が定義されます。  
  
-   FixedWidth 形式では、幅を使用して列と行を定義します。 またこの形式には、フィールドを幅いっぱいまで埋めるための文字も含まれています。  
  
-   RaggedRight 形式では、幅を使用して最終列以外のすべての列を定義します。最終列は、行区切り記号で区切られます。  
  
 フラット ファイル ソースは、次の方法で構成できます。  
  
-   変換出力に列を追加します。列には、フラット ファイル ソースによるデータの抽出元となるテキスト ファイルの名前が含まれています。  
  
-   フラット ファイル ソースで、列にある長さ 0 の文字列を NULL 値として解釈するかどうかを指定します。  
  
    > [!NOTE]  
    >  長さ 0 の文字列を NULL として解釈するには、フラット ファイル ソースで使用するフラット ファイル接続マネージャーを、Delimited 形式を使用するように構成する必要があります。 フラット ファイル接続マネージャーで FixedWidth 形式または RaggedRight 形式が使用される場合、空白文字で構成されるデータを NULL 値として解釈できません。  
  
 フラット ファイル ソースの出力にある出力列には、FastParse プロパティが含まれています。 FastParse は、列が、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に用意されているロケール非依存型の高速な解析ルーチンを使用するか、ロケール依存型の標準的な解析ルーチンを使用するかを示します。 詳細については、「 [Fast Parse](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 」および「 [Standard Parse](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)」を参照してください。  
  
 出力列には、UseBinaryFormat プロパティも含まれます。 このプロパティを使用して、パック 10 進形式を使用するデータなど、バイナリ データのサポートをファイルに実装します。 既定では、UseBinaryFormat を **false**に設定します。 バイナリ形式を使用する場合は、UseBinaryFormat を **true** に設定し、出力列のデータ型を **DT_BYTES**に設定します。 この設定を行った場合、フラット ファイル ソースはデータ変換をスキップし、データを出力列にそのまま渡します。 この場合は、派生列変換またはデータ変換などの変換を使用して **DT_BYTES** データを別のデータ型にキャストするか、スクリプト変換でカスタム スクリプトを記述してデータを解釈できます。 また、カスタム データ フロー コンポーネントを記述してデータを解釈することもできます。 **DT_BYTES** をキャストできるデータ型の詳細については、「[Cast (SSIS 式)](../../integration-services/expressions/cast-ssis-expression.md)」を参照してください。  
  
 フラット ファイル ソースは、フラット ファイル接続マネージャーを使用してテキスト ファイルにアクセスします。 フラット ファイル接続マネージャーでプロパティを設定することにより、ファイルおよびファイルの各列に関する情報を提供して、フラット ファイル ソースで、テキスト ファイルのデータをどのように処理するかを指定できます。 たとえば、ファイルの列と行を区切る文字や、各列のデータ型や長さを指定できます。 詳しくは「 [フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)」をご覧ください。  
  
 この変換は、1 つの出力と 1 つのエラー出力をとります。  
  
## <a name="configuration-of-the-flat-file-source"></a>フラット ファイル ソースの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [フラット ファイルのカスタム プロパティ](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 データ フロー コンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="flat-file-source-editor-connection-manager-page"></a>[フラット ファイル ソース エディター]\ ([接続マネージャー] ページ)
  **[フラット ファイル ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、フラット ファイル ソースが使用する接続マネージャーを選択できます。 フラット ファイル ソースは、区切り形式、固定幅形式、または区切りと固定幅が混在した形式のテキスト ファイルからデータを読み取ります。  
  
 フラット ファイル ソースは、次のいずれかの種類の接続マネージャーを使用できます。  
  
-   ソースが単一のフラット ファイルの場合は、フラット ファイル接続マネージャー。 詳しくは、「 [フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)」をご覧ください。  
  
-   ソースが複数フラット ファイルで、データ フロー タスクが For ループ コンテナーなどのループ コンテナーの内部にある場合は、複数フラット ファイル接続マネージャー。 コンテナーの各ループで、フラット ファイル ソースは、複数フラット ファイル接続マネージャーが提供する次のファイル名からデータを読み込みます。 詳細については、「 [複数フラット ファイル接続マネージャー](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **Flat file connection manager**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。  
  
 **[新規作成]**  
 新しい接続マネージャーを作成するには、 **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスを使用します。  
  
 **[データ ソースの NULL 値をデータ フローで NULL 値として保持する]**  
 データが抽出されたときに NULL 値を保持するかどうかを指定します。 このプロパティの既定値は **false**です。 この値が**false**である場合、フラット ファイル変換元は変換元データの NULL 値を各列の適切な既定値で置き換えます。たとえば、文字列型の列の場合は空の文字列、数値型の列の場合は 0 です。  
  
 **プレビュー**  
 **[データ ビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
## <a name="flat-file-source-editor-columns-page"></a>[フラット ファイル ソース エディター]\ ([列] ページ)
  **[フラット ファイル ソース エディター]** ダイアログ ボックスの **[列]** ノードを使用すると、出力列を各外部 (変換元) 列にマップできます。  
  
> [!NOTE]  
>  フラット ファイル ソースの **FileNameColumnName** プロパティおよびその出力列の **FastParse** プロパティは、 **[フラット ファイル ソース エディター]** ではアクセスできませんが、 **[詳細エディター]** を使用して設定できます。 これらのプロパティの詳細については、「 [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md)」の「フラット ファイル ソース」を参照してください。  
  
### <a name="options"></a>オプション  
 **使用できる外部列**  
 データ ソース内の使用できる外部列の一覧を表示します。 このテーブルを使用して列を追加または削除することはできません。  
  
 **[外部列]**  
 タスクで外部 (変換元) 列を読み取る順序を表示します。 この順序を変更するには、テーブルで選択した列を消去してから、別の順序で一覧から外部列を選択します。  
  
 **出力列**  
 各出力列の一意な名前を表示します。 既定では選択された外部 (変換元) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。 指定された名前は、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに表示されます。  
  
## <a name="flat-file-source-editor-error-output-page"></a>[フラット ファイル ソース エディター]\ ([エラー出力] ページ)
  **[フラット ファイル ソース エディター]** ダイアログ ボックスの **[エラー出力]** ページでは、エラー処理オプションの選択や、エラー出力列に対するプロパティの設定を行えます。  
  
### <a name="options"></a>オプション  
 **[入力または出力]**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[フラット ファイル ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで選択した外部 (変換元) 列を表示します。  
  
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
  
## <a name="see-also"></a>参照  
 [フラット ファイル変換先](../../integration-services/data-flow/flat-file-destination.md)   
 [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
  
