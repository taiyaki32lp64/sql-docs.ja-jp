---
title: データ プロファイル ビューアーの F1 ヘルプ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], viewer
ms.assetid: 3469c60a-8f4f-46ba-999a-cb9070197fea
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8572feb3e9eb3ac5ba7ba8a3d61abb2ad2dc1b5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059720"
---
# <a name="data-profile-viewer-f1-help"></a>Data Profile Viewer の F1 ヘルプ
  Data Profile Viewer を使用すると、データ プロファイル タスクの出力を表示できます。  
  
 Data Profile Viewer の使用方法の詳細については、「 [Data Profile Viewer](control-flow/data-profile-viewer.md)」を参照してください。 データ プロファイル タスクの使用方法の詳細については、「 [データ プロファイル タスクのセットアップ](control-flow/data-profiling-task.md)」を参照してください。データ プロファイル タスクを使用すると、Data Profile Viewer で分析するプロファイル出力を作成できます。  
  
## <a name="static-options"></a>静的オプション  
 **[ファイル]**  
 データ プロファイル タスクの出力を含む保存済みファイルを参照する場合にクリックします。  
  
 **[プロファイル]** ペイン  
 出力に含まれるプロファイルを表示するには、 **[プロファイル]** ペインのツリーを展開します。 プロファイルを選択し、そのプロファイルの結果を表示します。  
  
 **[メッセージ]** ペイン  
 状態を示すメッセージが表示されます。  
  
 **[ドリル ダウン]** ペイン  
 データ プロファイル タスクで使用されるデータ ソースが使用可能な場合は、出力の値と一致するデータの行が表示されます。  
  
 たとえば、US State 列に対する列の値分布プロファイルの出力を表示している場合に、 **[詳細な値分布]** ペインに "WA" の行が含まれているとします。 **[詳細な値分布]** ペインでこの行をダブルクリックすると、State 列が "WA" であるデータの行が [ドリル ダウン] ペインに表示されます。  
  
## <a name="dynamic-options"></a>動的オプション  
  
### <a name="profile-type--column-length-distribution-profile"></a>プロファイルの種類 = 列長分布プロファイル  
  
#### <a name="column-length-distribution-profile---column-pane"></a>列長分布プロファイル - \<列> ペイン  
 **[最小の長さ]**  
 この列の最小の長さが表示されます。  
  
 **[最大の長さ]**  
 この列の最大の長さが表示されます。  
  
 **[先頭のスペースを無視する]**  
 `IgnoreLeadingSpaces` の値に True または False のいずれを使用してこのプロファイルが計算されたかが表示されます。 このプロパティは、[データ プロファイル タスク エディター] の **[プロファイル要求]** ページで設定されています。  
  
 **[末尾のスペースを無視する]**  
 `IgnoreTrailingSpaces` の値に True または False のいずれを使用してこのプロファイルが計算されたかが表示されます。 このプロパティは、[データ プロファイル タスク エディター] の **[プロファイル要求]** ページで設定されています。  
  
 **行数**  
 テーブルまたはビューの行数が表示されます。  
  
#### <a name="detailed-length-distribution-pane"></a>[詳細な長さ分布] ペイン  
 **長さ**  
 プロファイルされた列の列長が表示されます。  
  
 **Count**  
 プロファイルされた列の値の長さが **[長さ]** 列に表示された長さである行の数が表示されます。  
  
 **[パーセント]**  
 プロファイルされた列の値の長さが **[長さ]** 列に表示された長さである行の割合が表示されます。  
  
### <a name="profile-type--column-null-ratio-profile"></a>プロファイルの種類 = 列の NULL 比プロファイル  
  
#### <a name="column-null-ratio-profile---column-pane"></a>列の NULL 比プロファイル - \<例> ペイン  
 **[NULL カウント]**  
 プロファイルされた列が NULL 値である行の数が表示されます。  
  
 **[NULL 比率]**  
 プロファイルされた列が NULL 値である行の割合が表示されます。  
  
 **行数**  
 テーブルまたはビューの行数が表示されます。  
  
### <a name="profile-type--column-pattern-profile"></a>プロファイルの種類 = 列パターン プロファイル  
  
#### <a name="column-pattern-profile---column-pane"></a>列パターン プロファイル - \<列> ペイン  
 **行数**  
 テーブルまたはビューの行数が表示されます。  
  
#### <a name="pattern-distribution-pane"></a>[パターン分布] ペイン  
 **パターン**  
 プロファイルされた列について計算されたパターンが表示されます。  
  
 **[パーセント]**  
 **[パターン]** 列に表示されたパターンに一致する値を持つ行の割合が表示されます。  
  
### <a name="profile-type--column-statistics-profile"></a>プロファイルの種類 = 列統計プロファイル  
  
#### <a name="column-statistics-profile---column-pane"></a>列統計プロファイル - \<列> ペイン  
 **最小**  
 プロファイルされた列の最小値が表示されます。  
  
 **[最大]**  
 プロファイルされた列の最大値が表示されます。  
  
 **平均**  
 プロファイルされた列の値の平均が表示されます。  
  
 **Standard Deviation**  
 プロファイルされた列の値の標準偏差が表示されます。  
  
