# Отдельный старт с R2. Сброс формы и два review

Этот репозиторий — только самостоятельная поздняя точка входа. Если вы уже прошли R1, оставайтесь в своей текущей папке `sdd-guide-credit-calculator-stage-1` и продолжайте по [основной инструкции R2](https://apolenkov.github.io/customdev-learning/guides/stage-2.html): второй clone и импорт не нужны.

Поздний старт сначала воспроизводит результат R1 из локальной [исходной спецификации](specification.md), затем добавляет R2 в следующей ветке того же checkout. Результат — накопительная `specification.md`, MR между двумя личными ветками и два человеческих review актуального diff. Node.js, OpenSpec и код калькулятора здесь не нужны.

Основной маршрут выполняется в браузере и VS Code. Точные команды терминала для сверки и восстановления собраны в одном блоке [«Через терминал»](#через-терминал--точные-команды-и-восстановление) — не выполняйте оба варианта подряд.

## Подготовьте fork и одну папку

Откройте [общий учебный эталон](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-2) в браузере, нажмите **Fork** и дождитесь создания своего fork. Откройте свой fork и скопируйте его HTTPS-адрес.

В VS Code вызовите **Git: Clone Repository** (палитра команд или кнопка на стартовом экране), вставьте скопированный HTTPS-адрес своего fork и выберите папку учебных проектов. Откройте клонированную папку: она останется рабочей на ступенях R1–R3, новый clone на следующих ступенях не нужен.

В этом checkout `origin` — ваш fork: личные ветки отправляются туда кнопкой **Publish Branch** (или **Push**) в VS Code. Второй remote для учебного маршрута не нужен. Не отправляйте решение в `main` и не обходите её защиту; после двух review учебный MR можно смёржить в личную base-ветку внутри своего fork, в общую `main` не сливайте. Для повторного прохождения добавьте одинаковый суффикс ко всем личным веткам.

Если дерево уже содержит неожиданные правки или нужное имя ветки занято, остановитесь и уточните папку/имя. Ничего не сбрасывайте и не используйте force push.

## Восстановите личный результат R1

1. Создайте личную ветку в VS Code: нажмите имя текущей ветки в строке состояния слева внизу → **Create new branch** → введите `course/your_login/stage-1-error-result`, заменив `your_login` своим логином GitLab. Ветка создаётся от `main` этого эталона — исходного baseline позднего старта.

2. Измените `specification.md` точно в трёх местах:

   - в «Требования и сценарии» добавьте правило очистки предыдущего результата до «—» и указания ошибочного поля;
   - добавьте сценарий `120 000 ₽`, `0%`, `12 месяцев` → `10 000 ₽`, затем `1,5 месяца` → ошибка срока и «—»;
   - удалите решённый вопрос из «Открытых вопросов» и оставьте «Для данного упражнения открытых вопросов нет».

   Сохраните четыре исходных сценария. Заполните [происхождение позднего старта](transfer.md) фактическим URL, полным SHA `origin/main` и именем личной ветки; не подставляйте запомнённые значения. Полный SHA baseline здесь нужен для происхождения — точная команда есть в блоке [«Через терминал»](#через-терминал--точные-команды-и-восстановление).

3. Сохраните и отправьте R1 в VS Code: в **Source Control** (значок ветки на левой панели) прочитайте весь diff `specification.md` и `transfer.md` — двойной щелчок по файлу открывает сравнение. Добавьте оба файла в staged кнопкой **+** у файла, ещё раз прочитайте staged diff, введите сообщение `docs: clarify result after invalid input` и нажмите **Commit**. Затем отправьте ветку кнопкой **Publish Branch** в `origin` и проверьте её появление в своём fork в браузере.

   Перед R2 убедитесь, что в строке состояния выбрана ваша ветка `course/your_login/stage-1-error-result`, а список изменений в Source Control пуст. Полный SHA R1 получите из блока «Через терминал», только если он нужен для передачи или записи происхождения.

## Добавьте требование R2

Учебное решение: действие «Сбросить» возвращает сумму к `3 000 000 ₽`, ставку к `16%`, срок к `240 месяцам`, очищает ошибки и результат до «—» и не запускает расчёт. Повторный сброс не меняет состояние, не запускает расчёт и не показывает ошибку.

1. Создайте ветку R2 от текущего принятого R1: нажмите имя ветки в строке состояния → **Create new branch** → введите `course/your_login/stage-2-reset`. Новая ветка создаётся от вашего принятого коммита R1, а не от `main`.

2. Добавьте правило и три сценария: сброс после успешного расчёта, сброс после ошибки и повторный сброс. В последнем сценарии явно укажите: состояние не меняется, расчёт не запускается, ошибка не показывается. Пять сценариев R1 должны сохраниться; итоговый договор содержит восемь сценариев.

3. Проверьте и отправьте R2: в **Source Control** прочитайте весь diff `specification.md`, добавьте в staged только `specification.md` кнопкой **+**, ещё раз прочитайте staged diff, введите сообщение `docs: specify form reset behavior` и нажмите **Commit**. Отправьте ветку кнопкой **Publish Branch** в `origin` и проверьте её в своём fork в браузере.

4. На странице своего fork откройте MR: source — `course/your_login/stage-2-reset`, target — `course/your_login/stage-1-error-result` в том же fork. Обе личные ветки лежат в одном корпоративном fork, поэтому MR создаётся внутри fork; общая `main` не является target учебного MR. Если GitLab предлагает target в upstream `example-group`, смените его на свой fork. Используйте [шаблон описания и вопросов](review/request.md).

Учебную задачу Jira ведите по [канонической инструкции R2](https://apolenkov.github.io/customdev-learning/guides/stage-2.html): откройте выданную лично вам Task проекта DEMO, а если её нет — создайте свою по той же инструкции и [порядку доступа к DEMO](https://apolenkov.github.io/customdev-learning/corporate-resources.html#jira). Добавьте в задачу ссылку на MR; полный SHA ветки укажите, только если он запрошен. Не создавайте случайный ключ/родителя и не пишите, что review получено, пока его нет.

## Получите два человеческих review

Сначала другой аналитик проверяет требования и восемь сценариев. После устранения его замечаний разработчик или архитектор проверяет реализуемость правила, сценариев и будущих тестов.

Каждое замечание примите и исправьте либо аргументированно отклоните в MR. После любого нового коммита оба человека подтверждают актуальный diff повторно. Автоматическая команда и ИИ не являются человеческим одобрением.

После первого полного цикла двух review можно выполнить необязательную [ИИ-предпроверку](ai/request.md) в этой же папке и R2-ветке. Если вы приняли правки ИИ, сделайте коммит, отправьте его в тот же MR и снова получите оба review уже нового diff. Если 2-ИИ пропущена, основной процесс остаётся полным.

Когда обсуждения разрешены и два подтверждения относятся к текущему source, сохраните ссылку на MR; точный SHA source-ветки зафиксируйте только для передачи или по требованию приёмки. В общем эталоне MR живёт внутри вашего корпоративного fork: после двух review смёржьте его в личную base-ветку fork и сохраните обе личные ветки; в общую `main` не сливайте. Если для технического walkthrough отзывы разрешено пропустить, прямо отметьте человеческую приёмку незавершённой.

## Продолжите R3 в этой же папке

Поздний старт не вводит новый обязательный clone на следующем шаге. Создайте `course/your_login/stage-3-reset-years` от принятой ветки `course/your_login/stage-2-reset` — тем же действием **Create new branch** в строке состояния — и следуйте [ручной инструкции R3](https://apolenkov.github.io/customdev-learning/guides/stage-3.html): обновите `AGENTS.md`, инициализируйте OpenSpec командой `openspec init --tools none` и поэтапно перенесите все восемь сценариев в активный Change. Интеграция `--tools kilocode` не нужна: она создаёт устаревший `.kilocode`, а навыки Kilo уже лежат в репозитории в `.kilo/skills` и вызываются по имени. В этом checkout нет приложения; Apply и реализация запрещены.

[3-ИИ](https://apolenkov.github.io/customdev-learning/guides/stage-3-ai.html) создаёт отдельный `add-payment-summary` в `course/your_login/stage-3-ai-payment-summary` и отдельный MR с target `course/your_login/stage-3-reset-years`.

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
git diff -- specification.md transfer.md
git add specification.md transfer.md
git diff --cached --check
git diff --cached -- specification.md transfer.md
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

## Карта семи стабильных страниц

- [R1 — спецификация в Git](https://apolenkov.github.io/customdev-learning/guides/stage-1.html)
- [1-ИИ — помощь с R1](https://apolenkov.github.io/customdev-learning/guides/stage-1-ai.html)
- [R2 — сброс, MR и два review](https://apolenkov.github.io/customdev-learning/guides/stage-2.html)
- [2-ИИ — необязательная предпроверка](https://apolenkov.github.io/customdev-learning/guides/stage-2-ai.html)
- [R3 — ручной переход в OpenSpec](https://apolenkov.github.io/customdev-learning/guides/stage-3.html)
- [3-ИИ — отдельный `add-payment-summary`](https://apolenkov.github.io/customdev-learning/guides/stage-3-ai.html)
- [R4 — изолированный продуктовый Store](https://apolenkov.github.io/customdev-learning/guides/stage-4.html)

Каталог курса: <https://apolenkov.github.io/customdev-learning/guides/>.

## Отдельная передача R2 в реализацию

Она не заменяет продолжение R3 и не входит в приёмку R2. После двух актуальных человеческих review передайте разработчику фактические URL репозитория, ветку, полный SHA и пути `specification.md`, `transfer.md`:

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
