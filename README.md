# AI Skills

AIごとに整理した、再利用できるスキルの公開リポジトリです。現在はCodex用のスキルを1件公開しています。

## はじめに

1. 下の一覧から使いたいスキルを選ぶ。
2. スキルのREADMEで機能・接続先・入力例を確認する。
3. スキルのフォルダを導入し、まず外部登録を伴わない入力で試す。

## スキル一覧

| AI | スキル | 内容 |
| --- | --- | --- |
| Codex | [plan-to-issues-calendar](codex/skills/plan-to-issues-calendar/README.md) | 予定と期日から作業をIssueに分解し、リンク付きのカレンダー予定を作成 |

## リポジトリ構成

```text
.
├── README.md
├── codex/
│   └── skills/
│       └── plan-to-issues-calendar/
│           ├── README.md
│           ├── SKILL.md
│           └── agents/
│               └── openai.yaml
├── shared/
│   └── skill-standard.md
└── templates/
    └── skill-template.md
```

スキル本体は `<AI名>/skills/<スキル名>/` に置きます。共通の作成ルールは `shared/`、新規作成用のひな形は `templates/` にまとめています。他のAI向けのスキルを追加するときに、対応するフォルダを増やします。

## インストール（Codex）

次のコマンドはリポジトリを手元へ取得し、対象スキルだけをCodexの個人用スキルフォルダへコピーします。`git clone` は未使用の作業フォルダで実行してください。

```sh
git clone https://github.com/robatodt74-byte/plan-to-issues-calendar.git
cd plan-to-issues-calendar

skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
skill_target="$skill_root/plan-to-issues-calendar"
mkdir -p "$skill_root"
if [ -e "$skill_target" ]; then
  echo "導入先が既にあります。内容を比較してから更新してください: $skill_target"
else
  cp -R codex/skills/plan-to-issues-calendar "$skill_target"
fi
```

導入後はCodexの新しい会話で `$plan-to-issues-calendar` を指定して使います。実際のIssue・カレンダー登録には、それぞれのサービスへの接続と書き込み権限が必要です。

以前のルート直下の構成で導入済みの場合も、今回のスキル本体の内容は同じです。更新時はリポジトリ全体ではなく `codex/skills/plan-to-issues-calendar/` の内容を配置してください。

## スキルの追加

[共通ルール](shared/skill-standard.md)を読み、[作成用テンプレート](templates/skill-template.md)を使って対象AIのフォルダ内に追加します。利用者向けの説明は各スキルのREADMEへ、エージェントへの指示はスキル本体へ記載します。

## 検証状況

現在のスキルは形式検証済みです。Issue・カレンダーへの実登録を伴う動作検証は未実施です。個別の使用例と確認方法は各スキルのREADMEを参照してください。
