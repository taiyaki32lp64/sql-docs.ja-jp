---
title: CDC ソースのカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 744e9357-94a9-4202-abe8-1d3d202697e9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b47e4f57101e05eb70dbdb464d6a4b36498dd3f7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293248"
---
# <a name="cdc-source-custom-properties"></a>CDC ソースのカスタム プロパティ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  次の表は、CDC ソースのカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|[説明]|  
|-------------------|---------------|-----------------|  
|接続|ADO.Net Connection|変更テーブルにアクセスするための [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC データベースへの ADO.NET 接続。|  
|StateVariable|String|現在の CDC 実行の CDC 状態を保持する SSIS 文字列パッケージ変数。|  
|CdcProcessingMode|Integer (列挙)|このモードは、処理方法を決定します。 有効なオプションは、 **[すべて]** 、 **[古い値を含むすべて]** 、 **[差分]** 、 **[更新マスクを含む差分]** 、 **[結合を含む差分]** です。<br /><br /> "すべて" という文字列が含まれるモードはすべての変更を返し、"差分" という文字列が含まれるモードは変更の差分のみを返します。<br /><br /> 主キーがないテーブルから取得できるのはすべての値のみです。<br /><br /> **[更新マスクを含む差分]** では、現在の変更行で変更された列を示す、 **__$\<column-name>\__Changed** というパターンの名前が付けられたブール値の列が追加されます。<br /><br /> このプロパティの値の詳細については、「[[CDC ソース エディター] ([接続マネージャー] ページ)](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)」を参照してください。|  
|CaptureInstance|String|読み取る CDC テーブルの CDC キャプチャ インスタンスの名前。 キャプチャされたソース テーブルには、スキーマの変更によりテーブル定義のシームレスな遷移を処理するためのキャプチャされたインスタンスが 1 ～ 2 個含まれることがあります。 キャプチャ対象のソース テーブルに複数のキャプチャ インスタンスが定義されている場合は、ここで使用するキャプチャ インスタンスを選択してください。 [スキーマ].[テーブル] という形式のテーブルの既定のキャプチャ インスタンス名は \<スキーマ>_\<テーブル> ですが、使用される実際のキャプチャ インスタンス名は異なる可能性があります。 読み取り元の実際のテーブルは、**cdc .\<キャプチャ インスタンス>_CT** という形式の CDC テーブルです。|  
|ReprocessingIndicator|Boolean|_ **_$reprocessing** 列を追加するかどうかを指定する値。 SSIS 開発者は、この特別な出力列を使用して、初期処理範囲の操作中に発生する一貫性エラーをさまざまな方法で処理できます。<br /><br /> **true**の場合、  **__$reprocessing** 列が追加されます。<br /><br /> CDC 処理範囲が初期処理範囲 (初期読み込みの期間に対応する LSN の範囲) と重なる場合か、CDC 処理範囲が前の実行でのエラーの後に再処理される場合、この列の値は **true** になります。 このインジケーター列を使用すると、SSIS 開発者は変更を再処理するときに、エラーを別々に処理できます (たとえば、非既存行の削除やキーの重複により失敗した挿入などの操作を無視できます)。<br /><br /> 既定値は **false**です。|  
|CommandTimeOut|Integer|この値は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] データベースと通信する際に使用されるタイムアウト (秒単位) を示します。 この値は、データベースからの応答時間が非常に遅い場合に使用されるため、既定値 (30 秒) は不十分です。|  
  
 CDC ソースの詳細については、「 [CDC ソース](../../integration-services/data-flow/cdc-source.md)」を参照してください。  
  
  
