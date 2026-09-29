# CodeBurn: установка и диагностика Codex

CodeBurn читает локальные журналы coding-агентов и показывает расход токенов по моделям, проектам и сессиям. Полезен, когда хотите понять, куда уходит контекст и что поменять в настройках Codex. Стоимость в отчёте — оценка по API-ставкам, а не фактическое списание за подписку.

[Официальная документация и исходники](https://github.com/getagentseal/codeburn#readme).

## Установка

Нужен [Node.js](https://nodejs.org/) **22.13+**. Команды вводите в терминале, например **Terminal → New Terminal** в VS Code. На Windows выберите PowerShell.

```bash
node --version
npm install -g codeburn
codeburn --version
```

На Windows при блокировке `.ps1` используйте `npm.cmd install -g codeburn` и `codeburn.cmd` вместо `codeburn`. После установки Node.js перезапустите VS Code, чтобы обновился PATH.

Можно попробовать без глобальной установки: `npx codeburn`. Для следующих команд нужен установленный CLI либо замените `codeburn` на `npx codeburn`.

## Базовые команды

Сначала поработайте с Codex, чтобы появились журналы сессий. Затем выполните:

```bash
# Проверить, найдены ли журналы Codex и нет ли ошибок разбора
codeburn doctor --provider codex --json

# Расход за неделю: интерактивный отчёт в терминале
codeburn report --period week --provider codex

# Тот же период в браузере
codeburn web --period week --provider codex

# Расход по моделям и список сессий
codeburn models --period week --provider codex
codeburn sessions --period week --provider codex --no-pager

# Предложения по настройке
codeburn optimize --period week --provider codex
```

Вместо `week` можно указать `today`, `30days`, `month` или `all`. `--provider codex` оставляет только Codex. Для обычного отчёта `--format json` выдаёт JSON вместо интерфейса терминала.

Чтобы разобрать одну сессию:

```bash
codeburn context --provider codex --list
codeburn context SESSION_ID --provider codex --full --json
```

Замените `SESSION_ID` полным ID из списка. `--full` берёт всю историю, без него — текущий контекст после компакции. Сверяйте параметры с `codeburn <команда> --help`: примеры проверены по версии **0.9.25**.

## Как передать диагностику Codex

1. Соберите свежие отчёты и несколько контекстных дампов по [подробной инструкции](diagnostics.md). В этом репозитории сохраняйте их в `tmp/`, который исключён из Git.
2. Откройте [audit-prompt.md](audit-prompt.md), укажите пути к репозиторию и диагностике, отправьте текст в чат Codex.
3. Сначала получите разбор и рекомендации. После выбора конкретных правок разрешите их применение и проверьте результат на реальных задачах.

`optimize` без `--apply` выводит предложения. `--apply` меняет файлы, поэтому для сбора диагностики его не добавляйте.

## Что лежит в этой папке

| Файл | Для чего |
| --- | --- |
| [README.md](README.md) | Установка и команды для быстрого старта. |
| [diagnostics.md](diagnostics.md) | Ручной сбор JSON-отчётов и контекстов, выбор сессий и разбор результатов. |
| [audit-prompt.md](audit-prompt.md) | Готовый промпт для аудита глобального Codex: сначала анализ, затем согласованные изменения конфигурации. |
| [doctor-prompt.md](doctor-prompt.md) | Дополнение к аудиту, если вы сохранили контексты и оценили их как успешные, неудачные или дорогие. Использовать вместе с основным промптом. |

Настройка самого Codex: [общее руководство](../codex/global/README.md) и [Windows / VS Code](../codex/global/README.windows.md).
