---
title: 計算列表現 (テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 190bfa92-2445-404d-86df-7cc94d283add
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a671f33fa26829e96cb53e1a040eb042406bc4eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62757707"
---
# <a name="calculated-column-representation-tabular"></a>計算列表現 (テーブル)
  計算列はテーブルに新しい列を作成する DAX 式で、取得した値はテーブルに格納されます。 計算列式はテーブルが処理されるたびに評価されます。  
  
## <a name="calculated-column-representation"></a>計算列表現  
  
### <a name="calculated-columns-in-amo"></a>AMO における計算列  
 AMO を使用してテーブル モデル テーブルを管理する場合、AMO 内の計算列に一対一で対応するオブジェクトは存在しません。 計算列は、<xref:Microsoft.AnalysisServices.Dimension> 属性と <xref:Microsoft.AnalysisServices.MeasureGroup> 属性によって表されます。  
  
 次のコード スニペットでは、計算列を既存のテーブル モデルに渡す方法を示します。 このコードでは、AMO データベース オブジェクトである newDatabase と、AMO キューブ オブジェクトである modelCube が存在していることを前提としています。  
  
```  
  
private void addCalculatedColumn(  
                   AMO.Database newDatabase  
                 , AMO.Cube modelCube  
                 , String ccTableName  
                 , String ccName  
                 , String newCalculatedColumnExpression  
             )  
{  
    if (string.IsNullOrEmpty(ccName) || string.IsNullOrWhiteSpace(ccName))  
    {  
        MessageBox.Show(String.Format("Calculated Column name is not defined."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
    if (string.IsNullOrEmpty(newCalculatedColumnExpression) || string.IsNullOrWhiteSpace(newCalculatedColumnExpression))  
    {  
        MessageBox.Show(String.Format("Calculated Column expression is not defined."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    if (newDatabase.Dimensions[ccTableName].Attributes.Contains(ccName))  
    {  
        MessageBox.Show(String.Format("Calculated Column name already defined."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
    //Add CC attribute to the Dimension  
    AMO.Dimension dim = newDatabase.Dimensions[ccTableName];  
    AMO.DimensionAttribute currentAttribute = dim.Attributes.Add(ccName, ccName);  
    currentAttribute.Usage = AMO.AttributeUsage.Regular;  
    currentAttribute.KeyUniquenessGuarantee = false;  
  
    currentAttribute.KeyColumns.Add(new AMO.DataItem(ccTableName, ccName, OleDbType.Empty));  
    currentAttribute.KeyColumns[0].Source = new AMO.ExpressionBinding(newCalculatedColumnExpression);  
    currentAttribute.KeyColumns[0].NullProcessing = AMO.NullProcessing.Preserve;  
    currentAttribute.NameColumn = new AMO.DataItem(ccTableName, ccName, System.Data.OleDb.OleDbType.WChar);  
    currentAttribute.NameColumn.Source = new AMO.ExpressionBinding(newCalculatedColumnExpression);  
    currentAttribute.NameColumn.NullProcessing = AMO.NullProcessing.ZeroOrBlank;  
  
    currentAttribute.OrderBy = AMO.OrderBy.Key;  
    AMO.AttributeRelationship currentAttributeRelationship = dim.Attributes["RowNumber"].AttributeRelationships.Add(currentAttribute.ID);  
    currentAttributeRelationship.Cardinality = AMO.Cardinality.Many;  
    currentAttributeRelationship.OverrideBehavior = AMO.OverrideBehavior.None;  
  
    //Add CC as attribute to the MG  
    AMO.MeasureGroup mg = modelCube.MeasureGroups[ccTableName];  
    AMO.DegenerateMeasureGroupDimension currentMGDim = (AMO.DegenerateMeasureGroupDimension)mg.Dimensions[ccTableName];  
    AMO.MeasureGroupAttribute mga = new AMO.MeasureGroupAttribute(ccName);  
  
    mga.KeyColumns.Add(new AMO.DataItem(ccTableName, ccName, OleDbType.Empty));  
    mga.KeyColumns[0].Source = new AMO.ExpressionBinding(newCalculatedColumnExpression);  
  
    currentMGDim.Attributes.Add(mga);  
  
    try  
    {  
        //Update Dimension, CubeDimension and MG in server  
        newDatabase.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
    }  
    catch (AMO.OperationException amoOpXp)  
    {  
        MessageBox.Show(String.Format("Calculated Column expression contains syntax errors, or references undefined or missspelled elements.\nError message: {0}", amoOpXp.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        return;  
    }  
    catch (AMO.AmoException amoXp)  
    {  
        MessageBox.Show(String.Format("AMO exception accessing the server.\nError message: {0}", amoXp.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        return;  
    }  
    catch (Exception)  
    {  
        throw;  
    }  
}  
  
```  
  
  
