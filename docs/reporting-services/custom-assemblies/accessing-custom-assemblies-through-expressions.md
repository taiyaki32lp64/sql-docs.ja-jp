---
title: 式を使用したカスタム アセンブリへのアクセス | Microsoft Docs
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- expressions [Reporting Services], custom assemblies
- static member calls
- instance member calls [Reporting Services]
- calling class members
- custom assemblies [Reporting Services], expressions
ms.assetid: 917c4d47-1a95-4f54-98b1-e8cb2165d90f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 101af9d59d4a3f1e48d85859c91f77c8be2e4719
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194364"
---
# <a name="accessing-custom-assemblies-through-expressions"></a>式を使用したカスタム アセンブリへのアクセス
  カスタム アセンブリを作成し、レポート デザイナーまたはレポート サーバーで利用可能にします。そして、適切なセキュリティ ポリシーを追加し、レポート定義のカスタム アセンブリへの参照を追加すると、レポートの式を使用してアセンブリ内のクラスのメンバーにアクセスできます。 式の中でカスタム コードを参照するには、アセンブリ内のクラスのメンバーを呼び出す必要があります。 呼び出す方法は、メソッドが静的であるかインスタンス ベースであるかにより異なります。  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>レポート定義ファイルから静的メンバーを呼び出す  
 静的メンバーはクラスまたは型そのものに所属し、インスタンス化されたオブジェクトには所属しません。 静的メンバーはクラスから直接呼び出すことによりアクセスできます。 可能な場合は常に、静的メンバーを使用してレポートのカスタム関数を呼び出す必要があります。その理由は、静的メンバーがパフォーマンス上最も優れているからです。 静的メンバーを呼び出すには、=*Namespace.Class.Method* の形をとる式として参照する必要があります。  
  
#### <a name="to-call-static-members"></a>静的メンバーを呼び出すには  
  
-   静的メンバーを呼び出すには、式と、完全に修飾されたメンバー名とを等しくします。メンバー名を完全に修飾するには、名前空間、クラス名、およびメンバー名を使用します。 次の例では、**ToGBP** メソッドを呼び出します。このメソッドは、**StandardCost** フィールドの値をドルから英ポンドに換算し、レポートに表示します。  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>静的フィールドおよび静的プロパティに関する重要な情報  
 現在のところ、すべてのレポートは同じアプリケーション ドメインで実行されます。 このことは、レポートのユーザー固有の静的データを、同じレポートの他のインスタンスから参照できることを意味します。 このような状況では、あるユーザーの静的データを、同時平行して個々のレポートを実行している他のすべてのユーザーが利用できる可能性があります。 そのため、カスタム アセンブリまたは **Code** 要素の中で静的フィールドおよび静的プロパティを使用しないよう、強くお勧めします。レポートの中ではインスタンス フィールドおよびインスタンス プロパティを使用してください。 しかし、静的メソッドは、状態やデータを保存しないため、使用可能です。  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>レポート定義ファイルからインスタンス メンバーを呼び出す  
 レポート定義内からアクセスする必要があるインスタンス メンバーがカスタム アセンブリ内に含まれている場合は、クラスのインスタンス名をレポートに追加する必要があります。 **[レポートのプロパティ]** ダイアログ ボックスの **[コード]** タブを使用してクラスのインスタンス名を追加できます。 レポートにクラスのインスタンスを追加する方法については、「[レポート デザイナーでカスタム コードやアセンブリを式から参照する &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)」を参照してください。  
  
 静的メンバーを呼び出すには、=Code *.InstanceName.Method* の形をとる式として参照する必要があります。  
  
#### <a name="to-call-instance-members"></a>インスタンス メンバーを呼び出すには  
  
-   カスタム アセンブリのインスタンス メンバーを呼び出すには、キーワード **Code** の後にインスタンス名とメソッドを記述して参照する必要があります。 次の例では、インスタンス メソッド **ToEUR** を呼び出します。このメソッドは、**StandardCost** フィールドの値をドルからユーロに換算し、レポートに表示します。  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>参照  
 [レポートでのカスタム アセンブリの使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
