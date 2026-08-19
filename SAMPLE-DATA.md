# Формат данных сайта (образцы для разработки)

Живые `state.json` / `votes.json` содержат **только настоящие данные**.
Образцы ниже — для локальной вёрстки: подставить, посмотреть, вернуть обратно.

**Почему не держим примеры на бою:** карточки «Manifestos we bought» и список
кандидатов называют реальные чужие токены. На публичном сайте это читается как
заявление «мы спонсировали этот проект» / «этот проект номинирован», хотя ни
того, ни другого не было. Бейдж «demo data» в углу такое не оправдывает.

## state.json

```json
{
  "demo": true,
  "ethUsd": 4400,
  "manifesto": { "worthUsd": 199, "handle": "@manifel", "sinceTs": 1786021665107,
                 "text": "We do not market. The machine markets." },
  "vault": { "eth": 0.0489, "address": "0x…", "spentUsd": 199 },
  "paidManifestos": [
    { "ca": "0x…", "symbol": "TICKER", "name": "Name", "image": "brand/logo.svg",
      "amountUsd": 299, "ts": 1786541400000, "mcapUsd": 1240000 }
  ],
  "feed": [
    { "ts": 1786021665107, "type": "pay", "usd": 199, "note": "Manifesto pinned", "tx": "0x…" },
    { "ts": 1786004520000, "type": "claim", "usd": 121, "note": "Fee sweep", "tx": "0x…" }
  ]
}
```

`type`: `claim` | `deposit` | `pay` | `outbid`. `tx` рисуется ссылкой только
если это валидный 32-байтный хеш. `mcapUsd` — фоллбек: сайт пытается получить
живую капу через DexScreener и подменяет значение, если источник ответил.

## votes.json

```json
{
  "round": 1,
  "snapshotNote": "snapshot at block 12345678",
  "candidates": [
    { "ca": "0x…", "symbol": "TICKER", "name": "Name", "weight": 4200000 }
  ]
}
```

`weight` — сумма балансов $MFUEL проголосовавших за кандидата на снапшоте;
проценты сайт считает сам.
