---
title: 多次元モデル オブジェクトの処理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- online mode [Analysis Services]
- processing objects [Analysis Services]
- partitions [Analysis Services], processing
- jobs [Analysis Services]
- objects [Analysis Services], processing
- reprocessing objects
- impact analysis [Analysis Services]
- dimensions [Analysis Services], processing
- project mode [Analysis Services]
- cubes [Analysis Services], processing
ms.assetid: 625aa5a6-aa09-4bac-be8a-778fa81c5a61
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d4952724f19a3c7010884feac0254f4f75d90ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073362"
---
# <a name="multidimensional-model-object-processing"></a>多次元モデルのオブジェクト処理
  "処理" とは、Analysis Services がリレーショナル データ ソースから多次元モデルにデータを読み込む 1 つまたは一連のステップです。 MOLAP ストレージを使用するオブジェクトの場合、データはディスクのデータベース ファイル フォルダーに保存されます。 ROLAP ストレージの場合、処理は要求に応じて、オブジェクトに対する MDX クエリへの応答として発生します。 ROLAP ストレージを使用するオブジェクトの場合の処理とは、クエリ結果を返す前にキャッシュを更新する操作のことを指します。  
  
 既定では、処理は、サーバーにソリューションを配置するときに発生します。 また、ソリューションの全体または一部を、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] や [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]などのツールを使用して随時処理したり、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] や SQL Server エージェントを使用してスケジュールに従って処理することもできます。 ディメンションの削除や互換性レベルの変更など、モデルの構造を変更するときは、モデルの物理的および論理的な構造を同期するために再度処理する必要があります。  
  
 このトピックのセクションは次のとおりです。  
  
 [前提条件](#bkmk_prereq)  
  
 [ツールまたは方法を選択する](#bkmk_tool)  
  
 [オブジェクトの処理](#bkmk_proc)  
  
 [Reprocessing Objects](#bkmk_reproc)  
  
##  <a name="bkmk_prereq"></a> 前提条件  
  
-   処理を行うには、Analysis Services のインスタンスに対する管理権限が必要です。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] や [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]から対話形式で処理を行う場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスのサーバー管理者ロールのメンバーである必要があります。 たとえば、SQL Server エージェントでスケジュールを設定した SSIS パッケージを使用するなど、自動的に実行される処理の場合は、パッケージの実行に使用するアカウントがサーバー管理者ロールのメンバーである必要があります。 管理者のアクセス許可の設定の詳細については、次を参照してください。[サーバーの管理者アクセス許可の付与&#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)します。  
  
-   データの取得に使用するアカウントは、データ ソース オブジェクトで指定されます。Windows 認証を使用する場合は権限借用オプションで指定され、データベース認証を使用する場合は接続文字列のユーザー名で指定されます。 このアカウントには、モデルで使用するリレーショナル データ ソースに対する読み取り権限が必要です。  
  
-   オブジェクトを処理する前に、プロジェクトまたはソリューションを配置する必要があります。  
  
     最初のうち、モデル開発の早い段階では、配置と処理が一緒に発生します。 ただし、ソリューションを配置した後は、モデルを処理するオプションを設定することができます。 配置の詳細については、「[Analysis Services プロジェクトの配置 (SSDT)](deploy-analysis-services-projects-ssdt.md)」を参照してください。  
  
##  <a name="bkmk_tool"></a> ツールまたは方法を選択する  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] や [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]などのクライアント アプリケーション、または SQL Server エージェント ジョブや [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージとして実行されるスクリプト操作を使用して、オブジェクトを対話形式で処理することができます。  
  
 データベースをどのように処理するかは、モデルが開発中か、実稼動しているかによって異なります。 いったんモデルが実稼動サーバーに配置されたら、多次元データの整合性や可用性を確保するために、処理は厳密に管理される必要があります。 オブジェクトどうしは、相互に依存するため、通常、処理はモデル間で連鎖的に影響を及ぼします。これは、他のオブジェクトも平行して処理されたり、処理されなかったりするためです。 いくつかのオブジェクトが未処理状態の場合、そのデータに対するクエリは解決せず、データを使用するレポートやアプリケーションは中断します。 実稼動データベースを処理する方法を開発する場合、演算子エラーや手順の見落としを避けるために、デバッグおよびテストが完了しているスクリプトまたは [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージの使用を検討してください。  
  
 詳細については、「[処理するためのツールと方法 (Analysis Services)](tools-and-approaches-for-processing-analysis-services.md)」を参照してください。  
  
##  <a name="bkmk_proc"></a> オブジェクトの処理  
 処理は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクト (メジャー グループ、パーティション、ディメンション、キューブ、マイニング モデル、マイニング構造、およびデータベース) に影響します。 あるオブジェクトに 1 つまたは複数のオブジェクトが含まれている場合は、最上位レベルのオブジェクトを処理すると、連鎖的に下位レベルのオブジェクトがすべて処理されます。 たとえば、通常、キューブには、1 つ以上のメジャー グループ (各メジャー グループには 1 つ以上のパーティションが含まれています) とディメンションが含まれています。 キューブを処理すると、そのキューブ内のメジャー グループと、その構成要素である、現在未処理の状態にあるディメンションがすべて処理されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトの処理に関する詳細については、「 [Analysis Services オブジェクトの処理 (Analysis Services)](processing-analysis-services-objects.md)」を参照してください。  
  
 処理ジョブの実行中は、クエリを実行するために、影響を受ける [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトにアクセスできます。 処理ジョブはトランザクション内で実行され、そのトランザクションはコミットまたはロールバックできます。 処理ジョブが失敗すると、トランザクションはロールバックされます。 処理ジョブが成功すると、変更がコミットされている間はオブジェクトが排他的にロックされます。つまり、このオブジェクトはクエリや処理に一時的に使用できなくなります。 トランザクションのコミット フェーズの間でも、クエリをオブジェクトに送信できますが、そのクエリはコミットが完了するまでキューに置かれます。  
  
 処理ジョブを実行するとき、オブジェクトの処理の有無およびその処理方法は、そのオブジェクトに設定されている処理オプションによって異なります。 各オブジェクトに適用できる特定の処理オプションの詳細については、「[処理オプションと設定 (Analysis Services)](processing-options-and-settings-analysis-services.md)」を参照してください。  
  
##  <a name="bkmk_reproc"></a> Reprocessing Objects  
 未処理の要素を含んでいるキューブは、参照する前に再処理する必要があります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 内のキューブには、キューブをクエリする前に処理する必要のあるメジャー グループとパーティションが含まれています。 キューブを処理すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、キューブの構成要素であるディメンションが未処理の状態にある場合、そのディメンションを処理します。 オブジェクトを最初に処理した後、次のような状態が発生した場合は、部分的または全体的にオブジェクトを再処理する必要があります。  
  
-   オブジェクトの構造が変化した場合 (ファクト テーブル内の列を削除するなど)  
  
-   オブジェクトの集計デザインが変化した場合  
  
-   オブジェクト内のデータを更新する必要がある場合  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でオブジェクトを処理する場合は、処理オプションを選択するか、適切な種類の処理を決定する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の機能を有効にすることができます。 使用可能な処理方法はオブジェクトごとに異なり、オブジェクトの種類に基づいています。 また、使用可能な方法は、オブジェクトの最後の処理後にオブジェクトに対して行われた変更に基づいています。 処理方法を自動的に選択する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の機能を有効にすると、オブジェクトを完全処理状態に最短時間で戻す方法が使用されます。 詳細については、「[Processing Options and Settings (Analysis Services)](processing-options-and-settings-analysis-services.md)」(処理オプションと設定 (Analysis Services)) を参照してください。  
  
## <a name="see-also"></a>参照  
 [論理アーキテクチャ (Analysis Services - 多次元データ)](olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [データベース オブジェクト (Analysis Services - 多次元データ)](olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
