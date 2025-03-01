---
app_id: rapdev-terraform
app_uuid: d7240832-9c24-4fc0-9a02-916bc57882c1
assets:
  dashboards:
    RapDev Terraform Dashboard: assets/dashboards/rapdev_terraform_overview.json
  integration:
    configuration:
      spec: assets/configuration/spec.yaml
    events:
      creates_events: false
    metrics:
      check: rapdev.terraform.org.count
      metadata_path: metadata.csv
      prefix: rapdev.terraform.
    service_checks:
      metadata_path: assets/service_checks.json
    source_type_name: RapDev Terraform
  logs: {}
author:
  homepage: https://www.rapdev.io
  name: RapDev
  sales_email: ddsales@rapdev.io
  support_email: datadog-engineering@rapdev.io
  vendor_id: rapdev
categories:
- マーケットプレイス
dependencies: []
display_on_public_website: true
draft: false
git_integration_title: rapdev_terraform
integration_id: rapdev-terraform
integration_title: Terraform
integration_version: ''
is_public: true
kind: integration
legal_terms:
  eula: assets/EULA.pdf
manifest_version: 2.0.0
name: rapdev_terraform
oauth: {}
pricing:
- billing_type: flat_fee
  includes_assets: true
  product_id: terraform
  short_description: このインテグレーションの定額料金
  unit_price: 100
public_title: Terraform インテグレーション
short_description: terraform アカウントと失敗した実行を監視する
supported_os:
- linux
- mac os
- windows
tile:
  changelog: CHANGELOG.md
  classifier_tags:
  - Supported OS::Linux
  - Supported OS::Mac OS
  - Supported OS::Windows
  - Category::Marketplace
  - Offering::Integration
  configuration: README.md#Setup
  description: terraform アカウントと失敗した実行を監視する
  media:
  - caption: Terraform ダッシュボード
    image_url: images/terraform_dashboard.png
    media_type: image
  overview: README.md#Overview
  support: README.md#Support
  title: Terraform インテグレーション
---



## 概要

Terraform とのインテグレーションにより、組織は Terraform のアカウントをアクティブに監視し、その動作状況や使用頻度をよりよく理解することができます。このインテグレーションはさらに権限の監査も提供します。

### ダッシュボード  

1. RapDev Terraform ダッシュボード

## サポート
サポートまたは機能リクエストをご希望の場合は、以下のチャンネルから RapDev.io にお問い合わせください。

- サポート: datadog-engineering@rapdev.io
- セールス: sales@rapdev.io
- チャット: [rapdev.io](https://www.rapdev.io/#Get-in-touch)
- 電話: 855-857-0222

---
ボストンより ❤️ を込めて

*お探しのインテグレーションが見つかりませんか？組織に役立つ重要なツールの導入をお考えですか？[こちら](mailto:datadog-engineering@rapdev.io)から RapDev へメッセージをお送りいただければ、導入をサポートいたします！*

[1]: https://www.terraform.io/docs/cloud/users-teams-organizations/users.html#api-tokens
[2]: https://docs.datadoghq.com/ja/agent/guide/agent-commands/#start-stop-and-restart-the-agent
[3]: https://docs.datadoghq.com/ja/agent/guide/agent-commands/#agent-status-and-information

---
このアプリケーションは Marketplace から入手でき、Datadog テクノロジーパートナーによってサポートされています。このアプリケーションを購入するには、<a href="https://app.datadoghq.com/marketplace/app/rapdev-terraform" target="_blank">こちらをクリック</a>してください。