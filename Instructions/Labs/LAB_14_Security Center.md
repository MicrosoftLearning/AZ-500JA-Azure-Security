---
lab:
    title: '14 - Azure Security Center'
    module: 'モジュール 04 - セキュリティ操作の管理'
---

# 課題 14: Azure Security Center
# 受講生用ラボ マニュアル

## ラボのシナリオ

ベースの環境の概念実証を作成するように求められました。具体的には、次のことを行います。

- 仮想マシンを監視するように Security Center を構成します。
- 仮想マシンの Security Center の推奨事項を確認します。
- ゲスト構成と Just In Time VM アクセスの推奨事項を実装します。 
- セキュア スコアを使用して、より安全なインフラストラクチャの作成に向けた進捗状況を判断する方法を確認します。

> このラボのすべてのリソースについて、**米国東部** リージョンを使用しています。クラスに使用する地域であることを講師に確認します。 

## ラボの目的

このラボでは、次の演習を行います。

- 演習 1: Security Center を実装する

### 演習 1: Security Center を実装する

この演習では、次のタスクを行います。

- タスク 1: Security Center を構成する
- タスク 2: ゲスト構成拡張機能をインストールするために Security Center の推奨事項を実装する
- タスク 3: Just In Time VM アクセスを有効にするために Security Center の推奨事項を実装する

#### タスク 1: Security Center を構成する

このタスクでは、Security Center をオンボードし、構成します。

1. Azure portal **`https://portal.azure.com/`** にサインインします。

    >**注意**: このラボで使用している Azure サブスクリプションで所有者ロールまたは共同作成者ロールを持つアカウントを使用して Azure ポータルにサインインします。

1. Azure portal の Azure portal ページの上部にある「**リソース、サービス、ドキュメントの検索**」 テキスト ボックスで、「**セキュリティ センター**」と入力し、**Enter** キーを押します。

1. 「**セキュリティ センター \| はじめに**」 ブレードで 、「**エージェントのインストール**」 をクリックします。
     
1. 「**セキュリティ センター \| 概要**」 ブレードの左側の垂直メニューの 「**管理**」 セクションで、「**価格と設定**」 をクリックします。

1. 「**セキュリティ センター \| 価格と設定**」 ブレードで、サブスクリプションを表すエントリをクリックし、「**設定 \| Azure Defenderのプラン**」 ブレードで、「**Azure Defender オン**」 が選択されていることを確認します。 

    >**注意**: Azure Defender レベルの一部として使用できるすべての機能を確認し、各リソースの種類で Azure Defender がオンになっていることを確認します。 

1. 変更を行った場合は、「**保存**」 をクリックします。

1. 「**設定 \| Azure Defender プラン**」ブレードの左側にある垂直メニューバーで、「**自動プロビジョニング**」 をクリックします。

1. 「**設定 \| 自動プロビジョニング**」 ブレードで、最初の項目である 「**Azure VM の Log Analytics エージェント**」 の**状態**が**オン**に設定されていることを確認します。 

1. 「**設定 \| 自動プロビジョニング**」 ブレードで、最初の項目である 「**Azure VM の Log Analytics エージェント**」 で、「**構成**」 列の 「**構成の編集**」 リンクをクリックします。 

1. 「**拡張機能のデプロイ構成**」 ブレードの 「**ワークスペースの構成**」 セクションで、「**Azure VM を別のワークスペースに接続する**」 オプションを選択し、ドロップダウン リストで、前のラボで作成した Log Analytics ワークスペースを選択します。 

1. 「**拡張機能のデプロイ構成**」 ブレードで、「**既存および新しいVM**」をクリックし、「**適用**」をクリックします。

1. 「**設定 \| 自動プロビジョニング**」 ブレードに戻り、左側の垂直メニューで、「**ワークフローの自動化**」をクリックします。

1. 「**設定 \| ワークフローの自動化**」 ブレードで 「**+ ワークフローの自動化の追加**」 をクリックし、ます。

1. 「**ワークフロー自動化の追加**」 ブレードで、使用可能な設定を確認します。 

    >**注意**: 脅威検出アラートおよび Security Center の推奨事項に基づいてアクションをトリガーできます。Logic Apps に基づいてアクションを構成することもできます。 

1. 「**ワークフロー自動化の追加**」 ブレードで、「**キャンセル**」 をクリックします。

    >**注意**: セキュリティ センターは、システムの更新状況、OS セキュリティ構成、エンドポイント保護など、仮想マシンに関する多くの洞察を提供します。

#### タスク 2: セキュリティ センター 推奨事項を導入します。

このタスクでは、仮想マシンにエンドポイント保護をインストールするための セキュリティ センターの推奨事項を実装します。 

1. Azure portal で、「**セキュリティ センター \| 概要**」 ブレードに移動します。 

1. 「**セキュリティ センター \| 概要**」 ブレードで、「**全体のセキュア スコア**」 タイルを確認します。

    >**注意**: あれば、現在のスコアを記録します。

1. 「**セキュリティ センター \| 概要**」 ブレードで、「**推奨事項を表示する**」 をクリックします。

1. 「**推奨事項**」ブレードで、「Endpoint Protection を有効にする」を展開し、「**仮想マシンに Endpoint Protection ソリューションをインストールする**」 エントリをクリックします。

1. **myVM** エントリを選択します。

    >**注意**: エントリが表示されるまで数分待ってから、ブラウザ ページを更新する必要がある場合があります。
    
1. 「**1 VM へインストール**」をクリックします。「**Microsoft Antimalware**」 を選択し、次に 「**作成**」 > 「**OK**」 を選択します

    >**注意**: ツール バーの 「**通知**」 アイコンをクリックして 「**通知**」 ブレードを表示して、インストールの進行状況を監視します。 

    >**注意**: セキュリティ センターは、仮想マシンを自動的に再スキャンします。これは、セキュア スコアの増加によって反映されます。

    >**注意**: インストールが完了するのを待たず、代わりに次のタスクに進みます。 

#### タスク 3: Just In Time VM アクセスを有効にするために Security Center の推奨事項を実装する

このタスクでは、仮想マシンでの Just In Time VM アクセスを有効にする Security Center の推奨事項を実装します。 

1. Azure portal で、「**セキュリティ センター \| Azure Defender**」 ブレードに移動します。 

1. 「**高度な保護**」項目の「**Just-In-Time VM アクセス**」をクリックし、「**仮想マシン**」項目の「**構成されていません**」タブを選択して、「**myVM**」 エントリをクリックします。

1. 「**1台の VM で JIT を有効にする**」 を選択します。

1. 「**JIT VM アクセス構成**」 ブレードの、ポート **22** を参照する行の右端で、省略記号ボタンをクリックしてから、「**削除**」 をクリックします。

1. 「**JIT VM アクセス構成**」 ブレードで、「**保存**」 をクリックします。

    >**注意**: ツールバーの 「**通知**」 アイコンをクリックして、「**通知**」 ブレードを表示して、構成の進行状況を監視します。 

    >**注意**: このラボでの推奨事項の実装がセキュア スコアに反映されるまでに時間がかかる場合があります。セキュア スコアを定期的にチェックして、これらの機能の実装による影響を判断します。 

> 結果: セキュリティ センターにオンボードし、仮想マシンの推奨事項を実装しています。 


>**注意**: Azure Sentinel ラボで必要ですので、リソースをこのラボから削除しないでください。
