---
title: 図形は一般にコマンド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09fec8bd07d036fd6a93b8f6bcb54a51a68150fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924174"
---
# <a name="shape-commands-in-general"></a>一般的な Shape コマンド
形状の列を定義するデータの整形**レコード セット**、列、および方法で表されるエンティティ間のリレーションシップ、**レコード セット**にデータを設定します。  
  
 形状を**Recordset**の次の種類の列で構成できます。  
  
|列の型|説明|  
|-----------------|-----------------|  
|data|フィールドを**レコード セット**データ プロバイダーには、クエリ コマンドによって返される、テーブル、または以前形**レコード セット**します。|  
|」の章|別の参照**レコード セット**という、*章*します。 チャプター列により、定義できる、 *、親子*リレーションシップで、*親*は、**レコード セット**チャプター列と、を含む*子*は、**レコード セット**」の章で表されます。|  
|集計 (aggregate)|実行することによって、列の値が派生した、*集計関数*のすべての行または子のすべての行の列で**レコード セット**します。 (次のトピックでは、集計関数を参照してください[集計関数、CALC 関数、および新しいキーワード](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md))。|  
|計算式|Visual Basic のアプリケーションの同じ行の列の式を計算することで、列の値が派生した、 **Recordset**します。 式では、CALC 関数の引数です。 (次のトピックでは、計算式を参照してください[集計関数、CALC 関数、および新しいキーワード](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)し[Visual Basic for Applications の関数](../../../ado/guide/data/visual-basic-for-applications-functions.md))。|  
|new|空で作成されるフィールドは後でデータを設定することができます。 列には、新しいキーワードが定義されます。 (新しいキーワードで、次のトピックを参照してください[集計関数、CALC 関数、および新しいキーワード](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。)。|  
  
 図形のコマンドを返す基になるデータ プロバイダーへのクエリ コマンドを指定する句を含めることができます、 **Recordset**オブジェクト。 クエリの構文は、基になるデータ プロバイダーの要件によって異なります。 これは普通、SQL、ADO では、特定のクエリ言語の使用は必要ありません。  
  
 図形のコマンドを発行できる**レコード セット**オブジェクトか、設定、 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)のプロパティ、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトと、呼び出し、 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)メソッド。  
  
 SQL の JOIN 句を使用して 2 つのテーブルを関連付けるただし、階層構造**Recordset**より効率的に情報を表すことができます。 各行を**レコード セット**テーブルの 1 つから冗長的参加の繰り返し情報によって作成します。 階層構造**レコード セット**が 1 つだけの親**レコード セット**の複数の子の各**Recordset**オブジェクト。  
  
 図形のコマンドは、入れ子にすることができます。 つまり、*親コマンド*または*子コマンド*自体の図形の別のコマンドがある可能性があります。  
  
 Shape プロバイダーは、ユーザーのカーソル位置を指定する場合でも常に、クライアント カーソルを返します**adUseServer**します。  
  
 アクセスすることができます、 **Recordset**形状のコンポーネント**レコード セット**プログラムまたは適切なビジュアル コントロールを使用します。  
  
 マイクロソフトは、図形のコマンドを生成するためのビジュアル ツールを提供しています (を参照してください、[データ環境デザイナー](https://go.microsoft.com/fwlink/?LinkId=5689) Visual Basic 6 のドキュメントで) と、(「"を使用して、Microsoft 階層的な階層カーソルを表示します。フレキシブル グリッド コントロール"Visual Basic 6 ドキュメント)。  
  
 階層構造を移動する方法については**Recordset**を参照してください[階層レコード セットの行にアクセスする](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)します。  
  
 構文的に正しい図形のコマンドに関する正確な情報は、次を参照してください。[図形の正式な文法](../../../ado/guide/data/formal-shape-grammar.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [集計関数、CALC 関数、NEW キーワード](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [基になるデータ プロバイダーにコマンドを発行する](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
