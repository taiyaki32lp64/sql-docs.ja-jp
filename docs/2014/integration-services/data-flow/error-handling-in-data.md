---
title: データのエラー処理 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data conversion errors [Integration Services]
- errors [Integration Services], data flow components
- lookups [Integration Services]
- errors [Integration Services]
- errors [Integration Services], data flow outputs
- error outputs [Integration Services]
- data flow [Integration Services], errors
- expressions [Integration Services], errors
ms.assetid: c61667b4-25cb-4d45-a52f-a733e32863f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b5a98877e04a077bf1bb1c0c527500f3102b862
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827149"
---
# <a name="error-handling-in-data"></a>データのエラー処理
  データ フロー コンポーネントが変換を列データに適用したり、変換元のデータを抽出したり、変換先にデータを読み込んだりするときに、エラーが発生する場合があります。 エラーが発生する原因の主なものは、予期しないデータ値です。 たとえば、数字ではなく文字列が列に含まれる場合、データ変換は失敗します。また、データは日付データであるが列のデータ型は数値の場合、データベース列への挿入は失敗します。あるいは、列の値が 0 の場合に数学的演算の結果が無効となり、それが原因で式の評価が失敗します。  
  
 エラーは一般的に、次のカテゴリのいずれかに分類されます。  
  
-   データ変換エラー。変換により、有効桁の損失、有効桁以外の桁の損失、および文字列の切り捨てなどの結果が返された場合に発生します。 要求された変換がサポートされていない場合にも、データ変換エラーは発生します。  
  
-   式の評価エラー。実行時に評価される式が無効な演算を実行したり、データ値の不足または無効のため構文的に間違った状態になる場合に発生します。  
  
-   参照エラー。参照操作が、参照テーブル内で一致を見つけられなかった場合に発生します。  
  
 多くのデータ フロー コンポーネントではエラー出力がサポートされています。これを利用すると、コンポーネントが行う、入力データと出力データの両方での行レベルのエラー処理の方法を制御できます。 入力または出力の個々の列にオプションを設定することにより、切り捨てまたはエラーが発生したときのコンポーネントの動作方法を指定します。 たとえば、顧客名のデータが切り捨てられたときは失敗するが、それよりも重要でないデータが含まれる別の列で切り捨てが発生した場合はエラーを無視するように、コンポーネントを指定できます。  
  
 エラー出力は、別の変換の入力に連結したり、エラー出力以外の別の変換先に読み込むことができます。 たとえば、エラー出力は、空白列に文字列を提供する派生列変換に連結できます。  
  
 次の図は、エラー出力が含まれる簡単なデータ フローを示しています。  
  
 ![エラー出力のあるデータ フロー](../media/mw-dts-11.gif "エラー出力のあるデータ フロー")  
  
 データ列の他に、エラー出力には **ErrorCode** 列と **ErrorColumn** 列が含まれています。 **ErrorCode** 列はエラーを識別し、 **ErrorColumn** 列にはエラー列の系列 ID が含まれます。 これらの列のメタデータを表示するには、エラー出力をデータ フロー内の次のコンポーネントに連結するパスをクリックします。 状況によっては、 **ErrorColumn** 列の値が 0 に設定されていることがあります。 これは、エラー状態が 1 列ではなく行全体に影響していることを示します。 たとえば、参照変換で参照に失敗した場合などです。  
  
 詳細については、「 [データ フロー](data-flow.md) 」と「 [Integration Services のパス](integration-services-paths.md)」を参照してください。  
  
 Integration Services のエラー、警告、および他のメッセージの一覧については、「 [Integration Services Error and Message Reference](../integration-services-error-and-message-reference.md)」を参照してください。  
  
## <a name="error-and-truncation-options"></a>エラーと切り捨てオプション  
 エラーは、エラーまたは切り捨ての、2 つのカテゴリのいずれかに分類されます。 エラーは決定的な失敗を示し、NULL 値の結果を生成します。 このようなエラーには、データ変換エラーまたは式の評価エラーが含まれます。 たとえば、英文字が含まれる文字列を数字に変換しようとすると、エラーが発生します。 データ変換、式の評価、および変数、プロパティ、データ列への式の結果の割り当ては、無効なキャストおよび互換性のないデータ型のために失敗する場合があります。 詳細については、「[Cast &#40;SSIS 式&#41;](../expressions/cast-ssis-expression.md)[式における Integration Services データ型](../expressions/integration-services-data-types-in-expressions.md), 」、および「[Integration Services のデータ型](integration-services-data-types.md)」を参照してください。  
  
 切り捨ては、エラーほど重大ではありません。 切り捨てによって生成される結果は、使用できる場合も、むしろ望ましい場合もあります。 切り捨てをエラーとして扱うか、または許容できる条件として扱うかを選択できます。 たとえば、15 文字の文字列を、文字幅が 1 文字のみの列に挿入する場合、文字列の切り捨てを選択できます。  
  
 変換元、変換、および変換先によるエラーと切り捨ての処理方法を構成できます。 次の表では、このオプションについて説明します。  
  
|オプション|説明|  
|------------|-----------------|  
|エラー コンポーネント|エラーまたは切り捨てが発生すると、データ フロー タスクは失敗します。 [失敗] は、エラーおよび切り捨ての既定のオプションです。|  
|エラーを無視する|エラーまたは切り捨ては無視され、データ行は変換または変換元の出力に送られます。|  
|行のリダイレクト|エラーまたは切り捨てのデータ行は、変換元、変換、または変換先のエラー出力に送られます。|  
  
## <a name="adding-the-error-description"></a>エラーの説明の追加  
 既定では、エラー出力により数値エラー コードが提供され、通常、エラー出力にはエラーが発生した列の ID が含まれています。 スクリプト コンポーネントを使用して追加列にエラーの説明を含めることができます。この操作は、1 行のスクリプトを使用して、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> インターフェイスの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> メソッドを呼び出して行います。  
  
 このスクリプト コンポーネントは、エラーをキャプチャするデータ フロー コンポーネントよりデータ フローの下流にある任意のエラー セグメントに追加できますが、エラー行を出力先に書き込む直前の位置に配置するのが普通です。 これによりスクリプトは、書き込まれたエラー行についてのみ、説明を参照することができます。 たとえば、データ フロー内のエラー セグメントでエラーの一部が修正され、出力先にエラー行が書き込まれないこともあり得るからです。 詳細については、次を参照してください。[スクリプト コンポーネントによるエラー出力の強化](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md)します。  
  
### <a name="to-configure-an-error-output"></a>エラー出力を構成するには  
  
-   [データ フロー コンポーネントでエラー出力を構成する](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="see-also"></a>参照  
 [データ フロー](data-flow.md)   
 [変換を使用してデータを変換する](transformations/transform-data-with-transformations.md)   
 [パスを使用してコンポーネントを連結する](../connect-components-with-paths.md)   
 [[データ フロー タスク]](../control-flow/data-flow-task.md)   
 [データ フロー](data-flow.md)  
  
  
