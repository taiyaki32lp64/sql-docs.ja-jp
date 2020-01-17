---
title: LocalDBShareInstance 関数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBShareInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 21eb3b9a-7d32-455b-89bb-f624198cd202
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 63407b3bf1a2860ad3f8c35b5cd8ecc4a4b125c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032335"
---
# <a name="localdbshareinstance-function"></a>LocalDBShareInstance 関数
  指定した共有名を使用して、指定した SQL Server Express LocalDB インスタンスをコンピューターの他のユーザーと共有します。  
  
 **ヘッダー ファイル:** sqlncli.h  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT LocalDBShareInstance(  
           PSID pOwnerSID,  
           PCWSTR pInstancePrivateName,  
           PCWSTR pInstanceSharedName,   
           DWORD dwFlags   
);  
```  
  
## <a name="parameters"></a>パラメーター  
 *pOwnerSID*  
 [入力] インスタンスの所有者の SID。  
  
 *pInstancePrivateName*  
 [入力] 共有する LocalDB インスタンスのプライベート名。  
  
 *pInstanceSharedName*  
 [入力] 共有する LocalDB インスタンスの共有名。  
  
 *dwFlags*  
 [入力] 将来の使用のために予約されています。 現時点では、0 に設定する必要があります。  
  
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
 指定したインスタンスは存在しません。  
  
 [LOCALDB_ERROR_ADMIN_RIGHTS_REQUIRED](../express-localdb-error-messages/localdb-error-admin-rights-required.md)  
 この操作を実行するためには、管理者権限が必要です。  
  
 [LOCALDB_ERROR_SHARED_NAME_TAKEN](../express-localdb-error-messages/localdb-error-shared-name-taken.md)  
 指定した共有名は既に使用されています。  
  
 [LOCALDB_ERROR_INSTANCE_ALREADY_SHARED](../express-localdb-error-messages/localdb-error-instance-already-shared.md)  
 指定したインスタンスは既に共有されています。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 予期しないエラーが発生しました。 詳細をイベント ログで確認してください。  
  
## <a name="remarks"></a>コメント  
 LocalDB API を使用するコード サンプルは、次を参照してください。 [SQL Server Express LocalDB リファレンス](../sql-server-express-localdb-reference.md)します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Express LocalDB ヘッダーとバージョン情報](sql-server-express-localdb-header-and-version-information.md)  
  
  
