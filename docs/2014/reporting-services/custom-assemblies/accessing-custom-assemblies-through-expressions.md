---
title: 式を使用したカスタム アセンブリへのアクセス | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
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
manager: kfile
ms.openlocfilehash: fb9e2ae87a82bf272e84a8d940606879aa3c1e9d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792802"
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
 レポート定義内からアクセスする必要があるインスタンス メンバーがカスタム アセンブリ内に含まれている場合は、クラスのインスタンス名をレポートに追加する必要があります。 **[レポートのプロパティ]** ダイアログ ボックスの **[コード]** タブを使用してクラスのインスタンス名を追加できます。 レポートにクラスのインスタンスを追加する方法については、「[レポート デザイナーでカスタム コードやアセンブリを式から参照する &#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)」を参照してください。  
  
 静的メンバーを呼び出す形をとる式として参照する必要があります。 コードを =*します。InstanceName.Method*します。  
  
#### <a name="to-call-instance-members"></a>インスタンス メンバーを呼び出すには  
  
-   カスタム アセンブリのインスタンス メンバーを呼び出すには、キーワード **Code** の後にインスタンス名とメソッドを記述して参照する必要があります。 次の例では、インスタンス メソッド **ToEUR** を呼び出します。このメソッドは、**StandardCost** フィールドの値をドルからユーロに換算し、レポートに表示します。  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>関連項目  
 [レポートでのカスタム アセンブリの使用](using-custom-assemblies-with-reports.md)  
  
  
