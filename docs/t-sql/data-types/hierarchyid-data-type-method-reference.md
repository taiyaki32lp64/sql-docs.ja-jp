---
title: hierarchyid (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- hierarchyid
- hierarchyid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Hierarchy data type
- hierarchyid data type
ms.assetid: 69b756e0-a1df-45b3-8a24-6ded8658aefe
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 122630048b7e4ff9cef34c49bfde68177020630f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077911"
---
# <a name="hierarchyid-data-type-method-reference"></a>hierarchyid データ型メソッド リファレンス
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**hierarchyid** データ型は可変長のシステム データ型です。 **hierarchyid** は、階層内の位置を表すために使用します。 **hierarchyid** 型の列が自動的にツリーを表すことはありません。 行と行の間に必要なリレーションシップが反映されるよう、 **hierarchyid** 値を生成して割り当てるのは、アプリケーションの役割です。
  
値、 **hierarchyid** データ型は、ツリー階層内の位置を表します。 値を **hierarchyid** 、次のプロパティがあります。
  
-   非常にコンパクト  
     *n* 個のノードを持つツリー内の、1 つのノードを表すために必要な平均ビット数は、平均ファンアウト (ノードあたりの子の平均数) によって決まります。 ファンアウトが小さい場合 (0 ～ 7)、サイズは約 6\*logA*n* ビットです (A は平均ファンアウト)。 平均ファンアウトが 6 レベルで、100,000 人から成る組織階層の場合、1 つのノードには約 38 ビットが必要です。 格納時には、これが 40 ビット (5 バイト) に切り上げられます。  
-   深さ優先順で比較  
     **a** と **b** の 2 つの **hierarchyid** 値がある場合、**a<b** は、ツリーの深さ優先検査において a が b の前に来ることを意味します。 インデックス **hierarchyid** に深さ優先順では、データ型があり、深さ優先検査で近接ノードは互いに近い格納します。 たとえば、あるレコードの子は、そのレコードに隣接して格納されます。 詳しくは、「[階層データ &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)」をご覧ください。  
-   任意の挿入および削除のサポート  
     [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) メソッドを使用すると、指定したノードの右側や左側、または任意の 2 つの兄弟間に、いつでも兄弟を生成できます。 階層に対して任意の数のノードを挿入または削除しても、比較の特性は維持されます。 ほとんどの挿入や削除では、コンパクトさも維持されます。 ただし、2 ノード間に挿入した場合は、hierarchyid 値のコンパクトさがやや失われます。  
-   **hierarchyid** 型で使用されるエンコーディングは 892 バイトに制限されます。 したがって、表現のレベルが多すぎて 892 バイトに収まらないノードについては、**hierarchyid** 型で表すことができません。  
  
**hierarchyid** 型は、CLR クライアントで **SqlHierarchyId** データ型として利用できます。
  
## <a name="remarks"></a>Remarks  
**hierarchyid** 型は、ツリーのルートからノードまでのパスをエンコードすることで、階層ツリーの 1 つのノードに関する情報を論理的にエンコードします。 このようなパスは、ルートの後にアクセスされたすべての子の一連のノード ラベルとして論理的に表されます。 この表現はスラッシュによって開始されます。ルートのみを表すパスは、単一スラッシュで表されます。 ルートの下のレベルの各ラベルは、ドットで区切られた一連の整数としてエンコードされます。 子と子の比較は、ドットで区切られた一連の整数を辞書順で比較することにより行われます。 各レベルの後ろには、スラッシュが続きます。 したがって、スラッシュは親と子を区切ります。 たとえば、次に示すのは、長さがそれぞれ 1、2、2、3、3 レベルの有効な **hierarchyid** パスです。
  
-   /  
  
-   /1/  
  
-   /0.3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
ノードは、任意の位置に挿入できます。 **/1/2/** の後ろで、かつ **/1/3/** の前に挿入されたノードは、 **/1/2.5/** として表されます。 0 の前に挿入されたノードの論理表現は、負の値となります。 たとえば、 **/1/1/** の前に位置するノードは、 **/1/-1/** として表されます。 ノードに先頭のゼロを付けることはできません。 たとえば、 **/1/1.1/** は有効ですが、 **/1/1.01/** は無効です。 エラーを回避するには、[GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) メソッドを使用してノードを挿入します。
  
## <a name="data-type-conversion"></a>データ型の変換
**hierarchyid** データ型は、次のように他のデータ型に変換できます。
-   **hierarchyid** 値を **nvarchar(4000)** データ型として論理表現に変換するには、[ToString()](../../t-sql/data-types/tostring-database-engine.md) メソッドを使用します。  
-   **hierarchyid** を **varbinary** に変換するには、[Read ()](../../t-sql/data-types/read-database-engine.md) と [Write ()](../../t-sql/data-types/write-database-engine.md) を使います。  
-   SOAP 経由で **hierarchyid** パラメーターを送信するには、最初にパラメーターを文字列としてキャストします。  
  
## <a name="upgrading-databases"></a>データベースのアップグレード
データベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードすると、新しいアセンブリおよび **hierarchyid** データ型が自動的にインストールされます。 アップグレード アドバイザーのルールにより、競合する名前を持つユーザー型またはアセンブリが検出されます。 アップグレード アドバイザーは、次のいずれかの方法によって、競合するアセンブリの名前の変更を推奨します。2 つの方法とは、競合する型の名前を変更するか、または 2 つの部分から構成される名前をコード内で使用して既存のユーザー型を参照するかのどちらかです。
  
データベースのアップグレード時に競合する名前を持つユーザー アセンブリが検出されると、このアセンブリの名前が自動的に変更され、データベースが問題のあるモードになります。
  
アップグレード時に競合する名前を持つユーザー型が検出された場合、特別な処理は実行されません。 アップグレード後は、古いユーザー型と新しいシステム型の両方が存在することになります。 ユーザー型は、2 つの部分から構成される名前を介してのみ使用できます。
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>レプリケートされたテーブルでの hierarchyid 列の使用
**hierarchyid** 型の列は、任意のレプリケートされたテーブルで使用できます。 アプリケーションの要件は、レプリケーション方法や (単方向または双方向)、使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンによって異なります。
  
### <a name="one-directional-replication"></a>単方向レプリケーション
単方向レプリケーションには、サブスクライバー側で変更が行われないスナップショット レプリケーション、トランザクション レプリケーション、およびマージ レプリケーションが含まれます。 **hierarchyid** 列が単方向レプリケーションとどのように連携するかは、サブスクライバーが実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンによって異なります。
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] パブリッシャーは、**hierarchyid** 列を [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サブスクライバーにレプリケートできます。特別な注意は必要ありません。  
-   [!INCLUDE[ssEW](../../includes/ssew-md.md)] または前バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているサブスクライバーにレプリケートするには、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] パブリッシャーは、**hierarchyid** 列を変換する必要があります。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] および前バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**hierarchyid** 列がサポートされません。 このどちらかのバージョンを使用している場合でも、サブスクライバーにデータをレプリケートすることは可能です。 そのためには、互換性のあるデータ型に列を変換できるように、スキーマ オプションまたはパブリケーションの互換性レベル (マージ レプリケーションの場合) を設定する必要があります。  
  
どちらのシナリオでも、列のフィルター選択はサポートされています。 これには、**hierarchyid** 列をフィルターで除外する処理が含まれます。 行のフィルター選択は、フィルターに **hierarchyid** 列が含まれない限りサポートされます。
  
### <a name="bi-directional-replication"></a>双方向レプリケーション
双方向レプリケーションには、サブスクライバー側で変更が行われる、更新サブスクリプションを使用したトランザクション レプリケーション、ピア ツー ピア トランザクション レプリケーション、およびマージ レプリケーションが含まれます。 レプリケーションを実行するには、**hierarchyid** 列を持つテーブルを双方向レプリケーション用に構成する必要があります。 以下の要件および考慮事項に注意してください。
-   パブリッシャーおよびすべてのサブスクライバーで [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を実行している必要があります。  
-   レプリケーションでは、データはバイトとしてレプリケートされます。階層の整合性を保証するための検証は行われません。  
-   レプリケート元 (サブスクライバーまたはパブリッシャー) で変更が加えられた階層は、レプリケート先にレプリケートするときに維持されません。  
-   **hierarchyid** 列のハッシュ値は、生成元のデータベースに固有です。 したがって、パブリッシャー側とサブスクライバー側とで同じ値が生成され、異なる行に適用される可能性があります。 レプリケーションではこの条件のチェックは行われません。また、IDENTITY 列に対して用意されているような値を区切るための組み込みの手段は、**hierarchyid** 列に対しては用意されていません。 アプリケーションでは、このような検出されない競合を避けるために、制約またはその他のメカニズムを使用する必要があります。  
-   サブスクライバー側で挿入された行が孤立する場合があります。 挿入された行の親の行がパブリッシャー側で削除されている可能性があります。 その結果、サブスクライバーの行がパブリッシャー側で挿入されたときに検出されない競合が発生します。  
-   列フィルターでは、NULL 値が許容されない **hierarchyid** 列を除外できません。パブリッシャー側の **hierarchyid** 列には既定値がないので、サブスクライバーからの挿入は失敗します。  
-   行のフィルター選択は、フィルターに **hierarchyid** 列が含まれない限りサポートされます。  
  
## <a name="see-also"></a>参照
[階層データ (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid データ型メソッド リファレンス](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
