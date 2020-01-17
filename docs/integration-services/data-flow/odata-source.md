---
title: OData ソース | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
- sql13.dts.designer.odatasource.connection.f1
- sql13.dts.designer.odatasource.columns.f1
- sql13.dts.designer.odatasource.erroroutput.f1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3972714722b800cdd4400739f40d8eb8c6c3eff7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298225"
---
# <a name="odata-source"></a>OData ソース

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Open Data Protocol (OData) サービスからのデータを使用するには、SSIS パッケージの OData ソース コンポーネントを使用します。

## <a name="supported-protocols-and-data-formats"></a>サポートされるプロトコルとデータ形式

このコンポーネントは、OData v3 プロトコルと v4 プロトコルをサポートします。  
  
-   OData V3 プロトコルでは、コンポーネントは ATOM および JSON データ形式をサポートします。  
  
-   OData V4 プロトコルでは、コンポーネントは JSON データ形式をサポートします。  

## <a name="supported-data-sources"></a>サポートされるデータ ソース

OData ソースには、次のデータ ソースのサポートが含まれます。
-   Microsoft Dynamics AX Online および Microsoft Dynamics CRM Online
-   SharePoint リスト。 SharePoint サーバーのすべてのリストを表示するには、 https://\<server>/_vti_bin/ListData.svc という URL を使用します。 SharePoint の URL の規則に関する詳細については、「 [SharePoint Foundation REST インターフェイス](https://msdn.microsoft.com/library/ff521587.aspx)」を参照してください。

## <a name="supported-data-types"></a>サポートされるデータ型

OData ソースは、次の単純なデータ型をサポートしています: int、byte[]、bool、byte、DateTime、DateTimeOffset、decimal、double、Guid、Int16、Int32、Int64、sbyte、float、string、TimeSpan。

データ ソース内の列のデータ型を確認するには、`https://<OData feed endpoint>/$metadata` ページをチェックしてください。

> [!IMPORTANT]
> SharePoint リストでは、複数選択項目など、複雑な種類を OData ソース コンポーネントで利用できません。

## <a name="odata-format-and-performance"></a>OData の形式とパフォーマンス
 ほとんどの OData サービスは、結果を複数の形式で返すことができます。 `$format` クエリ オプションを使用して、結果セットの形式を指定することができます。 JSON と JSON Light のような形式は、ATOM または XML より効率的であり、大量のデータを転送する場合により高いパフォーマンスを達成できる可能性があります。 次の表に、サンプル テストの結果を示します。 ここから理解できるように、ATOM から JSON に切り替えるとパフォーマンスが 30 ～ 53% 向上し、Atom から新しい JSON Light 形式 (WCF Data Services 5.1 で使用可能) に切り替えるとパフォーマンスが 67% 向上します。  
  
|[行]|ATOM|JSON|JSON (Light)|  
|-|-|-|-|  
|10000|113 秒|74 秒|68 秒|  
|1000000|1110 秒|853 秒|665 秒|  
  
## <a name="related-topics-in-this-section"></a>このセクションの関連トピック  
  
-   [チュートリアル: OData ソースの使用](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [実行時の OData ソース クエリの変更](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [OData ソースのプロパティ](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="odata-source-editor-connection-page"></a>[OData ソース エディター] ([接続] ページ)
  **[ODBC ソース エディター]** ダイアログ ボックスの **[接続]** ページを使用すると、OData ソースに対応する ODBC 接続マネージャーを選択できます。 また、このページで、コレクションまたはリソースのパスと、どのデータを OData ソースから取得する必要があるかを示すクエリ オプションを指定することができます。 
  
### <a name="static-options"></a>静的オプション  
 **OData 接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 接続マネージャーを選択または作成すると、接続マネージャーで使用されている OData プロトコルのバージョンがダイアログ ボックスに表示されます。  
  
 **[新規作成]**  
 新しい接続マネージャーを作成するには、 **[OData 接続マネージャー エディター]** ダイアログ ボックスを使用します。  
  
 **コレクションまたはリソースのパスを使用します。**  
 ソースからデータを選択する方法を指定します。  
  
|オプション|[説明]|  
|------------|-----------------|  
|Collection|コレクション名を使用して、Odata ソースからデータを取得します。|  
|リソースのパス|リソースのパスを使用して、Odata ソースからデータを取得します。|  
  
 **クエリ オプション**  
 クエリのオプションを指定します。 例: `$top=5` 
  
 **フィード URL**  
 このダイアログ ボックスで選択したオプションに基づいて、読み取り専用のフィード URL を表示します。  
  
 **プレビュー**  
 **[プレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 **プレビュー** では、最大で 20 行を表示できます。  
  
### <a name="dynamic-options"></a>動的オプション  
  
#### <a name="use-collection-or-resource-path--collection"></a>コレクション、またはリソースのパス = Collection を使用します。  
 **Collection**  
 ドロップダウン リストからコレクションを選択します。  
  
#### <a name="use-collection-or-resource-path--resource-path"></a>コレクションまたはリソースのパス = Resource Path を使用します。  
 **Resource path**  
 リソースのパスを入力します。 例:Employees  
  
## <a name="odata-source-editor-columns-page"></a>[OData ソース エディター] ([列] ページ)
  出力に含める外部 (変換元) 列を選択し、それらを出力列にマップするには、 **[OData ソース エディター]** ダイアログ ボックスの **[列]** ページを使用します。  
  
### <a name="options"></a>オプション  
 **使用できる外部列**  
 データ ソース内にある使用可能なソース列の一覧を表示します。 ページの下部にあるテーブルに対して列を追加または削除するには、一覧にあるチェック ボックスを使用します。 選択した列が出力に追加されます。  
  
 **[外部列]**  
 出力に含めるように選択したソース列を表示します。  
  
 **出力列**  
 各出力列の一意な名前を表示します。 既定では選択された外部 (変換元) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。  
  
## <a name="odata-source-editor-error-output-page"></a>[OData ソース エディター] ([エラー出力] ページ)
  **[OData ソース エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択したり、エラー出力列のプロパティを設定したりできます。  
  
### <a name="options"></a>オプション  
 **[入力または出力]**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[ODBC ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで選択されている外部 (変換元) 列を表示します。  
  
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
 [OData 接続マネージャー](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
