---
aliases:
- /ja/synthetics/browser_check
- /ja/synthetics/browser_test
description: 特定の場所からユーザー操作をシミュレートして監視します。
further_reading:
- link: https://www.datadoghq.com/blog/browser-tests/
  tag: ブログ
  text: ブラウザテストによるユーザーエクスペリエンスの監視
- link: https://learn.datadoghq.com/course/view.php?id=39
  tag: ラーニングセンター
  text: Synthetic テストの紹介
- link: /getting_started/synthetics/browser_test
  tag: Documentation
  text: ブラウザテストの概要
- link: https://www.datadoghq.com/blog/test-creation-best-practices/
  tag: ブログ
  text: エンドツーエンドテスト作成のベストプラクティス
- link: /synthetics/guide/
  tag: Documentation
  text: Synthetic モニタリングガイド
- link: https://registry.terraform.io/providers/DataDog/datadog/latest/docs/resources/synthetics_test
  tag: Terraform
  text: Terraform による Synthetic ブラウザテストの作成と管理
kind: ドキュメント
title: ブラウザテスト
---

## 概要

ブラウザテストは、Datadog が Web アプリケーション上で実行するシナリオです。世界中の複数の場所からさまざまなブラウザおよびデバイスを使用して実行され、テスト間隔は自由に設定できます。これらのテストは、アプリケーションが稼働してリクエストに応答していること、シナリオで定義された条件が満たされていることを確認します。

<div class="alert alert-info">MFA の背後にあるアプリケーションのテストに興味がある場合は、<a href="/synthetics/guide/app-that-requires-login/#multi-factor-authentication" target="_blank">専用ガイド</a>を読み、<a href="https://docs.google.com/forms/d/e/1FAIpQLSdjx8PDZ8kJ3MD2ehouTri9z_Fh7PoK90J8arRQgt7QFgFxog/viewform?usp=sf_link">フィードバックを送信</a>して、Synthetic Monitoring チームがお客様のチームにとって最も重要なシステムの構築をできるようサポートしてください。</div>

## テストコンフィギュレーション

ブラウザテストの構成を定義します。

1. <mrk mid="23" mtype="seg"/><mrk mid="24" mtype="seg"/>
2. **Advanced Options** (オプション): ブラウザテストに特定のオプションを設定します。

  {{< tabs >}}

  {{% tab "リクエストオプション" %}}

  クロスオリジンリソース共有 (CORS) ポリシーでテストがブロックされないようにするには、**Disable CORS** を選択します。

  * **Request Headers**: **Name** および **Value* フィールドでヘッダーを定義して、デフォルトのブラウザヘッダーに追加またはオーバーライドします。たとえば、ヘッダーに User Agent を設定して、[Datadog スクリプトを識別][1]できます。
  * **Cookies**: ブラウザのデフォルトのクッキーに追加するクッキーを定義します。1 行に 1 つのクッキーを入力し、[`Set-Cookie`][2] の構文を使用します。
  * **HTTP Authentication**: HTTP Basic、Digest または NTLM を使用し、ユーザー名とパスワードで認証を行います。資格情報は、ブラウザテストのすべてのステップで使用されます。

  リクエストオプションは、テストの実行ごとに設定され、記録時間ではなく、実行時にブラウザテストのすべてのステップに適用されます。
  次のステップを記録するためにこれらのオプションを有効にしたままにする必要がある場合は、記録元のページでオプションを手動で適用し、テスト内で次のステップを作成します。


[1]: /ja/synthetics/guide/identify_synthetics_bots/?tab=apitests
[2]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie
  {{% /tab %}}

  {{% tab "証明書" %}}

