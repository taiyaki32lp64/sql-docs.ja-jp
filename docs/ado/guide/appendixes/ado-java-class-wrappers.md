---
title: ADO Java クラス ラッパー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70486a27cfbe5c977d371906da89563059685093
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927006"
---
# <a name="ado-java-class-wrappers"></a>ADO Java クラス ラッパー
このコードは、ADO のインスタンスを宣言して[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)クラス ラッパーと、コードの同じ行でそれを初期化します。 さらに、それぞれの引数の変数を宣言、[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッド、特に[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)と[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (Java をサポートしていないため、列挙型型の場合)。 開きし、閉じます、 **Recordset**オブジェクト。 Java が使用されていないオブジェクトの体系的な断続的なリリースを実行するときに解放するには、その変数をスケジュールするだけで Rs1 を NULL に設定します。  
  
```java
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [Microsoft SDK for Java を使用する](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
