---
title: Sybase ASE と SQL Server データ型 (SybaseToSQL) のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 79313d2344f6feb978a064f3fbd92e1f7bc7dce5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028893"
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Sybase ASE と SQL Server データ型とのマッピング (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) データベースの型が異なる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベースの型。 ASE データベース オブジェクトを変換する際に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のオブジェクトを ASE からのデータ型にマップする方法を指定する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 既定のデータ型マッピングをそのまま使用できるまたはマッピングをカスタマイズするには、次のセクションで示すようにします。  
  
## <a name="default-mappings"></a>既定のマッピング  
SSMA では、データ型マッピングの既定セットがあります。 既定のマッピングの一覧で、次を参照してください。[プロジェクト設定&#40;型マッピングの&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)します。  
  
## <a name="type-mapping-inheritance"></a>継承のマッピングの種類  
プロジェクト レベル、オブジェクトのカテゴリ レベル (などすべてストアド プロシージャの場合)、またはオブジェクト レベルでは、型マッピングをカスタマイズすることができます。 設定は、下位のレベルでオーバーライドされない限りより高いレベルから継承されます。 たとえば、マップする**smallmoney**に**money**カテゴリ レベルのオブジェクトまたはオブジェクト レベルでマッピングをカスタマイズしない限り、このマッピング プロジェクト レベルでは、プロジェクト内のすべてのオブジェクトが使用されます。  
  
表示すると、**型マッピングの**SSMA、バック グラウンドのタブが色分けされ、どの型のマッピングは、継承を表示します。 型マッピングの背景は黄色、継承された型のマッピング、およびマッピングが現在のレベルで指定された任意の空白です。  
  
## <a name="customizing-data-type-mappings"></a>データ型マッピングのカスタマイズ  
次の手順では、プロジェクト、データベース、またはオブジェクト レベルでのデータ型にマップする方法を示します。  
  
**データ型をマップするには**  
  
1.  プロジェクト全体のデータ型マッピングをカスタマイズするには、開く、**プロジェクト設定** ダイアログ ボックス。  
  
    1.  **ツール**メニューの **プロジェクト設定**します。  
  
    2.  左側のウィンドウで次のように選択します。**型マッピングの**します。  
  
        右側のウィンドウでは、型マッピングの表とボタンが表示されます。  
  
    または、データの種類をカスタマイズするデータベース、テーブル、ビュー、またはストアド プロシージャのレベルにあるマッピング オブジェクトのデータベース、またはオブジェクト カテゴリの場合は、Sybase メタデータ エクスプ ローラーで選択。  
  
    1.  Sybase メタデータ エクスプ ローラーでフォルダーまたはカスタマイズするオブジェクトを選択します。  
  
    2.  右側のウィンドウでをクリックして、**型マッピングの**タブ。  
  
2.  新しいマッピングを追加するには、次の操作を行います。  
  
    1.  **[追加]** をクリックします。  
  
    2.  **ソースの種類**ASE のデータ型にマップを選択します。  
  
    3.  型には、長さが必要とする場合は、内でマッピングの最小限のデータ長を指定、**から**ボックスし、のマッピングの最大データ長を指定、**に**ボックス。  
  
        これにより、同じデータ型の値が小さくなりより大きなデータのマッピングをカスタマイズできます。  
  
    4.  **ターゲットの種類**、ターゲットを選択して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のデータ型。  
  
        一部の種類には、対象のデータ型の長さが必要です。 必要な場合は、入力内の新しいデータ長、**置き換えます**ボックス。  
  
    5.  **[OK]** をクリックします。  
  
3.  データ型のマッピングを編集するには、次の操作を行います。  
  
    1.  **[編集]** をクリックします。  
  
    2.  **ソースの種類**ASE のデータ型にマップを選択します。  
  
    3.  型には、長さが必要とする場合は、内でマッピングの最小限のデータ長を指定、**から**ボックスし、のマッピングの最大データ長を指定、**に**ボックス。  
  
        これにより、同じデータ型の値が小さくなりより大きなデータのマッピングをカスタマイズできます。  
  
    4.  **ターゲットの種類**、ターゲットを選択して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のデータ型。  
  
        一部の種類には、対象のデータ型の長さが必要です。 必要な場合は、入力内の新しいデータ長、**で置き換えます**ボックスをクリックして **[ok]** 。  
  
4.  カスタム データ型のマッピングを削除するには、次の操作を行います。  
  
    1.  削除するデータ型マッピングを格納する型マッピングの一覧で、行を選択します。  
  
    2.  **[削除]** をクリックします。  
  
        継承のマッピングを削除することはできません。 ただし、継承のマッピングは、特定のオブジェクトまたはオブジェクト カテゴリのカスタム マッピングによって上書きされます。  
  
## <a name="next-steps"></a>次の手順  
移行プロセスの次の手順は、いずれかに[評価レポートを作成する](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)または[変換 Sybase ASE データベース オブジェクトを SQL Server または SQL Azure の構文を](converting-sybase-ase-database-objects-sybasetosql.md)します。 評価レポートを作成する場合、Sybase ASE オブジェクトは、評価時に自動的に変換されます。  
  
## <a name="see-also"></a>参照  
[SQL Server - Azure SQL DB への Sybase ASE データベース移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