**Ignore server certificate error** を選択すると、サーバー証明書のエラーをスキップするようにテストが指示されます。

  * **Client Certificate**: クライアント証明書を必要とするシステムでテストを行うには、**Upload File** をクリックして、証明書ファイルと秘密鍵をアップロードしてください。PEM 証明書のみ受け付けます。
  * **Client Certificate Domains**: 証明書ファイルをアップロードすると、クライアント証明書は、開始 URL のドメインに適用されます。別のドメインにクライアント証明書を適用する場合は、**Value** 欄にドメインを指定します。 

  URL にワイルドカードを含めることができます。

  {{% /tab %}}

  {{% tab "プロキシ" %}}

  **Proxy URL** フィールドに、リクエストを送信するプロキシの URL を `http://<YOUR_USER>:<YOUR_PWD>@<YOUR_IP>:<YOUR_PORT>` として入力します。

  URL に[グローバル変数](#use-global-variables)を含めることができます。

  {{% /tab %}}

  {{% tab "Privacy" %}}

  **Do not capture any screenshots for this test** を選択して、テストステップでスクリーンショットが撮影されないようにします。

  このプライバシーオプションは、個々のテストステップレベルの[詳細オプション][1]として利用でき、テスト結果に機密データが表示されないようにすることができます。

  テストがスクリーンショットを撮らないようにすると、失敗のトラブルシューティングが難しくなります。詳しくは、[セキュリティ][2]を参照してください。

[1]: /ja/synthetics/browser_tests/advanced_options#prevent-screenshot-capture
[2]: /ja/security/synthetics
  {{% /tab %}}

  {{< /tabs >}}

3. <mrk mid="33" mtype="seg"/><mrk mid="34" mtype="seg"/>
4. **Select tags**: ブラウザのテストにアタッチされる `env` と関連するタグです。与えられた `<KEY>` に対する `<VALUE>` をフィルタリングするには、`<KEY>:<VALUE>` という形式を使用します。
5. **Browsers & Devices**: テストを実行するブラウザ (`Chrome`、`Firefox`、`Edge` など) とデバイス (`Laptop Large`、`Tablet`、`Mobile Small` など)。
   - 大型のラップトップデバイスの場合、寸法は 1440 ピクセル × 1100 ピクセルです。
   - タブレットデバイスの場合、寸法は 768 ピクセル × 1020 ピクセルです。
   - 小型のモバイルデバイスの場合、寸法は 320 ピクセル × 550 ピクセルです。
6. **Select locations**: テストを実行するための Datadog が管理するロケーションです。世界中の多くの AWS ロケーションが各サイトで利用可能です。また、[プライベートロケーション][1]を設定して、カスタムロケーションやプライベートネットワーク内部からブラウザテストを実行することも可能です。[Datadog アプリ][2]でロケーションの全リストを見るか、[API][3] を使用してください。 {{< site-region region="gov" >}}**注**: Datadog for Government のサイトでは、 West US (AWS GovCloud) のロケーションがサポートされています。{{< /site-region >}}
7. **Select test frequency**: 間隔は 5 分に 1 回から週に 1 回までさまざまです。1 分ごとの頻度については、[サポートにお問い合わせ][4]ください。

### グローバル変数を使用する

[**Settings** で定義したグローバル変数][5]は、**Starting URL** のほか、ブラウザテストの **Advanced Options** でも使用できます。変数の一覧を表示するには、フィールドに `{{` と入力します。

{{< img src="synthetics/browser_tests/using_variables_browser.mp4" alt="ブラウザテストで変数を使用する" video="true" width="80%" >}}

ブラウザテストの記録でグローバル変数を使用するには、記録したステップに移動して、**Start Recording** ボタンの下にある **+ Variables** をクリックします。ドロップダウンメニューから、**Global Variable** を選択します。

{{< img src="synthetics/browser_tests/available-global-variables.png" alt="利用可能なグローバル変数" style="width:50%;" >}}

利用可能なグローバル変数を検索し、**+** をクリックして記録パネルに追加します。グローバル変数の追加が完了したら、**OK** をクリックします。

### アラート条件を定義する

アラートの条件をカスタマイズして、通知アラートの送信をテストする状況を定義できます。

* `N` のうち `n` の数の場所で、`X` の時間（分）継続してアサーションが失敗した場合は、アラートがトリガーされます。このアラートルールにより、通知をトリガーする前にテストが失敗する必要がある時間と場所の数を指定できます。
* 場所が失敗としてマークされる前に、`X` 回再試行します。これにより、場所が失敗と見なされるために、連続していくつのテスト失敗が発生する必要があるかを定義できます。デフォルトでは、失敗したテストを再試行する前に 300 ミリ秒待機します。この間隔は、[API][6] で構成できます。

{{< img src="synthetics/browser_tests/alerting_rules.png" alt="ブラウザテストのアラートルール" >}}

### チームへの通知

通知はアラート設定の条件に従って送信されます。通知を構成するには以下の手順に従ってください。

1. ブラウザテストの**メッセージ**を入力します。このフィールドでは、標準の[マークダウン形式][7]のほか、以下の[条件付き変数][8]を使用できます。

    | 条件付き変数       | 説明                                                         |
    |----------------------------|---------------------------------------------------------------------|
    | `{{#is_alert}}`            | モニターがアラートする場合に表示                                            |
    | `{{^is_alert}}`            | モニターがアラートしない場合に表示                                          |
    | `{{#is_recovery}}`         | モニターがいずれかの ALERT から回復する場合に表示   |
    | `{{^is_recovery}}`         | モニターがいずれかの ALERT から回復しない場合に表示 |
    | `{{#is_renotify}}`         | モニターが再通知したときに表示します。   |
    | `{{^is_renotify}}`         | モニターが再通知しない限り表示します。 |
    | `{{#is_priority}}`         | モニターが優先順位 (P1～P5) に一致したときに表示します。   |
    | `{{^is_priority}}`         | モニターが優先順位 (P1～P5) に一致しない限り表示します。  |

    通知メッセージには、このセクションで定義された**メッセージ**や、失敗した場所に関する情報が記載されます。

2. 通知先の[サービス][9]あるいはチームメンバーを選択します。
3. 再通知の頻度を指定します。テストの失敗を再通知しない場合は、`Never renotify if the monitor has not been resolved` オプションを使用してください。
4. **Save Details and Record Test** をクリックします。

## ステップを記録する

テストの記録を実行できるのは [Google Chrome][10] だけです。テストを記録するには、[Google Chrome 用の Datadog test recorder][11] をダウンロードする必要があります。

アプリケーション上でアクションを実行するために (リンクをクリックして別のタブを開くなど) ブラウザテストの記録でタブを切り替え、別のテストステップを追加することができます。ブラウザテストは、[アサーション][12]を実行する前に、まず (クリックによって) ページと相互作用する必要があります。すべてのテストステップを記録することによって、ブラウザテストはテスト実行時に自動的にタブを切り替えることができます。

{{< img src="synthetics/browser_tests/browser_check_record_test.png" alt="ブラウザでのテストの記録" width="80%" >}}

1. 必要に応じて、ページの右上にある **Open in a pop-up** を選択して、別のポップアップウィンドウでテスト記録を開きます。これは、アプリケーションが iframe で開くことをサポートしていない場合、または記録時のサイズの問題を回避したい場合に役立ちます。**シークレットモード**でポップアップを開いて、ログイン済みのセッションや既存のブラウザからの Cookie などを使用せずに、新しいブラウザからテストの記録を開始することもできます。
2. オプションとして、ブラウザテストからステップの記録を実行する際に、Datadog が自動的に RUM データを収集するように設定します。詳細については、[RUM とセッションリプレイの探索][13]を参照してください。
3. **Start Recording** をクリックして、ブラウザテストの記録を開始します。
4. 監視したいユーザージャーニーを通過するアプリケーションをクリックすると、アクションが自動的に記録され、左側のブラウザテストシナリオ内で[ステップ][14]を作成するために使用されます。
5. 自動的に記録されたステップに加えて、左上隅にある[ステップ][14]を使用して、シナリオを強化することもできます。
    {{< img src="synthetics/browser_tests/manual_steps.png" alt="ブラウザテストのステップ" style="width:80%;">}}

    **注**: ブラウザテストによって実行されたジャーニーが期待される状態になったことを確認するために、常に**ブラウザテストは、[アサーション][12]で終了する**必要があります。
6. シナリオが終了したら、**Save and Launch Test** をクリックします。

## アクセス許可

デフォルトでは、[Datadog 管理者および Datadog 標準ロール][15]を持つユーザーのみが、Synthetic ブラウザテストを作成、編集、削除できます。Synthetic ブラウザテストの作成、編集、削除アクセスを取得するには、ユーザーをこれら 2 つの[デフォルトのロール][15]のいずれかにアップグレードします。

[カスタムロール機能][15]を使用している場合は、`synthetics_read` および `synthetics_write` 権限を含むカスタムロールにユーザーを追加します。

### アクセス制限

アカウントに[カスタムロール][16]を使用しているお客様は、アクセス制限が利用可能です。

組織内の役割に基づいて、ブラウザテストへのアクセスを制限することができます。ブラウザテストを作成する際に、(ユーザーのほかに) どのロールがテストの読み取りと書き込みを行えるかを選択します。

{{< img src="synthetics/settings/restrict_access.png" alt="テストのアクセス許可の設定" style="width:70%;" >}}

## その他の参考資料

{{< partial name="whats-next/whats-next.html" >}}

[1]: /ja/synthetics/private_locations/
[2]: https://app.datadoghq.com/synthetics/browser/create
[3]: /ja/api/latest/synthetics/#get-all-locations-public-and-private
[4]: /ja/help/
[5]: /ja/synthetics/settings/#global-variables
[6]: /ja/api/v1/synthetics/#create-or-clone-a-test
[7]: http://daringfireball.net/projects/markdown/syntax
[8]: /ja/monitors/notify/?tab=is_alert#integrations
[9]: /ja/integrations/#cat-notification
[10]: https://www.google.com/chrome
[11]: https://chrome.google.com/webstore/detail/datadog-test-recorder/kkbncfpddhdmkfmalecgnphegacgejoa
[12]: /ja/synthetics/browser_tests/actions/#assertion
[13]: /ja/synthetics/guide/explore-rum-through-synthetics/
[14]: /ja/synthetics/browser_tests/actions/
[15]: /ja/account_management/rbac#custom-roles
[16]: /ja/account_management/rbac/#create-a-custom-role