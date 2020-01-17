---
title: オブジェクト階層構文 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], hierarchy syntax
ms.assetid: 7ed8df86-9fd2-4e09-96bc-5381fec85f65
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3405621d604e6450756520f6d93b66a51d4d66c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941984"
---
# <a name="object-hierarchy-syntax-transact-sql"></a>オブジェクト階層構文 (Transac-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  *Propertyname* sp_OAGetProperty および sp_OASetProperty のパラメーターと*methodname* sp_OAMethod のパラメーターの次のようなオブジェクト階層構文をサポートして[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. この特殊な構文を使用する場合、パラメーターの一般的な形式は次のようになります。  
  
## <a name="syntax"></a>構文  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>引数  
 *TraversedObject*  
 OLE オブジェクトの下の階層で、 *objecttoken*ストアド プロシージャで指定します。 一連のコレクション、オブジェクト プロパティ、およびオブジェクトを返すメソッドを指定するには、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 構文を使用します。 一連のオブジェクト指定子内で、各オブジェクトはピリオド (.) で区切る必要があります。  
  
 一連の指定子の項目には、コレクション名を指定できます。 コレクションを指定するには、次の構文を使用します。  
  
 コレクション ("*項目*")  
  
 二重引用符 (") が必要です。 コレクションに [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 感嘆符 (!) 構文を使用することはできません。  
  
 *PropertyOrMethod*  
 メソッドまたはプロパティの名前には、 *TraversedObject*します。  
  
 sp_OAGetProperty、sp_OASetProperty、または sp_OAMethod パラメーター (sp_OAMethod 出力パラメーターのサポートを含む) を使用して、すべてのインデックスまたはメソッド パラメーターを指定するには、次の構文を使用します。  
  
 *PropertyOrMethod*  
  
 すべてのインデックスまたはメソッド パラメーターをかっこで囲んで指定するには、次の構文を使用します。この場合、sp_OAGetProperty、sp_OASetProperty、または sp_OAMethod のすべてのインデックスまたはメソッド パラメーターは無視されます。  
  
 *PropertyOrMethod*([ *ParameterName*: =]"*パラメーター*"[,...])  
  
 二重引用符 (") が必要です。 すべての名前付きのパラメーターは、位置で決まるパラメーターをすべて指定した後で指定する必要があります。  
  
## <a name="remarks"></a>コメント  
 場合*TraversedObject*が指定されていない*PropertyOrMethod*が必要です。  
  
 場合*PropertyOrMethod*が指定されていない、 *TraversedObject* OLE オートメーション ストアド プロシージャからオブジェクト トークン出力パラメーターとして返されます。 場合*PropertyOrMethod*が指定されているプロパティまたはメソッドの*TraversedObject*が呼び出され、OLE オートメーションから、プロパティ値またはメソッドの戻り値は出力パラメーターとして返されますが、ストアド プロシージャです。  
  
 いずれかの項目の場合、 *TraversedObject*一覧が OLE オブジェクトを返さない、エラーが発生します。  
  
 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] OLE オブジェクト構文の詳細については、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] のマニュアルを参照してください。  
  
 HRESULT のリターン コードの詳細については、次を参照してください。 [sp_OACreate &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)します。  
  
## <a name="examples"></a>使用例  
 SQL-DMO SQLServer オブジェクトを使用するオブジェクト階層構文の例を次に示します。  
  
```  
-- Get the AdventureWorks2012 Person.Address Table object.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address")',  
   @table OUT  
  
-- Get the Rows property of the AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").Rows',  
   @rows OUT  
  
-- Call the CheckTable method to validate the   
-- AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAMethod @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").CheckTable',  
   @checkoutput OUT  
```  
  
## <a name="see-also"></a>参照  
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [OLE オートメーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
