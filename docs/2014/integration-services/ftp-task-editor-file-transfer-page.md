---
title: FTP タスク エディター ([ファイル転送] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9386070902022e29ba191f24eb8fbfb10ed92b9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058434"
---
# <a name="ftp-task-editor-file-transfer-page"></a>[FTP タスク エディター] ([ファイル転送] ページ)
  **[FTP タスク エディター]** ダイアログ ボックスの **[ファイル転送]** ページを使用すると、タスクで実行される FTP 操作を構成できます。  
  
 このタスクの詳細については、「 [FTP タスク](control-flow/ftp-task.md)」を参照してください。  
  
## <a name="options"></a>および  
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
  
|ReplTest1|説明|  
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
  
## <a name="isremotepathvariable-dynamic-options"></a>[IsRemotePathVariable] の動的オプション  
  
### <a name="isremotepathvariable--true"></a>[IsRemotePathVariable] = [True]  
 **[RemoteVariable]**  
 既存のユーザー定義変数を選択するか、[\<**新しい変数...** >] をクリックしてユーザー定義変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、変数の追加  
  
### <a name="isremotepathvariable--false"></a>[IsRemotePathVariable] = [False]  
 **[RemotePath]**  
 既存の FTP 接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして接続マネージャーを作成します。  
  
 **関連トピック:** [FTP 接続マネージャー](connection-manager/ftp-connection-manager.md)、[FTP 接続マネージャー エディター](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
## <a name="islocalpathvariable-dynamic-options"></a>[IsLocalPathVariable] の動的オプション  
  
### <a name="islocalpathvariable--true"></a>[IsLocalPathVariable] = [True]  
 **[LocalVariable]**  
 既存のユーザー定義変数を選択するか、[\<**新しい変数...** >] をクリックして変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、変数の追加  
  
### <a name="islocalpathvariable--false"></a>[IsLocalPathVariable] = [False]  
 **[LocalPath]**  
 既存のファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして、接続マネージャーを作成します。  
  
 **関連トピック:** [フラット ファイル接続マネージャー](connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[FTP タスク エディター] ([全般] ページ)](general-page-of-integration-services-designers-options.md)   
 [[式] ページ](expressions/expressions-page.md)  
  
  
