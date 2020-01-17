---
title: XML データの取得および XML データに対するクエリの実行 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML data [SQL Server], retrieving
- XML instance retrieval
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f556bfccdd117b23db36bb9551e885f4c38614e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241203"
---
# <a name="retrieve-and-query-xml-data"></a>XML データの取得および XML データに対するクエリの実行
  このトピックでは、XML データのクエリを実行するために指定する必要があるクエリ オプションについて説明します。 また、XML インスタンスをデータベースに格納するときに保持されない部分についても説明します。  
  
##  <a name="features"></a> 保持されない XML インスタンスの機能  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、XML インスタンスの内容は保持されますが、XML データ モデルで重要と見なされない側面は保持されません。 つまり、取得した XML インスタンスは、サーバーに格納されたインスタンスと同一とは限りませんが、含まれている情報は同じです。  
  
### <a name="xml-declaration"></a>XML 宣言  
 インスタンスをデータベースに格納する場合は、そのインスタンスの XML 宣言は保持されません。 例 :  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 結果は `<doc/>`です。  
  
 `<?xml version='1.0'?>` などの XML 宣言は、XML データを `xml` データ型インスタンスに格納するときに保持されません。 これは仕様です。 XML 宣言 () とその属性 (バージョン/エンコード/スタンドアロン) が失われるデータは、型に変換されます`xml`します。 XML 宣言は、XML パーサーが使用するディレクティブとして扱われます。 XML データは、ucs-2 として内部的に保存されます。 XML インスタンスのその他すべての PI は保持されます。  
  
  
### <a name="order-of-attributes"></a>属性の順序  
 XML インスタンス内の属性の順序は保持されません。 `xml` 型の列に格納されている XML インスタンスにクエリを実行する場合、結果の XML の属性の順序は元の XML インスタンスとは異なる場合があります。  
  
  
### <a name="quotation-marks-around-attribute-values"></a>属性値を囲む引用符  
 属性を囲む単一引用符および二重引用符は、保持されません。 属性値は、名前と値の組としてデータベースに格納されます。 引用符は格納されません。 XML インスタンスに対して XQuery を実行すると、結果の XML はシリアル化され、属性が二重引用符で囲まれます。  
  
```  
DECLARE @x xml  
-- Use double quotation marks.  
SET @x = '<root a="1" />'  
SELECT @x  
GO  
DECLARE @x xml  
-- Use single quotation marks.  
SET @x = '<root a=''1'' />'  
SELECT @x  
GO  
```  
  
 どちらのクエリからも、 `<root a="1" />`が返されます。  
  
  
### <a name="namespace-prefixes"></a>名前空間プレフィックス  
 名前空間プレフィックスは保持されません。 `xml` 型の列に対して XQuery を指定した場合、結果のシリアル化された XML は、異なる名前空間プレフィックスを返す可能性があります。  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 結果の名前空間プレフィックスは、異なる可能性があります。 例 :  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
  
##  <a name="query"></a> 必要なクエリ オプションの設定  
 クエリを実行するときに`xml`型の列または変数を使用して`xml`示すように、データ型のメソッドを次のオプションを設定する必要があります。  
  
|SET オプション|設定する値|  
|-----------------|---------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNINGS|ON|  
|ARITHABORT|ON|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
  
 ように、クエリと変更のオプションが設定されていない場合`xml`データ型のメソッドは失敗します。  
  
  
## <a name="see-also"></a>参照  
 [XML データのインスタンスの作成](create-instances-of-xml-data.md)  
  
  
