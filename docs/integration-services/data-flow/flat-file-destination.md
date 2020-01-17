---
title: フラット ファイル変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfiledest.f1
- sql13.dts.designer.flatfiledestadapter.connection.f1
- sql13.dts.designer.flatfiledestadapter.mappings.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c837241abfaebe3776a21e03a9c2cbf4c4f5ee9d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292530"
---
# <a name="flat-file-destination"></a>フラット ファイル変換先

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  フラット ファイル変換先は、データをテキスト ファイルに書き込みます。 テキスト ファイルには、区切り形式、固定幅形式、行区切り記号を使用した固定幅形式、または幅合わせしない形式を使用できます。  
  
 フラット ファイル変換先は、次の方法で構成できます。  
  
-   データが書き込まれる前にファイルに挿入される、テキストのブロックを指定します。 このテキストには、列見出しなどの情報を設定できます。  
  
-   同じ名前の変換先ファイルにあるデータを上書きするかどうかを指定します。  
  
 この変換先では、フラット ファイル接続マネージャーを使用してテキスト ファイルにアクセスします。 フラット ファイル変換先が使用するフラット ファイル接続マネージャーでプロパティを設定することにより、フラット ファイル変換先がテキスト ファイルをフォーマットする方法と書き込む方法を指定できます。 フラット ファイル接続マネージャーを構成する際には、ファイルおよびファイル内の各列に関する情報を指定できます。 たとえば、ファイルの列と行を区切る文字や、各列のデータ型や長さを指定できます。 詳しくは、「 [フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)」をご覧ください。  
  
 フラット ファイル変換先には、Header カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳しくは、「[Integration Services &#40;SSIS&#41; の式](../../integration-services/expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../integration-services/expressions/use-property-expressions-in-packages.md)」、および「[フラット ファイルのカスタム プロパティ](../../integration-services/data-flow/flat-file-custom-properties.md)」をご覧ください。  
  
 この変換先は 1 つの出力をとります。 エラー出力はサポートされていません。  
  
## <a name="configuration-of-the-flat-file-destination"></a>フラット ファイル変換先の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [フラット ファイルのカスタム プロパティ](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 データ フロー コンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」をご覧ください。  
  
## <a name="flat-file-destination-editor-connection-manager-page"></a>[フラット ファイル変換先エディター] ([接続マネージャー] ページ)
  **[フラット ファイル変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、変換先のフラット ファイル接続を選択したり、既存の変換先ファイルに対して上書きまたは追加のどれを実行するかを指定したりできます。 フラット ファイル変換先は、データをテキスト ファイルに書き込みます。 テキスト ファイルには、区切り形式、固定幅形式、行区切り記号付き固定幅形式、または幅合わせしない形式を使用できます。  
  
### <a name="options"></a>オプション  
 **フラット ファイル接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[フラット ファイル形式]** および **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 標準のフラット ファイル形式である、区切り形式、固定幅形式、および幅合わせしない形式に加えて、 **[フラット ファイル形式]** ダイアログ ボックスには 4 つ目のオプションとして **[行区切り記号付きの固定幅]** が用意されています。 このオプションは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] がデータの最終列としてダミー列を追加する、特殊な幅合わせしない形式を表します。 このダミー列によって、最終列が固定幅であることが保証されます。  
  
 **[フラット ファイル接続マネージャー エディター]** では **[行区切り記号付きの固定幅]** オプションは使用できません。 必要に応じて、エディターでこのオプションをエミュレートすることができます。 このオプションをエミュレートするには、 **[フラット ファイル接続マネージャー エディター]** の **[全般]** ページにある **[形式]** で、 **[幅合わせしない]** を選択します。 次に、エディターの **[詳細設定]** ページで、データの最終列として新しいダミー列を追加します。  
  
 **[ファイル内のデータを上書きする]**  
 既存のファイルを上書きするか、データを追加するかを指定します。  
  
 **[ヘッダー]**  
 データが書き込まれる前にファイルに挿入するテキストのブロックを入力します。 このオプションをオンにすると、列見出しなどの追加情報を含めることができます。  
  
 **プレビュー**  
 **[データ ビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
## <a name="flat-file-destination-editor-mappings-page"></a>[フラット ファイル変換先エディター] ([マッピング] ページ)
  **[フラット ファイル変換先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用すると、入力列を変換先列にマップできます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 ドラッグ アンド ドロップ操作により、使用できる入力列を変換先列にマップします。  
  
 **使用できる変換先列**  
 使用できる変換先列の一覧を表示します。 ドラッグ アンド ドロップ操作により、使用できる変換先列を入力列にマップします。  
  
 **入力列**  
 このトピックの前の手順で選択した入力列を表示します。 **[使用できる入力列]** ボックスの一覧を使用して、マッピングを変更できます。 出力から列を除外するには、 **[\<無視>]** を選択します。  
  
 **変換先列**  
 マップされているかどうかに関係なく、使用できる変換先列を表示します。  
  
## <a name="see-also"></a>参照  
 [フラット ファイル ソース](../../integration-services/data-flow/flat-file-source.md)   
 [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
  
