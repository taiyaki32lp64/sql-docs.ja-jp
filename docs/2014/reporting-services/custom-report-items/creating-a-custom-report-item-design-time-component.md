---
title: カスタム レポート アイテムのデザイン時コンポーネントの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items, creating
ms.assetid: 323fd58a-a462-4c48-b188-77ebc0b4212e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1a57fe5449deeb4445dff3853335b19a62dbc589
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63265143"
---
# <a name="creating-a-custom-report-item-design-time-component"></a>カスタム レポート アイテムのデザイン時コンポーネントの作成
  カスタム レポート アイテムのデザイン時コンポーネントは、Visual Studio レポート デザイナー環境で使用できるコントロールです。 カスタム レポート アイテムのデザイン時コンポーネントは、ドラッグ アンド ドロップ操作を使用できるアクティブ化されたデザイン画面、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] プロパティ ブラウザーとの統合、およびカスタム プロパティ エディター機能を提供します。  
  
 カスタム レポート アイテムのデザイン時コンポーネントを使用すると、ユーザーは、デザイン環境のレポート上にカスタム レポート アイテムを配置し、カスタム レポート アイテムのカスタム データ プロパティを設定してから、カスタム レポート アイテムをレポート プロジェクトの一部として保存できます。  
  
 開発環境でデザイン時コンポーネントを使用して設定されるプロパティは、ホスト デザイン環境によってシリアル化およびシリアル化解除され、レポート定義言語 (RDL) ファイルに要素として格納されます。 レポート プロセッサによるレポートの実行時には、デザイン時コンポーネントを使用して設定されたプロパティが、レポート プロセッサによってカスタム レポート アイテムの実行時コンポーネントに渡されます。実行時コンポーネントは、カスタム レポート アイテムを表示してレポート プロセッサに返します。  
  
> [!NOTE]  
>  カスタム レポート アイテムのデザイン時コンポーネントは、[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] コンポーネントとして実装されます。 ここでは、カスタム レポート アイテムのデザイン時コンポーネントに固有の実装詳細について説明します。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] を使用したコンポーネント開発の詳細については、MSDN ライブラリの「[Visual Studio のコンポーネント](https://go.microsoft.com/fwlink/?LinkId=116576)」を参照してください。  
  
 完全に実装されたカスタム レポート アイテムの例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services の製品サンプル) を参照してください。  
  
## <a name="implementing-a-design-time-component"></a>デザイン時コンポーネントの実装  
 カスタム レポート アイテムのデザイン時コンポーネントのメイン クラスは、`Microsoft.ReportDesigner.CustomReportItemDesigner` クラスから継承されます。 コンポーネント クラスには、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] コントロールで使用される標準の属性に加えて、`CustomReportItem` 属性を定義してください。 この属性は、reportserver.config ファイルに定義されたカスタム レポート アイテム名と同じにする必要があります。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 属性の完全な一覧については、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK ドキュメントの「属性」を参照してください。  
  
 次のコード例では、カスタム レポート アイテムのデザイン時コントロールに属性が適用されています。  
  
```csharp  
namespace PolygonsCRI  
{  
    [LocalizedName("Polygons")]  
    [Editor(typeof(CustomEditor), typeof(ComponentEditor))]  
        [ToolboxBitmap(typeof(PolygonsDesigner),"Polygons.ico")]  
        [CustomReportItem("Polygons")]  
  
    public class PolygonsDesigner : CustomReportItemDesigner  
    {  
...  
```  
  
### <a name="initializing-the-component"></a>コンポーネントの初期化  
 カスタム レポート アイテム用にユーザーが指定したプロパティは、<xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> クラスを使用して渡されます。 コンポーネントの <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> クラスから新しいインスタンスを作成して既定値に設定する際には、`CustomReportItemDesigner` クラスの実装で `InitializeNewComponent` メソッドをオーバーライドしてください。  
  
 次のコードは、コンポーネントの <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> クラスを初期化する際に、カスタム レポート アイテムのデザイン時コンポーネント クラスで `CustomReportItemDesigner.InitializeNewComponent` メソッドをオーバーライドする例です。  
  
```csharp  
public override void InitializeNewComponent()  
        {  
            CustomData = new CustomData();  
            CustomData.DataRowHierarchy = new DataHierarchy();  
  
            // Shape grouping  
            CustomData.DataRowHierarchy.DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].Group.Name = Name + "_Shape";  
            CustomData.DataRowHierarchy.DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Point grouping  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.Name = Name + "_Point";  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Static column  
            CustomData.DataColumnHierarchy = new DataHierarchy();  
            CustomData.DataColumnHierarchy.DataMembers.Add(new DataMember());  
  
            // Points  
            IList<IList<DataValue>> dataValues = new List<IList<DataValue>>();  
            CustomData.DataRows.Add(dataValues);  
            CustomData.DataRows[0].Add(new List<DataValue>());  
            CustomData.DataRows[0][0].Add(NewDataValue("X", ""));  
            CustomData.DataRows[0][0].Add(NewDataValue("Y", ""));  
        }  
```  
  
### <a name="modifying-component-properties"></a>コンポーネントのプロパティの変更  
 `CustomData` プロパティをデザイン環境で変更するには、複数の方法があります。 デザイン時コンポーネントによって公開され、<xref:System.ComponentModel.BrowsableAttribute> 属性でマークされたあらゆるプロパティは、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] プロパティ ブラウザーを使用して変更できます。 また、プロパティを変更するには、カスタム レポート アイテムのデザイン画面にアイテムをドラッグする方法や、デザイン環境でコントロールを右クリックし、ショートカット メニューの **[プロパティ]** をクリックしてカスタム プロパティ ウィンドウを表示する方法もあります。  
  
 以下のコード例では、`Microsoft.ReportDesigner.CustomReportItemDesigner.CustomData` プロパティに <xref:System.ComponentModel.BrowsableAttribute> 属性が適用されています。  
  
