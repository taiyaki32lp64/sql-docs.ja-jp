---
title: ファイル システム タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.f1
helpviewer_keywords:
- File System task [Integration Services]
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c9a2244c5e6cddbc53ccd3aaec7faaaa3836a923
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831747"
---
# <a name="file-system-task"></a>ファイル システム タスク
  ファイル システム タスクは、ファイル システム内のファイルとディレクトリの操作を実行します。 たとえば、ファイル システム タスクを使用すると、パッケージはディレクトリやファイルの作成、移動、または削除を実行できます。 また、ファイル システム タスクを使用して、ファイルやディレクトリの属性を設定することもできます。 たとえば、ファイル システム タスクを使用すると、ファイルを非表示にしたり読み取り専用にできます。  
  
 ファイル システム タスクのすべての操作では、ファイルまたはディレクトリをソースとして使用します。 たとえば、タスクによりコピーされるファイルや、タスクにより削除されるディレクトリは、ソースと呼ばれます。 ソースを指定するには、ファイル接続マネージャーを使用してディレクトリまたはファイルをポイントするか、ソースへのパスが含まれる変数の名前を指定します。 詳細については、「[ファイル接続マネージャー](../connection-manager/file-connection-manager.md)」および「[Integration Services (SSIS) の変数](../integration-services-ssis-variables.md)」を参照してください。  
  
 ファイルやディレクトリをコピーまたは移動する操作、およびファイルの名前を変更する操作では、その操作の出力先となるファイルまたはディレクトリと、基になるファイルまたはディレクトリを使用します。 操作の出力先となるファイルまたはディレクトリは、ファイル接続マネージャーまたは変数を使用して指定します。 ファイル システム タスクの操作は、出力先のファイルやディレクトリの上書きを許可するように構成できます。 新しいディレクトリを作成する操作は、そのディレクトリが既に存在していても失敗するのではなく、指定した名前の既存のディレクトリが使用されるように構成できます。  
  
## <a name="predefined-file-system-operations"></a>定義済みのファイル システム操作  
 ファイル システム タスクには、定義済みの操作のセットが含まれています。 次の表では、これらの操作について説明します。  
  
|操作|Description|  
|---------------|-----------------|  
|ディレクトリのコピー|ある場所から別の場所にフォルダーをコピーします。|  
|ファイルのコピー|ある場所から別の場所にファイルをコピーします。|  
|ディレクトリの作成|指定した場所にフォルダーを作成します。|  
|ディレクトリの削除|指定した場所のフォルダーを削除します。|  
|ディレクトリ コンテンツの削除|フォルダー内のすべてのファイルおよびフォルダーを削除します。|  
|ファイルの削除|指定した場所のファイルを削除します。|  
|ディレクトリの移動|ある場所から別の場所にフォルダーを移動します。|  
|ファイルの移動|ある場所から別の場所にファイルを移動します。|  
|ファイル名の変更|指定した場所にあるファイル名を変更します。|  
|属性の設定|ファイルやディレクトリの属性を設定します。 属性には、アーカイブ、非表示、標準、読み取り専用、およびシステムが含まれます。 標準には属性がなく、他の属性と組み合わせることはできません。 他のすべての属性は、組み合わせて使用できます。|  
  
 ファイル システム タスクは、1 つのファイルまたはディレクトリのみを処理できます。 したがって、このタスクでは、ワイルドカード文字を使用して複数のファイルに同じ処理を行うことはできません。 ファイル システム タスクが複数のファイルやディレクトリに対して同じ処理を繰り返し行うようにするには、次の手順に示すように、ファイル システム タスクを Foreach ループ コンテナー内に配置します。  
  
-   **Foreach ループ コンテナーの構成** [Foreach ループ エディター] の **[コレクション]** ページで **[Foreach File 列挙子]** に列挙子を設定して、 **[ファイル]** の列挙子の構成としてワイルドカード式を入力します。 [Foreach ループ エディター] の **[変数のマッピング]** ページで、ファイル名を一度に 1 つずつファイル システム タスクに渡すために使用する変数をマップします。  
  
-   **ファイル システム タスクの追加と構成** ファイル システム タスクを Foreach ループ コンテナーに追加します。 [ファイル システム タスク エディター] の **[全般]** ページで、 **SourceVariable** プロパティまたは **DestinationVariable** プロパティに、Foreach ループ コンテナーで定義した変数を設定します。  
  
## <a name="custom-log-entries-available-on-the-file-system-task"></a>ファイル システム タスクで使用できるカスタム ログ エントリ  
 次の表では、ファイル システム タスクのカスタム ログ エントリを説明します。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`FileSystemOperation`|タスクで実行される操作を報告します。 ログ エントリは、ファイル システム操作の開始時に書き込まれます。これには、操作の基になるファイルと操作対象のファイルに関する情報が含まれます。|  
  
## <a name="configuring-the-file-system-task"></a>ファイル システム タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[ファイル システム タスク エディター]\([全般] ページ)](../general-page-of-integration-services-designers-options.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
 プログラムでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、データ ファイルをダウンロードまたはアップロードし、サーバー上のディレクトリを管理するタスクが含まれます。 詳細については、「 [FTP タスク](ftp-task.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
