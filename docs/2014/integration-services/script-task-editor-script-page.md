---
title: スクリプト タスク エディター ([スクリプト] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scripttask.script.f1
helpviewer_keywords:
- Script Task Editor
ms.assetid: 93da0e0d-83f5-406d-b144-4cce216571cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 037b176dfacd9420fba64a405d8c851c558e93e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056188"
---
# <a name="script-task-editor-script-page"></a>[スクリプト タスク エディター] \([スクリプト] ページ)
  **[スクリプト タスク エディター]** ダイアログ ボックスの **[スクリプト]** ページを使用すると、スクリプト プロパティを設定し、スクリプトによってアクセスできる変数を指定できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssISversion10](../includes/ssisversion10-md.md)] およびそれ以降のバージョンでは、すべてのスクリプトがプリコンパイル済みです。 以前のバージョンでは、 **PrecompileScriptIntoBinaryCode** プロパティを設定して、スクリプトを事前コンパイルするかどうかを指定していました。  
  
 スクリプト タスクの詳細については、「 [Script Task](control-flow/script-task.md) 」および「 [スクリプト タスク エディターでのスクリプト タスクの構成](extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)」を参照してください。 スクリプト タスクのプログラミングの詳細については、「 [Extending the Package with the Script Task](extending-packages-scripting/task/extending-the-package-with-the-script-task.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[ScriptLanguage]**  
 タスクのスクリプト言語を選択します。 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic または [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C# のいずれかです。  
  
 タスクのスクリプトを作成した後に、 **[ScriptLanguage]** プロパティの値を変更することはできません。  
  
 スクリプト タスクの既定のスクリプト言語を設定するには、 **[オプション]** ダイアログ ボックスの **[全般]** ページにある **[スクリプト言語]** オプションを使用します。 詳細については、「 [General Page](general-page-of-integration-services-designers-options.md)」を参照してください。  
  
 **[EntryPoint]**  
 スクリプト タスクのコードのエントリ ポイントとして [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ランタイムが呼び出すメソッドを指定します。 指定するメソッドは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA) プロジェクトの ScriptMain クラスに存在する必要があります。ScriptMain クラスは、スクリプト テンプレートによって生成される既定のクラスです。  
  
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
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [General Page](general-page-of-integration-services-designers-options.md)   
 [[スクリプト タスク エディター] &#40;[全般] ページ&#41;](../../2014/integration-services/script-task-editor-general-page.md)   
 [[式] ページ](expressions/expressions-page.md)   
 [スクリプト タスクの例](extending-packages-scripting-task-examples/script-task-examples.md)   
 [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)   
 [パッケージ内のユーザー定義変数のスコープの追加、削除、変更](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  
