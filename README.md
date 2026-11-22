# Шаг 2. Проверяем и согласуем: поздний старт

Репозиторий для тех, кто пришёл на шаг 2 без результата шага 1: здесь сначала восстанавливается результат шага 1, затем добавляется требование сброса формы. Место в маршруте: шаг 1 «Требования в Git» → шаг 2 «Проверяем и согласуем» → шаг 3 «Изменение в OpenSpec».

| | |
| --- | --- |
| Шаг курса | [Шаг 2. Проверяем и согласуем](https://apolenkov.github.io/customdev-learning/guides/s2-review.html) |
| Вход | Два варианта. (а) Вы прошли шаг 1 в fork `sdd-guide-credit-calculator-stage-1`: этот репозиторий не нужен, продолжайте в своей папке по странице шага 2. (б) Поздний старт: вы здесь, результат шага 1 сначала восстанавливается |
| Действие | Описать в личной ветке требование сброса формы и открыть запрос на review (PR, в GitLab — MR) к ветке шага 1 |
| Результат | PR между двумя личными ветками, одобренный владельцем продукта; в `specification.md` восемь сценариев |

**С чего начать.** На GitHub нажмите **Fork**. Если вы работаете в GitLab, создайте проект через
**New project → Import project → Repository by URL** и вставьте адрес
`https://github.com/apolenkov/sdd-guide-credit-calculator-stage-2.git`.

## Подготовьте fork и одну папку

Перед шагом 1 прочитайте [исходное обращение и ответы](request-and-answers.md) — это источник фактов упражнения. Заполните [общий шаблон замысла](intent-template.md) в `intents/clear-calculation-result.md`, затем сравните свой вариант с [предоставленным примером](examples/clear-calculation-result.md). Пример показывает один способ разбора; в рабочей ветке именно файл в `intents/` становится вашим единственным актуальным замыслом для шагов 1–3 и меняется при уточнении запроса. Поздний старт сначала воспроизводит шаг 1 из локальной [исходной спецификации](specification.md), затем добавляет шаг 2 в следующей ветке того же checkout. Это один запрос и один рабочий intent на шаги 1–3. Результат — накопительная `specification.md` и PR между двумя личными ветками. Node.js, OpenSpec и код калькулятора здесь не нужны.

Git нужен не ради ещё одной папки: он сохраняет актуальный текст и историю изменений в месте, откуда их могут проверить люди и использовать ИИ. Модель не всегда знает последние решения команды; общий репозиторий даёт ей правильный контекст. В будущем метарепозиторий свяжет требования, документы, схемы и код.

Основной маршрут выполняется в браузере и VS Code; рядом с каждым действием в интерфейсе стоит его команда терминала. Точные команды для сверки и восстановления собраны в блоке [«Через терминал»](#через-терминал--точные-команды-и-восстановление) — не выполняйте оба варианта подряд.

Откройте [общий учебный эталон](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-2) в браузере, нажмите **Fork** и дождитесь создания своего fork. Откройте свой fork (в GitLab — проект, созданный импортом) и скопируйте его HTTPS-адрес.

В VS Code вызовите **Git: Clone Repository** (палитра команд или кнопка на стартовом экране), вставьте скопированный HTTPS-адрес своего fork и выберите папку учебных проектов. Откройте клонированную папку: она останется рабочей на шагах 1–3, новый clone на следующих шагах не нужен. В терминале: `git clone https://github.com/your_login/sdd-guide-credit-calculator-stage-2.git` — вместо `your_login` подставьте свой логин; в GitLab возьмите адрес проекта, созданного импортом.

В этом checkout `origin` — ваш fork: личные ветки отправляются туда кнопкой **Publish Branch** (или **Push**) в VS Code. Второй remote для учебного маршрута не нужен. Не отправляйте решение в `main` и не обходите её защиту. Одобрение по текущему diff даёт владелец продукта: он нажимает Approve. Аналитик и техлид оставляют замечания в PR. Архитектора приглашают через @, если изменение затрагивает данные, интеграции, безопасность или производительность, либо при споре: он пишет замечания (и `design.md`), но одобряет по-прежнему владелец продукта. После одобрения учебный PR можно смёржить только в личную base-ветку внутри своего fork. Для повторного прохождения добавьте одинаковый суффикс ко всем личным веткам.

Если дерево уже содержит неожиданные правки или нужное имя ветки занято, остановитесь и уточните папку/имя. Ничего не сбрасывайте и не используйте force push. Проверка дерева в терминале: `git status --short --branch`

## Восстановите личный результат шага 1

1. Создайте личную ветку в VS Code: нажмите имя текущей ветки в строке состояния слева внизу → **Create new branch** → введите `course/your_login/stage-1-error-result`, заменив `your_login` своим логином. Ветка создаётся от `main` этого эталона — исходного baseline позднего старта. В терминале: `git switch -c course/your_login/stage-1-error-result`

2. Сформулируйте собственный intent по шаблону в `intents/clear-calculation-result.md` и сравните его с разобранным примером. Затем измените `specification.md` точно в трёх местах:

   - в «Требования и сценарии» добавьте правило очистки предыдущего результата до «—» и указания ошибочного поля;
   - добавьте сценарий `120 000 ₽`, `0%`, `12 месяцев` → `10 000 ₽`, затем `1,5 месяца` → ошибка срока и «—»;
   - удалите решённый вопрос из «Открытых вопросов» и оставьте «Для данного упражнения открытых вопросов нет».

   Сохраните четыре исходных сценария. Заполните [происхождение позднего старта](transfer.md) фактическим URL, полным SHA `origin/main` и именем личной ветки; не подставляйте запомнённые значения. Полный SHA baseline здесь нужен для происхождения. В терминале: `git rev-parse origin/main`

3. Сохраните и отправьте шаг 1 в VS Code: в **Source Control** (значок ветки на левой панели) прочитайте diff `intents/clear-calculation-result.md`, `specification.md` и `transfer.md` — двойной щелчок по файлу открывает сравнение. В терминале: `git diff -- intents/clear-calculation-result.md specification.md transfer.md`. Добавьте эти три файла в staged кнопкой **+** у файла. В терминале: `git add intents/clear-calculation-result.md specification.md transfer.md`. Ещё раз прочитайте staged diff (`git diff --cached -- intents/clear-calculation-result.md specification.md transfer.md`), введите сообщение `docs: clarify result after invalid input` и нажмите **Commit**. В терминале: `git commit -m "docs: clarify result after invalid input"`. Затем отправьте ветку кнопкой **Publish Branch** в `origin`. В терминале: `git push -u origin course/your_login/stage-1-error-result`. Проверьте появление ветки в своём fork в браузере; в терминале: `git ls-remote --heads origin course/your_login/stage-1-error-result`

   Перед шагом 2 убедитесь, что в строке состояния выбрана ваша ветка `course/your_login/stage-1-error-result` (в терминале: `git branch --show-current`), а список изменений в Source Control пуст (в терминале: `git status --short`). Полный SHA шага 1 получите командой `git rev-parse HEAD` только если он нужен для передачи или записи происхождения.

## Добавьте требование шага 2

Учебное решение: действие «Сбросить» возвращает сумму к `3 000 000 ₽`, ставку к `16%`, срок к `240 месяцам`, очищает ошибки и результат до «—» и не запускает расчёт. Повторный сброс не меняет состояние, не запускает расчёт и не показывает ошибку.

1. Создайте ветку шага 2 от текущего принятого шага 1: нажмите имя ветки в строке состояния → **Create new branch** → введите `course/your_login/stage-2-reset`. Новая ветка создаётся от вашего принятого коммита шага 1, а не от `main`. В терминале: `git switch -c course/your_login/stage-2-reset`

2. Добавьте правило и три сценария: сброс после успешного расчёта, сброс после ошибки и повторный сброс. В последнем сценарии явно укажите: состояние не меняется, расчёт не запускается, ошибка не показывается. Пять сценариев шага 1 должны сохраниться; итоговый договор содержит восемь сценариев. Когда сформулируете свой вариант, сверьтесь с [разобранным решением шага 2](https://github.com/apolenkov/sdd-guide-credit-calculator-stage-1/compare/course/example/stage-1-error-result...course/example/stage-2-reset): откройте в сравнении файл `specification.md` и найдите правило сброса и три новых сценария. Это один способ разбора, а не образец для копирования.

3. Проверьте и отправьте шаг 2: в **Source Control** прочитайте весь diff `specification.md`. В терминале: `git diff course/your_login/stage-1-error-result -- specification.md transfer.md`. Добавьте в staged только `specification.md` кнопкой **+**. В терминале: `git add specification.md`. Ещё раз прочитайте staged diff (`git diff --cached -- specification.md`), введите сообщение `docs: specify form reset behavior` и нажмите **Commit**. В терминале: `git commit -m "docs: specify form reset behavior"`. Отправьте ветку кнопкой **Publish Branch** в `origin`. В терминале: `git push -u origin course/your_login/stage-2-reset`. Проверьте ветку в своём fork в браузере; в терминале: `git ls-remote --heads origin course/your_login/stage-2-reset`

4. На странице своего fork откройте PR (в GitLab — MR): source — `course/your_login/stage-2-reset`, target — `course/your_login/stage-1-error-result` в том же fork. Обе личные ветки лежат в одном fork, поэтому PR создаётся внутри fork; общая `main` не является target учебного PR. Если платформа предлагает target в исходном репозитории курса, смените его на свой fork. На GitHub форма описания подставляется в PR автоматически из `.github/pull_request_template.md`. В GitLab шаблона нет: скопируйте текст из `.github/pull_request_template.md` в описание MR. Полные вопросы ревьюерам — в [review/request.md](review/request.md).

Учебная задача — issue в своём fork; если курс проходят в компании, это задача в трекере команды. Порядок ведения — на [странице шага 2](https://apolenkov.github.io/customdev-learning/guides/s2-review.html); порядок доступа к трекеру в компании — в [корпоративных ресурсах](https://apolenkov.github.io/customdev-learning/corporate-resources.html#jira). Добавьте в задачу ссылку на PR; полный SHA ветки укажите, только если он запрошен. Не создавайте случайный ключ или родителя и не пишите, что review получено, пока его нет.

## Получите одобрение по текущему diff

Одобрение по текущему diff даёт владелец продукта: он подтверждает цель и ожидаемый результат и нажимает Approve. Аналитик оставляет замечания о полноте требований и восьми сценариев, техлид — о реализуемости и проверках. Если изменение затрагивает данные, интеграции, безопасность или производительность либо остаётся спор, архитектора приглашают через @: он пишет замечания (и `design.md`), но одобряет по-прежнему владелец продукта.

На шаге 2 архитектурное решение записывает аналитик. Проверьте четыре признака и спор, затем запишите результат в шапке `specification.md` (под заголовком): «Архитектурный разбор: не требуется» или «Архитектурный разбор: запрошен (признак)». Если признак есть или аналитик и техлид не договорились, упомяните архитектора через @ в комментарии к PR и назовите признак или спор. Расчёт здесь локальный, введённые значения не сохраняются и не отправляются, поэтому обычно подходит «не требуется». Папка изменения появится только на шаге 3: там архитектор при необходимости пишет `design.md`, а аналитик ставит на него ссылку в шапке. Правка шапки — новый коммит: владелец продукта одобряет последнюю версию заново.

Каждое замечание примите и исправьте либо аргументированно отклоните в PR. После новых коммитов владелец продукта одобряет последнюю версию заново. Автор не одобряет свой запрос. Автоматическая команда и ИИ одобрение не заменяют.

После одобрения можно запросить необязательную [помощь ИИ](ai/request.md) в этой же папке и ветке шага 2. Если вы приняли предложения, сохраните их в том же diff: владелец продукта одобряет новую версию заново. Отдельные AI-ветки и параллельные упражнения в курсе не требуются.

Когда обсуждения решены и одобрение владельца продукта относится к последней версии, сохраните ссылку на PR; точный SHA source-ветки зафиксируйте для передачи или по требованию приёмки. В общем эталоне PR живёт внутри вашего fork: после одобрения смёржьте его в личную base-ветку fork и сохраните обе личные ветки; в общую `main` не сливайте. Если для технического walkthrough review разрешено пропустить, прямо напишите, что человеческая приёмка не завершена.

## Дальше по курсу

Следующий шаг — обязательный шаг 3 «Изменение в OpenSpec» ([страница шага](https://apolenkov.github.io/customdev-learning/guides/s3-openspec.html)); если практику SDD и OpenSpec из подготовки вы ещё не проходили, начните со [страницы практики](https://apolenkov.github.io/customdev-learning/guides/p3-sdd.html). В том же checkout обновите `AGENTS.md`, инициализируйте OpenSpec командой `openspec init --tools none` и перенесите восемь сценариев в активный Change. Полный `openspec init --tools kilocode` не нужен: он развернёт все 12 рабочих процессов, а для шагов достаточно planning-only набора. Навыки лежат в универсальном `.agents/skills` (`openspec-explore`, `openspec-propose`, `openspec-update-change`), который автоматически читают Kilo и другие агенты; для Kilo в VS Code дополнительно есть команды `.kilo/command` (`opsx-explore`, `opsx-propose`, `opsx-update`). В этом checkout нет приложения; Apply и реализация запрещены. Затем идут шаг 4 «Команда продукта» и шаг 5 «Контекст продукта».

Работать с требованиями на шагах 1–3 можно без модели. Если вы используете ИИ как помощника, оставляйте принятые правки в текущем документе и ветке; отдельные AI-ветки курса не нужны.

## Через терминал · точные команды и восстановление

Основной маршрут выше выполняется в браузере и VS Code. Команды ниже — для сверки состояния, восстановления и тех, кто сознательно работает в терминале.

<details><summary>Развернуть точные команды</summary>

Клонирование fork и проверка `origin` (замените `your_login` своим логином; в GitLab вместо этого адреса вставьте адрес проекта, созданного импортом):

```bash
git clone https://github.com/your_login/sdd-guide-credit-calculator-stage-2.git
cd sdd-guide-credit-calculator-stage-2
git remote get-url origin
git status --short --branch
```

Baseline и личная ветка шага 1 (полный SHA `origin/main` — для `transfer.md`):

```bash
git rev-parse origin/main
git show origin/main:specification.md
git switch -c course/your_login/stage-1-error-result
```

Проверка, коммит и отправка шага 1:

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

Ветка шага 2, проверка, коммит и отправка:

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

Состояние и полный SHA по запросу (передача, происхождение, точный след в учебной задаче):

```bash
git status --short --branch
git branch --show-current
git rev-parse HEAD
```

Восстановление: сверьте локальный шаг 1 с опубликованным в fork — оба значения `rev-parse` должны совпасть, при расхождении остановитесь. Ветку шага 2 создавайте от опубликованного шага 1; не подставляйте `main` и не применяйте force:

```bash
git status --short --branch
git fetch origin
git rev-parse HEAD origin/course/your_login/stage-1-error-result
git switch -c course/your_login/stage-2-reset origin/course/your_login/stage-1-error-result
```

Ветка шага 3 от принятого head шага 2:

```bash
git switch -c course/your_login/stage-3-reset-years course/your_login/stage-2-reset
```

</details>

## Основные страницы курса

- [Шаг 1. Требования в Git](https://apolenkov.github.io/customdev-learning/guides/s1-git.html)
- [Шаг 2. Проверяем и согласуем](https://apolenkov.github.io/customdev-learning/guides/s2-review.html)
- [SDD и OpenSpec — практика из подготовки](https://apolenkov.github.io/customdev-learning/guides/p3-sdd.html)
- [Шаг 3. Изменение в OpenSpec — обязательный](https://apolenkov.github.io/customdev-learning/guides/s3-openspec.html)
- [Шаг 4. Команда продукта](https://apolenkov.github.io/customdev-learning/guides/s4-team.html)
- [Шаг 5. Контекст продукта — изолированный продуктовый Store](https://apolenkov.github.io/customdev-learning/guides/s4-product.html)

Каталог курса: <https://apolenkov.github.io/customdev-learning/guides/>.

## Отдельная передача шага 2 в реализацию

Она не заменяет обязательный шаг 3 и не входит в приёмку шага 2. После одобрения владельца продукта по текущему diff передайте разработчику фактические URL репозитория, ветку, полный SHA и пути `specification.md`, `transfer.md`:

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
