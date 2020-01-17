---
title: クエリ ビルダー (レポート ウィザード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.dataview.vdtquerydesigner.f1
- sql12.rtp.rptwizard.querybuilder.f1
helpviewer_keywords:
- Query Builder [Reporting Services]
ms.assetid: 1b0904ea-28c1-448e-b56c-c0fdfbc8b222
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8d289466fcff56a78172c54f24a093e0af169484
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107994"
---
# <a name="query-builder-report-wizard"></a>クエリ ビルダー (レポート ウィザード)
  クエリ ビルダーを使用すると、レポートで使用する結果セットを取得するためのクエリを指定できます。 2 種類のクエリ ビルダーを選択できます。  
  
-   テキスト ベースのクエリ ビルダー (既定) は、クエリを指定して結果を表示するための単純なワークスペースを備えています。 複数の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント、カスタム データ処理拡張機能のクエリまたはコマンド構文、および式としてのクエリを指定できます。 汎用クエリ ビルダーはクエリを前処理せず、どんな種類のクエリ構文にも対応するので、レポート デザイナーの既定のクエリ ビルダー ツールとして設定されています。  
  
-   グラフィカル クエリ ビルダーでは、より視覚的な操作が可能です。 これは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] と [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の他の部分で使用されます。 式を作成しない場合や、複数の要素で構成される SQL ステートメントを作成しない場合に、グラフィカル クエリ ビルダーを使用できます。  
  
     グラフィカル クエリ ビルダーに切り替えるには、ウィンドウの左上隅にある **[テキストとして編集]** ボタンを切り替えます。  
  
 別のレポートからクエリをインポートすることもできます。  
  
## <a name="query-builder-options"></a>クエリ ビルダーのオプション  
 **[テキストとして編集]**  
 テキスト ベースのクエリ デザイナーとグラフィカル クエリ デザイナーを切り替えます (両方のデザイナーが使用できる場合)。  
  
 **[インポート]**  
 **[クエリのインポート]** ダイアログ ボックスを開き、利用可能なレポートの .rdl ファイルおよび .sql ファイルを表示します。 インポートされたクエリはそのまま使用することもできますが、クエリ ビルダーで修正することもできます。  
  
 **演算子(実行)**  
 クエリを実行し、クエリが有効であれば結果セットを返します。 クエリが式の場合、そのクエリは実行できません。 式に基づくクエリかどうかを確認するには、レポートをプレビューする必要があります。  
  
 **コマンドの種類**  
 テキスト、ストアド プロシージャ、またはテーブルを直接指定します。 使用できるコマンドの種類は、指定したデータ処理拡張機能によって異なります。  
  
 **[クエリ] ペイン**  
 クエリを入力します。  
  
 **結果ペイン**  
 クエリから返された結果セットが表示されます。  
  
## <a name="see-also"></a>参照  
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [レポート ウィザードのヘルプ](../../2014/reporting-services/report-wizard-help.md)  
  
  