```csharp  
[Browsable(true), Category("Data")]  
public string DataSetName  
{  
      get  
      {  
         return CustomData.DataSetName;  
      }  
      set  
      {  
         CustomData.DataSetName = value;  
      }  
   }  
  
```  
  
 デザイン時コンポーネントに、カスタム プロパティ エディター ダイアログ ボックスを挿入できます。 カスタム プロパティ エディターの実装では、<xref:System.ComponentModel.ComponentEditor> クラスを継承し、プロパティ編集用ダイアログ ボックスのインスタンスを作成する必要があります。  
  
 次の例は、<xref:System.ComponentModel.ComponentEditor> を継承し、カスタム プロパティ エディター ダイアログ ボックスを表示するクラスの実装です。  
  
```csharp  
internal sealed class CustomEditor : ComponentEditor  
{  
   public override bool EditComponent(  
      ITypeDescriptorContext context, object component)  
    {  
     PolygonsDesigner designer = (PolygonsDesigner)component;  
     PolygonProperties dialog = new PolygonProperties();  
     dialog.m_designerComponent = designer;  
     DialogResult result = dialog.ShowDialog();  
     if (result == DialogResult.OK)  
     {  
        designer.Invalidate();  
        designer.ChangeService().OnComponentChanged(designer, null, null, null);  
        return true;  
     }  
     else  
        return false;  
    }  
}  
```  
  
 カスタム プロパティ エディター ダイアログ ボックスで、レポート デザイナーの式エディターを呼び出すことができます。 次の例では、コンボ ボックスの最初の要素をユーザーが選択すると、式エディターが呼び出されます。  
  
```csharp  
private void EditableCombo_SelectedIndexChanged(object sender,   
    EventArgs e)  
{  
   ComboBox combo = (ComboBox)sender;  
   if (combo.SelectedIndex == 0 && m_launchEditor)  
   {  
      m_launchEditor = false;  
      ExpressionEditor editor = new ExpressionEditor();  
      string newValue;  
      newValue = (string)editor.EditValue(null, m_designerComponent.Site, m_oldComboValue);  
      combo.Items[0] = newValue;  
   }  
}  
  
```  
  
### <a name="using-designer-verbs"></a>デザイナー動詞の使用  
 デザイナー動詞は、イベント ハンドラーにリンクされたメニュー コマンドです。 デザイナー動詞を追加して、カスタム レポート アイテムの実行時コントロールのデザイン環境での使用時に、コンポーネントのショートカット メニューに表示できます。 実行時コンポーネントで `Verbs` プロパティを使用すると、使用可能なデザイナー動詞の一覧が返されます。  
  
 次のコード例では、デザイナー動詞とイベント ハンドラーが <xref:System.ComponentModel.Design.DesignerVerbCollection> に追加されています。イベント ハンドラー コードも示します。  
  
```csharp  
public override DesignerVerbCollection Verbs  
{  
    get  
    {  
        if (m_verbs == null)  
        {  
            m_verbs = new DesignerVerbCollection();  
            m_verbs.Add(new DesignerVerb("Proportional Scaling", new EventHandler(OnProportionalScaling)));  
         m_verbs[0].Checked = (GetCustomProperty("poly:Proportional") == bool.TrueString);  
        }  
  
        return m_verbs;  
    }  
}  
  
private void OnProportionalScaling(object sender, EventArgs e)  
{  
   bool proportional = !  
        (GetCustomProperty("poly:Proportional") == bool.TrueString);  
   m_verbs[0].Checked = proportional;  
   SetCustomProperty("poly:Proportional", proportional.ToString());  
   ChangeService().OnComponentChanged(this, null, null, null);  
   Invalidate();  
}  
```  
  
### <a name="using-adornments"></a>装飾の使用  
 カスタム レポート アイテム クラスには、`Microsoft.ReportDesigner.Design.Adornment` クラスを実装することもできます。 装飾を使用すると、カスタム レポート アイテムのコントロールで、デザイン画面のメインの四角形の外に領域を作成できます。 これらの領域では、マウス クリックやドラッグ アンド ドロップ操作などのユーザー インターフェイス イベントを扱うことができます。 `Adornment`クラスで定義されている、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] `Microsoft.ReportDesigner`名前空間はのパススルー実装、<xref:System.Windows.Forms.Design.Behavior.Adorner>クラスは、Windows フォームで見つかりました。 完全なドキュメントについて、`Adorner`クラスを参照してください[動作サービスの概要](https://go.microsoft.com/fwlink/?LinkId=116673)MSDN ライブラリ。 実装するサンプル コードについては、`Microsoft.ReportDesigner.Design.Adornment`クラスを参照してください[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)します。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] での Windows フォームを使ったプログラミングの詳細については、MSDN ライブラリの次のトピックを参照してください。  
  
-   コンポーネントのデザイン時属性  
  
-   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のコンポーネント  
  
-   チュートリアル: Visual Studio のデザイン時機能を活用した Windows フォーム コントロールの作成  
  
## <a name="see-also"></a>参照  
 [カスタム レポート アイテムのアーキテクチャ](custom-report-item-architecture.md)   
 [カスタム レポート アイテムの実行時コンポーネントの作成](creating-a-custom-report-item-run-time-component.md)   
 [カスタム レポート アイテムのクラス ライブラリ](custom-report-item-class-libraries.md)   
 [方法:カスタム レポート アイテムを配置する](how-to-deploy-a-custom-report-item.md)  
  
  
