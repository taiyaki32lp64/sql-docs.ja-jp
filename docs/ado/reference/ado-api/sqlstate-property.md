---
title: SQLState プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e43ace17f3f2b709c327f185a189a107b6b73065
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916884"
---
# <a name="sqlstate-property"></a>SQLState プロパティ
SQL 状態を示す、指定された[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 5 文字を返します**文字列**を ANSI SQL 標準に準拠し、エラー コードを示す値。  
  
## <a name="remarks"></a>コメント  
 使用して、 **SQLState**プロパティ プロバイダーを返す SQL ステートメントの処理中にエラーが発生したときに 5 文字のエラー コードを読み取る。 たとえば、ODBC 用の Microsoft OLE DB プロバイダーを使用して、Microsoft SQL Server データベースと、ときに SQL 状態のエラー コードは ODBC、ODBC に固有のエラーまたは、Microsoft SQL Server から ODBC にマップし、エラーのいずれかに基づくから送信されます。エラー。 これらのエラー コードは、ANSI SQL 標準に記載されていますが、さまざまなデータ ソースによって異なる方法で実装される場合があります。  
  
## <a name="applies-to"></a>適用対象  
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>参照  
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (vc++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
