---
title: 手順 5:DataControl が使用可能に (RDS チュートリアル) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1202a25c603b5dd4f9a824b031b5af91f5940052
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922058"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>手順 5:DataControl が使用可能になる (RDS チュートリアル)
返された**レコード セット**オブジェクトは、使用するために使用します。 確認、移動、またはその他のように編集**Recordset**します。 行うことができます、 **Recordset**環境によって異なります。 Visual Basic および Visual C を使用できるビジュアル コントロールがある、**レコード セット**直接的または間接的に有効にすると、データ コントロールの aid を使用します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 たとえば、Microsoft Internet Explorer で Web ページを表示する場合があります表示する、 **Recordset** visual コントロール内のデータをオブジェクトします。 Web ページ上のビジュアルのコントロールにアクセスできません、 **Recordset**オブジェクトに直接します。 ただし、アクセスできる、 **Recordset**オブジェクト、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)します。 **Rds.DataControl**ビジュアルで使用可能になりますが制御その[SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)プロパティに設定されて、 **Recordset**オブジェクト。  
  
 コントロールのビジュアル オブジェクトにはその**DATASRC**パラメーターに設定、 **rds.DataControl**、およびその**DATAFLD**プロパティに設定、**レコード セット**オブジェクト フィールド (列)。  
  
 このチュートリアルでは、設定、 **SourceRecordset**プロパティ。  
  
```vb
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>関連項目  
 [手順 6:変更 (RDS チュートリアル) サーバーに送信されます。](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS のチュートリアル (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
