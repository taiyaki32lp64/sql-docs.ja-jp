---
title: 属性階層の非表示と無効化 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 095039c2-7104-414c-a9a6-327b03ce79df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4381047ad4373a2a5b03dc9ba1c96274b37621f2
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530846"
---
# <a name="hiding-and-disabling-attribute-hierarchies"></a>属性階層の非表示化と無効化
  既定では、ディメンションの属性ごとに属性階層が 1 つ作成されます。また、それぞれの階層はディメンションのファクト データで使用できます。 属性階層は、"All" レベルと、その階層のすべてのメンバーを含む詳細レベルで構成されます。 既に学習したように、これらの属性をユーザー定義階層として整理し、キューブ内にナビゲーション パスを設けることができます。 状況によっては、一部の属性とその階層を無効にしたり、非表示にしたりする必要が生じます。 たとえば、社会保障番号 (身分登録番号)、給与、誕生日、ログイン情報などは、キューブ情報の生成には必要のない属性です。 一般に、これらの情報は、特定の属性メンバーの詳細情報としてのみ表示されます。 したがって、これらの属性階層を非表示にして、各属性のメンバー プロパティとしてのみ表示されるようにする必要があります。 また、顧客名、郵便番号など他の属性メンバーは、属性階層に個別に表示するのではなく、ユーザー階層からのみ表示されるようにする必要があります。 このような処理をするのは、属性階層内の独立したメンバーが非常に多いためです。 処理パフォーマンスを向上させるため、ユーザーが参照しない属性階層を無効にしてください。  
  
 **AttributeHierarchyEnabled** プロパティは、属性階層を作成するかどうかを指定します。 このプロパティを **False**に設定すると、属性階層は作成されず、その属性はユーザー階層のレベルとして使用できなくなります。つまり、属性階層がメンバー プロパティとしてのみ存在するようになります。 ただし、属性階層を無効にしても、その属性階層を使用して別の属性のメンバーを整理することはできます。 **AttributeHierarchyEnabled** プロパティを **True**に設定している場合は、ユーザー定義階層で属性階層が使用されているかどうかに関係なく、 **AttributeHierarchyVisible** プロパティの値によりその属性階層の表示、非表示が決定されます。  
  
 属性階層を有効にしている場合は、さらに次の 3 つのプロパティに値を指定できます。  
  
-   **IsAggregatable**  
  
     既定では、すべての属性階層に (All) レベルが定義されます。 有効な属性階層の (All) レベルを無効にするには、このプロパティを **False**に設定します。  
  
    > [!NOTE]  
    >  **IsAggregatable** プロパティが False に設定された属性は、ユーザー定義階層のルートとしてのみ使用できます。また、この属性には、指定された既定メンバーを割り当てる必要があります (これを行わなかった場合は、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] エンジンによって既定メンバーが選択されます)。  
  
-   **AttributeHierarchyOrdered**  
  
     既定では、処理中に  **が有効な属性階層のメンバーを整理し、Name や Key などの [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]OrderBy** プロパティの値に基づいてメンバーを格納します。 メンバーが順不同でもよい場合は、このプロパティの値を **False** に設定することにより、パフォーマンスを向上させることができます。  
  
-   **AttributeHierarchyOptimizedState**  
  
     既定では、処理中に [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] が有効な各属性階層のインデックスを作成します。これにより、クエリのパフォーマンスが向上します。 属性階層を表示する予定がない場合は、このプロパティの値を **NotOptimized**に設定することにより、パフォーマンスを向上させることができます。 ただし、非表示の属性をディメンションのキー属性として使用する場合は、属性メンバーのインデックスを作成することでパフォーマンスが向上します。  
  
 属性階層が無効になっている場合は、これらのプロパティが適用されません。  
  
 このトピックの実習では、Employee ディメンションの社会保障番号のほか、表示する必要のない他の属性を無効にします。 次に、Customer ディメンションの顧客名と郵便番号の属性階層を非表示にします。 ユーザー階層とは関係なく、これらの階層の属性メンバーが多いと、階層の表示が非常に遅くなります。  
  
## <a name="setting-attribute-hierarchy-properties-in-the-employee-dimension"></a>Employee ディメンションの属性階層プロパティの設定  
  
