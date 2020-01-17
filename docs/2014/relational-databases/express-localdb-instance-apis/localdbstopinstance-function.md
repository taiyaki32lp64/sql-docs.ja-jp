---
title: LocalDBStopInstance 関数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBStopInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 4bd73187-0aac-4f03-ac54-2b78e41917e5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6f28abbf9871d5f4e512e9c9ee0cfb5c7ad9db59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63135273"
---
# <a name="localdbstopinstance-function"></a>LocalDBStopInstance 関数
  指定した SQL Server Express LocalDB インスタンスの実行を停止します。  
  
 **ヘッダー ファイル:** sqlncli.h  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT LocalDBStopInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           ULONG ulTimeout   
);  
```  
  
## <a name="parameters"></a>パラメーター  
 *pInstanceName*  
 [入力] 停止する LocalDB インスタンスの名前。  
  
 *dwFlags*  
 [入力] インスタンスを停止する方法を指定する 1 つのフラグ値または複数フラグ値の組み合わせ。  
  
 使用できるフラグ:  
  
 LOCALDB_SHUTDOWN_KILL_PROCESS  
 オペレーティング システム コマンド kill process を使用して、すぐにシャットダウンします。  
  
 LOCALDB_SHUTDOWN_WITH_NOWAIT  
 WITH NOWAIT オプション Transact-SQL コマンドを使用して、シャットダウンします。  
  
 どのフラグも設定しない場合、LocalDB インスタンスは SHUTDOWN Transact-SQL コマンドを使用してシャットダウンされます。 両方のフラグを設定した場合、LOCALDB_SHUTDOWN_KILL_PROCESS フラグが優先されます。  
  
 *ulTimeout*  
 [入力] この操作の完了を待機する秒単位の時間。 この値が 0 の場合、この関数は LocalDB インスタンスの停止を待たずにすぐに値を返します。  
  
## <a name="returns"></a>戻り値  
 S_OK  
 関数が正常に実行されました。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB は、コンピューターにインストールされていません。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 指定した 1 つまたは複数の入力パラメーターが無効です。  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 指定したインスタンス名は無効です。  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../express-localdb-error-messages/localdb-error-unknown-instance.md)  
 インスタンスは存在しません。  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../express-localdb-error-messages/localdb-error-wait-timeout.md)  
 同期ロックを取得中にタイムアウトが発生しました。  
  
 [LOCALDB_ERROR_INSTANCE_STOP_FAILED](../express-localdb-error-messages/localdb-error-instance-stop-failed.md)  
 停止操作は、指定された時間内に完了できませんでした。  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 インスタンスを格納するパスの長さが MAX_PATH を超過しています。  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 ユーザー プロファイル フォルダーを取得できません。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 インスタンス フォルダーにアクセスできません。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 インスタンス レジストリにアクセスできません。  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 インスタンス構成が破損しています。  
  
 [LOCALDB_ERROR_CALLER_IS_NOT_OWNER](../express-localdb-error-messages/localdb-error-caller-is-not-owner.md)  
 API の呼び出し元は、LocalDB インスタンスの所有者ではありません。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 予期しないエラーが発生しました。 詳細をイベント ログで確認してください。  
  
## <a name="remarks"></a>コメント  
 LocalDB API を使用するコード サンプルは、次を参照してください。 [SQL Server Express LocalDB リファレンス](../sql-server-express-localdb-reference.md)します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Express LocalDB ヘッダーとバージョン情報](sql-server-express-localdb-header-and-version-information.md)  
  
  
