---
title: rrRenderingError - Reporting Services エラー | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rrRenderingError
ms.assetid: 0751efc3-b81b-44ee-8aac-8560f86ca322
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1fcfe999a7cfaf41cc4b6b9fad437ea14dfe2613
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575552"
---
# <a name="rrrenderingerror---reporting-services-error"></a>rrRenderingError - Reporting Services エラー
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|rrRenderingError|  
|イベント ソース|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources.Strings|  
|コンポーネント|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|メッセージ テキスト|レポートの表示中にエラーが発生しました。 (rrRenderingError) %1|  
  
## <a name="explanation"></a>説明  
 このメッセージは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] がレポートを表示またはエクスポートできない場合に返されます。  
  
 サイズがサポートされていないという内容のメッセージである場合、一般的な原因として、指定された RDL ページ サイズが無効であることが考えられます。 有効な RDL ページ サイズを指定してから再試行してください。  
  
 RDL サイズの単位がサポートされていないという内容のメッセージである場合、一般的な原因として、サポートされていない種類の単位が指定されたことが考えられます。 有効な単位は、cm、in、mm、pc、および pt です。 有効な単位を指定してから再試行してください。  
  
 負のサイズはサポートされていないという内容のメッセージである場合、一般的な原因として、ページ サイズに負の値 (-5 cm など) が指定されたことが考えられます。 ページ サイズに正の値を指定してから再試行してください。  
  
 RDL サイズの指定が範囲外であるという内容のメッセージである場合、一般的な原因として、ページ サイズに指定された値が、有効なページ余白サイズの範囲を超えていることが考えられます。 ページ余白サイズの範囲に収まる有効な値を指定してください。  
  
 指定された色がサポートされていないという内容のメッセージである場合、一般的な原因として、RDL で指定された色が無効であることが考えられます。 RDL でサポートされている色を選択してから再試行してください。  
  
 アクション ラベルは 1 つのアクションを使用している場合にのみ省略でき、複数のアクションを追加する場合はアクションごとにラベルが必要であるという内容のメッセージである場合、一般的な原因として、指定されたアクション ラベルが無効であることが考えられます。 アクションごとに有効なアクション ラベルを指定してください。  
  
 スタイル引数を特定の型にする必要があるという内容のメッセージである場合、一般的な原因として、そのデータ型に対して誤ったスタイル値が指定されていることが考えられます。 RDL 仕様では、各種の RDL 要素のスタイル値に使用できる有効な型が規定されています。 たとえば、背景色のスタイル値に "2pt" を指定したり、高さに "true" を指定したりすることはできません。 正しい値を指定してから再試行してください。  
  
 罫線のスタイルがサポートされていないという内容のメッセージである場合、一般的な原因として、指定された罫線のスタイルが無効であることが考えられます。 サポートされている罫線のスタイルを指定してから再試行してください。  
  
 画像の MIME の種類がサポートされていないという内容のメッセージである場合、一般的な原因として、画像レポート アイテムに指定された MIME の種類が無効であることが考えられます。 そのレポート アイテムにサポートされている MIME の種類を指定してから再試行してください。  
  
 行数が 1 シートの上限値を超えたという内容のメッセージである場合、一般的な原因として、Excel ワークシートの行数が上限を超えたことが考えられます。 Excel でサポートされる最大行数は 65,000 行です。  
  
 列数が 1 シートの上限値を超えたという内容のメッセージである場合、一般的な原因として、Excel ワークシートの列数が上限を超えたことが考えられます。  
  
## <a name="user-action"></a>ユーザーの操作  
  
## <a name="internal-only"></a>内部使用のみ  
  