### <a name="profile-type--column-value-distribution-profile"></a>プロファイルの種類 = 列の値分布プロファイル  
  
#### <a name="column-value-distribution-profile---column-pane"></a>列の値分布プロファイル - \<列> ペイン  
 **[個別の値数]**  
 プロファイルされた列の個別の値数が表示されます。  
  
 **行数**  
 テーブルまたはビューの行数が表示されます。  
  
#### <a name="detailed-value-distribution-pane"></a>[詳細な値分布] ペイン  
 **[値]**  
 プロファイルされた列の個別の値が表示されます。  
  
 **Count**  
 プロファイルされた列の値が **[値]** 列に表示された値である行の数が表示されます。  
  
 **[パーセント]**  
 プロファイルされた列の値が **[値]** 列に表示された値である行の割合が表示されます。  
  
### <a name="profile-type--candidate-key-profile"></a>プロファイルの種類 = 候補キー プロファイル  
  
#### <a name="candidate-key-profile---table-pane"></a>候補キー プロファイル - \<テーブル> ペイン  
 **[キー列]**  
 プロファイル対象の候補キーとして選択した列が表示されます。  
  
 **[キーの強さ]**  
 候補キーの列または列の組み合わせの強さがパーセンテージで表示されます。 キーの強さが 100% 未満である場合は、重複する値が存在することを示します。  
  
#### <a name="key-violations-pane"></a>[キー違反] ペイン  
 **\<列 1>、\<列 2>、など**  
 プロファイルされた列で見つかった重複する値が表示されます。  
  
 **Count**  
 指定された列の値が最初の列に表示された値である行の数が表示されます。  
  
### <a name="profile-type--functional-dependency-profile"></a>プロファイルの種類 = 機能依存プロファイル  
  
#### <a name="functional-dependency-profile-pane"></a>[機能依存プロファイル] ペイン  
 **[決定列]**  
 決定列として選択した列が表示されます。 米国郵便番号によって州が一意に決定される例の場合、郵便番号は決定列です。  
  
 **[依存列]**  
 依存列として選択した列が表示されます。 米国郵便番号によって州が一意に決定される例の場合、州は依存列です。  
  
 **[機能依存の強さ]**  
 列間の機能依存の強さがパーセンテージで表示されます。 キーの強さが 100% 未満である場合は、決定値によって依存値が決定されないケースがあることを示します。 米国郵便番号によって州が一意に決定される例でキーの強さが 100% 未満である場合は、無効な値が州の列に含まれていることを示します。  
  
#### <a name="functional-dependency-violations-pane"></a>[機能依存違反] ペイン  
  
> [!NOTE]  
>  データに含まれるエラー値の割合が高いと、機能依存プロファイルの結果が予期しない結果になることがあります。 たとえば、"98052" という郵便番号の値に対応する州の値として "WI" という値が 90% の行に含まれている場合、 機能依存プロファイルにより、正しい州の値である "WA" という値の行が違反として報告されます。  
  
 **\<決定列の名前>**  
 違反が検出された機能依存の決定列または列の組み合わせの値が表示されます。  
  
 **\<依存列の名前>**  
 違反が検出された機能依存の依存列の値が表示されます。  
  
 **サポート数 (Support Count)**  
 決定列の値によって依存列が決定される行の数が表示されます。  
  
 **[違反カウント]**  
 決定列の値によって依存列が決定されない行の数が表示されます (依存値が **\<依存列の名前>** 列に表示された値である行。)  
  
 **サポート比率 (Support Percentage)**  
 決定列によって依存列が決定される行の割合が表示されます。  
  
### <a name="profile-type--value-inclusion-profile"></a>プロファイルの種類 = 値包含プロファイル  
  
#### <a name="value-inclusion-profile-pane"></a>[値包含プロファイル] ペイン  
 **[サブセット側の列]**  
 スーパーセット列の一部であるかどうかを判断するためにプロファイルされた列または列の組み合わせが表示されます。  
  
 **[スーパーセット側の列]**  
 サブセット列の値が含まれているかどうかを判断するためにプロファイルされた列または列の組み合わせが表示されます。  
  
 **[包含の強さ]**  
 列間の重複の強さがパーセンテージで表示されます。 キーの強さが 100% 未満である場合は、サブセットの値がスーパーセットの値の中に含まれていないケースがあることを示します。  
  
#### <a name="inclusion-violations-pane"></a>[包含違反] ペイン  
 **\<列 1>、\<列 2>、など**  
 スーパーセット列に含まれていないサブセット列の値が表示されます。  
  
 **Count**  
 指定された列の値が最初の列に表示された値である行の数が表示されます。  
  
## <a name="see-also"></a>参照  
 [Data Profile Viewer](control-flow/data-profile-viewer.md)   
 [データ プロファイル タスクとビューアー](control-flow/data-profiling-task-and-viewer.md)  
  
  
