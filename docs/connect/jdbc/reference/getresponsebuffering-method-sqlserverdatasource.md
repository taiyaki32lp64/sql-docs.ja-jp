---
title: getResponseBuffering メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getResponseBuffering()
apilocation:
- SQLServerDataSource.getResponseBuffering()
apitype: Assembly
ms.assetid: 19585a93-88a4-415e-a20e-12ba58cddeaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4b3e53579b8c95cce0585e9614152053f39cafa8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980435"
---
# <a name="getresponsebuffering-method-sqlserverdatasource"></a>getResponseBuffering メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトの応答バッファリング モードが返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>戻り値  
 小文字の**完全**または**アダプティブ**を含む**文字列**。  
  
## <a name="remarks"></a>Remarks  
 **full** 値は、実行時にサーバーから結果全体を読み取ることを示します。  
  
 **adaptive** 値は、必要に応じて最小限のデータをバッファリングすることを示します。 既定のバッファリング モードは **adaptive** 値です。  
  
 応答バッファリングモードの使用方法の詳細については、「[アダプティブバッファリングの使用](../../../connect/jdbc/using-adaptive-buffering.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [setResponseBuffering メソッド &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
