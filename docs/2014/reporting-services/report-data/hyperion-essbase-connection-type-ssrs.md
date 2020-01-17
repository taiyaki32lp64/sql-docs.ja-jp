---
title: Hyperion Essbase の接続の種類 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 108a00b6-799f-4066-b796-da59e95c09fd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a0c38487f58a6db6e80d48c2b39b09e3ed93106
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107269"
---
# <a name="hyperion-essbase-connection-type-ssrs"></a>Hyperion Essbase の接続の種類 (SSRS)
  [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 外部データ ソースのデータをレポートに含めるには、種類が [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]のレポート データ ソースに基づいたデータセットが必要です。 このビルトイン データ ソースの種類は、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]のデータ拡張機能に基づいています。この拡張機能を使用すると、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 外部データ ソースから多次元データを取得できます。  
  
 このトピックの情報を使用して、データ ソースを構築してください。 手順については、[データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)を参照してください。  
  
##  <a name="Connection"></a> 接続文字列  
 次の接続文字列例では、13080 番ポートを使用してサーバー上の [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースを指定し、SOAP を使用してインターネット経由の XML for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (XMLA) を指定して、Sample カタログに接続しています。  
  
```  
Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample  
```  
  
 接続文字列の例の詳細については、「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)」を参照してください。  
  
  
##  <a name="Credentials"></a> [資格情報]  
 クエリの実行、ローカルでのレポートのプレビュー、およびレポート サーバーからのレポートのプレビューには、資格情報が必要です。  
  
 レポートをパブリッシュした後、そのデータ ソースに対する資格情報を変更する必要が生じる場合があります。そのレポートをレポート サーバーで実行するときに、データを取得するためのアクセス許可が有効な状態になるようにするためです。  
  
 詳しくは、「[データ接続、データ ソース、および接続文字列 (レポート ビルダーおよび SSRS)](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)」または[レポート ビルダーでの資格情報の指定](../specify-credentials-in-report-builder.md)に関する記事を参照してください。  
  
  
##  <a name="Query"></a> クエリ  
 クエリは、次の方法で指定できます。  
  
-   クエリを対話形式で作成します。 グラフィカル クエリ デザイナーのデザイン モードまたはクエリ モードを使用して、外部データ ソースのメタデータを参照しながら、多次元式 (MDX) 構文のクエリを生成します。  
  
    -   **デザイン ビュー** ディメンション、メンバー、メンバー プロパティ、メジャー、および KPI をメタデータ ブラウザーから **データ** ペインにドラッグして、MDX クエリを作成します。 計算されるメンバー ペインから、計算されるメンバーをデータ ペインにドラッグして、追加のデータセット フィールドを定義できます。  
  
    -   **クエリ ビュー** ： ディメンション、メンバー、メンバー プロパティ、メジャー、および KPI をメタデータ ブラウザーからクエリ ペインにドラッグして、MDX クエリを作成します。 クエリ ペインでは、直接 MDX テキストを編集できます。 計算されるメンバーを計算されるメンバー ペインからクエリ ペインにドラッグして、追加のデータセット フィールドを定義します。  
  
     詳細については、「[Hyperion Essbase クエリ デザイナーのユーザー インターフェイス (レポート ビルダー)](../hyperion-essbase-query-designer-user-interface-report-builder.md)」を参照してください。  
  
