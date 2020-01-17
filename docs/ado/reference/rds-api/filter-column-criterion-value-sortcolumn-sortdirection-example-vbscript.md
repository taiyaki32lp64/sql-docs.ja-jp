---
title: セットの rds.DataControl サーバーと HTML テーブル (VBScript) へのバインド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- FilterColumn property [ADO], VBScript example
- FilterCriterion property [ADO], VBScript example
- SortDirection property [RDS], VBScript example
- Reset method [ADO], VBScript example
- SortColumn property [RDS], VBScript example
- FilterValue property [ADO], VBScript example
ms.assetid: 8a74802f-34d6-4676-bf94-07df5f8bff66
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8703641b25f7e5956fe4204db9775b0ada90cba1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964136"
---
# <a name="filtercolumn-filtercriterion-filtervalue-sortcolumn-and-sortdirection-properties-and-reset-method-example-vbscript"></a>FilterColumn、FilterCriterion、FilterValue、SortColumn、SortDirection プロパティおよび Reset メソッドの例 (VBScript)
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 次のコードを設定する方法を示しています、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) **Server** designtime とデータ ソースを使用して、データ対応の HTML テーブルのバインド パラメーター。 切り取り、メモ帳または別のテキスト エディターに次のコードを貼り付けてととして保存**FilterColumnVBS.asp**します。  
  
