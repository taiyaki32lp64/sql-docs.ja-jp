---
title: Integration Services タスク | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [Integration Services], tasks
- files [Integration Services], task options
- workflow tasks [Integration Services]
- Integration Services, tasks
- adding package tasks
- tasks [Integration Services], listed
- SSIS tasks
- SSIS, tasks
- control flow [Integration Services], tasks
- tasks [Integration Services]
- grouping tasks
- tasks [Integration Services], about tasks
- SQL Server Integration Services tasks
- data preparation tasks [Integration Services]
- directory operations [Integration Services]
ms.assetid: 75c8901d-6966-4af3-abe5-10af6dd9313b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 89f73de6a8474b6e2842de7b1caf0b882ff2b5c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831452"
---
# <a name="integration-services-tasks"></a>Integration Services タスク
  タスクとは、パッケージ制御フローで実行される作業の単位を定義する、制御フローの要素のことです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、1 つ以上のタスクで構成されます。 パッケージに複数のタスクが含まれる場合、それらのタスクは優先順位制約によって順序が決定され、制御フロー内で連結されます。  
  
 また、COM をサポートする Visual Basic などのプログラミング言語や、C# などの .NET プログラミング言語を使用して、カスタム タスクを記述することもできます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーは、パッケージを操作するための [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のグラフィック ツールであり、パッケージ制御フローを作成するためのデザイン画面、およびタスクを構成するためのカスタム エディターが用意されています。 また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクト モデルをプログラムし、プログラムによってパッケージを作成することもできます。  
  
## <a name="types-of-tasks"></a>タスクの種類  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、次の種類のタスクが含まれます。  
  
 [データ フロー タスク]  
 データ フローを実行して、データの抽出、列レベルの変換の適用、およびデータの読み込みを行うタスクです。  
  
 データ準備タスク  
 ファイルやディレクトリのコピー、ファイルやデータのダウンロード、Web メソッドの実行、XML ドキュメントへの操作の適用、および最適化のためのデータのプロファイルを行うタスクです。  
  
 ワークフロー タスク  
 別のプロセスと通信して、パッケージの実行、プログラムまたはバッチ ファイルの実行、パッケージ間のメッセージの送受信、電子メール メッセージの送信、Windows Management Instrumentation (WMI) データの読み取り、および WMI イベントの監視を行うタスクです。  
  
 SQL Server のタスク  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のオブジェクトとデータにアクセスし、コピー、挿入、削除、および変更を行うタスクです。  
  
 スクリプト タスク  
 スクリプトを使用して、パッケージ機能を拡張するタスクです。  
  
 Analysis Services のタスク  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトを作成、変更、削除、および処理するタスクです。  
  
 メンテナンス タスク  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのバックアップと圧縮、インデックスの再構築と再編成、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの実行などの管理機能を実行するタスクです。  
  
 カスタム タスク  
 COM をサポートする Visual Basic などのプログラミング言語や、C# などの .NET プログラミング言語を使用して、カスタム タスクを記述することもできます。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでカスタム タスクにアクセスする場合、タスク用のユーザー インターフェイスを作成して登録できます。 詳細については、「 [カスタム タスクの開発](../extending-packages-custom-objects/task/developing-a-custom-task.md)」を参照してください。  
  
## <a name="configuration-of-tasks"></a>タスクの構成  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージには、1 つのタスクを含めることができます。たとえば、パッケージの実行時にデータベース テーブルのレコードを削除する、SQL 実行タスクを含めます。 ただし、通常のパッケージには複数のタスクが含まれており、各タスクはパッケージ制御フローのコンテキスト内で実行されるように設定されます。 イベント ハンドラーは、ランタイム イベントに応答して実行されるワークフローであり、ここにも複数のタスクを含めることができます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーを使用してパッケージにタスクを追加する方法の詳細については、「 [制御フローのタスクまたはコンテナーを追加または削除する](add-or-delete-a-task-or-a-container-in-a-control-flow.md)」を参照してください。  
  
 プログラムによってパッケージにタスクを追加する方法の詳細については、「 [プログラムによるタスクの追加](../building-packages-programmatically/adding-tasks-programmatically.md)」を参照してください。  
  
 各タスクは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで用意されている、各タスク用のカスタム ダイアログ ボックスを使用して、個別に構成できます。または、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]に含まれる [プロパティ] ウィンドウから構成できます。 パッケージには、6 つの SQL 実行タスクなど、同じ種類の複数のタスクを含めることができ、各タスクは個別に構成できます。 詳細については、「 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)」を参照してください。  
  
## <a name="tasks-connections-and-groups"></a>タスクの連結とグループ  
 タスクに複数のタスクが含まれる場合、それらのタスクは優先順位制約によって順序が決定され、制御フロー内で連結されます。 優先順位制約の詳細については、「 [優先順位制約](precedence-constraints.md)」を参照してください。  
  
 タスクをグループ化して 1 つの作業単位として実行したり、ループ内で繰り返すことができます。 詳細については、「 [Foreach ループ コンテナー](foreach-loop-container.md)」、「 [For ループ コンテナー](for-loop-container.md)」、および「 [シーケンス コンテナー](sequence-container.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [制御フローのタスクまたはコンテナーを追加または削除する](add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
  
