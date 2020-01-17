---
title: OData ソース | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ODATASOURCE.F1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b6b4aeb4059ba659a3188712b1ce76f10efd030
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771038"
---
# <a name="odata-source"></a>OData ソース
  SSIS パッケージ内で OData ソース コンポーネントを使用して、Open Data Protocol (OData) サービスから取得したデータを使用します。 このコンポーネントは、OData v2 と v3 の各プロトコル、および ATOM と JSON の各データ形式をサポートします。  
  
> [!NOTE]  
>  OData ソースを使用して、SharePoint リストから読み取りを行うことができます。 SharePoint サーバー上のすべてのリストを表示するには、次の URL を使用: http://\<server >//_vti_bin/listdata.svc。 SharePoint の URL の規則に関する詳細については、「 [SharePoint Foundation REST インターフェイス](https://msdn.microsoft.com/library/ff521587.aspx)」を参照してください。  
  
## <a name="odata-format"></a>OData の形式  
 ほとんどの OData サービスは、結果を複数の形式で返します。 $format クエリ オプションを使用して、結果セットの形式を指定することができます。 JSON と JSON Light のような形式は、ATOM/XML より効率的であり、大量のデータを転送する場合により高いパフォーマンスを達成できる可能性があります。 次の表に、サンプル テストの結果を示します。 ご覧のように、ATOM から新しい JSON light 形式 (WCF Data Services 5.1 で使用可能) に切り替える場合、ATOM から JSON と 67% パフォーマンスの向上に切り替える場合がありますが 30 ~ 53% パフォーマンスが向上します。  
  
|||||  
|-|-|-|-|  
|[行]|ATOM|JSON|JSON (Light)|  
|10000|113 秒|74 秒|68 秒|  
|1000000|1110 秒|853 秒|665 秒|  
  
> [!NOTE]  
>  SSIS OData ソースは、ODataLib 5.5.0 を使用して OData フィードを分析し、このライブラリでサポートされているすべてのフォーマットを読み取ることができます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [OData ソース コンポーネントのインストールと、アンインストール](../install-and-uninstall-odata-source-component.md)  
  
-   [チュートリアル: OData ソースを使用して&#91;SSIS&#93;](tutorial-using-the-odata-source.md)  
  
-   [実行時の OData ソース クエリの変更](modify-odata-source-query-at-runtime.md)  
  
-   [[OData ソース エディター] &#40;[接続] ページ&#41;](../odata-source-editor-connection-page.md)  
  
-   [[OData ソース エディター] &#40;[列] ページ&#41;](../odata-source-editor-columns-page.md)  
  
-   [OData ソース エディター &#40;[エラー出力] ページ&#41;](../odata-source-editor-error-output-page.md)  
  
-   [OData ソースのプロパティ](odata-source-properties.md)  
  
## <a name="see-also"></a>参照  
 [OData 接続マネージャー](../connection-manager/odata-connection-manager.md)  
  
  
