---
layout: HubPage
hide_bc: true
title: SQL Server のデータベースの設計
description: ビジネス ニーズに最適なデータベースを設計する際に役立つ SQL Server の機能を確認します。
ms.topic: hub-page
ms.prod: sql
author: MashaMSFT
ms.author: mathoma
ms.date: 12/15/2018
featureFlags:
- clicktale
ms.openlocfilehash: c08b067a8c92b7fea32b53cd8b14b7ecc13272d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077241"
---
<div id="main" class="v2">
    <div class="container">
        <ul class="cardsY panelContent featuredContent">
            <li>
                <a href="https://www.microsoft.com/evalcenter/evaluate-sql-server-2019-ctp">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-sql-server.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">SQL Server 2019 (プレビュー) の試用</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/get-azure-sql-vm.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">SQL Server がある仮想マシンの取得</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="/sql/ssms/download-sql-server-management-studio-ssms">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-ssms.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">SQL Server Management Studio のダウンロード</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>              
        </ul>
    </div>
    <div class="container">
        <h1>SQL Server:データベースの設計</h1>
        <ul class="pivots tabLess">
            <li class="pivotItem" style="display: list-item;" data-id="#products">
                <a href="#products" data-linktype="self-bookmark"></a>
                <ul id="products">
                    <li class="panelItem" data-index="0">
                        <a class="singlePanelNavItem selected" href="#products1" data-linktype="self-bookmark"></a>
                        <ul class="cardsD panelContent singlePanelContent" id="products1" style="margin-top: 0px; display: flex;">
                            <li>
                                <a href="/sql/relational-databases/collations/collation-and-unicode-support/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/collation.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>照合順序</h3>
                                                    <p>SQL Server の照合順序により、並べ替え規則、大文字と小文字の区別、およびアクセントの区別のプロパティをデータで利用できるようになります。 char や varchar などの文字データ型に使用する照合順序は、そのデータ型で表すことのできるコード ページおよび対応する文字を指定します。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/databases/databases/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/databases.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>データベース</h3>
                                                    <p>SQL Server のデータベースは、特定の構造化データを格納するテーブルの集合です。 テーブルは一連の行 (レコードまたはタプル) と列 (属性) から構成されます。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> <li>
                                <a href="/sql/relational-databases/blob/filestream-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/filestream.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Filestream</h3>
                                                    <p>Filestream を使用すると、SQL Server ベースのアプリケーションで非構造化データ (ドキュメントやイメージなど) をファイル システムに格納できます。  </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/blob/filetables-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/filetable.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Filetable</h3>
                                                    <p>FileTable により、アプリケーションは、ストレージとデータ管理コンポーネントを統合し、非構造化データおよびメタデータに対する統合 SQL Server サービス (フルテキスト検索、セマンティック検索など) を提供できます。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/graphs/sql-graph-overview/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/sql-graphs.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>グラフ</h3>
                                                    <p>グラフ データベースは、ノード (または頂点) とエッジ (またはリレーションシップ) のコレクションです。 ノードはエンティティ (たとえば人や組織) を表し、エッジはそれが接続する 2 つのノードのリレーションシップ (たとえば好感や友人) を表します。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/hierarchical-data-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/hierarchy-data.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>階層データ</h3>
                                                    <p>階層データは、階層リレーションシップで相互に関連付けられたデータ アイテムのセットとして定義されます。 あるデータ アイテムが別のアイテムの親となる場合は、そこに階層リレーションシップが存在します。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/indexes/indexes/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/indexes.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>インデックス</h3>
                                                    <p>データを編成するために SQL で使用されるさまざまな種類のインデックスの概要です。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/sequence-numbers/sequence-numbers/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/sequence-numbers.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>シーケンス番号</h3>
                                                    <p>シーケンスは、シーケンスが作成された仕様に従って数値のシーケンスを生成するユーザー定義のスキーマ バインド オブジェクトです。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/spatial/spatial-data-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/spatial-data.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>空間データ</h3>
                                                    <p>空間データは、幾何オブジェクトの物理的な位置と形状に関する情報を表します。 それらのオブジェクトは、点の位置である場合もあれば、国、道、湖などのより複雑なオブジェクトである場合もあります。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/stored-procedures/stored-procedures-database-engine/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/stored-procedures.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>ストアド プロシージャ</h3>
                                                    <p>SQL Server のストアド プロシージャは、1 つ以上の Transact-SQL ステートメント、または Microsoft .NET Framework 共通言語ランタイム (CLR) メソッドへの参照のグループです。 プロシージャは、他のプログラミング言語のコンストラクトに似ています。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/tables/tables/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/tables.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>テーブル</h3>
                                                    <p>テーブルは、データベースのすべてのデータを格納するデータベース オブジェクトです。 テーブルでは、スプレッドシートのように、データが論理的に行と列の形式にまとめられます。 各行は一意なレコードを表し、各列はレコードのフィールドを表します。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/track-changes/track-data-changes-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/track-changes.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>変更の追跡</h3>
                                                    <p>データの追跡を可能にする 2 つの機能の概要: 変更データ キャプチャと変更の追跡。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/triggers/logon-triggers/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/triggers.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>トリガー</h3>
                                                    <p>トリガーを使用すると、ログオンなどの特定のアクションや、alter database コマンドに対して自動で応答できます。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/views/views/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/views.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>ビュー</h3>
                                                    <p>ビューとは、クエリによって内容が定義される仮想テーブルです。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>  
                            <li>
                                <a href="/sql/relational-databases/xml/xml-data-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/xml-data.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>XML データ</h3>
                                                    <p>XML データ型、XML インデックス、XML スキーマ コレクションなどを使用して実行できることの概要です。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                                    <li>
                                      <a href="/sql/lp/sql-server/query-data/">
                                          <div class="cardSize">
                                              <div class="cardPadding">
                                                  <div class="card">
                                                      <div class="cardImageOuter">
                                                          <div class="cardImage">
                                                              <img src="media/index/query-data.svg" alt="" /> 
                                                          </div>
                                                      </div>
                                                      <div class="cardText">
                                                          <h3>クエリ データ</h3>
                                                          <p><b>カーソル、シノニム、スクリプト、結合、ユーザー定義関数、フルテキスト検索 </b></p>
                                                      </div>
                                                  </div>
                                              </div>
                                          </div>
                                      </a>
                                    </li>
                        </ul>
                    </li>
                </ul>
            </li>
        </ul>
    </div>
</div>
<div class="container centered pageFooter">
        <h2>情報を共有しましょう</h2>
        <ul class="links">
           <li>
                <a href="https://aka.ms/editsqldocs" data-linktype="external"> 投稿 </a>
            </li>
           <li>
                <a href="https://docs.microsoft.com/sql/sql-server/sql-server-get-help" data-linktype="external"> ヘルプ </a>
            </li>
           <li>
                <a href="https://aka.ms/sqldocsfeedback" data-linktype="external"> フィードバック </a>
            </li>
           <li>
                <a href="https://aka.ms/sqldocsurvey" data-linktype="external"> アンケート </a>
            </li>
           <li>
                <a href="https://cloudblogs.microsoft.com/sqlserver/" data-linktype="external"> ブログ </a>
            </li>
            <li>
                <a href="https://twitter.com/sqldocs" data-linktype="external"> Twitter </a>
            </li>
            <li>
                <a href="https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqldatabaseengine&filter=alltypes&sort=lastpostdesc" data-linktype="external"> MSDN フォーラム </a>
            </li>
            <li>
                <a href="https://feedback.azure.com/forums/908035-sql-server" data-linktype="external"> User Voice </a>
            </li>
        </ul>
    </div>