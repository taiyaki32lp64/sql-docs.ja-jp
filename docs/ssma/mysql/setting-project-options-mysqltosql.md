---
title: プロジェクト オプション (MySQLToSQL) の設定 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 346fcd2ea7f83abcb9a5c23a22cb0eded76acc0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944687"
---
# <a name="setting-project-options-mysqltosql"></a>プロジェクト オプションの設定 (MySQLToSQL)
SSMA プロジェクトごとに、プロジェクト レベルのオプションを設定することができます。 これらのオプションは、オブジェクトに変換する方法、データを移行する方法、およびソースのデータ型が対象のデータ型にマップする方法を指定します。  SQL Server または SQL Azure にオブジェクトを変換するか、または SQL Server または SQL Azure にデータを移行する前に、構成オプションが、プロジェクトの適切なことを確認します。  
  
SSMA では、すべてのプロジェクトの既定のオプションを構成できます。 これらのオプションは、作成した新しいプロジェクトに適用されます。 各プロジェクトのオプションをカスタマイズできます。  
  
## <a name="configuration-options-and-modes"></a>構成オプションとモード  
SSMA では、プロジェクトの設定の 5 つのセットがあります。  
  
-   プロジェクト情報  
  
-   [全般]\(変換、移行、および SQL Azure)  
  
-   Synchronization  
  
-   GUI  
  
-   型のマッピング  
  
4 つの方法では、プロジェクトの設定を構成できます。  
  
-   既定  
  
-   オプティミスティック  
  
-   [完全]  
  
-   カスタム  
  
ほとんどのユーザーには、既定のモードを使用することをお勧めします。 オプティミスティック モードでは、現在の MySQL の構文の詳細を保持しが読みやすくします。 ただし、現在の構文を維持することができない正確です。 MySQL の構文は、同等の SQL Server または SQL Azure の構文に変換する必要があります、完全なモードは最も包括的な変換を実行します。 結果のコードでは、ただし、場合があります読みにくくします。 カスタム モードでは、オプションを設定できます。  
  
設定と各モードで、設定を適用する方法の詳細については、次のトピックを参照してください。  
  
-   [プロジェクトの設定&#40;変換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [プロジェクトの設定&#40;移行&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [プロジェクトの設定 (GUI) (SSMA Common)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [プロジェクトの設定&#40;の種類のマッピング&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [プロジェクトの設定&#40;同期&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [プロジェクトの設定&#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>プロジェクト オプションの設定  
SSMA では、すべてのプロジェクトの既定の設定を構成できます。 これらの設定は SSMA の構成ファイルに保存し、作成した新しいプロジェクトに適用します。  
  
**既定のプロジェクトのオプションを設定するには**  
  
1.  **ツール** メニューのをクリックして**プロジェクト設定の既定の**します。  
  
2.  **プロジェクト設定の既定の**ダイアログ ボックスで、次の手順のいずれかを使用します。  
  
    1.  設定は、表示/から変更する必要を移行プロジェクトの種類を選択**移行ターゲット バージョン**ドロップダウンで、**全般**を選択し、左側のウィンドウの下部にある**変換または移行または SQL Azure**オプション。  
  
    2.  定義済みのモードを選択する**既定**、 **Optimistic**、または**完全**から、**モード** ボックスの一覧。  
  
    3.  カスタム設定を指定するには、選択するか、新しい設定または値を入力します。  
  
3.  クリックして**OK**設定を保存します。  
  
現在のプロジェクトの設定をカスタマイズすることもできます。 設定は、現在のプロジェクト ファイルに保存されます。  
  
**現在のプロジェクトの設定をカスタマイズするには**  
  
1.  **ツール** メニューのをクリックして**ProjectSettings**します。  
  
2.  **ProjectSettings**ダイアログ ボックスで、次の手順のいずれかを使用します。  
  
    1.  定義済みのモードを選択する**既定**、 **Optimistic**、または**完全**から、**モード** ボックスの一覧。  
  
    2.  カスタム モードを指定するには、次のように選択します。**カスタム**から、**モード** ボックスの一覧。 適切なプロジェクト設定を選択します。  
  
3.  クリックして**OK**設定を保存します。  
  
## <a name="next-step"></a>次の手順  
移行の次の手順は、プロジェクトのニーズによって異なります。  
  
-   ソースとターゲットのデータ型のマッピングをカスタマイズするを参照してください[マッピング MySQL および SQL Server データ型&#40;MySQLToSQL。&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   それ以外の場合、SQL Server または SQL Azure のオブジェクトの定義に MySQL データベースのオブジェクトの定義に変換できます。 詳細については、次を参照してください[MySQL データベースを変換する&#40;MySQLToSQL。&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>関連項目  
[MySQL と SQL Server データ型のマッピング&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