-   レポートから既存の MDX クエリをインポートします。 **[クエリのインポート]** ボタンを使用して、.rdl ファイルを参照し、クエリをインポートします。 クエリは、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースに基づく埋め込みデータセットを含むレポートからインポートできます。 MDX クエリを .mdx ファイルから直接インポートすることはできません。  
  
 デザイン時には、クエリを実行して結果セットを表示します。 クエリを作成した後、メタデータから生成されたデータセット フィールド コレクションがレポート データ ペインに表示されます。 レポートの実行時には、外部データ ソースから実際のデータが返されます。  
  
 この [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ処理拡張機能では、拡張データセット フィールド プロパティがサポートされています。 これらの値は外部データ ソースから取得できますが、レポート データ ペインには表示されません。 詳細については、このトピックの「 [拡張フィールド プロパティ](#Extended) 」を参照してください。  
  
  
##  <a name="Parameters"></a> パラメーター  
 クエリ パラメーターを含めるには、クエリ デザイナーのフィルター領域でフィルターを作成し、そのフィルターをパラメーターとして設定します。 各フィルターに対して、使用可能な値を提供するデータセットが自動的に作成されます。 既定では、これらのデータセットはレポート データ ペインに表示されません。 詳細については、「[多次元データのパラメーター値の非表示データセットの表示 &#40;レポート ビルダーおよび SSRS&#41;](show-hidden-datasets-for-parameter-values-multidimensional-data.md)」を参照してください。  
  
 各レポート パラメーターの既定のデータ型は **Text**です。 レポート パラメーターを作成した後に、既定値の変更が必要になる場合があります。 詳細については、「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../report-design/report-parameters-report-builder-and-report-designer.md)のレポート データ ソースに基づいたデータセットが必要です。  
  
  
##  <a name="Extended"></a> 拡張フィールド プロパティ  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ処理拡張機能では、拡張フィールド プロパティがサポートされています。 拡張フィールド プロパティは、`Value` と `IsMissing` に追加する形で、データ処理拡張機能によってデータセットのフィールドに定義されるプロパティです。 拡張プロパティには、定義済みプロパティとカスタム プロパティがあります。 定義済みのプロパティは、複数のデータ ソースに共通のプロパティです。 カスタム プロパティは、各データ ソースの固有のプロパティです。  
  
 拡張フィールド プロパティは、レポート レイアウトにドラッグすることのできるアイテムとして [レポート データ] ウィンドウには表示されません。 その代わりに、このプロパティの親フィールドをレポートにドラッグすることによって、既定のプロパティである `Value` を必要なプロパティに変更することが可能です。  
  
 クエリ デザイナーのメタデータ ペインでフィールドにカーソルを合わせると、拡張フィールド プロパティの名前がツールヒントに表示されます。 基になっているデータの調査に使用できるクエリ デザイナーの詳細については、「 [Hyperion Essbase クエリ デザイナーのユーザー インターフェイス](hyperion-essbase-query-designer-user-interface.md)」を参照してください。  
  
> [!NOTE]  
>  拡張フィールド プロパティに対応する値が存在するのは、そのプロパティが MDX 式に含まれており、レポートを実行して対応するデータセットのデータを取得する際に、データ ソースによって値が提供された場合のみです。 その場合、以下のセクションに示す構文を使用して、すべての式からこれらの `Field` プロパティ値を参照できます。 ただし、これらのフィールドはこのデータ プロバイダーに固有であり、レポート定義言語には含まれないため、これらの値に加えた変更はレポート定義には保存されません。  
  
  
### <a name="predefined-field-properties"></a>定義済みフィールド プロパティ  
 複数のデータ プロバイダーで一般的にサポートされ、レポート データセットの基となる MDX クエリに表示される定義済みフィールド プロパティ。 たとえば、MDX ディメンション プロパティ MEMBER_UNIQUE_NAME は、定義済みレポート データセット フィールド プロパティ `UniqueName` にマッピングされます。 一意な名前の値をテキスト ボックスに入力するには、`=Fields!` *\<FieldName>* `.UniqueName` という式を使用します。  
  
 次の表に、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースで使用できる定義済みフィールド プロパティの一覧を示します。  
  
|**プロパティ**|**型**|**説明/有効値**|  
|------------------|--------------|---------------------------------------|  
|`Value`|`Object`|フィールドのデータ値を指定します。<br /><br /> ディメンション プロパティの場合は、MEMBER_CAPTION にマッピングされます。 メジャーの場合は、データ値にマッピングされます。|  
|`IsMissing`|`Boolean`|フィールドが結果データセットに存在するかどうかを示します。|  
|`FormattedValue`|`String`|主要データの書式設定した値を返します。<br /><br /> MDX 式の FORMATTED_VALUE からマッピングされます。|  
|`BackgroundColor`|`String`|データベースで定義されたフィールドの背景色を返します。<br /><br /> MDX 式の BACK_COLOR からマッピングされます。|  
|`Color`|`String`|データベースで定義されたアイテムの前景色を返します。<br /><br /> MDX 式の FORE_COLOR からマッピングされます。|  
|`UniqueName`|`String`|レベルの完全修飾名を返します。<br /><br /> MDX 式の MEMBER_UNIQUE_NAME からマッピングされます。|  
  
 フィールドおよびフィールド プロパティを式で使用する方法の詳細については、「[式で使用される組み込みコレクション (レポート ビルダーおよび SSRS)](../report-design/built-in-collections-in-expressions-report-builder.md)」を参照してください。  
  
  
### <a name="custom-properties"></a>カスタム プロパティ  
 データ プロバイダーでサポートされ、レポート データセットの基となる MDX クエリで使用される一方で、レポートのデータセット ペインにはそのデータセットのフィールドとして表示されないカスタム フィールド プロパティ。 たとえば、 **[長い名前]** はディメンション レベルで定義されたメンバー プロパティです。 値をテキスト ボックスに入力するには、`=Fields!` *\<FieldName>* `("Long Names")` という式を使用します。 この式ではフィールド名の大文字と小文字が区別されます。  
  
 カスタム拡張プロパティを式の中で参照するには、次の構文を使用します。  
  
-   *Fields!FieldName("PropertyName")*  
  
 次の表に、 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースで使用できるカスタム フィールド プロパティを示します。  
  
|**プロパティ**|**型**|**説明/有効値**|  
|------------------|--------------|---------------------------------------|  
|`FORMAT_STRING`|`String`|メジャーで定義されます。String 型として使用できる `FormattedValue` です。|  
  
  
##  <a name="Remarks"></a> 解説  
 このデータ プロバイダーでは使用できないレポート配信モードもあります。 このデータ処理拡張機能では、データ ドリブン サブスクリプションを使ったレポートの配信はサポートされません。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312) の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のドキュメントの「[サブスクライバー データに対して外部データ ソースを使用する &#40;データ ドリブン サブスクリプション&#41;](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)」を参照してください。  
  
 詳細については、「 [SQL Server 2005 Reporting Services を Hyperion Essbase と組み合わせて使用する方法](https://go.microsoft.com/fwlink/?LinkId=81970)」を参照してください。  
  
  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 データ接続、データ ソース、およびデータセットを操作する手順について説明します。  
  
 [データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [データセットへのフィルターの追加 (レポート ビルダーおよび SSRS)](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 関連項目  
 次に示すセクションでは、レポート データの概念が詳細に説明されているほか、データに関連するレポートのパーツを定義し、カスタマイズし、使用する方法が説明されています。  
  
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-datasets-ssrs.md)  
 レポートのデータへのアクセスの概要について説明します。  
  
 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 データ接続とデータ ソースについて説明します。  
  
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 埋め込みデータセットと共有データセットについて説明します。  
  
 [データセット フィールド コレクション (レポート ビルダーおよび SSRS)](dataset-fields-collection-report-builder-and-ssrs.md)  
 データセット クエリによって生成されるフィールド コレクションについて説明します。  
  
 [Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312)の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ドキュメント)。  
 各データ拡張機能のプラットフォームおよびバージョン サポートに関する詳細な情報です。  
  
 [SQL Server 2005 Reporting Services を Hyperion Essbase と組み合わせて使用する方法](https://go.microsoft.com/fwlink/?LinkId=81970)  
 このデータ拡張機能の使用に関する詳細な情報です。  
  
  
## <a name="see-also"></a>参照  
 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
