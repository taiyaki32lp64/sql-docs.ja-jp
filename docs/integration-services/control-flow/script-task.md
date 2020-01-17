---
title: スクリプト タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.scripttask.f1
- sql13.dts.designer.scripttask.general.f1
- sql13.dts.designer.scripttask.script.f1
helpviewer_keywords:
- scripts [Integration Services], tasks
- Script task [Integration Services], about Script task
- Script task [Integration Services]
ms.assetid: f6cce7df-4bd6-4b75-9f89-6c37b4bb5558
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1cb9ca9739ca6f50a2424d9d68ee66263edf08f3
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542303"
---
# <a name="script-task"></a>スクリプト タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  スクリプト タスクでは、組み込みのタスクで利用できない関数を実行するコード、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で用意されている変換を実行するコードが用意されています。 また、スクリプト タスクを使用すると、複数のタスクおよび変換を使用しなくても、関数を 1 つのスクリプトに結合できます。 スクリプト タスクは、データ行ごとに 1 回ではなく、1 つのパッケージ内で 1 回 (または列挙されたオブジェクトごとに 1 回) 行う作業に使用します。  
  
 スクリプト タスクは、次の目的で使用できます。  
  
-   組み込みの接続の種類ではサポートされていないその他のテクノロジを使用して、データにアクセスします。 たとえば、スクリプトは、Active Directory Service Interfaces (ADSI) を使用して Active Directory のユーザー名にアクセスし、ユーザー名を抽出できます。  
  
-   パッケージ固有のパフォーマンス カウンターを作成します。 たとえば、スクリプトを使用して、複雑なタスクや時間のかかるタスクの実行中に更新されるパフォーマンス カウンターを作成できます。  
  
-   指定されたファイルが空かどうか、またはそれらのファイルに含まれている行数を判断し、その情報に基づいて、パッケージ内の制御フローを調整します。 たとえば、ファイル内の行数が 0 行の場合は、変数の値が 0 に設定され、値を評価する優先順位制約で、ファイル システム タスクによるファイルのコピーが回避されます。  
  
 スクリプトを使用してセット内のデータ行ごとに同じ作業を行う必要がある場合は、スクリプト タスクではなく、スクリプト コンポーネントを使用します。 たとえば、郵送料が妥当かどうかを評価し、極端に高いデータ行や極端に安いデータ行をスキップする場合は、スクリプト コンポーネントを使用します。 詳細については、「 [Script Component](../../integration-services/data-flow/transformations/script-component.md)」を参照してください。  
  
 複数のパッケージで 1 つのスクリプトを使用する場合は、スクリプト タスクを使用せず、カスタム タスクを記述することをお勧めします。 詳細については、「 [カスタム タスクの開発](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)」を参照してください。  
  
 スクリプト タスクがパッケージにとって適切な選択である場合、タスクが使用するスクリプトを開発して、タスク自体を構成する必要があります。  
  
