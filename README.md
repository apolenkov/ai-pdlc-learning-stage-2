# Поздний старт с R2. Сброс формы

Этот репозиторий — самостоятельная поздняя точка входа. Если вы уже прошли R1, оставайтесь в своей текущей папке `sdd-guide-credit-calculator-stage-1` и продолжайте по [инструкции R2](https://apolenkov.github.io/customdev-learning/guides/stage-2.html): второй clone и перенос файла не нужны. Полный маршрут курса: Введение → R1 → R2 → SDD и OpenSpec → R4; R3 — факультативное углубление.

Перед R1 прочитайте [исходное обращение и ответы](request-and-answers.md) — это источник фактов упражнения. Заполните [общий шаблон замысла](intent-template.md) в `intents/clear-calculation-result.md`, затем сравните свой вариант с [предоставленным примером](examples/clear-calculation-result.md). Пример показывает один способ разбора; в рабочей ветке именно файл в `intents/` становится вашим единственным актуальным замыслом для R1–R3 и меняется при уточнении запроса. Затем поздний старт сначала воспроизводит R1 из локальной [исходной спецификации](specification.md), затем добавляет R2 в следующей ветке того же checkout. Это один запрос и один рабочий intent на R1–R3. Результат — накопительная `specification.md` и MR между двумя личными ветками. Node.js, OpenSpec и код калькулятора здесь не нужны.

Git нужен не ради ещё одной папки: он сохраняет актуальный текст и историю изменений в месте, откуда их могут проверить люди и использовать ИИ. Модель не всегда знает последние решения команды; общий репозиторий даёт ей правильный контекст. В будущем метарепозиторий свяжет требования, документы, схемы и код.

Основной маршрут выполняется в браузере и VS Code. Точные команды терминала для сверки и восстановления собраны в одном блоке [«Через терминал»](#через-терминал--точные-команды-и-восстановление) — не выполняйте оба варианта подряд.

## Подготовьте fork и одну папку

Откройте [общий учебный эталон](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-2) в браузере, нажмите **Fork** и дождитесь создания своего fork. Откройте свой fork и скопируйте его HTTPS-адрес.

В VS Code вызовите **Git: Clone Repository** (палитра команд или кнопка на стартовом экране), вставьте скопированный HTTPS-адрес своего fork и выберите папку учебных проектов. Откройте клонированную папку: она останется рабочей на ступенях R1–R3, новый clone на следующих ступенях не нужен.

В этом checkout `origin` — ваш fork: личные ветки отправляются туда кнопкой **Publish Branch** (или **Push**) в VS Code. Второй remote для учебного маршрута не нужен. Не отправляйте решение в `main` и не обходите её защиту. Для текущего diff R2/R3/R4 курс требует три отметки: руководителя проекта, аналитика и технического руководителя; если затронута архитектура или есть спор — четвёртую отметку архитектора. После обязательных отметок учебный MR можно смёржить только в личную base-ветку внутри своего fork. Для повторного прохождения добавьте одинаковый суффикс ко всем личным веткам.

Если дерево уже содержит неожиданные правки или нужное имя ветки занято, остановитесь и уточните папку/имя. Ничего не сбрасывайте и не используйте force push.

## Восстановите личный результат R1

1. Создайте личную ветку в VS Code: нажмите имя текущей ветки в строке состояния слева внизу → **Create new branch** → введите `course/your_login/stage-1-error-result`, заменив `your_login` своим логином GitLab. Ветка создаётся от `main` этого эталона — исходного baseline позднего старта.

2. Сформулируйте собственный intent по шаблону в `intents/clear-calculation-result.md` и сравните его с разобранным примером. Затем измените `specification.md` точно в трёх местах:

   - в «Требования и сценарии» добавьте правило очистки предыдущего результата до «—» и указания ошибочного поля;
   - добавьте сценарий `120 000 ₽`, `0%`, `12 месяцев` → `10 000 ₽`, затем `1,5 месяца` → ошибка срока и «—»;
   - удалите решённый вопрос из «Открытых вопросов» и оставьте «Для данного упражнения открытых вопросов нет».

   Сохраните четыре исходных сценария. Заполните [происхождение позднего старта](transfer.md) фактическим URL, полным SHA `origin/main` и именем личной ветки; не подставляйте запомнённые значения. Полный SHA baseline здесь нужен для происхождения — точная команда есть в блоке [«Через терминал»](#через-терминал--точные-команды-и-восстановление).

3. Сохраните и отправьте R1 в VS Code: в **Source Control** (значок ветки на левой панели) прочитайте diff `intents/clear-calculation-result.md`, `specification.md` и `transfer.md` — двойной щелчок по файлу открывает сравнение. Добавьте эти три файла в staged кнопкой **+** у файла, ещё раз прочитайте staged diff, введите сообщение `docs: clarify result after invalid input` и нажмите **Commit**. Затем отправьте ветку кнопкой **Publish Branch** в `origin` и проверьте её появление в своём fork в браузере.

   Перед R2 убедитесь, что в строке состояния выбрана ваша ветка `course/your_login/stage-1-error-result`, а список изменений в Source Control пуст. Полный SHA R1 получите из блока «Через терминал», только если он нужен для передачи или записи происхождения.

## Добавьте требование R2

Учебное решение: действие «Сбросить» возвращает сумму к `3 000 000 ₽`, ставку к `16%`, срок к `240 месяцам`, очищает ошибки и результат до «—» и не запускает расчёт. Повторный сброс не меняет состояние, не запускает расчёт и не показывает ошибку.

1. Создайте ветку R2 от текущего принятого R1: нажмите имя ветки в строке состояния → **Create new branch** → введите `course/your_login/stage-2-reset`. Новая ветка создаётся от вашего принятого коммита R1, а не от `main`.

2. Добавьте правило и три сценария: сброс после успешного расчёта, сброс после ошибки и повторный сброс. В последнем сценарии явно укажите: состояние не меняется, расчёт не запускается, ошибка не показывается. Пять сценариев R1 должны сохраниться; итоговый договор содержит восемь сценариев.

3. Проверьте и отправьте R2: в **Source Control** прочитайте весь diff `specification.md`, добавьте в staged только `specification.md` кнопкой **+**, ещё раз прочитайте staged diff, введите сообщение `docs: specify form reset behavior` и нажмите **Commit**. Отправьте ветку кнопкой **Publish Branch** в `origin` и проверьте её в своём fork в браузере.

4. На странице своего fork откройте MR: source — `course/your_login/stage-2-reset`, target — `course/your_login/stage-1-error-result` в том же fork. Обе личные ветки лежат в одном корпоративном fork, поэтому MR создаётся внутри fork; общая `main` не является target учебного MR. Если GitLab предлагает target в upstream `example-group`, смените его на свой fork. Используйте [шаблон описания и вопросов](review/request.md).

Учебную задачу Jira ведите по [канонической инструкции R2](https://apolenkov.github.io/customdev-learning/guides/stage-2.html): откройте выданную лично вам Task проекта DEMO, а если её нет — создайте свою по той же инструкции и [порядку доступа к DEMO](https://apolenkov.github.io/customdev-learning/corporate-resources.html#jira). Добавьте в задачу ссылку на MR; полный SHA ветки укажите, только если он запрошен. Не создавайте случайный ключ/родителя и не пишите, что review получено, пока его нет.

## Получите отметки по текущему diff

Для текущей версии нужны три отметки: руководитель проекта подтверждает цель и ожидаемый результат, аналитик — полноту требований и восьми сценариев, технический руководитель — реализуемость и проверки. Если изменение затрагивает архитектуру или остаётся архитектурный спор, нужна четвёртая отметка архитектора.

Каждое замечание примите и исправьте либо аргументированно отклоните в MR. После содержательного изменения текущего diff нужные отметки получают заново. Автоматическая команда и ИИ не являются человеческим одобрением.

После отметок можно запросить необязательную [помощь ИИ](ai/request.md) в этой же папке и R2-ветке. Если вы приняли предложения, сохраните их в том же diff и получите необходимые отметки для новой версии. Отдельные AI-ветки и параллельные упражнения в курсе не требуются.

Когда обсуждения разрешены и обязательные отметки относятся к текущему source, сохраните ссылку на MR; точный SHA source-ветки зафиксируйте для передачи или по требованию приёмки. В общем эталоне MR живёт внутри вашего корпоративного fork: после отметок смёржьте его в личную base-ветку fork и сохраните обе личные ветки; в общую `main` не сливайте. Если для технического walkthrough отзывы разрешено пропустить, прямо отметьте человеческую приёмку незавершённой.

## Дальше по курсу

Основной маршрут после R2 ведёт к обязательной [практике SDD и OpenSpec](https://apolenkov.github.io/customdev-learning/guides/sdd-openspec.html), затем к R4. После SDD можно углубить ручное планирование в том же checkout на факультативной [R3](https://apolenkov.github.io/customdev-learning/guides/stage-3.html): обновите `AGENTS.md`, инициализируйте OpenSpec командой `openspec init --tools none` и перенесите восемь сценариев в активный Change. Полный `openspec init --tools kilocode` не нужен: он развернёт все 12 рабочих процессов, а для ступеней достаточно planning-only набора. Навыки лежат в универсальном `.agents/skills` (`openspec-explore`, `openspec-propose`, `openspec-update-change`), который автоматически читают Kilo и другие агенты; для Kilo в VS Code дополнительно есть команды `.kilo/command` (`opsx-explore`, `opsx-propose`, `opsx-update`). В этом checkout нет приложения; Apply и реализация запрещены. Ручной R3 полезен, когда нужно работать без модели, но не заменяет SDD и R4 в полном курсе.

Работать с требованиями на R1–R3 можно без модели. Если вы используете ИИ как помощника, оставляйте принятые правки в текущем документе и ветке; отдельные AI-ветки курса не нужны.

## Через терминал · точные команды и восстановление

Основной маршрут выше выполняется в браузере и VS Code. Команды ниже — для сверки состояния, восстановления и тех, кто сознательно работает в терминале.

<details><summary>Развернуть точные команды</summary>

Клонирование fork и проверка `origin`:

```bash
git clone https://gitlab.example.invalid/your_login/sdd-guide-credit-calculator-stage-2.git
cd sdd-guide-credit-calculator-stage-2
git remote get-url origin
git status --short --branch
```

Baseline и личная ветка R1 (полный SHA `origin/main` — для `transfer.md`):

```bash
git rev-parse origin/main
git show origin/main:specification.md
git switch -c course/your_login/stage-1-error-result
```

Проверка, коммит и отправка R1:

```bash
git diff --check
git diff -- intents/clear-calculation-result.md specification.md transfer.md
git add intents/clear-calculation-result.md specification.md transfer.md
git diff --cached --check
git diff --cached -- intents/clear-calculation-result.md specification.md transfer.md
git commit -m "docs: clarify result after invalid input"
git status --short
git push -u origin course/your_login/stage-1-error-result
git ls-remote --heads origin course/your_login/stage-1-error-result
```

Ветка R2, проверка, коммит и отправка:

```bash
git switch -c course/your_login/stage-2-reset
git diff --check
git diff course/your_login/stage-1-error-result -- specification.md transfer.md
git add specification.md
git diff --cached --check
git diff --cached -- specification.md
git commit -m "docs: specify form reset behavior"
git push -u origin course/your_login/stage-2-reset
git ls-remote --heads origin course/your_login/stage-2-reset
git diff course/your_login/stage-1-error-result...HEAD -- specification.md transfer.md
```

Состояние и полный SHA по запросу (передача, происхождение, точный след в Jira):

```bash
git status --short --branch
git branch --show-current
git rev-parse HEAD
```

Восстановление: сверьте локальный R1 с опубликованным в fork — оба значения `rev-parse` должны совпасть, при расхождении остановитесь. Ветку R2 создавайте от опубликованного R1; не подставляйте `main` и не применяйте force:

```bash
git status --short --branch
git fetch origin
git rev-parse HEAD origin/course/your_login/stage-1-error-result
git switch -c course/your_login/stage-2-reset origin/course/your_login/stage-1-error-result
```

Ветка R3 от принятого head R2:

```bash
git switch -c course/your_login/stage-3-reset-years course/your_login/stage-2-reset
```

</details>

## Основные страницы курса

- [R1 — спецификация в Git](https://apolenkov.github.io/customdev-learning/guides/stage-1.html)
- [R2 — сброс формы](https://apolenkov.github.io/customdev-learning/guides/stage-2.html)
- [SDD и OpenSpec — обязательный следующий шаг](https://apolenkov.github.io/customdev-learning/guides/sdd-openspec.html)
- [R3 — факультативное ручное углубление в OpenSpec](https://apolenkov.github.io/customdev-learning/guides/stage-3.html)
- [R4 — изолированный продуктовый Store](https://apolenkov.github.io/customdev-learning/guides/stage-4.html)

Каталог курса: <https://apolenkov.github.io/customdev-learning/guides/>.

## Отдельная передача R2 в реализацию

Она не заменяет обязательную практику SDD и OpenSpec и не входит в приёмку R2. После необходимых отметок по текущему diff передайте разработчику фактические URL репозитория, ветку, полный SHA и пути `specification.md`, `transfer.md`:

```bash
git status --short --branch
git remote get-url origin
git branch --show-current
source_sha=$(git rev-parse HEAD)
git cat-file -e "$source_sha^{commit}"
git show "${source_sha}:specification.md"
git show "${source_sha}:transfer.md"
```

Дерево должно быть чистым, оба `show` — выводить принятый договор и provenance позднего старта. В корне отдельного checkout сервиса откройте [общий практикум разработчика](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-3/blob/main/docs/developer-handoff.md) и выполните только начальную read-only проверку:

```bash
git status --short --branch
git rev-parse HEAD
sed -n '1,240p' docs/developer-handoff.md
```

Сообщение агенту:

```text
Прочитай docs/developer-handoff.md и AGENTS.md сервиса. Источник требований:
<URL репозитория>, <ветка>, <полный SHA>, пути specification.md и transfer.md.
Проверь доступность коммита и покажи оба файла из этого SHA. Сопоставь восемь
сценариев с текущим состоянием, перечисли пробелы и предложи план с проверками.
Пока не меняй файлы или код, не создавай Change, не запускай Apply и не
называй read-only проверку реализацией новых функций.
```

Если SHA недоступен, дерево грязное или файлы не совпадают с передачей, остановитесь. Переход к Change, Apply и коду требует отдельного разрешения.
