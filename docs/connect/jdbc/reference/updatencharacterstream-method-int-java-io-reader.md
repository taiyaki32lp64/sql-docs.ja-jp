---
title: updateNCharacterStream (int, java.io.Reader) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fc746413-bdbf-4109-aee0-385a1270c847
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ce089832227a9f44cd1adfd0a4682b53002a2fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998718"
---
# <a name="updatencharacterstream-method-int-javaioreader"></a>updateNCharacterStream (int, java.io.Reader) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列を文字ストリームの値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateNCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
 *x*  
  
 リーダーオブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この Updaten; Stream メソッドは、java. ResultSet インターフェイスの Updatenキャラクターストリームメソッドによって指定されます。  
  
 このメソッドは、リーダーオブジェクトから選択した**nchar**、 **nvarchar (max)** 、 **ntext** 、および**xml**列に Unicode 文字を渡します。 このメソッドを他のデータ型の列で使用すると、例外がスローされます。  
  
## <a name="see-also"></a>参照  
 [updateNCharacterStream メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
