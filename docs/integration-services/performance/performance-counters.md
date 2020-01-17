---
title: パフォーマンス カウンター | Microsoft Docs
ms.custom: supportability
ms.date: 08/27/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], performance counters
- performance counters [Integration Services]
- data flow [Integration Services], performance
- counters [Integration Services]
- data flow engine [Integration Services]
ms.assetid: 11e17f4e-72ed-44d7-a71d-a68937a78e4c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 890bd202912cea88491acd79906c873c44e53658
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71282620"
---
# <a name="performance-counters"></a>パフォーマンス カウンター

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、データ フロー エンジンのパフォーマンスを監視するために使用できるパフォーマンス カウンターのセットがインストールされます。 たとえば、"Buffers spooled" カウンターを調べると、パッケージの実行中にデータ バッファーがディスクに一時的に書き込まれているかどうかを判断できます。 このスワップは、パフォーマンスを低下させると共に、コンピューターのメモリが不足していることを示しています。  
  
> **注:** [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を実行するコンピューターに [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]をインストールした後、コンピューターを [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]にアップグレードすると、アップグレード プロセスにより [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のパフォーマンス カウンターがコンピューターから削除されます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のパフォーマンス カウンターをコンピューターに復元するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップを修復モードで実行してください。  
  
 次の表では、パフォーマンス カウンターについて説明します。  
  
|パフォーマンス カウンター|[説明]|  
|-------------------------|-----------------|  
|BLOB bytes read|データ フロー エンジンがすべてのソースから読み取ったバイナリ ラージ オブジェクト (BLOB) データのバイト数。|  
|BLOB bytes written|データ フロー エンジンがすべての出力先に書き込んだ BLOB データのバイト数。|  
|BLOB files in use|データ フロー エンジンがスプールのために現在使用している BLOB ファイル数。|  
|Buffer memory|使用中のメモリの量。 この数値には物理メモリと仮想メモリの両方が含まれている可能性があります。 数値が物理メモリ容量より大きい場合、メモリ スワップが増加していることを表す **Buffers Spooled** の数も増加します。 メモリ スワップが増加すると、データ フロー エンジンのパフォーマンスが低下します。|  
|Buffers in use|すべてのデータ フロー コンポーネントおよびデータ フロー エンジンが現在使用している、すべての種類のバッファー オブジェクト数。|  
|Buffers Spooled|ディスクに現在書き込まれているバッファー数。 データ フロー エンジンが使用する物理メモリが不足している場合、現在使用されていないバッファーはディスクに書き込まれ、必要になった時点で再読み込みされます。|  
|Flat buffer memory|すべてのフラット バッファーが使用するメモリ総量 (バイト単位)。 フラット バッファーはコンポーネントがデータの格納に使用するメモリ ブロックです。 フラット バッファーはバイト単位でアクセスできる大きなブロックです。|  
|Flat buffers in use|データ フロー エンジンが使用するフラット バッファー数。 フラット バッファーはすべてプライベート バッファーです。|  
|Private buffer memory|すべてのプライベート バッファーが使用しているメモリ総量。 データ フロー エンジンがデータ フローをサポートするために作成した場合、バッファーはプライベートではありません。 プライベート バッファーは、変換が一時作業のためだけに使用するバッファーです。 たとえば、集計変換は作業のためにプライベート バッファーを使用します。|  
|Private buffers in use|変換が使用するバッファー数。|  
|Rows read|ソースが生成した行数。 この数値には、参照変換が参照テーブルから読み込む行は含まれません。|  
|Rows written|出力先に出力された行数。 この数値には、出力先データ ストアに書き込まれた行は含まれません。|  
  
 Microsoft 管理コンソール (MMC) のパフォーマンス スナップインを使用して、パフォーマンス カウンターの値を取得するログを作成します。  
  
 パフォーマンスを向上させる方法については、「 [データ フロー パフォーマンス機能](../../integration-services/data-flow/data-flow-performance-features.md)」を参照してください。  
  
## <a name="obtain-performance-counter-statistics"></a>パフォーマンス カウンター統計の取得  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置された [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトについて、[dm_execution_performance_counters (SSISDB データベース)](../../integration-services/functions-dm-execution-performance-counters.md) 関数を使用してパフォーマンス カウンター統計を取得できます。  
  
 次の例では、ID が 34 である処理中の実行の統計を関数で返します。  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
 次の例では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーで処理中のすべての実行の統計を関数で返します。  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
> **重要!!** メンバーである場合、 **ssis_admin** データベース ロール、実行中のすべての実行のパフォーマンス統計が返されます。  メンバーでない場合、 **ssis_admin** データベース ロール、実行中に、アクセス許可を参照する実行のパフォーマンス統計が返されます。  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   codeplex.com のツール ([Business Intelligence Development Studio のための SSIS パフォーマンス ビジュアライゼーション (CodePlex Project)](https://go.microsoft.com/fwlink/?LinkId=146626))  
  
-   msdn.microsoft.com のビデオ ([社内の SSIS パッケージのパフォーマンスの測定と理解 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=150497))  
  
-   support.microsoft.com のサポート技術情報 ( [Windows Server 2008 へのアップグレード後にパフォーマンス モニターで SSIS パフォーマンス カウンターが使用できなくなる](https://go.microsoft.com/fwlink/?LinkId=235319))  

## <a name="add-a-log-for-data-flow-performance-counters"></a>データ フロー パフォーマンス カウンターのログを追加する
  この手順では、データ フロー エンジンによって提供されるパフォーマンス カウンターのログを追加する方法について説明します。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を実行するコンピューターに [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]をインストールした後、コンピューターを [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]にアップグレードすると、アップグレード プロセスにより [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のパフォーマンス カウンターがコンピューターから削除されます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のパフォーマンス カウンターをコンピューターに復元するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップを修復モードで実行してください。  
  
### <a name="to-add-logging-of-performance-counters"></a>パフォーマンス カウンターのログを追加するには  
  
1.  **[コントロール パネル]** で、クラシック表示を使用している場合は **[管理ツール]** をクリックします。 カテゴリ表示を使用している場合は、 **[パフォーマンスとメンテナンス]** をクリックしてから **[管理ツール]** をクリックします。  
  
2.  **[パフォーマンス]** をクリックします。  
  
3.  **[パフォーマンス]** ダイアログ ボックスで、 **[パフォーマンス ログと警告]** を展開して、 **[カウンター ログ]** を右クリックし、 **[新しいログの設定]** をクリックします。 ログの名前を入力します。 たとえば、「 **MyLog**」のように入力します。  
  
4.  **[OK]** をクリックします。  
  
5.  **[MyLog]** ダイアログ ボックスで、 **[カウンターの追加]** をクリックします。  
  
6.  ローカル コンピューターのパフォーマンス カウンターを記録するには、 **[ローカル コンピューターのカウンターを使う]** をオンにします。指定したコンピューターのパフォーマンス カウンターを記録するには、 **[次のコンピューターからカウンターを選ぶ]** をオンにし、一覧からコンピューターを選択します。  
  
7.  **[カウンターの追加]** ダイアログ ボックスで、 **[パフォーマンス オブジェクト]** 一覧の **[SQL Server:SSIS Pipeline]** をクリックします。  
  
8.  パフォーマンス カウンターを選択するには、次のいずれかの操作を行います。  
  
    -   すべてのパフォーマンス カウンターを記録する場合は、 **[すべてのカウンター]** をクリックします。  
  
    -   **[一覧からカウンターを選ぶ]** をオンにし、使用するパフォーマンス カウンターを選択します。  
  
9. **[追加]** をクリックします。  
  
10. **[閉じる]** をクリックします。  
  
11. **[MyLog]** ダイアログ ボックスの **[カウンター]** 一覧で、ログ パフォーマンス カウンターの一覧を確認します。  
  
12. カウンターを追加するには、手順 5. ～ 10. を繰り返します。  
  
13. **[OK]** をクリックします。  
  
    > [!NOTE]  
    >  [パフォーマンス ログと警告] サービスは、Administrators グループのメンバーであるローカル アカウントまたはドメイン アカウントを使用して起動する必要があります。  

## <a name="see-also"></a>参照  
 [プロジェクトとパッケージの実行](../packages/run-integration-services-ssis-packages.md) [Integration Services パッケージによって記録されたイベント](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
