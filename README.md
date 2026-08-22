# goodBadWordlist
OK/NG word list for speech recognition subtitling  
音声認識字幕ちゃんのためのOK/NG単語リスト  

## jimakuChan （音声認識字幕ちゃん）
- service: https://sayonari.github.io/jimakuChan/
- webpage: https://www.sayonari.com/trans_asr/index_asr.html
- github: https://github.com/sayonari/jimakuChan/

## Request　（お願い）
Everyone! Please keep this list updated!  
皆さん！リストを更新してください！  

## ファイル構成
各言語フォルダ（`ja/`, `en/`, `zh-CN/`, `zh-TW/`, `zh-HK/`, `ko/`, `es/`, `fr/`, `de/`, `it/`, `pt/`, `ru/`, `id/`, `nl/`, `pl/`, `sv/`, `th/`, `tr/`, `uk/`, `vi/`, `ar/`, `so/`）に以下の 2 ファイル（UTF-8，1 行 1 語）があります．
- `BadList.txt` : 伏字（`***`）にする語
- `GoodList.txt` : BadList の語を含んでいても伏字にしない語（誤検出の回避）
    - ASMR → 「SM」のせいで A**R となってしまうのを避ける
    - タイマンコラボ → 「マンコ」のせいで タイ***ラボ となってしまうのを避ける

## マッチングのルール（jimakuChan v2 以降）
伏字過多を防ぐため，文字体系によって判定方法が異なります．
| 文字体系 | 判定 | 例 |
|---|---|---|
| ラテン文字・キリル文字・ギリシャ文字・アラビア文字など（分かち書きする言語） | **単語単位**（前後が文字・数字でない）．大文字小文字は無視．複数形の `s` を許容 | `ass` は "class" にはマッチしない．`hell` は "hello" にはマッチしない |
| ハングル | 語頭のみ境界チェック（助詞が後ろに付くため） | `씨발` は "씨발놈아" にマッチ |
| 日本語・中国語・タイ語など（分かち書きしない言語） | 部分一致（従来どおり）．GoodList で保護 | `マンコ` は "タイマンコラボ" にもマッチするので GoodList に「タイマンコラボ」を入れる |
- 長い語が優先してマッチします（「アナル」より「アナルセックス」）
- 全角英数（ＳＥＸ）や NFKC 正規化した形も同時に検出します
- `#` で始まる行はコメントとして無視されます

## ⚠️ 従来版（v1）は部分一致のままです
上の単語単位の判定は **jimakuChan v2 以降**の話で，現在も多くの方が使っている**従来版（v1）は全言語で部分一致**です．
そのため BadList に短い語を入れると，従来版では一般語を巻き込みます（`cu` → `cultura` / `curso` / `documento`…）．

- **BadList に 3 文字以下の語を入れない**（どうしても必要なら，巻き込む一般語を GoodList に必ず追加する）
- GoodList は**活用形もそのまま書く**．従来版は部分一致なので `habiter` を入れても `habite` は守れません
- 判断に迷う語は，v2 だけで伏字にできれば十分か（＝BadList から外してよいか）を先に考える

## リストに入れる基準（2026-08 見直し）
- **入れる**：明確な猥褻語・性行為/性器の俗語，民族・障害・性的指向などへの蔑称
- **入れない**：話題語（銃・爆弾・薬物・賭博・死・自殺・暴力…ゲーム実況では日常語），軽い罵倒（idiot 系），医学用語，日常語に含まれる短い語（単漢字，`ass`/`cum` などの部分文字列 ※ラテン文字は単語単位判定なので v2 では問題になりにくい）
- 迷ったら「配信画面が `***` だらけになって困る方が，たまに 1 語すり抜けるより悪い」を基準に

## 2026-08-16 の更新
- es/fr/de/pt の BadList を UTF-8 に統一（旧ファイルは Latin-1 で保存されており非 ASCII 行が一致していなかった），pt の GoodList の文字化け修正，zh-TW（破損）を再生成
- 全言語で話題語・単漢字・日常語を削除し，明確な猥褻語・蔑称を追加，GoodList を補強
- nl / pl / sv / th / tr / uk / vi / ar / so の初期リストを追加（LDNOOBW 等を参考に機械的に作成．**ネイティブの方の確認・修正を歓迎します**）

## 2026-08-22 の更新
- es / de / pt の GoodList に残っていた文字化け（Latin-1 の二重変換）を修正．pt は正しい綴りが別行にあったため壊れた行を削除
- 従来版（部分一致）で誤って伏字になる正当語を GoodList へ追加
  - es：`computadora` `diputado` `disputa` `reputación` `amputar` `penetrar` `ampolla` `envergadura` `semental` ほか（活用形を含む）
  - pt：`cultura` `curso` `cuidado` `escuro` `desculpa` `discutir` `documento` `ocupado` `executar` `controlar` `enviado` ほか
  - fr：`calcul` `ridicule` `masculin` `véhicule` `majuscule` `violence` `violon` `député` `réputation` `habiter` `orbite` `arbitre` ほか（活用形を含む）
  - id：`masuk` `pantai` `santai` `asuransi` `pasukan` ほか／nl：`pikant`／tr：`koç`
- **pt の BadList から `cu` を削除**．2 文字のため従来版で `cultura` / `curso` / `documento` などを巻き込む一方，v2 では単語単体しか伏字にならず残す利点が小さいため

## Reference / Thanks list
- ja : https://github.com/MosasoM/inappropriate-words-ja
- id : https://github.com/dikako/list_badword
- multi : https://github.com/LDNOOBW/List-of-Dirty-Naughty-Obscene-and-Otherwise-Bad-Words
- multi : https://github.com/surge-ai/profanity ／ https://github.com/censor-text/profanity-list
- vi : https://github.com/blue-eyes-vn/vietnamese-offensive-words
