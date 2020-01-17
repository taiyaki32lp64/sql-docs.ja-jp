---
title: Integration Services の変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transformations [Integration Services], listed
- transformations [Integration Services], types
- transformations [Integration Services]
- data flow [Integration Services], transformations
- business intelligence transformations [Integration Services]
- join transformations
- split transformations [Integration Services]
- custom transformations [Integration Services]
- row transformations [Integration Services]
- rowset transformations [Integration Services]
ms.assetid: c70c4f6e-82dd-4948-b923-fd5193f67f7e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 26b22a82491d3f4c586c3fb259bf50c6d7216367
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297908"
---
# <a name="integration-services-transformations"></a>Integration Services の変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] の変換とは、パッケージのデータ フロー内にある、データを集計、マージ、配信、および変更するコンポーネントのことです。 変換では、参照操作を実行してサンプル データセットを生成することもできます。 このセクションでは、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] に含まれる変換と、その機能について説明します。  
  
## <a name="business-intelligence-transformations"></a>ビジネス インテリジェンス変換  
 次の変換は、データのクリーンアップ、テキストのマイニング、データ マイニング予測クエリの実行などのビジネス インテリジェンス操作を実行します。  
  
|変換|[説明]|  
|--------------------|-----------------|  
|[緩やかに変化するディメンション変換](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)|緩やかに変化するディメンションの更新を構成する変換です。|  
|[あいまいグループ化変換](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)|列データの値を標準化する変換です。|  
|[あいまい参照変換](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)|あいまい一致を使用して、参照テーブル内の値を参照する変換です。|  
|[用語抽出変換](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)|テキストから用語を抽出する変換です。|  
|[用語参照変換](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)|参照テーブル内の用語を参照し、テキストから抽出した用語をカウントする変換です。|  
|[データ マイニング クエリ変換](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|データ マイニング予測クエリを実行する変換です。|  
|[DQS クレンジング変換](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)|作成されたルールを接続されたデータ ソースに適用することにより、そのデータ ソースのデータを修正する変換です。|  
  
## <a name="row-transformations"></a>行の変換  
 次の変換は、列の値を更新して新しい列を作成します。 この変換は、変換入力の各行に適用されます。  
  
|変換|[説明]|  
|--------------------|-----------------|  
|[文字マップ変換](../../../integration-services/data-flow/transformations/character-map-transformation.md)|文字列関数を文字データに適用する変換です。|  
|[列コピー変換](../../../integration-services/data-flow/transformations/copy-column-transformation.md)|入力列のコピーを変換出力に追加する変換です。|  
|[データ変換の変換](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)|列のデータ型を別のデータ型に変換する変換です。|  
|[派生列変換](../../../integration-services/data-flow/transformations/derived-column-transformation.md)|式の結果を列に設定する変換です。|  
|[列エクスポート変換](../../../integration-services/data-flow/transformations/export-column-transformation.md)|データ フローのデータをファイルに挿入する変換です。|  
|[列インポート変換](../../../integration-services/data-flow/transformations/import-column-transformation.md)|ファイルのデータを読み取り、データ フローに追加する変換です。|  
|[スクリプト コンポーネント](../../../integration-services/data-flow/transformations/script-component.md)|スクリプトを使用して、データの抽出、変換、または読み込みを行う変換です。|  
|[OLE DB コマンド変換](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)|データ フローの各行で、SQL コマンドを実行する変換です。|  
  
## <a name="rowset-transformations"></a>行セットの変換  
 次の変換は、新しい行セットを作成します。 行セットには、集計された値や並べ替えた値、サンプル行セット、またはピボットされた行セットとピボットされていない行セットを含めることができます。  
  
|変換|[説明]|  
|--------------------|-----------------|  
|[集計変換](../../../integration-services/data-flow/transformations/aggregate-transformation.md)|AVERAGE、SUM、COUNT などの集計を実行する変換です。|  
|[並べ替え変換](../../../integration-services/data-flow/transformations/sort-transformation.md)|データを並べ替える変換です。|  
|[比率サンプリング変換](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)|サンプル サイズを指定する割合を使用して、サンプル データを作成する変換です。|  
|[行サンプリング変換](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)|サンプルの行数を指定して、サンプル データセットを作成する変換です。|  
|[ピボット変換](../../../integration-services/data-flow/transformations/pivot-transformation.md)|正規化されたテーブルの、正規化されていないバージョンを作成する変換です。|  
|[ピボット解除変換](../../../integration-services/data-flow/transformations/unpivot-transformation.md)|正規化されていないテーブルの、正規化されたバージョンを作成する変換です。|  
  
## <a name="split-and-join-transformations"></a>分割および結合変換  
 次の変換は、別の出力への行の配信、変換入力のコピーの作成、1 つの出力への複数入力の結合、および参照操作の実行を行います。  
  
|変換|[説明]|  
|--------------------|-----------------|  
|[条件分割変換](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)|データ行を別の出力にルーティングする変換です。|  
|[マルチキャスト変換](../../../integration-services/data-flow/transformations/multicast-transformation.md)|データセットを複数の出力に配信する変換です。|  
|[全体結合変換](../../../integration-services/data-flow/transformations/union-all-transformation.md)|複数のデータセットをマージする変換です。|  
|[マージ変換](../../../integration-services/data-flow/transformations/merge-transformation.md)|並べ替えた 2 つのデータセットをマージする変換です。|  
|[マージ結合変換](../../../integration-services/data-flow/transformations/merge-join-transformation.md)|FULL、LEFT、または INNER 結合を使用して、2 つのデータセットを結合する変換です。|  
|[参照変換](../../../integration-services/data-flow/transformations/lookup-transformation.md)|完全一致を使用して、参照テーブル内の値を参照する変換です。|  
|[キャッシュ変換](../../../integration-services/data-flow/transformations/cache-transform.md)|データ フロー内で接続中のデータ ソースからキャッシュ接続マネージャーにデータを書き込み、データをキャッシュ ファイルに保存する変換です。 参照変換は、キャッシュ ファイル内のデータに対する参照を実行します。|  
|[Balanced Data Distributor (BDD) 変換](../../../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md)|この変換は、複数の着信バッファーを、個別のスレッド上に存在する出力に対して一様に分配することにより、マルチコアおよびマルチプロセッサのサーバーで実行されている SSIS パッケージのパフォーマンスを向上させます。|  
  
## <a name="auditing-transformations"></a>監査変換  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、監査情報の追加や行のカウントを行う、次のような変換が含まれています。  
  
|変換|[説明]|  
|--------------------|-----------------|  
|[監査変換](../../../integration-services/data-flow/transformations/audit-transformation.md)|環境に関する情報を、パッケージ内のデータ フローで利用可能にする変換です。|  
|[行数変換](../../../integration-services/data-flow/transformations/row-count-transformation.md)|変換の処理を行うときに行をカウントし、最終的なカウントを変数に格納する変換です。|  
  
## <a name="custom-transformations"></a>カスタム変換  
 カスタムの変換を記述することもできます。 詳細については、「 [同期出力型のカスタム変換コンポーネントの開発](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) 」と「 [非同期出力型のカスタム変換コンポーネントの開発](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)」を参照してください。  
  
  
