---
title: タスク 6:マスター データ マネージャーを使用してドメイン ベースの属性を作成することを確認 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6e90517a-910c-4c33-8f11-92ac3cff4fdc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: fe3f404d4f41e2977ef389216dcbc9106327266a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488950"
---
# <a name="task-6-verify-that-the-domain-based-attribute-is-created-using-master-data-manager"></a>タスク 6:マスター データ マネージャーを使用してドメイン ベースの属性が作成されていることを確認する
  ここでは、**State** エンティティが **MDS** で作成されたことと、**Supplier** エンティティの **State** 属性が **State** エンティティに依存するドメイン ベースの属性であることを、**マスター データ マネージャー**を使用して確認します。  
  
1.  **マスター データ マネージャー** Web アプリケーションに切り替えます。  
  
2.  上部に表示されている **[SQL Server 2012 マスター データ サービス]** をクリックして、ホーム ページに移動します。  
  
3.  **Suppliers** モデルがオンになっていることを確認し、 **[エクスプローラー]** をクリックします。 **エクスプローラー**が既に開いている場合は、ページを更新します。  
  
4.  マウス カーソルを置く**エンティティ**今後、メニュー バーでは、2 つのエンティティがあります。**サプライヤー**と**状態**します。  
  
     ![州と仕入先にエンティティ メニュー](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-01.jpg "州と仕入先にエンティティ メニュー")  
  
5.  エンティティがまだ開いていない場合は **[State]** をクリックします。  
  
6.  一覧から **[GA]** を選択します。  
  
7.  **[詳細]** ペインの**右ペイン**で **[名前]** を "**Georgia**" に変更し、 **[OK]** をクリックします。  
  
8.  その他の州について前の手順を繰り返します。  
  
    |コード|名前|  
    |----------|----------|  
    |CA|California|  
    |CO|Colorado|  
    |IL|Illinois|  
    |DC|District of Columbia|  
    |FL|Florida|  
    |AL|Alabama|  
    |KY|Kentucky|  
    |MA|Massachusetts|  
    |AZ|Arizona|  
    |MI|Michigan|  
    |MN|Minnesota|  
    |NJ|New Jersey|  
    |NV|Nevada|  
    |NY|New York|  
    |OH|Ohio|  
    |OK|Oklahoma|  
    |スイッチまたは|Oregon|  
    |PA|Pennsylvania|  
    |SC|South Carolina|  
    |KS|Kansas|  
    |TN|Tennessee|  
    |TX|Texas|  
    |UT|Utah|  
    |VA|Virginia|  
    |WA|Washington|  
    |WI|Wisconsin|  
    |HI|Hawaii|  
    |MD|Maryland|  
    |CT|Connecticut|  
  
9. 州のいずれかのエントリを選択し、ツール バーの **[トランザクションの表示]** をクリックします。 先ほど行った更新に関するトランザクションが、トランザクションの一覧に表示されます。  
  
10. **[エンティティ]** メニューにマウス カーソルを合わせ、 **[Supplier]** をクリックします。  
  
11. ここで、 **[State]** フィールドの値は、 **[詳細]** ペインでドロップダウン リストを使用して変更できることに注意してください。 また、左側の一覧と **[詳細]** ペインのドロップダウン リストでは、最初に表示されたコードに続いて中かっこで囲まれた名前が表示されます。 **[詳細]** ペインでは、その他の値も変更できます。  
  
     ![更新されたコードと名前を持つ属性の状態](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-02.jpg "更新されたコードと名前を持つ属性の状態")  
  
## <a name="next-step"></a>次の手順  
 [タスク 7:Excel でマスター データ マネージャーを使用して行った更新を表示](../../2014/tutorials/task-7-viewing-updates-made-using-master-data-manager-in-excel.md)  
  
  
