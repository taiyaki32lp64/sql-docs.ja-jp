---
title: XML エディター (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.editor.xml.f1
- sql13.swb.editorxml.f1
- vs.xmleditor
- sql13.swb.xmleditor.f1
helpviewer_keywords:
- XML Designer [SQL Server Management Studio]
ms.assetid: 0824a5ce-e67b-4b53-98d9-d371faf2d23c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f9b82bec0f3def57ac575b4e338e437c05f0bbd1
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68252827"
---
# <a name="xml-editor-sql-server-management-studio"></a>XML エディター (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  XML スキーマ、ADO.NET データセット、および XML ドキュメントを操作するためのビジュアルなツールのセットが用意されています。 XML デザイナーは、WC3 (World Wide Web Consortium) で定義されている XML スキーマ定義 (XSD) 言語をサポートします。 デザイナーは、DTD (文書型定義) や XDR (XML-Data Reduced) などのその他の XML スキーマ言語をサポートしません。  
  
 デザイナーを表示するには、データセット、XML スキーマ、または XML ファイルをプロジェクトに追加するか、次の表に示す種類のファイルを開きます。  
  
> [!CAUTION]  
>  スキーマ ビューでは、 **[元に戻す]** コマンドを使用できません。 作業を慎重に計画すると共に、頻繁にファイルを保存してください。  
  
 デザイナーで XML ファイル、XML スキーマ、およびデータセットを操作する場合は、次の 3 つのビュー (またはモード) を使用できます。  
  
|表示|[説明]|サポートされるファイルの種類|  
|----------|-----------------|--------------------------|  
|**[スキーマ]**|XML スキーマおよび ADO.NET データセットをビジュアルに作成および変更するために使用します。|.xsd|  
|**データ**|XML データ ファイルを構造化データ グリッドでビジュアルに変更するために使用します。|.xml|  
|**XML**|XML を編集するために使用します。ソース エディターには、色分け表示機能や、入力候補およびメンバーの一覧を含む IntelliSense 機能があります。|.xml、.xsd、.xslt、.wsdl、.web、.resx、.tdl、.wsf、.hta、.disco、.vsdisco、.config|  
|**プラン表示**|SET SHOWPLAN_XML ON オプションを使用して作成された XML クエリ プランを表示します。|.showplan|  
  
## <a name="schema-view"></a>スキーマ ビュー  
 スキーマ ビューでは、XML スキーマおよび ADO.NET データセットを構成する要素、属性、型などをビジュアルに表示します。  
  
 スキーマ ビューでは、ツールボックスの [XML スキーマ] タブまたはサーバー エクスプローラーからデザイン領域に要素をドロップすることによって、スキーマおよびデータセットを構築できます。 また、デザイン領域上で右クリックし、ショートカット メニューの [追加] をクリックして、要素をデザイナーに追加することもできます。  
  
 スキーマ ビューでは、次の操作を行うことができます。  
  
-   既存の XML スキーマおよび ADO.NET データセットを構築および変更する。  
  
-   テーブル間の関係を作成および編集する。  
  
-   キーを作成および編集する。  
  
-   XML スキーマから ADO.NET データセットを生成する。  
  
> [!NOTE]  
>  スキーマ ビューでの要素のレイアウトは、.xsx ファイルに保存されます。このファイルを確認するには、[ソリューション エクスプローラー] のツール バーの **[すべてのファイルを表示]** をクリックし、目的の .xsd ファイルを展開します。 .xsd ファイルが存在しない場合は、これまで XML デザイナーでは .xsd ファイルを開いていないことを示しています。  
  
### <a name="customizing-schema-view"></a>スキーマ ビューのカスタマイズ  
 次の機能を使用すると、スキーマ ビューでの要素のビジュアルなレイアウトを変更できます。  
  
-   ズーム  
  
-   入れ子になった要素の展開と折りたたみ  
  
-   要素の自動レイアウト  
  
-   展開された要素の既定の状態のリセット  
  
##### <a name="to-expand-hidden-nested-elements"></a>入れ子になった非表示の要素を展開するには  
  
-   要素の下部の正符号アイコンをクリックします。  
  
##### <a name="to-collapse-nested-elements"></a>入れ子になった要素を折りたたむには  
  
-   デザイナーに表示する最下位レベルにある要素の負符号アイコンをクリックします。  
  
## <a name="data-view"></a>データ ビュー  
 データ ビューでは、.xml ファイルを編集するためにデータ グリッドを使用できます。 データ ビューでは、XML ファイルの内容 (タグおよび構造体を除く) だけを編集できます。  
  
 データ ビューには 2 つの独立した領域があります: **[データ テーブル]** と **[データ]** です。 **[データ テーブル]** 領域には、XML ファイルに定義されている関係の一覧がその入れ子の順 (最も外側から最も内側の順) に示されます。 **[データ]** 領域は、[データ テーブル] 領域の選択内容に基づいてデータを表示するデータ グリッドです。  
  
> [!NOTE]  
>  新しく作成された XML ファイルにはデータは含まれていないので、データ ビューに表示することはできません。 また、データ ビューをまったく呼び出すことができない XML ドキュメントのインスタンスもあります。 XML は適切な形式と見なされますが、構造化データではない場合、データ ビューに切り替えようとすると次のメッセージが表示されます:「このドキュメントは正しい形式ですが、データ ビューで表示できない構造を含んでいます。」  
  
 データ ビューでは、次の操作を行うことができます。  
  
-   データ テーブルに手動でデータを入力する。  
  
-   既存のデータ テーブルを編集する。  
  
-   XML ドキュメントから XML スキーマを生成する。  
  
## <a name="xml-view"></a>XML ビュー  
 XML ビューは、生の XML を編集するためのエディターを提供すると共に、IntelliSense および色分け表示機能を提供します。 入力候補機能は、関連スキーマを持つ .xsd ファイルおよび .xml ファイルを操作している場合に使用できます。 「<」と入力してタグを開始すると、その位置で有効な要素の一覧が表示されます。 要素名を入力し、Space キーを押すと、その要素でサポートされる属性の一覧が表示されます。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense オプションは、ツール バーからは利用できません。 XML エディターを使用しているときにこれらのオプションにアクセスするには、 **[編集]** メニューの **[IntelliSense]** をクリックします。  
  
## <a name="showplan-view"></a>プラン表示ビュー  
 クエリ プランは、作成時に SET SHOWPLAN_XML ON オプションを使用して XML 形式で保存できます。 拡張子が .showplan のファイルをダブルクリックすると、クエリ プランが表示されます。  
  
## <a name="see-also"></a>参照  
 [XML 形式での実行プランの保存](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