```  
<!-- BeginFilterColumnVBS -->  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript" Content="VBScript">  
  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<TITLE>FilterColumn, FilterCriterion, FilterValue, SortColumn, and SortDirection   
Properties and Reset Method Example (VBScript)</TITLE>  
</HEAD>  
<BODY>  
<h1>FilterColumn, FilterCriterion, FilterValue, SortColumn, and SortDirection   
Properties and Reset Method Example (VBScript)</h1>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS HEIGHT=1 WIDTH=1>  
   <PARAM NAME="SQL" VALUE="Select FirstName, LastName, Title, ReportsTo, Extension from Employees">  
   <PARAM NAME="SERVER" VALUE="<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=SQLOLEDB;Initial Catalog=Northwind;Integrated Security=SSPI">  
</OBJECT>  
  
Sort Column: <SELECT NAME="cboSortColumn">   
              <OPTION VALUE=""></OPTION>  
                  <OPTION VALUE=ID>ID</OPTION>  
                  <OPTION VALUE=FirstName>FirstName</OPTION>  
                  <OPTION VALUE=LastName>LastName</OPTION>  
                  <OPTION VALUE=Title>Title</OPTION>  
                  <OPTION VALUE=Title>ReportsTo</OPTION>  
                  <OPTION VALUE=Phone>Extension</OPTION>  
             </SELECT>  
             <br>  
Sort Direction: <SELECT NAME="cboSortDir">   
              <OPTION VALUE=""></OPTION>  
                  <OPTION VALUE=TRUE>Ascending</OPTION>  
                  <OPTION VALUE=FALSE>Descending</OPTION>  
                </SELECT>  
<HR WIDTH="25%">  
Filter Column: <SELECT NAME="cboFilterColumn">   
              <OPTION VALUE=""></OPTION>  
                  <OPTION VALUE=FirstName>FirstName</OPTION>  
                  <OPTION VALUE=LastName>LastName</OPTION>  
                  <OPTION VALUE=Title>Title</OPTION>  
                  <OPTION VALUE=Room>ReportsTo</OPTION>  
                  <OPTION VALUE=Phone>Extension</OPTION>  
             </SELECT>  
             <br>  
Filter Criterion: <SELECT NAME="cboCriterion">   
                    <OPTION VALUE=""></OPTION>  
                    <OPTION VALUE="=">=</OPTION>  
                    <OPTION VALUE=">">></OPTION>  
                    <OPTION VALUE="<"><</OPTION>  
                    <OPTION VALUE=">=">>=</OPTION>  
                    <OPTION VALUE="<="><=</OPTION>  
                    <OPTION VALUE="<>"><></OPTION>  
                  </SELECT>   
              <br>  
Filter Value: <INPUT NAME="txtFilterValue">  
<HR WIDTH="25%">  
<INPUT TYPE=BUTTON NAME=Clear VALUE="CLEAR ALL">    
<INPUT TYPE=BUTTON NAME=SortFilter VALUE="APPLY">  
  
<HR>  
<TABLE DATASRC=#RDS ID="DataTable">  
<THEAD>  
  <TR>  
    <TH>FirstName</TH>  
    <TH>LastName</TH>  
    <TH>Title</TH>  
    <TH>Reports To</TH>  
    <TH>Extension</TH>  
  </TR>  
</THEAD>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
    <TD><SPAN DATAFLD="Title"></SPAN></TD>  
    <TD><SPAN DATAFLD="ReportsTo"></SPAN></TD>  
    <TD><SPAN DATAFLD="Extension"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<Script Language="VBScript">  
<!--  
Const adFilterNone = 0  
  
Sub SortFilter_OnClick  
   Dim vCriterion  
   Dim vSortDir  
   Dim vSortCol  
   Dim vFilterCol  
  
   ' The value of SortColumn will be the   
   ' value of what the user picks in the  
   ' cboSortColumn box.  
   vSortCol = cboSortColumn.options(cboSortColumn.selectedIndex).value  
  
   If(vSortCol <> "") then  
      RDS.SortColumn = vSortCol  
   End If  
  
   ' The value of SortDirection will be the   
   ' value of what the user specifies in the  
   ' cboSortdirection box.  
  
   If (vSortCol <> "") then  
      vSortDir = cboSortDir.options(cboSortDir.selectedIndex).value  
      If (vSortDir = "") then  
         MsgBox "You must select a direction for the sort."  
         Exit Sub  
      Else  
         If vSortDir = "Ascending" Then vSortDir = "TRUE"  
         If vSortDir = "Descending" Then vSortDir = "FALSE"  
         RDS.SortDirection = vSortDir  
      End If  
   End If  
  
   ' The value of FilterColumn will be the   
   ' value of what the user specifies in the  
   ' cboFilterColumn box.  
   vFilterCol = cboFilterColumn.options(cboFilterColumn.selectedIndex).value  
  
   If(vFilterCol <> "") then  
      RDS.FilterColumn = vFilterCol  
   End If  
  
   ' The value of FilterCriterion will be the   
   ' text value of what the user specifies in the  
   ' cboCriterion box.  
   vCriterion = cboCriterion.options(cboCriterion.selectedIndex).value  
   If (vCriterion <> "") Then  
      RDS.FilterCriterion = vCriterion  
   End If  
  
   ' txtFilterValue is a rich text box  
   ' control. The value of FilterValue will be the   
   ' text value of what the user specifies in the  
   ' txtFilterValue box.  
   If (txtFilterValue.value <> "") Then  
      RDS.FilterValue = txtFilterValue.value  
   End If  
  
   ' Execute the sort and filter on a client-side  
   ' Recordset based on the specified sort and filter  
   ' properties. Calling Reset refreshes the result set  
   ' that is displayed in the data-bound controls to  
   ' display the filtered, sorted recordset.  
   RDS.Reset  
End Sub  
  
Sub Clear_onClick()  
   'clear the HTML input controls  
   cboSortColumn.selectedIndex = 0  
   cboSortDir.selectedIndex = 0  
   cboFilterColumn.selectedIndex = 0  
   cboCriterion.selectedIndex = 0  
   txtFilterValue.value = ""  
  
   'clear the filter  
   RDS.FilterCriterion = ""  
   RDS.Reset(FALSE)  
End Sub  
-->  
</Script>  
  
</BODY>  
</HTML>  
<!-- EndFilterColumnVBS -->  
```  
  
## <a name="see-also"></a>関連項目  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [FilterColumn プロパティ (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterCriterion プロパティ (RDS)](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [FilterValue プロパティ (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [Reset メソッド (RDS)](../../../ado/reference/rds-api/reset-method-rds.md)   
 [SortColumn プロパティ (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection プロパティ (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


