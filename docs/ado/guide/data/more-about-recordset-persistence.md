---
title: 詳細については、レコード セットの保持 |Microsoft Docs
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
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bee7d185d5f598a2f0a086bb7e3bea49ddfff88c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924911"
---
# <a name="more-about-recordset-persistence"></a>レコードセットの保持に関する詳細情報
ADO レコード セット オブジェクトのサポートの内容を格納する、**レコード セット**を使用してファイル内のオブジェクトその[保存](../../../ado/reference/ado-api/save-method.md)メソッド。 永続的に保存されたファイルがローカルに存在してドライブ、サーバー、またはサイトとして、Web 上の URL。 ファイルを復元して、いずれかで、後で、[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)のメソッド、 **Recordset**オブジェクトまたは[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)のメソッド、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
 さらに、 [GetString](../../../ado/reference/ado-api/getstring-method-ado.md)メソッドに変換を**レコード セット**を行と列が、指定した文字で区切られたはフォーム オブジェクト。  
  
 永続化する、 **Recordset**ファイルに格納できる形式に変換することから始めます。 **レコード セット**専用 adtg 高度なデータ TableGram (形式) 形式またはオープン拡張マークアップ言語 (XML) 形式でオブジェクトを格納できます。 Adtg 形式の例は、次のセクションに表示されます。 XML の永続化の詳細については、次を参照してください。 [XML 形式で保持するレコード](../../../ado/guide/data/persisting-records-in-xml-format.md)します。  
  
 保留中の変更を永続化されたファイルに保存します。 これを返すクエリを発行することができます、**レコード セット**オブジェクト、編集、**レコード セット**、し、保留中の変更を保存、復元後、**レコード セット**、し、保存されたデータ ソースが更新保留中の変更。  
  
 永続的に保存する方法について**Stream** 、オブジェクトを参照してください[ストリームと永続性](../../../ado/guide/data/streams-and-persistence.md)します。  
  
 例については**Recordset**永続化、XML レコード セットの永続化のシナリオを参照してください。  
  
## <a name="example"></a>例  
  
### <a name="save-a-recordset"></a>レコード セットを保存します。  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>Recordset.Open で永続化されたファイルを開きます。  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 必要に応じて場合、 **Recordset**はない、アクティブな接続がある、すべての既定値をそのまま使用し、次のコードします。  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Connection.Execute で永続化されたファイルを開きます。  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Rds. で永続化されたファイルを開くDataControl:  
 ここで、 **Server**プロパティは設定されません。  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>参照  
 [GetString メソッド (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Microsoft OLE DB の永続化プロバイダー (サービス プロバイダーの ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [ストリームと永続性](../../../ado/guide/data/streams-and-persistence.md)
