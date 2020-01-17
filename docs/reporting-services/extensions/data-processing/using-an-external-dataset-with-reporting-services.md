---
title: Reporting Services での外部データセットの使用 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- DataSet objects [Reporting Services]
- data processing extensions [Reporting Services], custom DataSet objects
- custom DataSet objects [Reporting Services]
- external DataSet objects [Reporting Services]
ms.assetid: 11daa013-ec17-4760-80e3-6d84cd8d5722
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1c3b4ad599864bc2ddb752982ed61bf73684c2f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193867"
---
# <a name="using-an-external-dataset-with-reporting-services"></a>Reporting Services での外部データセットの使用
  非接続の分散データ シナリオを [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] でサポートする場合、その中心となるのが **DataSet** オブジェクトです。 **DataSet** オブジェクトはメモリ上に保持されたデータを表し、データ ソースとは無関係に一貫したリレーショナル プログラミング モデルを提供します。 また、複数の異なるデータ ソースや XML データで使用でき、アプリケーションのデータをローカルに管理することも可能です。 **DataSet** オブジェクトは、関連テーブル、制約、およびテーブル間のリレーションシップを含む、完全なデータセットを表します。 **DataSet** オブジェクトには、データを格納し、表示するための柔軟な機能が備わっています。そのため、データに関するレポートを生成するときは、多くの場合、事前にそのデータが処理され、**DataSet** オブジェクトに変換されます。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のデータ処理拡張機能を使用すると、外部アプリケーションによって作成されたあらゆるカスタム **DataSet** オブジェクトを統合できます。 そのためには、**DataSet** オブジェクトとレポート サーバー間の橋渡し役となるカスタム データ処理拡張機能を [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] に作成してください。 この **DataSet** オブジェクトを処理するためのコードのほとんどは、作成する **DataReader** クラスに含まれています。  
  
 **DataSet** オブジェクトをレポート サーバーに公開する場合、最初に **DataSet** オブジェクトを設定できるプロバイダー固有のメソッドを **DataReader** クラスに実装します。 次の例は、**DataReader** クラスのプロバイダー固有メソッドを使用して、静的データを **DataSet** オブジェクトに読み込む方法を示しています。  
  
```vb  
'Private members of the DataReader class  
Private m_dataSet As System.Data.DataSet  
Private m_currentRow As Integer  
  
'Method to create a dataset  
Friend Sub CreateDataSet()  
   ' Create a dataset.  
   Dim ds As New System.Data.DataSet("myDataSet")  
   ' Create a data table.   
   Dim dt As New System.Data.DataTable("myTable")  
   ' Create a data column and set various properties.   
   Dim dc As New System.Data.DataColumn()  
   dc.DataType = System.Type.GetType("System.Decimal")  
   dc.AllowDBNull = False  
   dc.Caption = "Number"  
   dc.ColumnName = "Number"  
   dc.DefaultValue = 25  
   ' Add the column to the table.   
   dt.Columns.Add(dc)  
   ' Add 10 rows and set values.   
   Dim dr As System.Data.DataRow  
   Dim i As Integer  
   For i = 0 To 9  
      dr = dt.NewRow()  
      dr("Number") = i + 1  
      ' Be sure to add the new row to the DataRowCollection.   
      dt.Rows.Add(dr)  
   Next i  
  
   ' Fill the dataset.  
   ds.Tables.Add(dt)  
  
   ' Use a private variable to store the dataset in your  
   ' DataReader.  
   m_dataSet = ds  
  
   ' Set the current row to -1.  
   m_currentRow = - 1  
End Sub 'CreateDataSet  
```  
  
```csharp  
// Private members of the DataReader class  
private System.Data.DataSet m_dataSet;  
private int m_currentRow;  
  
// Method to create a dataset  
internal void CreateDataSet()  
{  
   // Create a dataset.  
   System.Data.DataSet ds = new System.Data.DataSet("myDataSet");  
   // Create a data table.   
   System.Data.DataTable dt = new System.Data.DataTable("myTable");  
   // Create a data column and set various properties.   
   System.Data.DataColumn dc = new System.Data.DataColumn();   
   dc.DataType = System.Type.GetType("System.Decimal");   
   dc.AllowDBNull = false;   
   dc.Caption = "Number";   
   dc.ColumnName = "Number";   
   dc.DefaultValue = 25;   
   // Add the column to the table.   
   dt.Columns.Add(dc);   
   // Add 10 rows and set values.   
   System.Data.DataRow dr;   
   for(int i = 0; i < 10; i++)  
   {   
      dr = dt.NewRow();   
      dr["Number"] = i + 1;   
      // Be sure to add the new row to the DataRowCollection.   
      dt.Rows.Add(dr);  
   }  
  
   // Fill the dataset.  
   ds.Tables.Add(dt);  
  
   // Use a private variable to store the dataset in your  
   // DataReader.  
   m_dataSet = ds;  
  
   // Set the current row to -1.  
   m_currentRow = -1;  
}  
```  
  
```csharp  
public bool Read()  
{  
   m_currentRow++;  
   if (m_currentRow >= m_dataSet.Tables[0].Rows.Count)   
   {  
      return (false);  
   }   
   else   
   {  
      return (true);  
   }  
}  
  
public int FieldCount  
{  
   // Return the count of the number of columns, which in  
   // this case is the size of the column metadata  
   // array.  
   get { return m_dataSet.Tables[0].Columns.Count; }  
}  
  
public string GetName(int i)  
{  
   return m_dataSet.Tables[0].Columns[i].ColumnName;  
}  
  
public Type GetFieldType(int i)  
{  
   // Return the actual Type class for the data type.  
   return m_dataSet.Tables[0].Columns[i].DataType;  
}  
  
public Object GetValue(int i)  
{  
   return m_dataSet.Tables[0].Rows[m_currentRow][i];  
}  
  
public int GetOrdinal(string name)  
{  
   // Look for the ordinal of the column with the same name and return it.  
   // Returns -1 if not found.  
   return m_dataSet.Tables[0].Columns[name].Ordinal;  
}  
```  
  
 データセットを作成または取得したら、**DataReader** クラスの **Read**、**GetValue**、**GetName**、**GetOrdinal**、**GetFieldType**、および **FieldCount** の各メンバーの実装に **DataSet** オブジェクトを使用できます。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [データ処理拡張機能の実装](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
