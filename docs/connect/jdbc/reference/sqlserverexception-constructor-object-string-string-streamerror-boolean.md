---
title: SQLServerException コンストラクター (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1cc42a09e455fa42d3f89b05903a22afc945424
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971125"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-streamerror-boolean"></a>SQLServerException コンストラクター (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **オブジェクト**、**文字列**オブジェクト、**文字列**オブジェクト、 **streamerror**オブジェクト、および**ブール値**が指定された場合に、 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)クラスの新しいインスタンスを初期化します。

## <a name="syntax"></a>構文  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            StreamError streamError,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>パラメーター  
 *obj*  
  
 例外を生成した IO バッファー。

 *errText*  
  
 エラーテキストを表す文字列です。
  
 *sqlState*  
  
 SQL 状態を格納している列挙オブジェクト。
 
 *streamError*  
  
 エラーの詳細を格納している StreamError オブジェクト。
 
 *bStack*  
  
 スタックトレースを生成する必要があるかどうかを示すブール値。
  
## <a name="see-also"></a>参照  
 [SQLServerException のコンストラクター](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException のメンバー](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException クラス](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
