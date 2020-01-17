---
title: Integration Services のパス | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.patheditor.general.f1
- sql13.dts.designer.patheditor.metadata.f1
- sql13.dts.designer.patheditor.visualizers.f1
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f70ce04ebe25c752f3cc12d4888f1ff5c967b805
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292405"
---
# <a name="integration-services-paths"></a>Integration Services のパス

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  パスは、データ フロー コンポーネントの出力を別のコンポーネントの入力に連結することにより、データ フロー内の 2 つのコンポーネントを連結します。 パスには連結元と連結先があります。 たとえば、パスが OLE DB ソースと並べ替え変換を連結する場合、OLE DB ソースはパスの連結元であり、並べ替え変換はパスの連結先になります。 連結元とはパスが開始するコンポーネントで、連結先とはパスが終了するコンポーネントのことです。  
  
 パッケージを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで実行する場合、データ ビューアーをパスにアタッチすることにより、データ フロー内のデータを表示できます。 データ ビューアーを構成し、グリッドにデータを表示できます。 データ ビューアーは、デバッグ用のツールとして便利です。 詳細については、「 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md)」を参照してください。  
  
## <a name="configure-the-path"></a>パスの構成  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは **[データ フロー パス エディター]** ダイアログ ボックスが用意され、これを使用すると、パスのプロパティの設定、パスに渡されるデータ列のメタデータの表示、およびデータ ビューアーの構成を行うことができます。  
  
 構成可能なパスのプロパティは、パスの名前、説明、および注釈です。 パスはプログラムによって構成することもできます。 詳細については、「 [プログラムによるデータ フロー コンポーネントの接続](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)」を参照してください。  
  
 パスの注釈を設定すると、 **デザイナーの** [データ フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブにあるデザイン画面に、パスの連結元の名前またはパスの名前が表示されます。 パスの注釈は、データ フロー、制御フロー、およびイベント ハンドラーに追加できる注釈と同様です。 唯一の違いは、パスの注釈はパスにアタッチされるのに対し、他の注釈は、 **デザイナーの**[データ フロー] **、** [制御フロー] **、および**[イベント ハンドラー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブに表示される点です。  
  
 パスの注釈のメタデータは、各列の名前、データ型、有効桁数、小数点以下桁数、長さ、コード ページ、およびソース コンポーネントを、直前のコンポーネントの出力内で表示します。 ソース コンポーネントとは、列を作成したデータ フロー コンポーネントのことです。 このコンポーネントは、データ フロー内で最初のコンポーネントである場合もあれば、そうでない場合もあります。 たとえば、全体結合変換と並べ替え変換では独自の列が作成され、その列が出力列のソースになります。 対照的に、列コピー変換では、列を変更しないまま渡したり、入力列をコピーして新しい列を作成できます。 列コピー変換は、新しい列に対してのみ変換元コンポーネントとなります。  

## <a name="set-the-properties-of-a-path-with-the-data-flow-path-editor"></a>データ フロー パス エディターを使用してパスのプロパティを設定する
パスは、2 つのデータ フロー コンポーネントを連結します。 パスのプロパティを設定する場合、データ フローには、2 つ以上の連結されたデータ フロー コンポーネントをあらかじめ含めておく必要があります。
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、パスをダブルクリックします。  
  
4.  **[データ フロー パス エディター]** ダイアログ ボックスで、 **[全般]** をクリックします。 ここで、パスの既定の名前を編集したり、パスに関する説明を入力できます。 PathAnnotation プロパティを変更することもできます。  
  
5.  **[OK]** をクリックします。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

## <a name="general-page---data-flow-path-editor"></a>[全般] ページ - データ フロー パス エディター
**[データ フロー パス エディター]** ダイアログ ボックスを使用すると、パス プロパティの設置、列メタデータの表示、およびパスにアタッチされるデータ ビューアーの管理を行うことができます。  
  
 **[データ フロー パス エディター]** ダイアログ ボックスの **[全般]** ノードを使用して、パスに名前を付けて説明を記述したり、パスの注釈のオプションを指定したりできます。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 パスの一意な名前を指定します。  
  
 **ID**  
 パスの系列 ID です。 このプロパティは読み取り専用です。  
  
 **[IdentificationString]**  
 パスを識別する文字列です。 上記で入力した名前から自動的に生成されます。  
  
 **[説明]**  
 パスの説明を記述します。  
  
 **[PathAnnotation]**  
 使用する注釈の種類を指定します。 注釈を無効にする場合は **[Never]** 、注釈を必要に応じて有効にする場合は **[AsNeeded]** 、 **[SourceName]** オプションの値を使用して自動的に注釈を付ける場合は **[SourceName]** 、 **[Name]** プロパティの値を使用して自動的に注釈を付ける場合は **[PathName]** を選択します。  
  
 **[DestinationName]**  
 パスの末尾の入力を表示します。  
  
 **[SourceName]**  
 パスの先頭の出力を表示します。  
 
## <a name="metadata-page---data-flow-path-editor"></a>[メタデータ] ページ - [データ フロー パス エディター]
**[データ フロー パス エディター]** ダイアログ ボックスの **[メタデータ]** ページを使用すると、パス列のメタデータを表示できます。  
  
### <a name="options"></a>オプション  
 **[パスのメタデータ]**  
 列のメタデータが一覧表示されます。 列のデータを並べ替えるには、列ヘッダーをクリックします。  
  
 **[名前]**  
 列名が一覧表示されます。  
  
 **[データ型]**  
 列のデータ型が一覧表示されます。  
  
 **[精度]**  
 数値の桁数が一覧表示されます。  
  
 **[スケール]**  
 数値の中で小数点より右側の桁数が一覧表示されます。  
  
 **[データ型]**  
 列の現在の長さが一覧表示されます。  
  
 **コード ページ**  
 列のコード ページが一覧表示されます。 値 **0** は、その列でコード ページが使用されないことを示します。 これは、データが Unicode であるか、数値、日付、または時刻のデータ型である場合です。  
  
 **[並べ替えキーの位置]**  
 列の並べ替えキーの位置が一覧表示されます。 値 **0** は、その列が並べ替えられないことを示します。  
  
> [!NOTE]  
>  マイナス記号 (-) のプレフィックスは、列が降順で並べ替えられていることを示します。  
  
 **[比較フラグ]**  
 列に適用されている比較フラグが一覧表示されます。  
  
 **[基になるコンポーネント]**  
 列の基になるデータ フロー コンポーネントが一覧表示されます。  
  
 **[クリップボードにコピー]**  
 列のメタデータをクリップボードにコピーします。 既定では、すべてのメタデータ行が現在表示されている順序でコピーされます。  
 
## <a name="data-viewers-page---data-flow-path-editor"></a>[データ ビューアー] ページ - [データ フロー パス エディター]
**[データ フロー パス エディター]** ダイアログ ボックスの **[データ ビューアー]** ページを使用すると、パスにアタッチされているデータ ビューアーを管理できます。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 データ ビューアーが一覧表示されます。  
  
 **[データ ビューアーの種類]**  
 データ ビューアーの種類が一覧表示されます。  
  
 **[追加]**  
 クリックすると、 **[データ ビューアーの構成]** ダイアログ ボックスを使用してデータ ビューアーを追加できます。  
  
 **削除**  
 クリックすると、選択したデータ ビューアーが削除されます。  
  
 **構成**  
 クリックすると、選択したデータ ビューアーを **[データ ビューアーの構成]** ダイアログ ボックスを使用して構成できます。  
 
## <a name="path-properties"></a>パスのプロパティ
[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクト モデルでは、データ フロー オブジェクトのコンポーネント、入力、出力、入力列、および出力列の各レベルに、共通プロパティとカスタム プロパティがあります。 多くのプロパティの値は読み取り専用で、実行時にデータ フロー エンジンによって割り当てられます。  
  
 このトピックでは、データ フロー オブジェクトを連結するパスのカスタム プロパティの一覧を示し、それらのプロパティについて説明します。  
  
### <a name="custom-properties-of-a-path"></a>パスのカスタム プロパティ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクト モデルでは、データ フロー内のコンポーネントを連結するパスは <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> インターフェイスを実装します。  
  
 次の表は、データ フロー内のパスの、値が設定できるプロパティを示しています。 データ フロー エンジンは、この一覧にない追加の読み取り専用プロパティにも値を割り当てます。  
  
|プロパティ名|データ型|[説明]|  
|-------------------|---------------|-----------------|  
|[PathAnnotation]|Integer (列挙)|注釈をパスと共にデザイナー画面に表示するかどうかを示す値。 指定できる値は、 **AsNeeded**、 **SourceName**、 **PathName**、 **Never**です。 既定値は **AsNeeded**です。|  
|[DestinationName]|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|パスに関連付けられた入力|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|パスに関連付けられた出力|  
