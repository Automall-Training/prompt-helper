# Скиллы Automall для Codex — установка

Семь скиллов команды Automall. Каждый лежит в своём репозитории организации Automall-Training и в папке «3_Скиллы» плейбука — в одной и той же версии, под тем же именем. Подробно, с примерами — плейбук команды: https://automall-playbook.vercel.app (страница «Скиллы»).

## Установка с GitHub в Codex

| Репозиторий | Что внутри |
|---|---|
| [Automall-Training/prompt-helper](https://github.com/Automall-Training/prompt-helper) | `prompt-helper` — превращает задачу в один готовый промпт |
| [Automall-Training/proverka-faktov](https://github.com/Automall-Training/proverka-faktov) | `proverka-faktov` — сверка ответа ИИ с документом |
| [Automall-Training/korporativnaya-perepiska](https://github.com/Automall-Training/korporativnaya-perepiska) | `korporativnaya-perepiska` — деловые письма по правилам компании |
| [Automall-Training/analitik](https://github.com/Automall-Training/analitik) | `analitik` — финансовый аналитик |
| [Automall-Training/one-big-feature](https://github.com/Automall-Training/one-big-feature) | `one-big-feature` — большая задача по шагам силами нескольких агентов |
| [Automall-Training/content-workflow](https://github.com/Automall-Training/content-workflow) | шесть скиллов `content-…` — от темы до пакета материалов |
| [Automall-Training/legal-engine](https://github.com/Automall-Training/legal-engine) | десять скиллов `legal-…` — агент-юрист, вход `legal-workflow` |

`$skill-installer` — встроенный скилл Codex: он скачивает скилл с GitHub и кладёт в `~/.agents/skills`. Откройте новый чат Codex и отправьте:

```text
$skill-installer Установи с GitHub скиллы для использования в любых проектах, в папку ~/.agents/skills, все рядом (ветка main):
- пять скиллов из корня репозитория (путь "."), имя — как у репозитория, адрес https://github.com/Automall-Training/<имя>: prompt-helper, proverka-faktov, korporativnaya-perepiska, analitik, one-big-feature;
- шесть скиллов из https://github.com/Automall-Training/content-workflow — пути skills/content-workflow, skills/content-research, skills/content-asset-creation, skills/content-publishing, skills/content-workflow-setup, skills/content-workflow-update; имя каждого — последняя часть пути.
Если скилл уже установлен, сохрани его и продолжи со следующим. Сообщи результат по каждому скиллу. Остальное в ~/.agents/skills не трогай.
```

Codex спросит разрешение выйти в интернет и записать в папку скиллов — нажмите «Разрешить». `legal-engine` этим запросом не ставится: он нужен только юристам, блок ниже.

## Юристам: установка legal-engine (только Mac)

Скрипт для Mac; на Windows `legal-engine` так не ставится. Нужны около 10 минут и Терминал — программа, куда команды вводят текстом.

1. Откройте Терминал: **Cmd + Пробел**, наберите «Терминал», Enter.
2. Скопируйте папку `legal-engine` из «3_Скиллы» в домашнюю папку (Finder → **Cmd + Shift + H**): должно получиться `~/legal-engine`. Или с GitHub, командой в Терминале: `git clone https://github.com/Automall-Training/legal-engine ~/legal-engine`. Если Mac предложит «установить инструменты разработчика», нажмите «Установить», дождитесь окончания и повторите команду.
3. Установите `uv` — служебную программу, на которой работает движок. Вставьте строку `curl -LsSf https://astral.sh/uv/install.sh | sh` и нажмите Enter. Потом закройте Терминал и откройте заново.
4. Поставьте Python 3.12 (системный на Mac старый, движку нужен 3.10 или новее): `uv python install 3.12 --default`. Закройте и откройте Терминал, проверьте `python3 --version` — должно быть 3.12.
5. Вставьте команду установки и дождитесь `READY`: `cd ~/legal-engine && SKILLS_DIR=~/.agents/skills bash ./install.sh`.
6. В конце скрипт напишет «open Claude Code and say…» — пропустите: в Codex настройка — `$legal-workflow-setup`. Перезапустите Codex. Папку `legal-engine` не удаляйте и не переносите: скиллы подключены к ней ссылками.

**Если не вышло.** Скрипт написал `NOT READY` и «python3 … 3.10 or newer» — повторите шаг 4 (Python), потом шаг 5.

После установки откройте **новую** сессию Codex: новые скиллы видны только в ней. Наберите `$` — скиллы в списке.

Перед первой работой: `analitik` и `korporativnaya-perepiska` при первом запуске сами предложат заполнить правила компании вопросами по одному. Для своих скиллов по правилам компании сначала заполните «Шаблон инструкции аналитика» — он на сайте плейбука https://automall-playbook.vercel.app (сценарий С12).
