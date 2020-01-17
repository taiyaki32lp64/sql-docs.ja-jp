---
title: XML へのエクスポート (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 11d72068-2d97-495e-948f-12d1e8c1957d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8e8809b53078387fa58a961458693122753698e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107896"
---
# <a name="exporting-to-xml-report-builder-and-ssrs"></a>XML へのエクスポート (レポート ビルダーおよび SSRS)
  XML 表示拡張機能では、レポートが XML 形式で返されます。 レポート XML のスキーマは、レポート固有のものであり、データのみを含んでいます。 XML 表示拡張機能では、レイアウト情報はレンダリングされません。また、改ページ位置も維持されません。 この拡張機能で生成された XML は、データベースにインポートしたり、XML データ メッセージとして使用したり、カスタム アプリケーションに送信することができます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItems"></a> レポート アイテム  
 次の表で、レポート アイテムがどのように表示されるかについて説明します。  
  
|アイテム|表示動作|  
|----------|------------------------|  
|レポート|XML ドキュメントのトップレベルの要素として表示されます。|  
|データ領域|コンテナーの要素内部の要素として表示されます。 データ領域には、データをテキストおよびグラフとして表示するテーブル、マトリックス、一覧、およびデータを視覚化するデータ バー、スパークライン、ゲージ、インジケーターが含まれます。|  
|グループ セクションおよび詳細セクション|各インスタンスにより、コンテナーの要素内部の要素として表示されます。|  
|テキスト ボックス|コンテナー内部の属性または要素として表示されます。|  
|四角形|コンテナー内部の要素として表示されます。|  
|マトリックスの列グループ|行グループ内部の要素として表示されます。|  
|マップ|コンテナーの要素内部の要素として表示されます。 マップ レイヤーはマップの子要素で、各マップ レイヤーにはそのマップ メンバーの要素とマップ メンバーの属性が含まれています。|  
|グラフ|コンテナーの要素内部の要素として表示されます。 系列はグラフの子要素であり、カテゴリは系列の子要素です。 それぞれのグラフ値にすべてのグラフ ラベルをレンダリングします。 ラベルと値は属性として含まれています。|  
|データ バー|グラフと同様、コンテナーの要素内部の要素としてレンダリングされます。 通常、データ バーには値のみが含まれ、階層またはラベルは含まれません。|  
|スパークライン|グラフと同様、コンテナーの要素内部の要素としてレンダリングされます。 通常、スパークラインには値のみが含まれ、階層またはラベルは含まれません。|  
|ゲージ|コンテナーの要素内部の要素として表示されます。 スケールの最小値/最大値、範囲の開始値/終了値、および属性としてポインターの値を含む単一の要素としてレンダリングします。|  
|インジケーター|ゲージと同様、コンテナーの要素内部の要素としてレンダリングされます。 アクティブな状態名、使用可能な状態、およびデータ値を属性として持つ単一の要素としてレンダリングされます。|  
  
 また、XML 表示拡張機能を使用してレンダリングされるレポートには、以下の規則があります。  
  
-   XML 要素および XML 属性は、レポート定義に出現する順序で表示されます。  
  
-   ページ割り当ては無視されます。  
  
-   ページのヘッダーおよびフッターはレンダリングされません。  
  
-   表示/非表示を切り替えても表示できない非表示アイテムはレンダリングされません。 最初に表示されているアイテムと、表示/非表示を切り替えると表示できる非表示アイテムは表示されます。  
  
-   `Images, lines, and custom report items`画像、線、およびカスタム レポート アイテムは無視されます。  
  
##  <a name="DataTypes"></a> データ型  
 テキスト ボックスの要素または属性には、テキスト ボックスに表示される値に基づいた XSD データ型が割り当てられます。  
  
|テキスト ボックスの値|割り当てられるデータ型|  
|--------------------------------|---------------------------|  
|`Int16`, `Int32`, `Int64`, `UInt16`, `UInt32`, `UInt64`, `Byte`, `SByte`|**xsd:integer**|  
|`Decimal` (または `Decimal` と任意の整数かバイト データ型)|**xsd:decimal**|  
|`Float` (または `Decimal` と任意の整数かバイト データ型)|**xsd:float**|  
|`Double` (または `Decimal` と任意の整数かバイト データ型)|**xsd:double**|  
|`DateTime or DateTime Offset`|**xsd:dateTime**|  
|`Time`|**xsd:string**|  
|`Boolean`|**xsd:boolean**|  
|`String`, `Char`|**xsd:string**|  
|その他|**xsd:string**|  
  
##  <a name="XMLSpecificRenderingRules"></a> XML 固有の表示規則  
 次のセクションでは、レポート内のアイテムが XML 表示拡張機能によってどのように解釈されるかについて説明します。  
  
### <a name="report-body"></a>レポート本文  
 レポートは、XML ドキュメントのルート要素としてレンダリングされます。 要素の名前は、プロパティ ペインで設定された DataElementName プロパティから取得されます。  
  
 レポート要素には、XML 名前空間の定義とスキーマ参照属性も含まれます。 以下の例では、変数が太字で示されています。  
  
 \<**Report** xmlns="**SchemaName**" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xsi:**schemaLocation**="**SchemaNameReportURL**&amp;rc%3aSchema=true" Name="ReportName">  
  
 それぞれの変数の値は次のとおりです。  
  
|名前|値|  
|----------|-----------|  
|レポート|Report.DataElementName|  
|ReportURL|サーバー上のレポートに対する絶対 URL です。URL エンコードされます。|  
|SchemaName|Report.SchemaName。 NULL の場合は、Report.Name になります。 Report.Name が使用された場合、まず XmlConvert.EncodeLocalName でエンコードされます。|  
|ReportName|レポートの名前です。|  
  
### <a name="text-boxes"></a>テキスト ボックス  
 テキスト ボックスは、DataElementStyle RDL プロパティに応じて、要素または属性としてレンダリングされます。 要素名または属性名は TextBox.DataElementName RDL プロパティから取得されます。  
  
### <a name="charts-data-bars-and-sparklines"></a>グラフ、データ バー、およびスパークライン  
 グラフ、データ バー、およびスパークラインは XML でレンダリングされます。 データは構造化されます。  
  
### <a name="gauges-and-indicators"></a>ゲージとインジケーター  
 ゲージとインジケーターは XML でレンダリングされます。 データは構造化されます。  
  
### <a name="subreports"></a>サブレポート  
 サブレポートは要素としてレンダリングされます。 要素名は DataElementName RDL プロパティから取得されます。 レポートの TextBoxesAsElements プロパティ設定は、サブレポートのプロパティ設定をオーバーライドします。 サブレポート要素に名前空間および XSLT 属性は追加されません。  
  
### <a name="rectangles"></a>四角形  
 四角形は要素としてレンダリングされます。 要素名は DataElementName RDL プロパティから取得されます。  
  
### <a name="custom-report-items"></a>カスタム レポート アイテム  
 表示拡張機能は、CustomReportItems (CRI) を認識しません。 レポートにカスタム レポート アイテムが存在した場合は、標準的なレポート アイテムとしてレンダリングされます。  
  
### <a name="images"></a>画像  
 画像はレンダリングされません。  
  
### <a name="lines"></a>線  
 線はレンダリングされません。  
  
### <a name="tables-matrices-and-lists"></a>テーブル、マトリックス、および一覧  
 テーブル、マトリックス、および一覧は要素としてレンダリングされます。 要素の名前は、Tablix の DataElementName RDL プロパティから取得されます。  
  
#### <a name="rows-and-columns"></a>行および列  
 列は行内にレンダリングされます。  
  
#### <a name="tablix-corner"></a>Tablix コーナー  
 コーナーはレンダリングされません。 レンダリングされるのは、コーナーの内容のみです。  
  
#### <a name="tablix-cells"></a>Tablix セル  
 Tablix セルは、要素としてレンダリングされます。 要素名は、セルの DataElementName RDL プロパティから取得されます。  
  
#### <a name="automatic-subtotals"></a>自動集計  
 Tablix 自動集計はレンダリングされません。  
  
#### <a name="row-and-column-items-that-do-not-repeat-with-a-group"></a>グループ単位で繰り返し表示されることのない行アイテムと列アイテム  
 ラベル、小計、合計など、グループ単位で繰り返し表示されることのないアイテムは、要素としてレンダリングされます。 要素の名前は、TablixMember.DataElementName RDL プロパティから取得されます。  
  
 非繰り返しアイテムがレンダリングされるかどうかは、TablixMember.DataElementOutput RDL プロパティによって制御されます。  
  
 Tablix メンバーの DataElementName プロパティが設定されていなかった場合は、非繰り返しアイテムの名前が、次の形式で動的に生成されます。  
  
 RowX – 非繰り返し行の場合 (X は、現在の親内の 0 から始まる行インデックス)。  
  
 ColumnY – 非繰り返し列の場合 (Y は、現在の親内の 0 から始まる列インデックス)。  
  
 非繰り返しヘッダーは、グループ単位で繰り返し表示されることのない行または列の子としてレンダリングされます。  
  
 非繰り返しメンバーに対応する Tablix セルが存在しない場合、そのメンバーはレンダリングされません。 このようなケースとしては、複数の列にまたがる Tablix セルなどが考えられます。  
  
#### <a name="rows-and-columns-that-repeat-with-a-group"></a>グループ単位で繰り返し表示される行と列  
 グループ単位で繰り返し表示される行および列は、Tablix.DataElementOutput の規則に従ってレンダリングされます。 要素名は DataElementName プロパティから取得されます。  
  
 グループ内の一意の値は、それぞれ、そのグループの子要素としてレンダリングされます。 要素名は Group.DataElementName プロパティから取得されます。  
  
 DataElementOutput プロパティの値が Output と等しい場合、繰り返しアイテムのヘッダーが、detail 要素の子としてレンダリングされます。  
  
##  <a name="CustomFormatsXSLTransformations"></a> カスタム形式および XSL 変換  
 XML 表示拡張機能で生成した XML ファイルは、XSL 変換 (XSLT) を使用してほとんどすべての形式に変換できます。 この機能を使用すると、既存の表示拡張機能ではサポートされていない形式でデータを生成できます。 独自の表示拡張機能の作成を試みる前に、XML 表示拡張機能および XSLT を使用することを検討してください。  
  
##  <a name="DuplicateName"></a> 重複する名前  
 同じスコープ内に重複するデータ要素名が存在する場合、レンダラーからエラー メッセージが表示されます。  
  
##  <a name="XSLTTransformations"></a> XSLT 変換  
 XML レンダラーでは、元の XML データに対し、サーバー側で XSLT 変換を適用できます。 XSLT が適用された場合、元の XML データの代わりに、変換済みのコンテンツが出力されます。 変換はクライアント側ではなく、サーバー側で実行されます。  
  
 出力結果に適用する XSLT は、レポート定義ファイル内で、レポートの DataTransform プロパティまたは XSLT の *DeviceInfo* パラメーターで定義します。 いずれかの値が設定されている場合、XML レンダラーを使用するたびに変換が実行されます。 サブスクリプションを使用する場合は、RDL DataTransform プロパティで XSLT を定義する必要があります。  
  
 DataTransform 定義プロパティおよびデバイス情報設定の両方で XSLT ファイルを指定した場合は、最初に DataTransform で指定された XSLT が適用され、続けて、デバイス情報設定による XSLT が適用されます。  
  
###  <a name="DeviceInfo"></a> デバイス情報設定  
 デバイス情報設定を変更することによって、このレンダラーの既定の設定の一部を変更することができます。変更できる設定には、次のようなものがあります。  
  
-   XML に適用する変換 (XSLT)  
  
-   XML ドキュメントの MIME の種類  
  
-   データに書式文字列を適用するかどうか  
  
-   XML 出力をインデントするかどうか  
  
-   XML スキーマ名を含めるかどうか  
  
-   XML ドキュメントのエンコーディング。  
  
-   XML ドキュメントのファイル拡張子  
  
 詳細については、「 [XML デバイス情報設定](../xml-device-information-settings.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services の改ページ &#40;レポート ビルダーおよび SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [さまざまなレポート表示拡張機能の対話機能 &#40;レポート ビルダーおよび SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [レポート アイテムのレンダリング &#40;レポート ビルダーおよび SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
