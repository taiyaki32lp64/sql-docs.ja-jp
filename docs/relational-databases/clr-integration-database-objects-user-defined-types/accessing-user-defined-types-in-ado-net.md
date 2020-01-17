---
title: ADO.NET でのユーザー定義型へのアクセス |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
ms.openlocfilehash: b4bdbf184cc1528b3eb5156173f52dca44aece76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009609"
---
# <a name="accessing-user-defined-types-in-adonet"></a>ADO.NET でのユーザー定義型へのアクセス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  サポートされる言語のいずれかを使用してユーザー定義型 (Udt) が記述された、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 共通言語ランタイム (CLR) 検証可能なコードを生成します。 サポートされる言語には、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# や [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic などがあります。 UDT では、オブジェクトやカスタム データ構造を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに格納できます。 データは、.NET Framework のクラスまたは構造体のパブリック メンバーとして公開され、動作は .NET Framework のクラスまたは構造体のメソッドによって定義されます。 UDT は、テーブルの列定義、[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチの変数、または [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数やストアド プロシージャの引数として使用することができます。  
  
 ADO.NET では、 **System.Data.SqlClient**プロバイダーは、次の方法で Udt を公開します。  
  
-   を通じて、 **System.Data.SqlClient.SqlDataReader**オブジェクトとして。  
  
-   を通じて、 **SqlDataReader**未処理のバイトとして。  
  
-   パラメーターとして、 **System.Data.SqlClient.SqlParameter**オブジェクト。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [UDT データの取得](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 UDT データを取得する方法とパラメーターを指定する方法について説明します。  
  
 [データ アダプターによる UDT 列の更新](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Udt を操作する方法について説明します**データセット**UDT を使用してデータを更新する方法と**Dataadapter**します。  
  
## <a name="see-also"></a>関連項目  
 [CLR ユーザー定義型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
