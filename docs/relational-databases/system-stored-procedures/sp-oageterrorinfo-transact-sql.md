---
title: sp_OAGetErrorInfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
author: stevestein
ms.author: sstein
ms.openlocfilehash: e263308713a80ffaad4bfd9c484d061f5c19b94e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107914"
---
# <a name="spoageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OLE オートメーションのエラー情報を取得します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_OAGetErrorInfo [ objecttoken ]  
    [ , source OUTPUT ]   
    [ , description OUTPUT ]   
    [ , helpfile OUTPUT ]   
    [ , helpid OUTPUT ]   
```  
  
## <a name="arguments"></a>引数  
 *objecttoken*  
 使用して作成した OLE オブジェクトのオブジェクト トークン**sp_OACreate**または null を指定します。 場合*objecttoken*が指定すると、そのオブジェクトのエラー情報が返されます。 NULL を指定した場合は、そのバッチ全体のエラー情報が返されます。  
  
 _ソース_**出力**  
 エラー情報のソースです。 指定する場合、ローカルがする必要があります**char**、 **nchar**、 **varchar**、または**nvarchar**変数。 戻り値は必要に応じてローカル変数のサイズに切り捨てられます。  
  
 _説明_**出力**  
 エラーの説明です。 指定する場合、ローカルがする必要があります**char**、 **nchar**、 **varchar**、または**nvarchar**変数。 戻り値は必要に応じてローカル変数のサイズに切り捨てられます。  
  
 _helpfile_ **出力**  
 OLE オブジェクトのヘルプ ファイルです。 指定する場合、ローカルがする必要があります**char**、 **nchar**、 **varchar**、または**nvarchar**変数。 戻り値は必要に応じてローカル変数のサイズに切り捨てられます。  
  
 _helpid_ **出力**  
 ヘルプ ファイル コンテキスト ID です。 指定する場合、ローカルがする必要があります**int**変数。  
  
> [!NOTE]  
>  このストアド プロシージャのパラメーターは、名前ではなく位置で指定されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0、失敗した場合は OLE オートメーション オブジェクトによって返される HRESULT の 0 以外の整数値を返します。  
  
 HRESULT のリターン コードの詳細については、次を参照してください。 [OLE オートメーションのリターン コードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)します。  
  
## <a name="result-sets"></a>結果セット  
 出力パラメーターを指定しない場合、エラー情報は結果セットとしてクライアントに返されます。  
  
|列名|データ型|説明|  
|------------------|---------------|-----------------|  
|**Error**|**binary(4)**|エラー番号の 2 進表記。|  
|**Source**|**nvarchar(nn)**|エラーのソース。|  
|**[説明]**|**nvarchar(nn)**|エラーの説明。|  
|**Helpfile**|**nvarchar(nn)**|ソースのヘルプ ファイル。|  
|**HelpID**|**int**|ヘルプ ソース ファイルのヘルプ コンテキスト ID。|  
  
## <a name="remarks"></a>コメント  
 OLE オートメーションを呼び出すたびにストアド プロシージャ (を除く**sp_OAGetErrorInfo**) エラー情報をリセットします。 したがって、 **sp_OAGetErrorInfo**最新 OLE に関してのみ、エラー情報を取得します。オートメーション ストアド プロシージャの呼び出しです。 ため**sp_OAGetErrorInfo**エラー情報はリセットされません呼び出せる何度も同じエラー情報を取得します。  
  
 次の表は、OLE オートメーション エラーと一般的な原因の一覧です。  
  
|エラーおよび HRESULT|一般的な原因|  
|-----------------------|------------------|  
|**無効な変数型 (0x80020008)**|データ型、[!INCLUDE[tsql](../../includes/tsql-md.md)]メソッド パラメーターと一致しませんでしたとして渡される値、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]メソッド パラメーター、または NULL 値のデータ型は、メソッド パラメーターとして渡されました。|  
|**不明な名前 (です 0x8002006)**|指定したプロパティ名またはメソッド名が、指定したオブジェクトに見つかりませんでした。|  
|**無効なクラス文字列 (です 0x800401f3)**|指定した ProgID または CLSID は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに OLE オブジェクトとして登録されていません。 使用してインスタンスできます前に、カスタム OLE オートメーション サーバーを登録する必要があります**sp_OACreate**します。 これを行うプロセス (.dll) サーバーでは、Regsvr32.exe ユーティリティを使用して、または **/REGSERVER**コマンド ライン スイッチをローカル (.exe) サーバー。|  
|**サーバーの実行に失敗しました (0x80080005)**|指定した OLE オブジェクトは、ローカル OLE サーバー (.exe ファイル) として登録されていますが、.exe ファイルが見つからないか、起動できません。|  
|**指定されたモジュールは見つかりませんでした (0x8007007e)**|指定した OLE オブジェクトは、組み込み OLE サーバー (.dll ファイル) として登録されていますが、.dll ファイルが見つからないか、読み込むことができません。|  
|**型が一致しません (0x80020005)**|プロパティ値またはメソッドの戻り値を格納するために使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] ローカル変数のデータ型が、プロパティ値またはメソッドの戻り値の [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] データ型と一致しません。 または、プロパティやメソッドの戻り値を要求しましたが、そのプロパティやメソッドで戻り値が返されません。|  
|**sp_OACreate の 'context' パラメーターのデータ型または値が無効です。(0x8004275B)**|コンテキスト パラメーターの値には、いずれかを指定する必要があります。1、4、または 5 です。|  
  
 HRESULT のリターン コードの処理に関する詳細については、次を参照してください。 [OLE オートメーションのリターン コードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**固定サーバー ロールまたはアクセス許可をこのストアド プロシージャを直接実行します。 `Ole Automation Procedures` 構成でなければなりません**有効になっている**OLE オートメーションに関連するすべてのシステム プロシージャを使用します。  
  
## <a name="examples"></a>使用例  
 次の例では、OLE オートメーションのエラー情報を表示します。  
  
```  
DECLARE @output varchar(255);  
DECLARE @hr int;  
DECLARE @source varchar(255);  
DECLARE @description varchar(255);  
PRINT 'OLE Automation Error Information';  
EXEC @hr = sp_OAGetErrorInfo @object, @source OUT, @description OUT;  
IF @hr = 0  
BEGIN  
    SELECT @output = '  Source: ' + @source  
    PRINT @output  
    SELECT @output = '  Description: ' + @description  
    PRINT @output  
END  
ELSE  
BEGIN  
    PRINT '  sp_OAGetErrorInfo failed.'  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>参照  
 [OLE オートメーション ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
