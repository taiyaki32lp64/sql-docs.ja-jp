---
title: レポートにコードを追加する (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom code [Reporting Services]
- expressions [Reporting Services], code
- adding code
- reports [Reporting Services], code
ms.assetid: 00ef8fc6-99fe-49b2-8a22-7eb475881dc4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e8109678c3e9695b842eb57b976da9e653afd737
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106657"
---
# <a name="add-code-to-a-report-ssrs"></a>レポートにコードを追加する (SSRS)
  どの式でも独自のカスタム コードを呼び出すことができます。 次の 2 つの方法でコードを提供できます。  
  
-   [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] で記述されたコードをレポートに直接埋め込みます。 コードが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] または <xref:System.Math> ではない <xref:System.Convert>を参照する場合は、レポートへの参照を追加する必要があります。 詳細については、「 [レポートにアセンブリへの参照を追加する &#40;SSRS&#41;](add-an-assembly-reference-to-a-report-ssrs.md)」を参照してください。 コードから行うことのできる参照については、「[レポート デザイナーでカスタム コードやアセンブリを式から参照する &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)」を参照してください。  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]を使用して、カスタム コード アセンブリを指定します。 カスタム アセンブリを指定する場合、レポートの作成場所のコンピューターとレポートを表示するレポート サーバーの両方にそれをインストールする必要があります。 詳細については、「 [レポートでのカスタム アセンブリの使用](../custom-assemblies/using-custom-assemblies-with-reports.md)」を参照してください。  
  
### <a name="to-add-embedded-code-to-a-report"></a>レポートに埋め込みコードを追加するには  
  
1.  **[デザイン]** ビューで、デザイン画面のレポートの罫線の外を右クリックし、 **[レポートのプロパティ]** をクリックします。  
  
2.  **[コード]** をクリックします。  
  
3.  **[カスタム コード]** でコードを入力します。 コード内にエラーがあると、レポートの実行時に警告が生成されます。 次の例では、" `ChangeWord` " という単語を "`Bike`" で置き換える`Bicycle`という名前のカスタム関数が作成されます。  
  
    ```  
    Public Function ChangeWord(ByVal s As String) As String  
       Dim strBuilder As New System.Text.StringBuilder(s)  
       If s.Contains("Bike") Then  
          strBuilder.Replace("Bike", "Bicycle")  
          Return strBuilder.ToString()  
          Else : Return s  
       End If  
    End Function  
    ```  
  
4.  次の例は、式で Category という名前のデータセット フィールドをこの関数に渡す方法を示しています。  
  
    ```  
    =Code.ChangeWord(Fields!Category.Value)  
    ```  
  
     この式をカテゴリの値を表示するテーブル セルに追加すると、"Bike" という単語がその行のデータセット フィールドに現れるたびに、テーブル セルの値は "Bicycle" という単語を表示します。  
  
## <a name="see-also"></a>関連項目  
 [[コード] ([レポートのプロパティ] ダイアログ ボックス)](../report-properties-dialog-box-code.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [Parameters コレクションの参照 (レポート ビルダーおよび SSRS)](built-in-collections-parameters-collection-references-report-builder.md)  
  
  
