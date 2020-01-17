---
title: 優先順位制約 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- control flow [Integration Services], precedence constraints
- precedence constraints [Integration Services]
- constraints [Integration Services]
- sequence execution options [Integration Services]
- containers [Integration Services], precedence constraints
ms.assetid: c5ce5435-fd89-4156-a11f-68470a69aa9f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da27e10af2a5483583976a13e54bf9087c20e9b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831708"
---
# <a name="precedence-constraints"></a>優先順位制約
  優先順位制約は、パッケージ内の実行可能ファイル、コンテナー、およびタスクをリンクして制御フローを作成し、実行可能ファイルを実行するかどうかを決定する条件を指定します。 実行可能ファイルには、For ループ コンテナー、Foreach ループ コンテナー、シーケンス コンテナー、タスク、またはイベント ハンドラーを設定できます。 また、イベント ハンドラーは優先順位制約を使用して実行可能ファイルをリンクし、制御フローを作成します。  
  
 優先順位制約は、優先実行可能オブジェクトと制約付きの実行可能オブジェクトを連結します。 優先実行可能オブジェクトは制約付きの実行可能オブジェクトの前に実行され、優先実行可能オブジェクトの実行結果により、制約付きの実行可能オブジェクトを実行するかどうかが決まる場合があります。 次の図は、優先順位制約によってリンクされた 2 つの実行可能ファイルを示しています。  
  
 ![優先順位制約によってリンクされた実行可能ファイル](../media/ssis-pcsimple.gif "優先順位制約によってリンクされた実行可能ファイル")  
  
 直線的な制御フロー、つまり分岐のない制御フローでは、優先順位制約のみがタスクの実行順序を制御します。 制御フローに分岐がある場合には、[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ランタイム エンジンが、分岐の直後に続くタスクとコンテナーの実行順序を決定します。 ランタイム エンジンは、制御フロー内で連結されていないワークフローの実行順序も決定します。  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のアーキテクチャではコンテナーを入れ子にできるので、1 つのタスクのみをカプセル化するタスク ホスト コンテナーを除き、すべてのコンテナーに他のコンテナーと独自の制御フローを含めることができます。 For ループ コンテナー、Foreach ループ コンテナー、およびシーケンス コンテナーには、タスクとその他のコンテナーを複数含めることができます。さらに、そのコンテナーにも複数のタスクとコンテナーを含めることができます。 たとえば、スクリプト タスクとシーケンス コンテナーを持つパッケージに、そのスクリプト タスクとシーケンス コンテナーをリンクする優先順位制約を含めます。 シーケンス コンテナーには 3 つのスクリプト タスクが含まれ、その優先順位制約は 3 つのスクリプト タスクをリンクして制御フローを作成します。 次の図は、2 レベルの入れ子構造のパッケージの優先順位制約を示しています。  
  
 ![パッケージの優先順位制約](../media/mw-dts-12.gif "パッケージの優先順位制約")  
  
 パッケージは、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] コンテナー階層の最上層にあるため、複数のパッケージを優先順位制約によってリンクすることはできません。ただし、パッケージ実行タスクをパッケージに追加して、別のパッケージを間接的に制御フローにリンクできます。  
  
 優先順位制約は、次の方法で構成できます。  
  
-   評価操作を指定します。 優先順位制約は、制約値および式の両方、またはいずれか 1 つを使用して、制約付き実行可能ファイルを実行するかどうかを決定します。  
  
-   優先順位制約で実行結果を使用する場合、成功、失敗、完了のいずれかの実行結果を指定できます。  
  
-   優先順位制約で実行結果を使用する場合、ブール型に評価される式を指定できます。  
  
-   優先順位制約を単独で評価するか、制約付き実行可能ファイルに適用する別の制約と共に評価するかを指定します。  
  
## <a name="evaluation-operations"></a>評価操作  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、次の評価操作が用意されています。  
  
-   優先順位付き実行可能ファイルの実行結果のみを使用して、制約付き実行可能ファイルを実行するかどうかを決定する制約。 優先順位付き実行可能ファイルの実行結果には、完了、成功、または失敗を設定できます。 これは既定の操作です。  
  
-   評価する式。これを使用して制約付き実行可能ファイルを実行するかどうかを決定します。 式が TRUE に評価された場合、制限付き実行可能ファイルは実行されます。  
  
-   優先順位付き実行可能ファイルの実行結果と、式を評価した戻り結果の両方を必須とする、式および制約。  
  
-   優先順位付き実行可能ファイルの実行結果か、式を評価した戻り結果を使用する、式または制約。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでは、優先順位制約の種類を色で識別します。 成功制約は緑、失敗制約は赤、完了制約は青で表示されます。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーで制約の種類を示すテキスト ラベルを表示するには、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーのユーザー補助機能を構成する必要があります。  
  
 式は、有効な [!INCLUDE[ssIS](../../../includes/ssis-md.md)] の式である必要があります。この式には、関数、演算子、システム関数およびカスタム関数を含めることができます。 詳細については、「[Integration Services &#40;SSIS&#41; の式](../expressions/integration-services-ssis-expressions.md)」および「[Integration Services &#40;SSIS&#41; の変数](../integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="execution-results"></a>実行結果  
 優先順位制約は、次の実行結果を単独で、または式との組み合わせで使用できます。  
  
-   完了。制約付き実行可能ファイルを実行するには、結果にかかわらず優先順位付き実行可能ファイルが完了することだけが必要です。  
  
-   成功。制約付き実行可能ファイルを実行するには、優先順位付き実行可能ファイルが正常に完了する必要があります。  
  
-   失敗。制約付き実行可能ファイルを実行するには、優先順位付き実行可能ファイルが失敗する必要があります。  
  
> [!NOTE]  
>  同じ `Precedence Constraint` コレクションのメンバーである優先順位制約のみが、論理 AND 条件でグループ化できます。 たとえば、2 つの Foreach ループ コンテナーの優先順位制約を組み合わせることはできません。  
  
## <a name="configuration-of-the-precedence-constraint"></a>優先順位制約の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーで設定できるプロパティについては、「 [優先順位制約エディター](../precedence-constraint-editor.md)」を参照してください。  
  
 これらのプロパティのプログラムでの設定については、「 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [優先順位制約のプロパティを設定する](../set-the-properties-of-a-precedence-constraint.md)  
  
-   [ショートカット メニューを使用して優先順位制約の値を設定する](../set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)  
  
-   [既定の優先順位制約を使用してタスクとコンテナーを連結する](../connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)  
  
     このトピックでは、優先順位制約の既定の動作を設定する方法、および既定の優先順位制約を使用して実行可能ファイルを連結する方法について説明しています。  
  
## <a name="related-content"></a>関連コンテンツ  
 social.technet.microsoft.com の技術記事「 [SSIS 式の例](https://go.microsoft.com/fwlink/?LinkId=220761)」  
  
## <a name="see-also"></a>参照  
 [優先順位制約に式を追加します。](../add-expressions-to-precedence-constraints.md)   
 [複数の優先順位制約](../multiple-precedence-constraints.md)  
  
  
