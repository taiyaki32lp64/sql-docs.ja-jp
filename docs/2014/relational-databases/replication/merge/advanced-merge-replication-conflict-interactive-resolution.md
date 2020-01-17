---
title: インタラクティブな競合解決 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- interactive conflict resolution [SQL Server replication]
- interactive resolver [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 43347190c53331d0a30ba0f29d795cce981eec34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245119"
---
# <a name="interactive-conflict-resolution"></a>Interactive Conflict Resolution
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーションでは、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 同期マネージャーでの要求時同期中に、手動で競合を解決できるインタラクティブ競合回避モジュールを利用できます。 インタラクティブ競合回避モジュールを実行時に有効化すると、グラフィカル インターフェイスに競合する各行のデータが表示されます。ここから、競合するデータを表示および編集し、個々の競合を解決できます。  
  
 インタラクティブ競合回避モジュールは競合表示モジュールに似ています。 ただし、競合表示モジュールではマージ同期後に解決済みの競合の結果が表示されるのに対して、インタラクティブ競合回避モジュールでは解決の前に各競合が表示されるため、マージ同期時に取り込むデータを指定できます。 いずれかのユーザーが、競合発生時にインタラクティブ競合回避モジュールを監視できるようになっている必要があります。  
  
> [!NOTE]  
>  インタラクティブな競合回避には Windows 同期マネージャーが必要です。 同期が Windows 同期マネージャーの外部で (スケジュールされた同期、または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] かレプリケーション モニターでの要求時同期として) 実行される場合、競合は、アーティクルに指定された競合回避モジュールに従って、ユーザーの介入なしに自動的に解決されます。 論理レコードに関連する競合は、インタラクティブ競合回避モジュールには表示されません。 これらの競合に関する情報を表示するには、レプリケーション ストアド プロシージャを使用します。 詳細については、「[マージ パブリケーションの競合情報の表示 (レプリケーション Transact-SQL プログラミング)](../view-conflict-information-for-merge-publications.md)」を参照してください。  
  
## <a name="article-resolvers-and-the-interactive-resolver"></a>アーティクル競合回避モジュールおよびインタラクティブ競合回避モジュール  
 競合回避モジュール (既定の競合回避モジュール、ビジネス ロジック ハンドラー、カスタム競合回避モジュールのいずれか) は、パブリケーションの作成時に特定のアーティクルに割り当てられます。そこでルールのセットによって、競合している行データを入力したときにどのデータセットを使用するかが決まります。 インタラクティブ競合回避モジュールは、競合でどのデータを優先するかを指定するルールを持つ独立した競合回避モジュールではなく、既定またはカスタムの競合回避モジュールと組み合わせて使用するツールです。 アーティクル競合回避モジュールでは、どの行を競合で優先し、どの行を優先しないかが指定されますが、インタラクティブ競合回避モジュールでは、その結果にユーザーが介入し、データを受け入れたり、拒否したり、変更したりすることができます。  
  
 インタラクティブ競合回避モジュールを使用するには、競合回避を必要とする各アーティクルまたはサブスクリプションに対して、インタラクティブな競合回避を有効にしておく必要があります。 1 つ以上のアーティクルまたはサブスクリプションで有効にしておくと、マージ同期中に競合が検出された場合、インタラクティブ競合回避モジュールを使用できます。  
  
 インタラクティブ競合回避モジュールを使用するには、「[Specify Interactive Conflict Resolution for Merge Articles](..//publish/specify-merge-replication-properties.md#interactive-conflict-resolution)」 (マージ アーティクルにインタラクティブな競合解決を指定する) と「[Synchronize a Subscription Using Windows Synchronization Manager (Windows Synchronization Manager)](../synchronize-a-subscription-using-windows-synchronization-manager.md)」 (Windows 同期マネージャーを使用してサブスクリプションを同期する) を参照してください。  
  
## <a name="see-also"></a>参照  
 [マージ レプリケーションの競合検出および解決の詳細](advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