## <a name="writing-and-running-the-script-that-the-task-uses"></a>タスクが使用するスクリプトの記述と実行  
 スクリプト タスクでは、スクリプトを記述する環境、およびそのスクリプトを実行するエンジンとして [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) を使用します。  
  
 VSTA には、色分け表示が可能な [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] エディター、IntelliSense、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] オブジェクト エクスプローラー **など、** 環境での標準機能がすべて含まれています。 VSTA には、他の [!INCLUDE[msCoName](../../includes/msconame-md.md)] の開発ツールに付属しているのと同じデバッガーも含まれています。 スクリプト内のブレークポイントは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のタスクやコンテナーのブレークポイントとシームレスに動作します。 VSTA では、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic と [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# の両方のプログラミング言語がサポートされます。  
  
 スクリプトを実行するには、パッケージを実行するコンピューターに VSTA がインストールされている必要があります。 パッケージを実行すると、タスクはスクリプト エンジンを読み込み、スクリプトを実行します。 プロジェクト内のアセンブリへの参照を追加すると、スクリプトから外部の .NET アセンブリにアクセスできます。 現在、.NET Core および .NET Standard のアセンブリ参照はサポートされていません。  
  
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
 次の表では、スクリプト タスクでログに記録できる **ScriptTaskLogEntry** イベントについて説明します。 **ScriptTaskLogEntry** イベントは、 **[SSIS ログの構成]** ダイアログ ボックスの **[詳細]** タブでログ記録の対象として選択できます。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**ScriptTaskLogEntry**|スクリプト内でのログ記録の実装結果を報告します。 タスクは、 **Dts** オブジェクトの **Log** メソッドを呼び出すたびにログ エントリを書き込みます。 タスクは、これらのエントリをコードの実行時に書き込みます。 詳細については、「 [スクリプト タスクでのログ記録](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)」を参照してください。|  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[スクリプト タスク エディター] &#40;[全般] ページ&#41;](../../integration-services/control-flow/script-task-editor-general-page.md)  
  
-   [[スクリプト タスク エディター] &#40;[スクリプト] ページ&#41;](../../integration-services/control-flow/script-task-editor-script-page.md)  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="configuring-the-script-task-programmatically"></a>プログラムによるスクリプト タスクの構成  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask>  
  
## <a name="script-task-editor-general-page"></a>[スクリプト タスク エディター] \([全般] ページ)
  **[スクリプト タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、スクリプト タスクの名前と説明を入力できます。  
  
 スクリプト タスクの詳細については、「 [Script Task](../../integration-services/control-flow/script-task.md) 」および「 [スクリプト タスク エディターでのスクリプト タスクの構成](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)」を参照してください。 スクリプト タスクのプログラミングの詳細については、「 [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **Name**  
 スクリプト タスクの固有の名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **説明**  
 スクリプト タスクの説明を入力します。  
  
## <a name="script-task-editor-script-page"></a>[スクリプト タスク エディター] \([スクリプト] ページ)
  **[スクリプト タスク エディター]** ダイアログ ボックスの **[スクリプト]** ページを使用すると、スクリプト プロパティを設定し、スクリプトによってアクセスできる変数を指定できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] およびそれ以降のバージョンでは、すべてのスクリプトがプリコンパイル済みです。 以前のバージョンでは、 **PrecompileScriptIntoBinaryCode** プロパティを設定して、スクリプトを事前コンパイルするかどうかを指定していました。  
  
 スクリプト タスクの詳細については、「 [Script Task](../../integration-services/control-flow/script-task.md) 」および「 [スクリプト タスク エディターでのスクリプト タスクの構成](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)」を参照してください。 スクリプト タスクのプログラミングの詳細については、「 [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[ScriptLanguage]**  
 タスクのスクリプト言語を選択します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic または [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# のいずれかです。  
  
 タスクのスクリプトを作成した後に、 **[ScriptLanguage]** プロパティの値を変更することはできません。  
  
 スクリプト タスクの既定のスクリプト言語を設定するには、 **[オプション]** ダイアログ ボックスの **[全般]** ページにある **[スクリプト言語]** オプションを使用します。 詳細については、「 [General Page](../../integration-services/control-flow/script-task-editor-general-page.md)」を参照してください。  
  
 **EntryPoint**  
 スクリプト タスクのコードのエントリ ポイントとして [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ランタイムが呼び出すメソッドを指定します。 指定するメソッドは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) プロジェクトの ScriptMain クラスに存在する必要があります。ScriptMain クラスは、スクリプト テンプレートによって生成される既定のクラスです。  
  
 VSTA プロジェクトでメソッドの名前を変更する場合は、 **EntryPoint** プロパティの値を変更する必要があります。  
  
 **[ReadOnlyVariables]**  
 スクリプトに使用できる読み取り専用の変数の一覧をコンマ区切りで入力するか、省略記号ボタン ( **[...]** ) をクリックして **[変数の選択]** ダイアログ ボックスで変数を選択します。  
  
> [!NOTE]  
>  変数名では大文字と小文字が区別されます。  
  
 **[ReadWriteVariables]**  
 スクリプトに使用できる読み取り/書き込み用の変数の一覧をコンマ区切りで入力するか、省略記号ボタン ( **[...]** ) をクリックして **[変数の選択]** ダイアログ ボックスで変数を選択します。  
  
> [!NOTE]  
>  変数名では大文字と小文字が区別されます。  
  
 **[スクリプトの編集]**  
 スクリプトを作成または変更できる VSTA IDE が開きます。  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   shareourideas.com の技術記事「 [配信通知付きで電子メールを送信する方法 (C#)](https://go.microsoft.com/fwlink/?LinkId=237625)」  
  
  
