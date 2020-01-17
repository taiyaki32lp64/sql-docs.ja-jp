---
title: getConnection (java.lang.String, java.lang.String) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87d3dfc2183bdc00261417a024507b41ea5fde28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952740"
---
# <a name="getconnection-method-javalangstring-javalangstring"></a>getConnection (java.lang.String, java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡されたユーザー名とパスワードを使用して、[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトが示すデータ ソースとの接続の確立を試みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *username*  
  
 ユーザー名を含む**文字列**です。  
  
 *password*  
  
 パスワードを含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 この getConnection メソッドは、javax.mail インターフェイスの getConnection メソッドによって指定されます。  
  
 Null 以外のユーザー名またはパスワードを使用して getConnection メソッドを呼び出すと、SQLServerConnection オブジェクトを初期化するときに、SQLServerDataSource クラスに設定されているユーザー名とパスワードのプロパティが置き換えられます。 たとえば、データ ソースに対して [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) と [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) を呼び出した後、getConnection を呼び出して null 以外のユーザー名またはパスワードを指定した場合、setUser と setPassword で設定したユーザー名とパスワードが getConnection に渡したユーザー名とパスワードに置き換えられます。  
  
> [!NOTE]  
>  この場合、[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) メソッドを呼び出して URL 内に設定したユーザー名とパスワードは変更されません。  
  
## <a name="see-also"></a>参照  
 [getConnection メソッド &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
