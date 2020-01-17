---
title: sp_OACreate (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OACreate
- sp_OACreate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OACreate
ms.assetid: eb84c0f1-26dd-48f9-9368-13ee4a30a27c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2ad8059466ac520b6f9f793af7670cbd73b96b38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107932"
---
# <a name="spoacreate-transact-sql"></a>sp_OACreate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OLE オブジェクトのインスタンスを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>引数  
 *progid*  
 作成する OLE オブジェクトのプログラム ID (ProgID) を指定します。 この文字の文字列は OLE オブジェクトのクラスをについて説明し、フォーム。 **'** _OLEComponent_ **.** _オブジェクト_ **'**  
  
 *OLEComponent* 、OLE オートメーション サーバーのコンポーネントの名前と*オブジェクト*OLE オブジェクトの名前を指定します。 指定した OLE オブジェクトが有効にする必要があり、サポートする必要があります、 **IDispatch**インターフェイス。  
  
 たとえば、SQLDMO です。Sql Server は、SQL-DMO の ProgID **SQLServer**オブジェクト。 SQL-DMO は SQLDMO のコンポーネント名、 **SQLServer**オブジェクトが、有効であり (すべての SQL-DMO のようなオブジェクト)、 **SQLServer**オブジェクト サポート**IDispatch**します。  
  
 *clsid*  
 作成する OLE オブジェクトのクラス ID (CLSID) を指定します。 この文字の文字列が OLE オブジェクトのクラスをについて説明し、フォーム: **' {** _nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn_ **}'** します。 指定した OLE オブジェクトが有効にする必要があり、サポートする必要があります、 **IDispatch**インターフェイス。  
  
 たとえば、{00026BA1-0000-0000-C000-000000000046} には、SQL-DMO の CLSID **SQLServer**オブジェクト。  
  
 _objecttoken_ **出力**  
 返されるオブジェクト トークンは、データ型のローカル変数にする必要があります**int**します。このオブジェクト トークンは、作成する OLE オブジェクトを識別するもので、その他の OLE オートメーション ストアド プロシージャの呼び出しに使用されます。  
  
 *context*  
 新しく作成した OLE オブジェクトを実行するときの実行条件を指定します。 指定する場合は、次のいずれかの値を指定する必要があります。  
  
 **1**プロセス (.dll) OLE サーバーのみを = です。  
  
 **4** = ローカル (.exe) OLE サーバーのみです。  
  
 **5** = インプロセスおよびローカル OLE サーバーが許可されています。  
  
 指定されていない場合、既定値は**5**します。 この値は、 *dwClsContext*への呼び出しのパラメーター **CoCreateInstance**します。  
  
 インプロセス OLE サーバーが許可されている場合 (のコンテキスト値を使用して**1**または**5**またはコンテキストの値を指定しない)、メモリへのアクセス権があるし、その他のリソースを所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 組み込み OLE サーバーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のメモリやリソースに損傷を与え、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアクセス違反など予期しない結果を招く場合があります。  
  
 コンテキストの値を指定すると**4**、ローカル OLE サーバーでは、いずれかにアクセスできない[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]リソース、およびそれが破損することはできません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メモリまたはリソースします。  
  
> [!NOTE]  
>  このストアド プロシージャのパラメーターは、名前ではなく位置で指定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0、失敗した場合は OLE オートメーション オブジェクトによって返される HRESULT の 0 以外の整数値を返します。  
  
 HRESULT のリターン コードの詳細については、次を参照してください。 [OLE オートメーションのリターン コードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)します。  
  
## <a name="remarks"></a>コメント  
 OLE オートメーション プロシージャが有効な場合に呼び出し**sp_OACreate** OLE オートメーションの共有実行環境が開始します。 OLE オートメーションを有効にする方法の詳細については、次を参照してください。 [Ole Automation Procedures サーバー構成オプション](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)します。  
  
 作成された OLE オブジェクトは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント バッチの最後に自動的に破棄されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**固定サーバー ロールまたはアクセス許可をこのストアド プロシージャを直接実行します。 `Ole Automation Procedures` 構成でなければなりません**有効になっている**OLE オートメーションに関連するすべてのシステム プロシージャを使用します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-progid"></a>A. ProgID を使用する  
 次の例は、SQL-DMO **SQLServer** ProgID を使用してオブジェクト。  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate 'SQLDMO.SQLServer', @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
### <a name="b-using-clsid"></a>B. CLSID を使用する  
 次の例は、SQL-DMO **SQLServer**の CLSID を使用してオブジェクト。  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate '{00026BA1-0000-0000-C000-000000000046}',  
    @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [OLE オートメーション ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ole Automation Procedures サーバー構成オプション](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
