---
title: SQLServerParameterMetaData Members |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f9ebb203-2013-4feb-94f5-494b7f098f9a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 82e005a4e81dd08643613f0c90dafbd9124dd3bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970874"
---
# <a name="sqlserverparametermetadata-members"></a>SQLServerParameterMetaData のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表では、[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) クラスによって公開されるメンバーを示します。  
  
## <a name="constructors"></a>コンストラクター  
 [なし] :  
  
## <a name="fields"></a>フィールド  
 [なし] :  
  
## <a name="inherited-fields"></a>継承されたフィールド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|java.sql.ParameterMetaData|parameterModeIn、parameterModeInOut、parameterModeOut、parameterModeUnknown、parameterNoNulls、parameterNullable、parameterNullableUnknown|  
  
## <a name="methods"></a>メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[getParameterClassName](../../../connect/jdbc/reference/getparameterclassname-method-sqlserverparametermetadata.md)|[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスの [setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) メソッドにインスタンスを渡す必要のある、Java クラスの完全修飾名を取得します。|  
|[getParameterCount](../../../connect/jdbc/reference/getparametercount-method-sqlserverparametermetadata.md)|[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) オブジェクトに情報が含まれる [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) オブジェクトのパラメーター数を取得します。|  
|[getParameterMode](../../../connect/jdbc/reference/getparametermode-method-sqlserverparametermetadata.md)|指定されたパラメーターのモードを取得します。|  
|[getParameterType](../../../connect/jdbc/reference/getparametertype-method-sqlserverparametermetadata.md)|指定されたパラメーターの SQL 型を取得します。|  
|[getParameterTypeName](../../../connect/jdbc/reference/getparametertypename-method-sqlserverparametermetadata.md)|指定されたパラメーターのデータベース固有の型名を取得します。|  
|[getPrecision](../../../connect/jdbc/reference/getprecision-method-sqlserverparametermetadata.md)|指定されたパラメーターの 10 進の桁数を取得します。|  
|[getScale](../../../connect/jdbc/reference/getscale-method-sqlserverparametermetadata.md)|指定されたパラメーターの小数点以下の桁数を取得します。|  
|[isNullable](../../../connect/jdbc/reference/isnullable-method-sqlserverparametermetadata.md)|指定されたパラメーターで null 値が許可されるかどうかを取得します。|  
|[isSigned](../../../connect/jdbc/reference/issigned-method-sqlserverparametermetadata.md)|指定されたパラメーターの値が符号付き数値かどうかを取得します。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>参照  
 [SQLServerParameterMetaData クラス](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
