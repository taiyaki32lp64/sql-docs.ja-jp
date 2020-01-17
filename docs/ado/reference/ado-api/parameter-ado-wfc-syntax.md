---
title: パラメーター (ADO - WFC 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22f9d928cf008396346067a3e166fa281be4093d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931716"
---
# <a name="parameter-ado---wfc-syntax"></a>Parameter (ADO - WFC 構文)
## <a name="package-commswfcdata"></a>パッケージ com.ms.wfc.data  
  
### <a name="constructor"></a>コンストラクター  
  
```  
public Parameter()  
public Parameter(String name)  
public Parameter(String name, int type)  
public Parameter(String name, int type, int dir)  
public Parameter(String name, int type, int dir, int size)  
public Parameter(String name, int type, int dir, int size, Object value)  
```  
  
### <a name="methods"></a>メソッド  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
```  
  
### <a name="properties"></a>Properties  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getDirection()  
public void setDirection(int dir)  
public String getName()  
public void setName(String name)  
public int getNumericScale()  
public void setNumericScale(int scale)  
public int getPrecision()  
public void setPrecision(int prec)  
public int getSize()  
public void setSize(int size)  
public int getType()  
public void setType(int type)  
public com.ms.com.Variant getValue()  
public void setValue(Object v)  
public AdoProperties getProperties()  
```  
  
## <a name="parameter-accessor-methods"></a>パラメーターのアクセサー メソッド  
 [値](../../../ado/reference/ado-api/value-property-ado.md)のプロパティを[パラメーター](../../../ado/reference/ado-api/parameter-object.md)オブジェクトを取得またはそのオブジェクトの内容を設定します。 コンテンツは、バリアントの値を割り当てることができるオブジェクトの型と任意のいくつかのデータ型として表されます。  
  
 ADO と WFC を実装して、**値**プロパティを**getValue** 、バリアント オブジェクトを返すメソッドと**setValue**メソッドを引数としてのバリアント。 バリアントは、Microsoft Visual Basic などの特定の言語で効率的です。  
  
 加え、**値**プロパティ、ADO と WFC 提供*アクセサー*メソッドを取得および設定のコンテンツ Java データ型を使用する**パラメーター**オブジェクト。 これらのメソッドのほとんどは、フォームの名前を持つ**取得**_DataType_または**設定**_DataType_します。  
  
 1 つの注目すべき例外があります。ない**注意する必要**プロパティが代わりに、 **isNull**フィールドが null かどうかを示すブール値を返します。  
  
```  
public boolean getBoolean()  
public void setBoolean(boolean v)  
public byte getByte()  
public void setByte(byte v)  
public double getDouble()  
public void setDouble(double v)  
public float getFloat()  
public void setFloat(float v)  
public int getInt()  
public void setInt(int v)  
public long getLong()  
public void setLong(long v)  
public short getShort()  
public void setShort(short v)  
public String getString()  
public void setString(String v)  
public boolean isNull()  
public void setNull()  
```  
  
## <a name="see-also"></a>関連項目  
 [Parameter オブジェクト](../../../ado/reference/ado-api/parameter-object.md)
