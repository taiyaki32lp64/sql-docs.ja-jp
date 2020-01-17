---
title: スクリプト タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scripttask.f1
helpviewer_keywords:
- scripts [Integration Services], tasks
- Script task [Integration Services], about Script task
- Script task [Integration Services]
ms.assetid: f6cce7df-4bd6-4b75-9f89-6c37b4bb5558
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7c710065bf0a87b5ec3850010344f2ef5114022e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830563"
---
# <a name="script-task"></a>スクリプト タスク
  スクリプト タスクでは、組み込みのタスクで利用できない関数を実行するコード、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で用意されている変換を実行するコードが用意されています。 また、スクリプト タスクを使用すると、複数のタスクおよび変換を使用しなくても、関数を 1 つのスクリプトに結合できます。 スクリプト タスクは、データ行ごとに 1 回ではなく、1 つのパッケージ内で 1 回 (または列挙されたオブジェクトごとに 1 回) 行う作業に使用します。  
  
 スクリプト タスクは、次の目的で使用できます。  
  
-   組み込みの接続の種類ではサポートされていないその他のテクノロジを使用して、データにアクセスします。 たとえば、スクリプトは、Active Directory Service Interfaces (ADSI) を使用して Active Directory のユーザー名にアクセスし、ユーザー名を抽出できます。  
  
-   パッケージ固有のパフォーマンス カウンターを作成します。 たとえば、スクリプトを使用して、複雑なタスクや時間のかかるタスクの実行中に更新されるパフォーマンス カウンターを作成できます。  
  
-   指定されたファイルが空かどうか、またはそれらのファイルに含まれている行数を判断し、その情報に基づいて、パッケージ内の制御フローを調整します。 たとえば、ファイル内の行数が 0 行の場合は、変数の値が 0 に設定され、値を評価する優先順位制約で、ファイル システム タスクによるファイルのコピーが回避されます。  
  
 スクリプトを使用してセット内のデータ行ごとに同じ作業を行う必要がある場合は、スクリプト タスクではなく、スクリプト コンポーネントを使用します。 たとえば、郵送料が妥当かどうかを評価し、極端に高いデータ行や極端に安いデータ行をスキップする場合は、スクリプト コンポーネントを使用します。 詳細については、「 [Script Component](../data-flow/transformations/script-component.md)」を参照してください。  
  
 複数のパッケージで 1 つのスクリプトを使用する場合は、スクリプト タスクを使用せず、カスタム タスクを記述することをお勧めします。 詳細については、「 [カスタム タスクの開発](../extending-packages-custom-objects/task/developing-a-custom-task.md)」を参照してください。  
  
 スクリプト タスクがパッケージにとって適切な選択である場合、タスクが使用するスクリプトを開発して、タスク自体を構成する必要があります。  
  
## <a name="writing-and-running-the-script-that-the-task-uses"></a>タスクが使用するスクリプトの記述と実行  
 スクリプト タスクでは、スクリプトを記述する環境、およびそのスクリプトを実行するエンジンとして [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) を使用します。  
  
 VSTA には、色分け表示が可能な [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] エディター、IntelliSense、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] オブジェクト エクスプローラー **など、** 環境での標準機能がすべて含まれています。 VSTA には、他の [!INCLUDE[msCoName](../../includes/msconame-md.md)] の開発ツールに付属しているのと同じデバッガーも含まれています。 スクリプト内のブレークポイントは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のタスクやコンテナーのブレークポイントとシームレスに動作します。 VSTA では、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic と [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# の両方のプログラミング言語がサポートされます。  
  
 スクリプトを実行するには、パッケージを実行するコンピューターに VSTA がインストールされている必要があります。 パッケージを実行すると、タスクはスクリプト エンジンを読み込み、スクリプトを実行します。 プロジェクト内のアセンブリへの参照を追加すると、スクリプトから外部の .NET アセンブリにアクセスできます。  
  
> [!NOTE]  
>  スクリプトをプリコンパイルするかどうかを指定できた以前のバージョンとは異なり、 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 以降のバージョンではすべてのスクリプトがプリコンパイルされます。 スクリプトがプリコンパイルされると、実行時に言語エンジンを読み込まないため、パッケージの実行速度が向上します。 ただし、コンパイル済みのバイナリ ファイルは多量のディスク領域を使用します。  
  
## <a name="configuring-the-script-task"></a>スクリプト タスクの構成  
 スクリプト タスクは、次の方法で構成できます。  
  
-   タスクを実行するカスタム スクリプトを指定します。  
  
-   スクリプト タスク コードのエントリ ポイントとして [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ランタイムが呼び出す、VSTA プロジェクトのメソッドを指定します。  
  
-   スクリプト言語を指定します。  
  
-   必要に応じて、スクリプトで使用する読み取り専用の変数および読み取り/書き込み変数の一覧を指定します。  
  
 これらのプロパティは [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定するか、またはプログラムによって設定します。  
  
### <a name="configuring-the-script-task-in-the-designer"></a>デザイナーでのスクリプト タスクの構成  
 次の表では、スクリプト タスクでログに記録できる `ScriptTaskLogEntry` イベントについて説明します。 `ScriptTaskLogEntry`でログ記録イベントが選択されている、**詳細**のタブ、 **SSIS ログの構成** ダイアログ ボックス。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|スクリプト内でのログ記録の実装結果を報告します。 タスクは、`Log` オブジェクトの `Dts` メソッドを呼び出すたびにログ エントリを書き込みます。 タスクは、これらのエントリをコードの実行時に書き込みます。 詳細については、「 [スクリプト タスクでのログ記録](../extending-packages-scripting/task/logging-in-the-script-task.md)」を参照してください。|  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[スクリプト タスク エディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [[スクリプト タスク エディター] &#40;[スクリプト] ページ&#41;](../script-task-editor-script-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="configuring-the-script-task-programmatically"></a>プログラムによるスクリプト タスクの構成  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask>  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   shareourideas.com の技術記事「 [配信通知付きで電子メールを送信する方法 (C#)](https://go.microsoft.com/fwlink/?LinkId=237625)」  
  
  
