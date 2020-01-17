---
title: FTP タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ftptask.f1
- sql13.dts.designer.ftptask.general.f1
- sql13.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- FTP task [Integration Services]
ms.assetid: 41c3f2c4-ee04-460a-9822-bb9ae4036c2e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d606e66c3ad7a78edf3808578fe3021d2933b22d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294139"
---
# <a name="ftp-task"></a>FTP タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  FTP タスクは、データ ファイルをダウンロードまたはアップロードし、サーバー上のディレクトリを管理します。 たとえば、パッケージは、リモート サーバーまたはインターネット サイトから、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ ワークフローの一部としてデータ ファイルをダウンロードできます。 FTP タスクは、次の目的で使用できます。  
  
-   データを移動し、変換をデータに適用する前または後で、あるディレクトリから別のディレクトリに、ディレクトリやデータ ファイルをコピーします。  
  
-   コピー元の FTP サイトにログインし、ファイルやパッケージをコピー先のディレクトリにコピーします。  
  
-   データをデータベースに読み込む前に、FTP サイトからファイルをダウンロードし、変換を列データに適用します。  
  
 実行時には、FTP タスクは FTP 接続マネージャーを使用してサーバーに接続します。 FTP 接続マネージャーは、FTP タスクとは別に構成され、FTP タスク内で参照されます。 FTP 接続マネージャーには、サーバーの設定、FTP サーバーへのアクセス資格情報、および、サーバーへの接続のタイムアウトや再試行回数などのオプションが含まれています。 詳細については、「 [FTP 接続マネージャー](../../integration-services/connection-manager/ftp-connection-manager.md)」を参照してください。  
  
