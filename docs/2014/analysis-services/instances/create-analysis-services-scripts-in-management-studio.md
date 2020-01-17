---
title: Management Studio での Analysis Services スクリプトの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services objects, scripts
- objects [Analysis Services], scripts
- scripts [Analysis Services], objects
ms.assetid: 4f1b965c-9ca6-427b-8f4d-0ce1eea7c0fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e3cca216f7c2312b4e7b54f2236a5d1f7bafd9e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080109"
---
# <a name="create-analysis-services-scripts-in-management-studio"></a>Management Studio での Analysis Services スクリプトの作成
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、スクリプトの生成機能、テンプレート、および Analysis Services オブジェクトとタスクのスクリプトを作成するために使用できるエディターが含まれています。  
  
## <a name="script-analysis-services-tasks-in-management-studio"></a>Management Studio で Analysis Services タスクのスクリプトを作成する  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のタスクのスクリプト作成は、タスク指向のダイアログ ボックスで、いずれかのスクリプト オプションをクリックすることで実現します。 バックアップやデータベースの復元、オブジェクトの処理、集計のデザインなどのタスクを実行するために使用するすべてのダイアログ ボックスには、ダイアログ ボックスの上部にスクリプト オプションがあります。 これらのオプションのいずれかを選択すると、ダイアログ ボックス内の情報と設定に基づいて、XMLA スクリプトが生成されます。  
  
 既定では、スクリプトが生成され、XMLA クエリ エディター内に配置されますが、スクリプト オプション リストを拡張して、Windows クリップボードやファイルにスクリプトを出力することもできます。  
  
#### <a name="to-script-an-analysis-services-task"></a>Analysis Services タスクのスクリプトを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続します。  
  
2.  データベースを右クリックし、 **[バックアップ]** をクリックします。 [データベースのバックアップ] ダイアログ ボックスが開きます。 バックアップのファイル名を指定し、このバックアップに必要なオプションを選択します。  
  
3.  ダイアログ ボックスの上部にある **[スクリプト]** をクリックします。 スクリプト機能は、Management Studio 内のすべてのタスク ベースのダイアログ ボックスに含まれています。 次のオプションがあります。**スクリプト アクションを新規クエリ ウィンドウに**クエリ エディター ウィンドウを開く**ファイルにスクリプト アクション**XMLA スクリプトをファイルに保存するまたは**スクリプト操作をクリップボードに**する XMLA スクリプトを保存する、クリップボード。  
  
     Management Studio でスクリプト オプションとして表示される **[スクリプト操作をジョブに保存]** オプションは、Analysis Services スクリプトではサポートされていないことに注意してください。  
  
4.  既定のオプションである **[スクリプト操作を新規クエリ ウィンドウに保存]** を選択すると、生成されたスクリプトは、XMLA クエリ ウィンドウに配置されます。  
  
     [データベースのバックアップ] ダイアログ ボックスを閉じて、XMLA スクリプトを直接、編集または実行できます。  
  
## <a name="script-analysis-services-objects-in-management-studio"></a>Management Studio で Analysis Services オブジェクトのスクリプトを作成する  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクトを右クリックし、 **[CREATE]** 、 **[ALTER]** 、または **[DELETE]** を選択して、オブジェクトのスクリプト作成を実行します。 これらの各オプションは、ウィンドウまたはファイルに出力できますが、スクリプトの出力先に関係なく、XMLA ラッパーの DDL スクリプトの形式で出力されます。 このようなスクリプトは、指定するどのサーバーに対しても実行できるという大きな利点があります。 また、スクリプトの名前は変更可能で、オブジェクトの大量作成、変更、または削除を反復的に行うことができます。  
  
 スクリプトを作成できるオブジェクトには、データ ソース、データ ソース ビュー、キューブ、ディメンション、マイニング構造、およびロールを含む [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの要素が含まれます。  
  
 前提条件として XML for Analysis (XMLA) を理解している必要があります。 しかし、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、キューブなどのオブジェクトの作成に必要な XMLA スクリプトを自動的に作成する機能があります。 この自動化機能により、XMLA の習得の必要性が緩和されます。 XMLA の使用方法の詳細については、「 [Analysis Services での XMLA による開発](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)」を参照してください。 XMLA の使用方法の詳細については、「 [Analysis Services での XMLA による開発](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Role オブジェクトのスクリプトを作成する場合、セキュリティ権限はオブジェクトが関連付けられているセキュリティ ロールではなく、オブジェクト自体に含まれていることに注意してください。  
  
#### <a name="to-script-analysis-services-objects"></a>Analysis Services オブジェクトのスクリプトを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続します。  
  
2.  オブジェクトの作成、変更、削除のいずれかを行うスクリプトを作成するオブジェクトを選択します。  
  
3.  オブジェクトを右クリックし、**キューブをスクリプト化**、 をポイント**Create**、 **Alter**、または**を削除する**のいずれかをクリックし、次のオプション:**新しいクエリ エディター ウィンドウ**クエリ エディター ウィンドウを開く**ファイル**XMLA スクリプトをファイルに保存するまたは**クリップボード**XMLA スクリプトをクリップボードに保存します。  
  
    > [!NOTE]  
    >  通常、複数の異なるバージョンのファイルを作成する場合は、 **[ファイル]** を選択します。  
  
## <a name="see-also"></a>参照  
 [Analysis Services の管理タスクのスクリプト作成](../script-administrative-tasks-in-analysis-services.md)   
 [XMLA クエリ エディター (Analysis Services - 多次元データ)](../xmla-query-editor-analysis-services-multidimensional-data.md)  
  
  
