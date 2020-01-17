---
title: Hyperion Essbase の接続の種類 (SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 108a00b6-799f-4066-b796-da59e95c09fd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 904a3bbc5b7a3d4987cd6c06b257ff680e4e8343
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593835"
---
# <a name="hyperion-essbase-connection-type-ssrs"></a>Hyperion Essbase の接続の種類 (SSRS)
  [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 外部データ ソースのデータをレポートに含めるには、種類が [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]のレポート データ ソースに基づいたデータセットが必要です。 このビルトイン データ ソースの種類は、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]のデータ拡張機能に基づいています。この拡張機能を使用すると、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 外部データ ソースから多次元データを取得できます。  
  
 このトピックの情報を使用して、データ ソースを構築してください。 手順については、「 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)」を参照してください。  
  
##  <a name="Connection"></a> 接続文字列  
 次の接続文字列例では、13080 番ポートを使用してサーバー上の [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースを指定し、SOAP を使用してインターネット経由の XML for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (XMLA) を指定して、Sample カタログに接続しています。  
  
```  
Data Source=https://localhost:13080/aps/XMLA; Initial Catalog=Sample  
```  
  
 接続文字列の例の詳細については、「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。  
  
  
##  <a name="Credentials"></a> [資格情報]  
 クエリの実行、ローカルでのレポートのプレビュー、およびレポート サーバーからのレポートのプレビューには、資格情報が必要です。  
  
 レポートをパブリッシュした後、レポートをレポート サーバーで実行するときに、データを取得するための権限が有効な状態になるように、データ ソースの資格情報を変更する必要が生じる場合があります。  
  
 詳細については、「[データ接続、データソース、および&#40;接続文字列レポートビルダー&#41;と SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 」または「[レポートデータソースに関する資格情報と接続情報の指定](specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
  
##  <a name="Query"></a> クエリ  
 クエリは、次の方法で指定できます。  
  
-   クエリを対話形式で作成します。 グラフィカル クエリ デザイナーのデザイン モードまたはクエリ モードを使用して、外部データ ソースのメタデータを参照しながら、多次元式 (MDX) 構文のクエリを生成します。  
  
    -   **デザイン ビュー** ディメンション、メンバー、メンバー プロパティ、メジャー、および KPI をメタデータ ブラウザーから **データ** ペインにドラッグして、MDX クエリを作成します。 計算されるメンバー ペインから、計算されるメンバーをデータ ペインにドラッグして、追加のデータセット フィールドを定義できます。  
  
    -   **クエリ ビュー** ： ディメンション、メンバー、メンバー プロパティ、メジャー、および KPI をメタデータ ブラウザーからクエリ ペインにドラッグして、MDX クエリを作成します。 クエリ ペインでは、直接 MDX テキストを編集できます。 計算されるメンバーを計算されるメンバー ペインからクエリ ペインにドラッグして、追加のデータセット フィールドを定義します。  
  
     詳細については、「[Hyperion Essbase クエリ デザイナーのユーザー インターフェイス (レポート ビルダー)](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)」を参照してください。  
  
-   レポートから既存の MDX クエリをインポートします。 **[クエリのインポート]** ボタンを使用して、.rdl ファイルを参照し、クエリをインポートします。 クエリは、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースに基づく埋め込みデータセットを含むレポートからインポートできます。 MDX クエリを .mdx ファイルから直接インポートすることはできません。  
  
 デザイン時には、クエリを実行して結果セットを表示します。 クエリを作成した後、メタデータから生成されたデータセット フィールド コレクションがレポート データ ペインに表示されます。 レポートの実行時には、外部データ ソースから実際のデータが返されます。  
  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ処理拡張機能では、拡張データセット フィールド プロパティがサポートされています。 これらの値は外部データ ソースから取得できますが、レポート データ ペインには表示されません。 詳細については、このトピックの「 [拡張フィールド プロパティ](#Extended) 」を参照してください。  
  
  
##  <a name="Parameters"></a> クエリ パラメーター  

 クエリ パラメーターを含めるには、クエリ デザイナーのフィルター領域でフィルターを作成し、そのフィルターをパラメーターとして設定します。 各パラメーターに対して、使用可能な値を提供するデータセットが自動的に作成されます。 既定では、これらのデータセットはレポート データ ペインに表示されません。 詳細については、「[多次元データのパラメーター値の非表示データセットの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md)」を参照してください。

 各レポート パラメーターの既定のデータ型は **Text**です。 レポート パラメーターを作成した後に、既定値の変更が必要になる場合があります。 詳細については、「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)のレポート データ ソースに基づいたデータセットが必要です。  
  
  
##  <a name="Extended"></a> 拡張フィールド プロパティ  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ処理拡張機能では、拡張フィールド プロパティがサポートされています。 拡張フィールド プロパティは、 **Value** と **IsMissing** に追加する形で、データ処理拡張機能によってデータセットのフィールドに定義されるプロパティです。 拡張プロパティには、定義済みプロパティとカスタム プロパティがあります。 定義済みのプロパティは、複数のデータ ソースに共通のプロパティです。 カスタム プロパティは、各データ ソースの固有のプロパティです。  
  
 拡張フィールド プロパティは、レポート レイアウトにドラッグすることのできるアイテムとして [レポート データ] ウィンドウには表示されません。 その代わりに、このプロパティの親フィールドをレポートにドラッグすることによって、既定のプロパティである **Value** を必要なプロパティに変更することが可能です。  
  
 クエリ デザイナーのメタデータ ペインでフィールドにカーソルを合わせると、拡張フィールド プロパティの名前がツールヒントに表示されます。 基になっているデータの調査に使用できるクエリ デザイナーの詳細については、「 [Hyperion Essbase クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)」を参照してください。  
  
> [!NOTE]  
>  拡張フィールド プロパティに対応する値が存在するのは、そのプロパティが MDX 式に含まれており、レポートを実行して対応するデータセットのデータを取得する際に、データ ソースによって値が提供された場合のみです。 その場合、次のセクションに示す構文を使用して、すべての式からこれらの **Field** プロパティ値を参照できます。 ただし、これらのフィールドはこのデータ プロバイダーに固有であり、レポート定義言語には含まれないため、これらの値に加えた変更はレポート定義には保存されません。  
  
  
### <a name="predefined-field-properties"></a>定義済みフィールド プロパティ  
 複数のデータ プロバイダーで一般的にサポートされ、レポート データセットの基となる MDX クエリに表示される定義済みフィールド プロパティ。 たとえば、MDX ディメンション プロパティ MEMBER_UNIQUE_NAME は、定義済みレポート データセット フィールド プロパティ **UniqueName**にマッピングされます。 一意な名前の値をテキスト ボックスに入力するには、`=Fields!` *\<FieldName>* `.UniqueName` という式を使用します。  
  
 次の表に、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースで使用できる定義済みフィールド プロパティの一覧を示します。  
  
|**プロパティ**|**型**|**説明/有効値**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**オブジェクト**|フィールドのデータ値を指定します。<br /><br /> ディメンション プロパティの場合は、MEMBER_CAPTION にマッピングされます。 メジャーの場合は、データ値にマッピングされます。|  
|**IsMissing**|**Boolean**|フィールドが結果データセットに存在するかどうかを示します。|  
|**FormattedValue**|**String**|主要データの書式設定した値を返します。<br /><br /> MDX 式の FORMATTED_VALUE からマッピングされます。|  
|**BackgroundColor**|**String**|データベースで定義されたフィールドの背景色を返します。<br /><br /> MDX 式の BACK_COLOR からマッピングされます。|  
|**色**|**String**|データベースで定義されたアイテムの前景色を返します。<br /><br /> MDX 式の FORE_COLOR からマッピングされます。|  
|**UniqueName**|**String**|レベルの完全修飾名を返します。<br /><br /> MDX 式の MEMBER_UNIQUE_NAME からマッピングされます。|  
  
 フィールドおよびフィールド プロパティを式で使用する方法の詳細については、「[式で使用される組み込みコレクション (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)」を参照してください。  
  
  
### <a name="custom-properties"></a>カスタム プロパティ  
 データ プロバイダーでサポートされ、レポート データセットの基となる MDX クエリで使用される一方で、レポートのデータセット ペインにはそのデータセットのフィールドとして表示されないカスタム フィールド プロパティ。 たとえば、 **[長い名前]** はディメンション レベルで定義されたメンバー プロパティです。 値をテキスト ボックスに入力するには、`=Fields!` *\<FieldName>* `("Long Names")` という式を使用します。 この式ではフィールド名の大文字と小文字が区別されます。  
  
 カスタム拡張プロパティを式の中で参照するには、次の構文を使用します。  
  
-   *Fields!FieldName("PropertyName")*  
  
 次の表に、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースで使用できるカスタム フィールド プロパティを示します。  
  
|**プロパティ**|**型**|**説明/有効値**|  
|------------------|--------------|---------------------------------------|  
|**FORMAT_STRING**|**String**|メジャーで定義されます。String 型として使用できる **FormattedValue** です。|  
  
  
##  <a name="Remarks"></a> 解説  
 このデータ プロバイダーでは使用できないレポート配信モードもあります。 このデータ処理拡張機能では、データ ドリブン サブスクリプションを使ったレポートの配信はサポートされません。 詳細については、「[サブスクライバー データに対して外部データ ソースを使用する (データ ドリブン サブスクリプション)](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)」を参照してください。 
  
 詳細については、「 [SQL Server 2005 Reporting Services を Hyperion Essbase と組み合わせて使用する方法](https://go.microsoft.com/fwlink/?LinkId=81970)」を参照してください。  
  
  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 データ接続、データ ソース、およびデータセットを操作する手順について説明します。  
  
 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [データセットへのフィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 関連項目  
 次に示すセクションでは、レポート データの概念が詳細に説明されているほか、データに関連するレポートのパーツを定義し、カスタマイズし、使用する方法が説明されています。  
  
 [レポート データセット (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
 レポートのデータへのアクセスの概要について説明します。  
  
 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 データ接続とデータ ソースについて説明します。  
  
 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 埋め込みデータセットと共有データセットについて説明します。  
  
 [データセット フィールド コレクション (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 データセット クエリによって生成されるフィールド コレクションについて説明します。  
  
 [Reporting Services &#40;&#41; SSRS によってサポートされるデータソース](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)各データ拡張機能のプラットフォームとバージョンのサポートについて詳しく説明します。  
  
 [SQL Server 2005 Reporting Services を Hyperion Essbase と組み合わせて使用する方法](https://go.microsoft.com/fwlink/?LinkId=81970)  
 このデータ拡張機能の使用に関する詳細な情報です。  
  
  
## <a name="see-also"></a>参照  
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
