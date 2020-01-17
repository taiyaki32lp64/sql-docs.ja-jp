---
title: エラーのコレクション (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e3c8f981d4dc40a4a6f618f3cca387379d51def9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932978"
---
# <a name="errors-collection-ado"></a>Errors コレクション (ADO)
すべてが含まれています、[エラー](../../../ado/reference/ado-api/error-object.md)単一のプロバイダーに関連の障害への応答で作成されたオブジェクト。  
  
## <a name="remarks"></a>コメント  
 ADO オブジェクトに関連するすべての操作には、1 つまたは複数のプロバイダー エラーを生成できます。 各エラーが発生すると、1 つまたは複数**エラー**でオブジェクトを配置できる、**エラー**のコレクション、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。 ADO の別の操作は、エラーを生成するときに、**エラー**コレクションをクリアし、一連の新しい**エラー**でオブジェクトを配置できる、**エラー**コレクション。  
  
 各**エラー**オブジェクトは ADO エラーではなく、特定のプロバイダー エラーを表します。 ADO エラーは、実行時の例外処理機構に公開されます。 Microsoft Visual Basic では、ADO 固有エラーの発生がトリガーなど、 [onError](../../../ado/reference/rds-api/onerror-event-rds.md)イベントに表示し、 **Err**オブジェクト。  
  
 エラーを生成しない ADO 操作があるない影響、**エラー**コレクション。 使用して、[オフ](../../../ado/reference/ado-api/clear-method-ado.md)手動でクリアする方法、**エラー**コレクション。  
  
 一連の**エラー**内のオブジェクト、**エラー**コレクションが 1 つのステートメントへの応答で発生したすべてのエラーについて説明します。 特定のエラーを列挙する、**エラー**コレクションにより、エラー処理ルーチンより正確に、原因と、エラーの発生源を判断し、回復する適切な手順を実行します。  
  
 プロパティとメソッドの一部として表示される警告を返す**エラー**内のオブジェクト、**エラー**コレクションが、プログラムの実行は停止しないでください。 呼び出す前に、[再同期](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)、または[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッド、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、 [を開く](../../../ado/reference/ado-api/open-method-ado-connection.md)メソッドを**接続**オブジェクト、または設定、[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティを**レコード セット**オブジェクトを呼び出し、 **をオフに**メソッドを**エラー**コレクション。 その方法を読み取ることができます、[カウント](../../../ado/reference/ado-api/count-property-ado.md)のプロパティ、**エラー**コレクションをテストするには、警告が返されます。  
  
> [!NOTE]
>  参照してください、**エラー**オブジェクトについての 1 つの ADO 操作で複数のエラーを生成できる方法について詳しく説明します。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [エラーのコレクションのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
