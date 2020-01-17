---
title: PowerPivot から復元 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f90ea08269e79e57c623af41fc2f0fbc09e2fb42
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066637"
---
# <a name="restore-from-powerpivot"></a>PowerPivot から復元
  SQL Server Management Studio の PowerPivot から復元機能を使って、テーブル モードで実行されている Analysis Services インスタンス上に新しいテーブル モデル データベースを作成したり、PowerPivot ブック (.xlsx) から既存のデータベースに復元したりできます。  
  
> [!NOTE]  
>  SQL Server Data Tools の PowerPivot からのインポート プロジェクト テンプレートが同様の機能を提供します。 詳細については、次を参照してください。 [PowerPivot からインポート&#40;SSAS 表形式&#41;](import-from-power-pivot-ssas-tabular.md)します。  
  
 PowerPivot から復元機能を使用する場合、次の点に注意してください。  
  
-   PowerPivot から復元機能を使用するには、サーバー管理者ロールのメンバーとして Analysis Services インスタンスにログオンしている必要があります。  
  
-   Analysis Services インスタンス サービス アカウントには、復元するブック ファイルの読み取り権限が必要です。  
  
-   既定では、PowerPivot からデータベースを復元する場合は、テーブル モデル データベースのデータ ソースの権限借用情報プロパティは既定値に設定されており、Analysis Services インスタンス サービス アカウントを指定します。 権限借用の資格情報をデータベース プロパティの Windows ユーザー アカウントに変更することをお勧めします。 詳細については、「[権限借用 (SSAS テーブル)](impersonation-ssas-tabular.md)」を参照してください。  
  
-   PowerPivot データ モデルのデータは、Analysis Services インスタンス上の既存または新規のテーブル モデル データベースにコピーされます。 PowerPivot ブックにリンク テーブルが含まれている場合は、新規テーブルを使用して作成されたテーブルのように、データ ソースを使用せずにテーブルとして再作成されます。  
  
### <a name="to-restore-from-powerpivot"></a>PowerPivot から復元するには  
  
1.  SSMS で、復元する Active Directory インスタンスで右クリック**データベース**、 をクリックし、 **PowerPivot から復元**します。  
  
2.  **PowerPivot から復元** ダイアログ ボックスで**復元元**の**バックアップ ファイル**、 をクリックして**参照**、.abf または .xslx を選択します復元するファイル。  
  
3.  **[復元対象]** の **[データベースの復元]** で、新しいデータベースまたは既存のデータベースの名前を入力します。 名前を指定しない場合は、ブック名が使用されます。  
  
4.  **[ストレージの場所]** で、 **[参照]** をクリックし、データベースを格納する場所を選択します。  
  
5.  **[オプション]** で、 **[セキュリティ情報を含める]** チェック ボックスをオンのままにします。 PowerPivot ブックから復元する場合は、この設定は適用されません。  
  
## <a name="see-also"></a>参照  
 [表形式モデルのデータベース (SSAS 表形式)](tabular-model-databases-ssas-tabular.md)   
 [PowerPivot からインポート&#40;SSAS 表形式&#41;](import-from-power-pivot-ssas-tabular.md)  
  
  
