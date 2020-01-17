---
title: getSendStringParametersAsUnicode メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df27a5368dfea7f417fb84e2ebe38a8987165aec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979968"
---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>getSendStringParametersAsUnicode メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  サーバーへの文字列パラメーターの UNICODE 形式による送信が有効になっているかどうかを示す **boolean** 値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>戻り値  
 サーバーに文字列パラメーターが UNICODE 形式で送信される場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>Remarks  
 sendStringParametersAsUnicode プロパティが **true** (既定値) に設定されている場合、文字列パラメーターは、UNICODE 形式でサーバーに送信されます。 sendStringParametersAsUnicode が **false** に設定されている場合、UNICODE ではなく ASCII/MBCS 形式で、文字列パラメーターがサーバーに送信されます。 sendStringParametersAsUnicode が設定されていない場合、getSendStringParametersAsUnicode は既定値の **true** を返します。  
  
 sendStringParametersAsUnicode 接続プロパティについて詳しくは、「[接続プロパティの設定](../../../connect/jdbc/setting-the-connection-properties.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
