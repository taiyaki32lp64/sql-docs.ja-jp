---
title: アップデートの Qlxml メソッド (int, java .sql. SQLXML) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5170751-fbe1-433b-96f5-4f237ba55f60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee90c33b2b546a3eaf48d52b7577200b7c23306b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998280"
---
# <a name="updatesqlxml-method-int-javasqlsqlxml"></a>updateSQLXML (int, java.sql.SQLXML) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列を java.sql.SQLXML 値で更新します  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateSQLXML(int columnIndex,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
 *xmlObject*  
  
 SQLXML オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 このアップデートの Qlxml メソッドは、java. ResultSet インターフェイスのアップデートの Qlxml メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [updateSQLXML メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
