---
title: フィールド (ADO - WFC 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 583e6de7dc8c3ea05d61dda53c3e630d05e4d5f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918748"
---
# <a name="field-ado---wfc-syntax"></a>Field (ADO - WFC 構文)
## <a name="package-commswfcdata"></a>パッケージ com.ms.wfc.data  
  
### <a name="methods"></a>メソッド  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
public byte[] getByteChunk(int len)  
public char[] getCharChunk(int len)  
public String getStringChunk(int len)  
```  
  
### <a name="properties"></a>Properties  
  
```  
public int getActualSize()  
public int getAttributes()  
public void setAttributes(int pl)  
public com.ms.com.IUnknown getDataFormat()  
public void setDataFormat(com.ms.com.IUnknown format)  
```  
  
 (詳細については、com.ms.wfc.data.IDataFormat インターフェイスのドキュメントを参照してください)。  
  
```  
public int getDefinedSize()  
public void setDefinedSize(int pl)  
public String getName()  
public int getNumericScale()  
public void setNumericScale(byte pbNumericScale)  
public Variant getOriginalValue()  
public int getPrecision()  
public void setPrecision(byte pbPrecision)  
public int getType()  
public void setType(int pDataType)  
public Variant getUnderlyingValue()  
public Variant getValue()  
public void setValue(Variant value)  
public AdoProperties getProperties()  
```  
  
### <a name="field-accessor-methods"></a>フィールド アクセサー メソッド  
 [値](../../../ado/reference/ado-api/value-property-ado.md)のプロパティを[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクトを取得またはそのオブジェクトの内容を設定します。 コンテンツは、バリアントの値を割り当てることができるオブジェクトの型と任意のいくつかのデータ型として表されます。  
  
 ADO と WFC を実装して、**値**プロパティを**getValue** 、バリアント オブジェクトを返すメソッドと**setValue**メソッドを引数としてのバリアント。 バリアントは、Microsoft Visual Basic などの特定の言語で効率的です。  
  
 加え、**値**プロパティ、ADO と WFC 提供*アクセサー*メソッドを取得および設定のコンテンツ Java データ型を使用する**フィールド**オブジェクト。 これらのメソッドのほとんどは、フォームの名前を持つ**取得**_DataType_または**設定**_DataType_します。  
  
 2 つの注目すべき例外があります。1 つ、 **getObject**メソッドは、指定したクラスに強制型変換オブジェクトを返します。 ない**注意する必要**プロパティが代わりに、 **isNull**フィールドが null かどうかを示すブール値を返します。  
  
```  
public native boolean getBoolean();  
public void setBoolean(boolean v)  
public native byte getByte();  
public void setByte(byte v)  
public native byte[] getBytes();  
public void setBytes(byte[] v)  
public native double getDouble();  
public void setDouble(double v)  
public native float getFloat();  
public void setFloat(float v)  
public native int getInt();  
public void setInt(int v)  
public native long getLong();  
public void setLong(long v)  
public native short getShort();  
public void setShort(short v)  
public native String getString();  
public void setString(String v)  
public native boolean isNull();  
public void setNull()  
public Object getObject()  
public Object getObject(Class c)  
public void setObject(Object value)  
```  
  
## <a name="see-also"></a>関連項目  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)