1.  Employee ディメンションのディメンション デザイナーに切り替え、 **[ブラウザー]** タブをクリックします。  
  
2.  **[階層]** ボックスの一覧に、次の属性階層が表示されていることを確認します。  
  
    -   **Base Rate**  
  
    -   **Birth Date**  
  
    -   **Login ID**  
  
    -   **Manager SSN**  
  
    -   **SSN**  
  
3.  **[ディメンション構造]** タブに切り替え、 **[属性]** ペインで次の属性を選択します。 Ctrl キーを押しながらクリックすると、複数のメジャーを選択できます。  
  
    -   **Base Rate**  
  
    -   **Birth Date**  
  
    -   **Login ID**  
  
    -   **Manager SSN**  
  
    -   **SSN**  
  
4.  [プロパティ] ウィンドウで、選択した属性の **AttributeHierarchyEnabled** プロパティの値を **False** に設定します。  
  
     **[属性]** ペインを見ると、各属性のアイコンが変わり、無効になっていることがわかります。  
  
     次の図では、選択した属性の **AttributeHierarchyEnabled** プロパティが False に設定されています。  
  
     ![AttributeHierarchyEnabled プロパティが False に設定 される](../../2014/tutorials/media/l4-hierarchyenabled-1.gif "AttributeHierarchyEnabled プロパティが False に設定")される  
  
5.  **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
6.  処理が完了したら **[ブラウザー]** タブに切り替え、 **[再接続]** をクリックします。その後、変更後の属性階層を表示してみてください。  
  
     変更した属性のメンバーは、 **[階層]** ボックスの一覧に属性階層として表示されません。 無効にしたいずれかの階層属性をユーザー階層のレベルとして追加しようとすると、ユーザー定義階層に追加するには、その属性階層を有効にしなければならないことを知らせるエラーが表示されます。  
  
## <a name="setting-attribute-hierarchy-properties-in-the-customer-dimension"></a>Customer ディメンションの属性階層プロパティの設定  
  
1.  Customer ディメンションのディメンション デザイナーに切り替え、 **[ブラウザー]** タブをクリックします。  
  
2.  **[階層]** ボックスの一覧に、次の属性階層が表示されていることを確認します。  
  
    -   **Full Name**  
  
    -   **Postal Code**  
  
3.  **[ディメンション構造]** タブに切り替え、 **[属性]** ペインで次の属性を選択します。複数の属性を選択するときは、Ctrl キーを押しながら各属性をクリックします。  
  
    -   **[名前]**  
  
    -   **Postal Code**  
  
4.  [プロパティ] ウィンドウで、選択した属性の **AttributeHierarchyVisible** プロパティの値を **False** に設定します。  
  
     これらの属性階層のメンバーはファクト データの多次元化に使用されるため、メンバーを整理して最適化することによりパフォーマンスが向上します。 このため、これらの属性のプロパティは変更しないでください。  
  
     次の図では、 **AttributeHierarchyVisible** プロパティが False に設定されています。  
  
     ![AttributeHierarchyVisible プロパティが False に設定される](../../2014/tutorials/media/l4-hierarchyvisible-1.gif "AttributeHierarchyVisible プロパティが False に設定")される  
  
5.  **[属性]** ペインの **Postal Code** 属性を、 **[階層とレベル]** ペインの **Customer Geography** ユーザー階層 ( **City** レベルのすぐ下) にドラッグします。  
  
     属性が非表示に設定されていても、ユーザー階層にレベルとして追加することができます。  
  
6.  **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
7.  配置が正常に完了したら、Customer ディメンションの **[ブラウザー]** タブに切り替え、 **[再接続]** をクリックします。  
  
8.  **[階層]** ボックスの一覧から、変更した属性階層のいずれかを選択してみます。  
  
     **[階層]** ボックスの一覧には、変更した属性階層は何も表示されないはずです。  
  
9. **[階層]** ボックスの一覧で **[Customer Geography]** をクリックし、ブラウザー ペインに各レベルを表示します。  
  
     ユーザー定義階層には、非表示にした **Postal Code** レベルと **Full Name**レベルが表示されます。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [2 次属性に基づく属性メンバーの並べ替え](lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md)  
  
  
