---
title: エラー オブジェクト |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5018dc921267663d64037024ef21c82ac6e3f7c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932963"
---
# <a name="error-object"></a>Error オブジェクト
プロバイダーを含む 1 つの操作に関連するデータ アクセス エラーの詳細が含まれています。  
  
## <a name="remarks"></a>コメント  
 ADO オブジェクトに関連するすべての操作には、1 つまたは複数のプロバイダー エラーを生成できます。 各エラーが発生すると、1 つまたは複数**エラー**に配置されたオブジェクト、[エラー](../../../ado/reference/ado-api/errors-collection-ado.md)のコレクション、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。 ADO の別の操作は、エラーを生成するときに、**エラー**コレクションをクリアし、一連の新しい**エラー**でオブジェクトを配置、**エラー**コレクション。  
  
> [!NOTE]
>  各**エラー**オブジェクトは ADO エラーではなく、特定のプロバイダー エラーを表します。 ADO エラーは、実行時の例外処理機構に公開されます。 Microsoft Visual Basic では、ADO 固有エラーの発生がトリガーなど、 **On Error**イベントに表示し、**エラー**オブジェクト。 ADO エラーの完全な一覧を参照してください、 [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)トピック。  
  
 読み取ることができます、**エラー**オブジェクトのプロパティを取得して、次を含む、各エラーに関する特定の詳細。  
  
-   [説明](../../../ado/reference/ado-api/description-property.md)プロパティで、エラーのテキストが含まれています。 これは、既定のプロパティです。  
  
-   [数](../../../ado/reference/ado-api/number-property-ado.md)が含まれるプロパティ、**長い**エラー定数の整数値。  
  
-   [ソース](../../../ado/reference/ado-api/source-property-ado-error.md)プロパティで、エラーが発生したオブジェクトを識別します。 いくつかがある場合に特に有効です**エラー**内のオブジェクト、**エラー**コレクションの次のデータ ソースを要求します。  
  
-   [SQLState](../../../ado/reference/ado-api/sqlstate-property.md)と[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)プロパティは、SQL データ ソースからの情報を提供します。  
  
 プロバイダー エラーが発生したときに配置されて、**エラー**のコレクション、**接続**オブジェクト。 ADO は、プロバイダーに固有のエラー情報を許可する 1 つの ADO 操作で複数のエラーの戻り値をサポートしています。 エラー ハンドラーには、この詳細なエラー情報を取得するには、言語や、使用している環境の適切なエラー トラップ機能を使用してそれぞれのプロパティを列挙する入れ子になったループを使用して**エラー**オブジェクトに、**エラー**コレクション。  
  
> [!NOTE]
>  **Microsoft Visual Basic と VBScript ユーザー**が有効な場合**接続**オブジェクト、エラー情報を取得する必要があります、**エラー**オブジェクト。  
  
 プロバイダーと同様には、ADO のクリア、 **OLE エラー情報**オブジェクトの呼び出しを行う可能性があります、新しいプロバイダー エラーを生成できる前にします。 ただし、**エラー**コレクションに、**接続**オブジェクトはクリアされ、プロバイダーは新たなエラーを生成するときにのみ、またはに設定されます、[クリア](../../../ado/reference/ado-api/clear-method-ado.md)メソッドが呼び出されます。  
  
 プロパティとメソッドの一部として表示される警告を返す**エラー**内のオブジェクト、**エラー**コレクションが、プログラムの実行は停止しないでください。 呼び出す前に、[再同期](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)、または[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッド、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、 [を開く](../../../ado/reference/ado-api/open-method-ado-connection.md)メソッドを**接続**オブジェクトまたは設定、[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティを**レコード セット**オブジェクトを呼び出し、 **をオフに**メソッドを**エラー**コレクション。 そうすることが読み取ることができます、[カウント](../../../ado/reference/ado-api/count-property-ado.md)のプロパティ、**エラー**コレクションをテストするには、警告が返されます。  
  
 **エラー**オブジェクトは、スクリプトを実行することはありません。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Error オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (vc++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [エラーのコレクション (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