> [!IMPORTANT]  
>  FTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
 ローカル ファイルまたはローカル ディレクトリにアクセスする場合、FTP タスクは、ファイル接続マネージャー、または変数に格納されたパス情報を使用します。 それに対し、リモート ファイルまたはリモート ディレクトリにアクセスする場合、FTP タスクは、FTP 接続マネージャーで直接指定されたリモート サーバーのパス、または変数に格納されたパス情報を使用します。 詳細については、「[ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)」および「[Integration Services (SSIS) の変数](../../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
 したがって、FTP タスクは複数のファイルを受信し、複数のリモート ファイルを削除できます。ただし、FTP タスクが接続マネージャーを使用している場合には、1 つのファイルのみを送信し、1 つのローカル ファイルのみを削除できます。ファイル接続マネージャーがアクセスできるのは 1 ファイルのみであるためです。 複数のローカル ファイルにアクセスするには、FTP タスクで変数を使用してパス情報を指定する必要があります。 たとえば、"C:\Test\&#42;.txt" を含む変数は、Test ディレクトリ内で .txt 拡張子を持つすべてのファイルの削除または送信をサポートするパスを提供します。  
  
 複数のファイルを送信したり、複数のローカル ファイルまたはディレクトリにアクセスするには、Foreach ループに FTP タスクを含めて、複数回実行する方法もあります。 Foreach ループは、For Each File 列挙子を使用して、ディレクトリ内のファイル全体を列挙します。 詳細については、「 [Foreach ループ コンテナー](../../integration-services/control-flow/foreach-loop-container.md)」を参照してください。  
  
 FTP タスクでは、パス内で *?* および *\** ワイルドカード文字がサポートされます。 これによってタスクは複数のファイルにアクセスできます。 ただし、ワイルドカードが使用できるのは、パスのファイル名を指定する部分のみです。 たとえば、C:\MyDirectory\\*.txt は有効なパスですが、C:\\\*\MyText.txt は無効なパスです。  
  
 操作に失敗した場合にファイル システムに関するタスクを停止したり、ファイルを ASCII モードで転送するように FTP 操作を構成できます。 ファイルのコピーを送受信する操作は、コピー先のファイルおよびディレクトリを上書きするように構成できます。  
  
## <a name="predefined-ftp-operations"></a>定義済みの FTP 操作  
 FTP タスクには、定義済みの操作のセットが含まれています。 次の表では、これらの操作について説明します。  
  
|操作|[説明]|  
|---------------|-----------------|  
|ファイルの送信|ローカル コンピューターのファイルを FTP サーバーに送信します。|  
|ファイルの受信|FTP サーバーのファイルをローカル コンピューターに保存します。|  
|ローカル ディレクトリの作成|ローカル コンピューター上にフォルダーを作成します。|  
|リモート ディレクトリの作成|FTP サーバー上にフォルダーを作成します。|  
|ローカル ディレクトリの削除|ローカル コンピューター上のフォルダーを削除します。|  
|リモート ディレクトリの削除|FTP サーバー上のフォルダーを削除します。|  
|ローカル ファイルの削除|ローカル コンピューターのファイルを削除します。|  
|リモート ファイルの削除|FTP サーバーのファイルを削除します。|  
  
## <a name="custom-log-entries-available-on-the-ftp-task"></a>FTP タスクで使用できるカスタム ログ エントリ  
 次の表は、FTP タスクのカスタム ログ エントリの一覧です。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**FTPConnectingToServer**|タスクで FTP サーバーへの接続が開始されたことを示します。|  
|**FTPOperation**|タスクで実行された FTP 操作の開始および種類を報告します。|  
  
## <a name="related-tasks"></a>Related Tasks  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 これらのプロパティを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定する方法の詳細については、「 [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)」を参照してください。  
  
 プログラムによってこれらのプロパティを設定する方法の詳細については、「 <xref:Microsoft.SqlServer.Dts.Tasks.FtpTask.FtpTask>」を参照してください。  
  
## <a name="ftp-task-editor-general-page"></a>[FTP タスク エディター] ([全般] ページ)
  **[FTP タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、タスクの通信先の FTP サーバーに接続する FTP 接続マネージャーを指定できます。 また、FTP タスクの名前と説明を入力することもできます。  
  
### <a name="options"></a>オプション  
 **[FtpConnection]**  
 既存の FTP 接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして接続マネージャーを作成します。  
  
> [!IMPORTANT]  
>  FTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
 **関連トピック:** [FTP 接続マネージャー](../../integration-services/connection-manager/ftp-connection-manager.md)、[FTP 接続マネージャー エディター](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
 **[StopOnFailure]**  
 FTP 操作が失敗した場合に FTP タスクを終了するかどうかを示します。  
  
 **[名前]**  
 FTP タスクの一意な名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 FTP タスクの説明を入力します。  
  
## <a name="ftp-task-editor-file-transfer-page"></a>[FTP タスク エディター] ([ファイル転送] ページ)
  **[FTP タスク エディター]** ダイアログ ボックスの **[ファイル転送]** ページを使用すると、タスクで実行される FTP 操作を構成できます。  
  
### <a name="options"></a>オプション  
 **[IsRemotePathVariable]**  
 リモート パスが変数に格納されているかどうかを表します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**True**|対象になるパスは変数に格納されます。 この値を選択すると、動的オプションの **[RemoteVariable]** が表示されます。|  
|**False**|対象になるパスは、ファイル接続マネージャーで指定されます。 この値を選択すると、動的オプションの **[RemotePath]** が表示されます。|  
  
 **[OverwriteFileAtDestination]**  
 転送先でファイルを上書きできるかどうかを指定します。  
  
 **[IsLocalPathVariable]**  
 ローカル パスが変数に格納されているかどうかを表します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**True**|対象になるパスは変数に格納されます。 この値を選択すると、動的オプションの **[LocalVariable]** が表示されます。|  
|**False**|対象になるパスは、ファイル接続マネージャーで指定されます。 この値を選択すると、動的オプションの **[LocalPath]** が表示されます。|  
  
 **操作**  
 実行する FTP 操作を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**ファイルの送信**|ファイルを送信します。 この値を選択すると、動的オプションの **[LocalVariable]** 、 **[LocalPathRemoteVariable]** 、 **[RemotePath]** が表示されます。|  
|**ファイルの受信**|ファイルを受信します。 この値を選択すると、動的オプションの **[LocalVariable]** 、 **[LocalPathRemoteVariable]** 、 **[RemotePath]** が表示されます。|  
|**ローカル ディレクトリの作成**|ローカル ディレクトリを作成します。 この値を選択すると、動的オプションの **[LocalVariable]** および **[LocalPath]** が表示されます。|  
|**リモート ディレクトリの作成**|リモート ディレクトリを作成します。 この値を選択すると、動的オプションの **[RemoteVariable]** および **[RemotePath]** が表示されます。|  
|**ローカル ディレクトリの削除**|ローカル ディレクトリを削除します。 この値を選択すると、動的オプションの **[LocalVariable]** および **[LocalPath]** が表示されます。|  
|**リモート ディレクトリの削除**|リモート ディレクトリを削除します。 この値を選択すると、動的オプションの **[RemoteVariable]** および **[RemotePath]** が表示されます。|  
|**ローカル ファイルの削除**|ローカル ファイルを削除します。 この値を選択すると、動的オプションの **[LocalVariable]** および **[LocalPath]** が表示されます。|  
|**リモート ファイルの削除**|リモート ファイルを削除します。 この値を選択すると、動的オプションの **[RemoteVariable]** および **[RemotePath]** が表示されます。|  
  
 **[IsTransferASCII]**  
 リモート FTP サーバーへ転送されるファイル、およびリモート FTP サーバーから転送されるファイルを ASCII モードで転送するかどうかを指定します。  
  
### <a name="isremotepathvariable-dynamic-options"></a>[IsRemotePathVariable] の動的オプション  
  
#### <a name="isremotepathvariable--true"></a>[IsRemotePathVariable] = [True]  
 **[RemoteVariable]**  
 既存のユーザー定義変数を選択するか、[\<**新しい変数...** >] をクリックしてユーザー定義変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、変数の追加  
  
#### <a name="isremotepathvariable--false"></a>[IsRemotePathVariable] = [False]  
 **[RemotePath]**  
 既存の FTP 接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして接続マネージャーを作成します。  
  
 **関連トピック:** [FTP 接続マネージャー](../../integration-services/connection-manager/ftp-connection-manager.md)、[FTP 接続マネージャー エディター](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
### <a name="islocalpathvariable-dynamic-options"></a>[IsLocalPathVariable] の動的オプション  
  
#### <a name="islocalpathvariable--true"></a>[IsLocalPathVariable] = [True]  
 **[LocalVariable]**  
 既存のユーザー定義変数を選択するか、[\<**新しい変数...** >] をクリックして変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、変数の追加  
  
#### <a name="islocalpathvariable--false"></a>[IsLocalPathVariable] = [False]  
 **[LocalPath]**  
 既存のファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして、接続マネージャーを作成します。  
  
 **関連トピック:** [フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
