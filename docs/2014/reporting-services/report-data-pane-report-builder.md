---
title: レポート データ ペイン (レポート ビルダー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: 1492aa39-aeb1-4509-ab97-b9edd0901b7e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fa8ae6d36ddd7c23b48ec65f8fab387e690f1d83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107557"
---
# <a name="report-data-pane-report-builder"></a>[レポート データ] ペイン (レポート ビルダー)
  **[レポート データ]** ペインを使用すると、レポート内で現在定義されているパラメーター、データ ソース、データセット、フィールド コレクション、および画像が表示されます。 [レポート データ] では、レポート内のデータを表すアイテムの階層ビューが表示されます。 最上位のノードは、組み込みフィールド、パラメーター、画像、およびデータ ソース参照を表します。 データ アイテムを表示するには、各ノードを展開します。 たとえば、データ ソース ノードを展開すると、そのデータ ソース用に定義されたデータセットが表示されます。 データセットを展開すると、そのフィールド コレクションが表示されます。 データをレポート ページ上の選択したレポート アイテムにリンクするには、アイテムをレポート デザイン画面または [グループ化] ペインにドラッグします。 詳細については、「[レポート デザイン ビュー &#40;レポート ビルダー&#41;](report-builder/report-design-view-report-builder.md)」を参照してください。  
  
## <a name="options"></a>および  
 **組み込みフィールド**  
 レポート名、ページ番号など、レポートでよく使用されるフィールドを表します。 詳細については、「[式で使用される組み込みコレクション &#40;レポート ビルダーおよび SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md)」を参照してください。  
  
 **パラメーター**  
 レポート パラメーターのコレクションを表します。各パラメーターには単一の値または複数の値を指定できます。 詳細については、「[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
 **イメージ**  
 レポートで使用されている画像のセットを表します。 詳細については、「[画像 &#40;レポート ビルダーおよび SSRS& #41;](report-design/images-report-builder-and-ssrs.md)」を参照してください。  
  
 **[データ ソース]**  
 埋め込みデータ ソースまたは共有データ ソースの参照を表します。 データ ソースは、レポートのデータのソースを表します。 データ ソースは、そのデータ ソースを使用するデータセットのコレクションの親ノードです。 詳細については、次を参照してください。[レポートへのデータの追加&#40;レポート ビルダーおよび SSRS&#41; ](report-data/report-datasets-ssrs.md)と[データ接続、データ ソース、およびレポート ビルダーでの接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)します。  
  
 **データセット**  
 1 つのコマンドを実行することによってデータ ソースから取得されるデータを表します。たとえば、[!INCLUDE[tsql](../includes/tsql-md.md)] データベースからデータを取得する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリなどがあります。 データセットは、クエリで指定されたフィールドのほか、計算フィールドも含むコレクションの親ノードです。 レポート ビルダーでは、クエリを指定できるようにクエリ デザイナーがサポートされています。 詳細については、次を参照してください。[レポートへのデータの追加&#40;レポート ビルダーおよび SSRS&#41;](report-data/report-datasets-ssrs.md)します。  
  
## <a name="see-also"></a>参照  
 [データセット フィールド コレクション &#40;レポート ビルダーおよび SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [レポート ビルダーのダイアログ ボックス、ペイン、およびウィザードに関するヘルプ](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [グループ化ペイン &#40;レポート ビルダー&#41;](report-design/grouping-pane-report-builder.md)   
 [レポートの検索、表示、管理 &#40;レポート ビルダーおよび SSRS&#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
