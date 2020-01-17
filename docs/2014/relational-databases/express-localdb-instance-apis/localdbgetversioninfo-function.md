---
title: LocalDBGetVersionInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBGetVersionInfo
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4350badedcaf2a4e2b977b57cf9e6cfde6c1b275
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032230"
---
# <a name="localdbgetversioninfo-function"></a>LocalDBGetVersionInfo 関数
  指定した SQL Server Express LocalDB バージョンの情報を返します。たとえば、存在するかどうか、LocalDB 完全バージョン番号 (ビルド番号やリリース番号を含む) などです。  
  
 形式で、情報が返されます、`struct`という**LocalDBVersionInfo**、次の定義を持ちます。  
  
```  
typedef struct _LocalDBVersionInfo  
{  
      // Contains the size of the LocalDBVersionInfo struct  
      DWORD  cbLocalDBVersionInfoSize;  
  
      // Holds the version name  
      TLocalDBVersionwszVersion;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
} LocalDBVersionInfo;  
  
```  
  
 **ヘッダー ファイル:** sqlncli.h  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT LocalDBGetVersionInfo(  
           PCWSTR wszVersionName,           PLocalDBVersionInfo pVersionInfo,           DWORD dwVersionInfoSize);  
```  
  
## <a name="parameters"></a>パラメーター  
 *wszVersionName*  
 [入力] LocalDB バージョンの名前。  
  
 *pVersionInfo*  
 [出力] LocalDB バージョンについての情報を格納するバッファー。  
  
 *dwVersionInfoSize*  
 [入力]サイズを保持する、 *VersionInfo*バッファー。  
  
## <a name="returns"></a>戻り値  
 S_OK  
 関数が正常に実行されました。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB は、コンピューターにインストールされていません。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 指定した 1 つまたは複数の入力パラメーターが無効です。  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../express-localdb-error-messages/localdb-error-unknown-version.md)  
 指定された LocalDB バージョンが存在しません。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 予期しないエラーが発生しました。 詳細をイベント ログで確認してください。  
  
## <a name="details"></a>詳細  
 概要の背後にある"the rationale"、`struct`サイズ引数 (*lpVersionInfoSize*) を返す別のバージョンの API を有効にするのには、 **LocalDBVersionInfostruct**、効果的に上位および下位互換性を有効にします。  
  
 場合、`struct`サイズ引数 (*lpVersionInfoSize*) の既知のバージョンのサイズに合った、 **LocalDBVersionInfostruct**、そのバージョンの`struct`が返されます。 それ以外の場合、LOCALDB_ERROR_INVALID_PARAMETER が返されます。  
  
 典型的な例**LocalDBGetVersionInfo**次のような API の使用量。  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>コメント  
 LocalDB API を使用するコード サンプルは、次を参照してください。 [SQL Server Express LocalDB リファレンス](../sql-server-express-localdb-reference.md)します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Express LocalDB ヘッダーとバージョン情報](sql-server-express-localdb-header-and-version-information.md)  
  
  
