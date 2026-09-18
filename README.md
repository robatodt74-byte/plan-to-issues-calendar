# AI Skills

AIごとに整理した、再利用できるスキルの公開リポジトリです。現在はCodex用のスキルを1件公開しています。

## はじめに

1. 下の一覧から使いたいスキルを選ぶ。
2. スキルのREADMEで機能・接続先・入力例を確認する。
3. スキルのフォルダを導入し、まず外部登録を伴わない入力で試す。

## スキル一覧

| AI | スキル | 内容 |
| --- | --- | --- |
| Codex | [plan](codex/skills/plan/README.md) | 予定と期日から作業をIssueに分解し、リンク付きのカレンダー予定を作成 |

## リポジトリ構成

```text
.
├── README.md
├── codex/
│   └── skills/
│       └── plan/
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
skill_target="$skill_root/plan"
mkdir -p "$skill_root"
if [ -e "$skill_target" ]; then
  echo "導入先が既にあります。内容を比較してから更新してください: $skill_target"
else
  cp -R codex/skills/plan "$skill_target"
fi
```

導入後はCodexの新しい会話で `$plan` を指定して使います。実際のIssue・カレンダー登録には、それぞれのサービスへの接続と書き込み権限が必要です。

旧名 `plan-to-issues-calendar` で導入済みの場合は、既存フォルダを `plan` に改名し、新しい `SKILL.md` と `agents/openai.yaml` に更新してください。独自の変更があれば比較して反映します。呼び出し名は `$plan` になりました。GitHubのリポジトリURLは変更していません。

## スキルの追加

[共通ルール](shared/skill-standard.md)を読み、[作成用テンプレート](templates/skill-template.md)を使って対象AIのフォルダ内に追加します。利用者向けの説明は各スキルのREADMEへ、エージェントへの指示はスキル本体へ記載します。

## 検証状況

現在のスキルは形式検証済みです。Issue・カレンダーへの実登録を伴う動作検証は未実施です。個別の使用例と確認方法は各スキルのREADMEを参照してください。
