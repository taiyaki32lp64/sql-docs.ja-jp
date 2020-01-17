---
title: Size プロパティ (ADO Parameter) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3796f772dedb961ec34eb0639034350989f99142
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931054"
---
# <a name="size-property-ado-parameter"></a>Size プロパティ (ADO Parameter)
バイト数または文字で、最大サイズを示す、[パラメーター](../../../ado/reference/ado-api/parameter-object.md)オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**長い**バイトまたは内の値の文字の最大サイズを示す値を**パラメーター**オブジェクト。  
  
## <a name="remarks"></a>コメント  
 使用して、**サイズ**プロパティに書き込まれた値の最大サイズを決定したり読み取ったり、[値](../../../ado/reference/ado-api/value-property-ado.md)のプロパティを**パラメーター**オブジェクト。  
  
 可変長データ型を指定するかどうか、**パラメーター**オブジェクト (たとえば、いずれか**文字列**などの入力**adVarChar**)、オブジェクトを設定する必要があります**サイズ**プロパティに追加する前に、[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクションです。 それ以外の場合、エラーが発生します。  
  
 追加した場合、**パラメーター**オブジェクトを**パラメーター**のコレクションを[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトとする可変長データ型にその型を変更する必要があります設定、**パラメーター**オブジェクトの**サイズ**プロパティを実行する前に、**コマンド**オブジェクト。 それ以外の場合、エラーが発生します。  
  
 使用する場合、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)プロバイダーからパラメーター情報を取得するメソッドが 1 つまたは複数の可変長データ型を返します**パラメーター**オブジェクトの場合、ADO が基づくパラメーターのメモリを割り当てることができます潜在的なサイズの最大の実行中にエラーが発生する可能性があります。 エラーを防ぐためを明示的に設定する、**サイズ**コマンドを実行する前にこれらのパラメーター プロパティ。  
  
 **サイズ**読み取り/書き込みプロパティです。  
  
## <a name="applies-to"></a>適用対象  
 [Parameter オブジェクト](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>関連項目  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、サイズ、および方向プロパティの例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、サイズ、および方向プロパティの例 (vc++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、サイズ、および方向プロパティの例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size プロパティ (ADO Stream)](../../../ado/reference/ado-api/size-property-ado-stream.md)
