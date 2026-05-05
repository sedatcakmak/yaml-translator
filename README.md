# yaml-translator

A small Python CLI for translating string values inside YAML files
between languages. It preserves structure, comments and placeholders
like `{name}`, `%player%` and `<arg>`, and runs translations in parallel.

## Features

- Translates only string values, leaves keys and structure untouched
- Skips placeholders (`{...}`, `%...%`, `<...>`) so things like
  `%player%` come out as `%player%`
- Protected-keys list — never translate values under specific keys
- Multi-threaded translation
- 10 translator backends

## Installation

```
pip install -r requirements.txt
```

## Usage

```
python translate_yaml.py -i INPUT.yml -o OUTPUT.yml -s SRC -t DST -w N
```

Example: translate `input.yml` from English to Turkish with 10 workers:

```
python translate_yaml.py -i input.yml -o output.yml -s en -t tr -w 10
```

Arguments:

- `-i` — input YAML file
- `-o` — output YAML file
- `-s` — source language code (e.g. `en`, `tr`, `ko`)
- `-t` — target language code
- `-w` — worker threads (controls request rate)

## Configuration

`settings.yml` controls:

- `translator` — which backend to use
- `api_key` — required by some backends
- `protected_keys` — list of YAML keys whose values should not be translated

## Supported Translators

- GoogleTranslator
- ChatGptTranslator
- MicrosoftTranslator
- PonsTranslator
- LingueeTranslator
- MyMemoryTranslator
- YandexTranslator
- PapagoTranslator
- DeeplTranslator
- QcriTranslator

Note: each backend has its own request limits. Tune the `-w` worker
count to stay under them.
