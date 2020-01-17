---
title: SQLServerNClob Members |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 303742b8e7b7bf8221565e09cf23d2e18cdca8de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970946"
---
# <a name="sqlservernclob-members"></a>SQLServerNClob のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表は、[SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md) クラスによって公開されるメンバーを示しています。  
  
## <a name="constructors"></a>コンストラクター  
 [なし] :  
  
## <a name="fields"></a>フィールド  
 [なし] :  
  
## <a name="inherited-fields"></a>継承されたフィールド  
 [なし] :  
  
## <a name="methods"></a>メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|このメソッドは、**NCLOB** オブジェクトと、それが占有していたリソースを解放します。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|**NCLOB**オブジェクトによって指定された**NCLOB**値を ASCII ストリームとして取得します。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|**NCLOB**オブジェクトによって指定された**NCLOB**値を取得します。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|**NCLOB**オブジェクトによって指定された**NCLOB**値内の指定した部分文字列のコピーを取得します。|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|**NCLOB**オブジェクトによって指定された**NCLOB**値の文字数を取得します。|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|指定された開始位置に基づいて、指定された **java.sql.NClob** オブジェクトまたは **java.sql.NClob** の substring の文字位置を取得します。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|この **java.sql.NClob** オブジェクトが表す **NCLOB** 値の指定された位置から ASCII 文字を書き込むために使用するストリームを取得します。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|この **java.sql.NClob** オブジェクトが表す **NCLOB** 値の指定された位置から Unicode 文字のストリームを書き込むために使用するストリームを取得します。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|指定した**文字列**を**NCLOB**の指定した位置から書き込みます。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|**NCLOB** 値を指定された長さに切り捨てます。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|--------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Clob|free、getAsciiStream、getCharacterStream、getSubString、length、position、setAsciiStream、setCharacterStream、setString、truncate|  
  
## <a name="see-also"></a>参照  
 [SQLServerClob クラス](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
