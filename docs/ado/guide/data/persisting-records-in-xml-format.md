---
title: XML 形式で保持するレコード |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 263f83093c46f4265559fe0b1844112687d4fc67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924591"
---
# <a name="persisting-records-in-xml-format"></a>レコードを XML 形式で保持する
Adtg 形式の形式のような**Recordset** XML 形式で永続化は、Microsoft OLE DB 永続化プロバイダーが実装されます。 このプロバイダーは、保存されている XML ファイルまたは ADO によって生成されるスキーマ情報を格納しているストリームから順方向専用、読み取り専用の行セットを生成します。 同様に、ADO をかかる**Recordset**、XML を生成し、ファイルまたは COM を実装する任意のオブジェクトに保存、 **IStream**インターフェイス。 (ファイルをサポートするオブジェクトのもう 1 つの例は、実際には、 **IStream**)。依存に XML を読み込むには Microsoft XML Parser (MSXML) バージョン 2.5 以降では、ADO、 **Recordset**; したがって行いますが必要です。  
  
> [!NOTE]
>  階層を保存するときにいくつかの制限が適用**レコード セット**(データ図形) を XML 形式にします。 場合、XML に保存することはできません、階層**レコード セット**保留中の更新プログラムが含まれています。 パラメーター化されたを保存することはできませんと階層**レコード セット**します。 詳細については、次を参照してください。[永続化、フィルター処理され、階層レコード セット](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)します。  
  
 XML にデータを保持し、再び読み込む最も簡単な方法は、もう一度 ADO では、**保存**と**オープン**メソッドでは、それぞれします。 ADO のコード例を次に示します内のデータの保存、**タイトル**titles.sav がという名前のファイルにテーブルです。  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 ADO には常に全体が引き続き発生する**Recordset**オブジェクト。 行のサブセットを保持するかどうか、 **Recordset**オブジェクトを使用して、**フィルター**行を限定または、選択句を変更する方法。 ただし、開く必要があります、 **Recordset**クライアント側カーソルを使用してオブジェクト (**CursorLocation** = **adUseClient**) を使用する、 **をフィルター処理**行のサブセットを保存するためのメソッド。 たとえば、文字"b"で始まるタイトルを取得することができますフィルターを適用する、オープンする**Recordset**オブジェクト。  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO が常に、クライアント カーソル エンジン行セットを使用して、スクロール可能、ブックマークを設定**Recordset**永続化プロバイダーによって生成された順方向専用のデータの上にオブジェクト。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [XML 保存形式](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [名前空間](../../../ado/guide/data/namespaces.md)  
  
-   [スキーマ セクション](../../../ado/guide/data/schema-section.md)  
  
-   [データ セクション](../../../ado/guide/data/data-section.md)  
  
-   [XML での階層レコードセット](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [XML でのレコードセットの動的プロパティ](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [XSLT 変換](../../../ado/guide/data/xslt-transformations.md)  
  
-   [XML DOM オブジェクトへの保存](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [XML のセキュリティに関する考慮事項](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [XML レコードセットの保持シナリオ](../../../ado/guide/data/xml-recordset-persistence-scenario.md)
