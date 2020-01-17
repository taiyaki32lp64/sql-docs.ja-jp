---
title: 変換を使用してデータを変換する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], transformations
- transformations [Integration Services], about transformations
- transforming data [Integration Services]
ms.assetid: e1340b6f-ef75-4b14-af6f-823586eff0ed
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9fb4014688f1899e813d1df3e677caf9ad7bfbf1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770305"
---
# <a name="transform-data-with-transformations"></a>変換を使用してデータを変換する
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、変換元、変換、および変換先という 3 種類のデータ フロー コンポーネントが含まれています。  
  
 次の図は、1 つの変換元、2 つの変換、および 1 つの変換先を持つ、簡単なデータ フローを示しています。  
  
 ![Data flow](../../media/mw-dts-08.gif "Data flow")  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] の変換では、次の機能が用意されています。  
  
-   行セットを分割、コピー、およびマージしたり、参照操作を実行します。  
  
-   小文字を大文字に変更する変換などを適用することにより、列の値を更新して新しい列を作成します。  
  
-   データのクリーンアップ、テキストのマイニング、データ マイニング予測クエリの実行などのビジネス インテリジェンス操作を実行します。  
  
-   集計または並べ替えられた値、サンプル データ、またはピボットされたデータおよびピボット解除されたデータで構成される、新しい行セットを作成します。  
  
-   データのエクスポートおよびインポート、監査情報の提供、緩やかに変化するディメンションの処理などを行うタスクを実行します。  
  
 詳しくは、「 [Integration Services の変換](integration-services-transformations.md)」をご覧ください。  
  
 カスタムの変換を記述することもできます。 詳しくは、「 [カスタム データ フロー コンポーネントの開発](../../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 」と「 [特定の種類のデータ フロー コンポーネントの開発](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)」をご覧ください。  
  
 変換をデータ フロー デザイナーに追加した後で、変換を構成する前に、データ フロー内の別の変換または変換元の出力をこの変換の入力に連結することにより、変換をデータ フローに連結します。 2 つのデータ フロー コンポーネント間のコネクタは、パスと呼ばれます。 コンポーネントの連結とパスを使用した作業の詳細については、「 [パスを使用してコンポーネントを連結する](../../connect-components-with-paths.md)」をご覧ください。  
  
### <a name="to-add-a-transformation-to-a-data-flow"></a>変換をデータ フローに追加するには  
  
-   [データ フローでコンポーネントを追加または削除する](../add-or-delete-a-component-in-a-data-flow.md)  
  
### <a name="to-connect-a-transformation-to-a-data-flow"></a>変換をデータ フローに連結するには  
  
-   [データ フロー内でコンポーネントを連結する](../connect-components-in-a-data-flow.md)  
  
### <a name="to-set-the-properties-of-a-transformation"></a>変換のプロパティを設定するには  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>参照  
 [[データ フロー タスク]](../../control-flow/data-flow-task.md)   
 [データ フロー](../data-flow.md)   
 [パスを使用してコンポーネントを連結する](../../connect-components-with-paths.md)   
 [データのエラー処理](../error-handling-in-data.md)   
 [データ フロー](../data-flow.md)  
  
  
