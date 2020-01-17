---
title: LocalDBFormatMessage 関数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBFormatMessage
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d5aa59cdb3b1c59b78a0ef99fb7d375275d370e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091220"
---
# <a name="localdbformatmessage-function"></a>LocalDBFormatMessage 関数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  指定した SQL Server Express LocalDB エラーについてのローカライズされた説明テキストを返します。  
  
 **ヘッダー ファイル:** sqlncli.h  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT LocalDBFormatMessage(  
           HRESULT hrLocalDB,  
           DWORD dwFlags,   
           DWORD dwLanguageId,   
           LPWSTR wszMessage,   
           LPDWORD lpcchMessage   
);  
```  
  
## <a name="parameters"></a>パラメーター  
 *hrLocalDB*  
 [入力] LocalDB のエラー コード。  
  
 *dwFlags*  
 [入力] この関数の動作を指定するフラグ。  
  
 使用できるフラグ:  
  
 LOCALDB_TRUNCATE_ERR_MESSAGE  
 入力バッファーが短かすぎる場合、バッファーに合わせてエラー メッセージが切り捨てられます。  
  
 *dwLanguageId*  
 [入力] 目的の言語 (LANGID) または 0。0 の場合、Win32 FormatMessage 言語順序が使用されます。  
  
 *wszMessage*  
 [出力] LocalDB エラー メッセージを格納するバッファー。  
  
 *lpcchMessage*  
 [入力/出力]入力のサイズが含まれています、 *wszMessage*文字バッファー。 出力側では、所定のバッファー サイズが小さすぎる場合、末尾の NULL も含め、必要なバッファー サイズ (単位は文字数) を格納します。 関数を正常に実行できた場合、このメッセージ内の文字数を格納します。ただし、末尾の NULL は除外します。  
  
## <a name="returns"></a>戻り値  
 S_OK  
 関数が正常に実行されました。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB は、コンピューターにインストールされていません。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 指定した 1 つまたは複数の入力パラメーターが無効です。  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 要求されたメッセージは存在しません。  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 メッセージは、要求された言語では用意されていません。  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 入力バッファー *wszMessage*小さすぎる場合は、切り捨ては要求されません。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 予期しないエラーが発生しました。 詳細をイベント ログで確認してください。  
  
## <a name="remarks"></a>コメント  
 LocalDB API を使用するコード サンプルは、次を参照してください。 [SQL Server Express LocalDB リファレンス](../../relational-databases/sql-server-express-localdb-reference.md)します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Express LocalDB ヘッダーとバージョン情報](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
