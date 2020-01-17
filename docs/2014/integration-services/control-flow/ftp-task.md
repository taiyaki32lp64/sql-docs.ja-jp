---
title: FTP タスク | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.f1
helpviewer_keywords:
- FTP task [Integration Services]
ms.assetid: 41c3f2c4-ee04-460a-9822-bb9ae4036c2e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fcc071c10a2daa31190727dfc9f3cbe617bdcb66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831540"
---
# <a name="ftp-task"></a>FTP タスク
  FTP タスクは、データ ファイルをダウンロードまたはアップロードし、サーバー上のディレクトリを管理します。 たとえば、パッケージは、リモート サーバーまたはインターネット サイトから、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ ワークフローの一部としてデータ ファイルをダウンロードできます。 FTP タスクは、次の目的で使用できます。  
  
-   データを移動し、変換をデータに適用する前または後で、あるディレクトリから別のディレクトリに、ディレクトリやデータ ファイルをコピーします。  
  
-   コピー元の FTP サイトにログインし、ファイルやパッケージをコピー先のディレクトリにコピーします。  
  
-   データをデータベースに読み込む前に、FTP サイトからファイルをダウンロードし、変換を列データに適用します。  
  
 実行時には、FTP タスクは FTP 接続マネージャーを使用してサーバーに接続します。 FTP 接続マネージャーは、FTP タスクとは別に構成され、FTP タスク内で参照されます。 FTP 接続マネージャーには、サーバーの設定、FTP サーバーへのアクセス資格情報、および、サーバーへの接続のタイムアウトや再試行回数などのオプションが含まれています。 詳細については、「 [FTP 接続マネージャー](../connection-manager/ftp-connection-manager.md)」を参照してください。  
  
> [!IMPORTANT]  
>  FTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
 ローカル ファイルまたはローカル ディレクトリにアクセスする場合、FTP タスクは、ファイル接続マネージャー、または変数に格納されたパス情報を使用します。 それに対し、リモート ファイルまたはリモート ディレクトリにアクセスする場合、FTP タスクは、FTP 接続マネージャーで直接指定されたリモート サーバーのパス、または変数に格納されたパス情報を使用します。 詳細については、「[ファイル接続マネージャー](../connection-manager/file-connection-manager.md)」および「[Integration Services (SSIS) の変数](../integration-services-ssis-variables.md)」を参照してください。  
  
 したがって、FTP タスクは複数のファイルを受信し、複数のリモート ファイルを削除できます。ただし、FTP タスクが接続マネージャーを使用している場合には、1 つのファイルのみを送信し、1 つのローカル ファイルのみを削除できます。ファイル接続マネージャーがアクセスできるのは 1 ファイルのみであるためです。 複数のローカル ファイルにアクセスするには、FTP タスクで変数を使用してパス情報を指定する必要があります。 たとえば、"C:\Test\\*.txt" を含む変数は、Test ディレクトリ内で .txt 拡張子を持つすべてのファイルの削除または送信をサポートするパスを提供します。  
  
 複数のファイルを送信したり、複数のローカル ファイルまたはディレクトリにアクセスするには、Foreach ループに FTP タスクを含めて、複数回実行する方法もあります。 Foreach ループは、For Each File 列挙子を使用して、ディレクトリ内のファイル全体を列挙します。 詳細については、「 [Foreach ループ コンテナー](foreach-loop-container.md)」を参照してください。  
  
 FTP タスクでは、パス内で *?* および *\** ワイルドカード文字がサポートされます。 これによってタスクは複数のファイルにアクセスできます。 ただし、ワイルドカードが使用できるのは、パスのファイル名を指定する部分のみです。 たとえば、C:\MyDirectory\\*.txt は有効なパスですが、C:\\\*\MyText.txt は無効なパスです。  
  
 操作に失敗した場合にファイル システムに関するタスクを停止したり、ファイルを ASCII モードで転送するように FTP 操作を構成できます。 ファイルのコピーを送受信する操作は、コピー先のファイルおよびディレクトリを上書きするように構成できます。  
  
## <a name="predefined-ftp-operations"></a>定義済みの FTP 操作  
 FTP タスクには、定義済みの操作のセットが含まれています。 次の表では、これらの操作について説明します。  
  
|操作|説明|  
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
 次の表は、FTP タスクのカスタム ログ エントリの一覧です。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`FTPConnectingToServer`|タスクで FTP サーバーへの接続が開始されたことを示します。|  
|`FTPOperation`|タスクで実行された FTP 操作の開始および種類を報告します。|  
  
## <a name="related-tasks"></a>Related Tasks  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 これらのプロパティを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定する方法の詳細については、「 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)」を参照してください。  
  
 プログラムによってこれらのプロパティを設定する方法の詳細については、「 <xref:Microsoft.SqlServer.Dts.Tasks.FtpTask.FtpTask>」を参照してください。  
  
## <a name="see-also"></a>参照  
 [[FTP タスク エディター] ([全般] ページ)](../general-page-of-integration-services-designers-options.md)   
 [FTP タスク エディター ([ファイル転送] ページ)](../ftp-task-editor-file-transfer-page.md)   
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
