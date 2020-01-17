---
title: ビルド コントリビューターと配置コントリビューターを使用してデータベースのビルドと配置をカスタマイズする | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: fe2064bb-e01e-4a12-9f12-a99aa9a5203f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aa22592bbe86707ec4efa43ba0c188c21a07351e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110571"
---
# <a name="customize-database-build-and-deployment-by-using-build-and-deployment-contributors"></a>ビルド コントリビューターと配置コントリビューターを使用してデータベースのビルドと配置をカスタマイズする
Visual Studio には、データベース プロジェクトのビルド操作および配置操作の動作を変更するための拡張ポイントが用意されています。  
  
## <a name="available-extensibility-points"></a>使用可能な拡張ポイント  
次の表に示されているように、拡張ポイントに対して拡張機能を作成できます。  
  
|**操作**|**コントリビューターの種類**|**注**|  
|--------------|------------------------|-------------|  
|ビルド|BuildContributor|この種類の拡張機能は、プロジェクト モデルの検証が完了した後、SQL プロジェクトをビルドするときに実行されます。 ビルド コントリビューターは、ビルド タスクのすべてのプロパティ、およびすべてのカスタム引数に加えて、完成したモデルにもアクセスできます。|  
|配置|DeploymentPlanModifier|この種類の拡張機能は、配置計画が生成されてからその配置計画が実行されるまでの間、配置パイプラインの一環として、SQL プロジェクトを配置するときに実行されます。 DeploymentPlanModifier を使用すると、ステップの追加または削除によって配置計画を変更できます。 配置コントリビューターは、配置計画、比較結果、およびソース モデルとターゲット モデルにアクセスできます。|  
|配置|DeploymentPlanExecutor|この種類の拡張機能は、配置計画の実行時に実行され、配置計画への読み取り専用アクセスを提供します。 DeploymentPlanExectutor は、配置計画に基づく操作を実行します。|  
  
### <a name="supported-extensibility-scenarios"></a>サポートされている機能拡張シナリオ  
ビルド コントリビューターまたは配置コントリビューターを実装することで、次のサンプル シナリオを実現できます。  
  
-   **プロジェクトのビルド中にスキーマ ドキュメントを生成する** - このシナリオをサポートするには、[BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx) を実装し、OnExecute メソッドをオーバーライドしてスキーマ ドキュメントを生成します。 拡張機能を実行するかどうかを制御する既定の引数を定義するターゲット ファイルを作成し、出力ファイルの名前を指定できます。  
  
-   **SQL プロジェクトの配置時に差分レポートを生成する** - このシナリオをサポートするには、SQL プロジェクトを配置するときに XML ファイルを生成する [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) を実装します。  
  
-   **配置計画を変更してデータの移動タイミングを変更する** - このシナリオをサポートするには、[DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) を実装し、配置計画を繰り返します。 その計画に含まれる SqlTableMigrationStep ごとに、比較結果を調べ、そのステップを実行するかスキップするかを決定します。  
  
-   **SQL プロジェクトを配置するときにファイルを生成された dacpac にコピーする** - このシナリオをサポートするには、配置コントリビューターを実装し、OnEstablishDeploymentConfiguration メソッドをオーバーライドして、プロジェクト システムによって DeploymentExtensionConfiguration とマークされているファイルを指定します。 これらのファイルは、出力フォルダーにコピーし、生成された dacpac に追加する必要があります。 また、複数のファイルを 1 つの新しいファイルにマージし、それを出力フォルダーにコピーして配置マニフェストに追加するように、コントリビューターを変更することもできます。 配置時に、OnApplyDeploymentConfiguration メソッドを実装し、それらのファイルを dacpac から抽出して OnExecute メソッドで使用できるように準備することができます。  
  
さらに、コントリビューターからカスタマイズされた名前と値の引数のペアを公開し、データベース プロジェクト ファイルに書き込むこともできます。 これらの引数を使用すると、コントリビューターが MSBuild から情報を抽出したり、コントリビューターのエンド ユーザーが動作をカスタマイズしたりできるようになります。 たとえば、ユーザーが入力ファイルまたは出力ファイルの名前を指定できるようにすることも可能です。  
  
## <a name="common-tasks"></a>一般的なタスク  
  
|**一般的なタスク**|**関連する参照先**|  
|--------------------|--------------------------|  
|**拡張ポイントの詳細を理解する:** ビルド コントリビューターおよび配置コントリビューターの実装に使用する基本クラスについて確認できます。|[BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx)<br /><br />[DeploymentContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentcontributor.aspx)|  
|**サンプル コントリビューターを作成する:** ビルド コントリビューターまたは配置コントリビューターの作成に必要な手順について説明します。 これらのチュートリアルを実行する場合は、次のタスクを実行します。<br /><br />-   モデル内のすべての要素が表示されるレポートを生成するビルド コントリビューターを作成する。<br />-   配置計画を実行前に変更する配置コントリビューターを作成する。<br />-   SQL プロジェクトの配置時に配置レポートを生成する配置コントリビューターを作成する。<br /><br />コントリビューターをチームに配布する方法に応じて、すべてのコントリビューターを単一のアセンブリ内に作成することも、複数のアセンブリに分けて作成することもできます。|[チュートリアル:モデルの統計を生成するためのデータベース プロジェクトのビルドの拡張](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)<br /><br />[チュートリアル:配置計画を変更するためにデータベース プロジェクトの配置を拡張する](../ssdt/walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan.md)<br /><br />[チュートリアル:配置計画を分析するためのデータベース プロジェクトの配置の拡張](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)|  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストのカスタム テスト条件](https://msdn.microsoft.com/library/jj860449(v=vs.103).aspx)  
  
