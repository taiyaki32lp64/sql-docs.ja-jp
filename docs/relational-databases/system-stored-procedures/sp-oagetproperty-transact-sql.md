---
title: sp_OAGetProperty (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetProperty_TSQL
- sp_OAGetProperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetProperty
ms.assetid: 240eeeb9-6d8b-4930-b912-1d273ca0ab38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6efc0b620dcec300b5342ea5a0f63358fcdfadc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107880"
---
# <a name="sp_oagetproperty-transact-sql"></a>sp_OAGetProperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OLE オブジェクトのプロパティ値を取得します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_OAGetProperty objecttoken , propertyname   
    [ , propertyvalue OUTPUT ]  
    [ , index...]   
```  
  
## <a name="arguments"></a>引数  
 *objecttoken*  
 使用して作成した OLE オブジェクトのオブジェクト トークン**sp_OACreate**します。  
  
 *propertyname*  
 返される OLE オブジェクトのプロパティ名です。  
  
 *propertyvalue* **出力**  
 返されるプロパティ値です。 指定する場合は、適切なデータ型のローカル変数でなければなりません。  
  
 プロパティは OLE オブジェクトを返す場合*propertyvalue*データ型のローカル変数にする必要があります**int**します。オブジェクト トークンがローカル変数に格納され、このオブジェクト トークンを他の OLE オートメーション ストアド プロシージャで使用できます。  
  
 ローカル変数を指定するか、プロパティが 1 つの値を返す場合*propertyvalue*、ローカル変数の値または指定しないプロパティが返されます*propertyvalue*、返された、単一列、単一行の結果セットとしてクライアントにプロパティ値です。  
  
 場合に、プロパティが、配列を返す場合*propertyvalue*を指定すると、NULL に設定されます。  
  
 場合*propertyvalue*が指定されているが、プロパティは、値を返されないため、エラーが発生します。 プロパティが 3 次元以上の配列を返す場合は、エラーが発生します。  
  
 *index*  
 インデックス パラメーターです。 指定した場合*インデックス*適切なデータ型の値を指定する必要があります。  
  
 プロパティの一部はパラメーターを持っています。 このようなプロパティをインデックス付きプロパティ、パラメーターをインデックス パラメーターと呼びます。 1 つのプロパティが複数のインデックス パラメーターを持つことができます。  
  
> [!NOTE]  
>  このストアド プロシージャのパラメーターは、名前ではなく位置で指定されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0、失敗した場合は OLE オートメーション オブジェクトによって返される HRESULT の 0 以外の整数値を返します。  
  
 HRESULT のリターン コードの詳細については、次を参照してください。 [OLE オートメーションのリターン コードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)します。  
  
## <a name="result-sets"></a>結果セット  
 プロパティが 1 次元または 2 次元の配列を返す場合、配列は結果セットとしてクライアントに返されます。  
  
-   1 次元の配列の場合は、配列内の要素数と同数の列を持つ 1 行の結果セットとしてクライアントに返されます。 つまり、配列は列数として返されます。  
  
-   2 次元の配列の場合は、最初の次元の配列の要素数を列数とし、2 番目の次元の配列の要素数を行数とした結果セットとしてクライアントに返します。 つまり、配列を (列数,行数) として返します。  
  
 ときに、プロパティの戻り値またはメソッドの戻り値は、配列**sp_OAGetProperty**または**sp_OAMethod**クライアントに結果セットを返します。 メソッドの出力パラメーターを配列にすることはできません。これらのプロシージャは、配列内のすべてのデータ値をスキャンし、結果セットのそれぞれの列に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の適切なデータ型とデータ長を決定します。 これらのプロシージャは必要なデータ型とデータ長を使用して、特定の列内のすべてのデータ値を表現します。  
  
 列内のすべてのデータ値が同じデータ型を共有する場合は、そのデータ型を列全体で使用します。 1 列のデータ値がそれぞれ異なるデータ型である場合、列全体に適用されるデータ型は次の表を基に選択されます。  
  
||int|FLOAT|money|DATETIME|varchar|NVARCHAR|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>コメント  
 使用することも**sp_OAMethod**プロパティ値を取得します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**固定サーバー ロールまたはアクセス許可をこのストアド プロシージャを直接実行します。 `Ole Automation Procedures` 構成でなければなりません**有効になっている**OLE オートメーションに関連するすべてのシステム プロシージャを使用します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-a-local-variable"></a>A. ローカル変数を使用する  
 次の例では、取得、`HostName`プロパティ (の前に作成**SQLServer**オブジェクト)、ローカル変数に格納します。  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAGetProperty @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END  
PRINT @property;  
```  
  
### <a name="b-using-a-result-set"></a>B. 結果セットを使用する  
 次の例では、取得、`HostName`プロパティ (の前に作成**SQLServer**オブジェクト) をクライアントに結果セットとして返します。  
  
```  
EXEC @hr = sp_OAGetProperty @object, 'HostName';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>参照  
 [OLE オートメーション ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
