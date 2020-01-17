---
title: Parameters コレクション (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e062c67f0dedf55d63a076725b46d4405918741
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917702"
---
# <a name="parameters-collection-ado"></a>Parameters コレクション (ADO)
すべてが含まれています、[パラメーター](../../../ado/reference/ado-api/parameter-object.md)のオブジェクトを[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト。  
  
## <a name="remarks"></a>コメント  
 A**コマンド**オブジェクトには、**パラメーター**から成るコレクション**パラメーター**オブジェクト。  
  
 使用して、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)メソッドを**コマンド**オブジェクトの**パラメーター**コレクションは、ストアド プロシージャまたはパラメーター化されたクエリ プロバイダー パラメーター情報を取得します。指定されている、**コマンド**オブジェクト。 ストアド プロシージャの呼び出しまたはパラメーター化されたクエリの一部のプロバイダーをサポートしません。呼び出す、**更新**メソッドを**パラメーター**コレクションがこのようなプロバイダーを使用する場合はエラーを返します。  
  
 独自に定義するしていない場合**パラメーター**オブジェクトとしたアクセス、**パラメーター**コレクションを呼び出す前に、**更新**メソッド、ADO の呼び出しが自動的に、メソッドのコレクション。  
  
 呼び出すストアド プロシージャに関連付けられたまたはパラメーター化されたクエリ パラメーターのプロパティがわかっている場合は、パフォーマンスを向上させるために、プロバイダーに呼び出しを最小限に抑えることができます。 使用して、 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)メソッドを作成する**パラメーター**オブジェクトを使用して適切なプロパティの設定、 [Append](../../../ado/reference/ado-api/append-method-ado.md)メソッドに追加する、 **パラメーター**コレクション。 これにより設定およびパラメーターについては、プロバイダーに連絡しなくてもパラメーターの値を取得できます。 手動で設定する必要がある、パラメーター情報を提供しないプロバイダーを作成している場合、**パラメーター**このメソッドを使用して、すべてのパラメーターを使用することができるコレクションです。 使用して、[削除](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)を削除する**パラメーター**オブジェクトから、**パラメーター**コレクションのために必要な場合。  
  
 内のオブジェクト、**パラメーター**のコレクションを**レコード セット**(したがって利用できなくなる) のスコープ外に移動時に、**レコード セット**が閉じられました。  
  
 使用してストアド プロシージャを呼び出すときに**コマンド**、ストアド プロシージャの戻り値の出力パラメーターは次のように取得されます。  
  
1.  パラメーター、ストアド プロシージャを呼び出すことがあるないとき、**更新**メソッドを**パラメーター**コレクションを呼び出す前に呼び出す必要があります、 **Execute**メソッドを**コマンド**オブジェクト。  
  
2.  パラメーターとパラメーターを明示的に追加することをストアド プロシージャを呼び出すときに、**パラメーター**コレクション**追加**、戻り値の出力パラメーターが、に追加される**パラメーター**コレクション。 戻り値にまず追加する必要があります、**パラメーター**コレクション。 使用**Append**に他のパラメーターを追加する、**パラメーター**定義の順序のコレクション。 たとえば、ストアド プロシージャ SPWithParam では、2 つのパラメーターがあります。 最初のパラメーターでは、*で*、adVarChar (20) として定義されている入力パラメーターと 2 番目のパラメーターは、 *OutParam*adVarChar (20) として定義されている出力パラメーターです。 次のコードで戻り値の出力パラメーターを取得することができます。  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOutput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  パラメーターと呼び出すことによって、パラメーターの構成を使用してストアド プロシージャを呼び出すときに、**項目**メソッドを**パラメーター**コレクション、ストアド プロシージャの戻り値の出力パラメーターのことができます取得する、**パラメーター**コレクション。 たとえば、ストアド プロシージャ SPWithParam では、2 つのパラメーターがあります。 最初のパラメーターでは、*で*、adVarChar (20) として定義されている入力パラメーターと 2 番目のパラメーターは、 *OutParam*adVarChar (20) として定義されている出力パラメーターです。 次のコードで戻り値の出力パラメーターを取得することができます。  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Item("InParam").value = "hello world" ' input parameter  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of stored procedure  
    ' Access ccmd.parameters(2) or ccmd.parameters("OutParam") as the output parameter.  
    ```  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Parameters コレクションのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [Append メソッド (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter メソッド (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameter オブジェクト](../../../ado/reference/ado-api/parameter-object.md)
