---
title: prepareStatement メソッド (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c91b965498c0b617a02c7707e369a2ba61c0065
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976156"
---
# <a name="preparestatement-method-javalangstring"></a>prepareStatement (java.lang.String) メソッド

パラメーター化された SQL ステートメントをデータベースに送信するための [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) オブジェクトを作成します。

## <a name="syntax"></a>構文

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>パラメーター
*sql*

SQL ステートメントを含む**文字列**です。

## <a name="return-value"></a>戻り値
PreparedStatement オブジェクトです。

## <a name="exceptions"></a>例外  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Remarks
この指定されたステートメントメソッドは、java. .sql. 接続インターフェイスの "ドステートメント" メソッドによって指定されます。

## <a name="see-also"></a>参照

[prepareStatement メソッド &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[SQLServerConnection のメンバー](./sqlserverconnection-members.md)

[SQLServerConnection クラス](./sqlserverconnection-class.md)
