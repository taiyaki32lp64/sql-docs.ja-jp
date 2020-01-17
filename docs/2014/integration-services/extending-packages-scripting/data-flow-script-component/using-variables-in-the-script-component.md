---
title: スクリプト コンポーネントでの変数の使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 922454c7bc04a211d6f54754d48331fdfdffeb07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62894971"
---
# <a name="using-variables-in-the-script-component"></a>スクリプト コンポーネントでの変数の使用
  変数には、パッケージとそのコンテナー、タスク、およびイベント ハンドラーが実行時に使用できる値が格納されます。 詳細については、「 [Integration Services &#40;SSIS&#41; の変数](../../integration-services-ssis-variables.md)」を参照してください。  
  
 読み取り専用のために既存の変数を使用できるようにしたり読み取り/書き込みアクセス、カスタム スクリプトで変数のコンマ区切りのリストを入力して、`ReadOnlyVariables`と`ReadWriteVariables`フィールドに、**スクリプト**のページ**スクリプト変換エディター**します。 変数名の大文字と小文字は区別されることに注意してください。 `Value` プロパティを使用して、各変数に対する読み取りおよび書き込みを行います。 スクリプトが実行時に変数を処理すると、スクリプト コンポーネントは状況に応じて自動的に必要なロックを処理します。  
  
> [!IMPORTANT]  
>  `ReadWriteVariables` のコレクションは、`PostExecute` メソッド内でのみ、パフォーマンスを最大化し、ロックによる競合のリスクを最小限に抑えるために使用できます。 したがって、データ行を処理するたびにパッケージ変数の値を直接増やすことはできません。 このような場合、ローカル変数の値を増やし、すべてのデータが処理された後で、`PostExecute` メソッド内でパッケージ変数の値をローカル変数の値に設定します。 また、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> プロパティを使用してこの制限を回避できます。この方法については、このトピックの後半で説明します。 ただし、各行が処理されているときにパッケージ変数に直接書き込みを行うと、パフォーマンスに悪影響を与え、ロックによる競合のリスクが増えます。  
  
 **[スクリプト変換エディター]** の **[スクリプト]** ページの詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](configuring-the-script-component-in-the-script-component-editor.md)」および「[スクリプト変換エディター &#40;[スクリプト] ページ&#41;](../../script-transformation-editor-script-page.md)」を参照してください。  
  
 スクリプト コンポーネントは、`Variables` プロジェクト アイテム内に、`ComponentWrapper` コレクション クラスを作成します。ここには、構成済みの各変数の値に対して、変数自体と同じ名前を持つ、厳密に型指定されたアクセサー プロパティがあります。 このコレクションは、`Variables` クラスの `ScriptMain` プロパティを介して公開されます。 アクセサー プロパティにより、変数の値が読み取り専用か読み取り/書き込み用かが決まります。 たとえば、`MyIntegerVariable` という整数型の変数を `ReadOnlyVariables` 一覧に追加した場合、次のコードを使用して、この値をスクリプト内で取得できます。  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 スクリプト コンポーネントで変数を扱うには、`Me.VariableDispenser` を呼び出してアクセスする <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> プロパティを使用することもできます。 この場合には、変数の型指定された名前付きのアクセサー プロパティを使用せずに、直接的に変数にアクセスします。 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> を使用する場合は、コード内で、ロック セマンティクスと、変数値のデータ型のキャストの両方を処理する必要があります。 デザイン時には使用できないが、実行時にプログラムによって生成される変数を扱う必要がある場合は、名前付きの型指定されたアクセサー プロパティではなく、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> プロパティを使用する必要があります。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の変数](../../integration-services-ssis-variables.md)   
 [パッケージで変数を使用する](../../use-variables-in-packages.md)  
  
  
