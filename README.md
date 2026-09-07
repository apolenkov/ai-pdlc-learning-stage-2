# Отдельный старт с R2. Сброс формы и два review

Этот репозиторий — только самостоятельная поздняя точка входа. Если вы уже прошли R1, оставайтесь в своей текущей папке `sdd-guide-credit-calculator-stage-1` и продолжайте по [основной инструкции R2](https://apolenkov.github.io/customdev-learning/guides/stage-2.html): второй clone и импорт не нужны.

Поздний старт сначала воспроизводит результат R1 из локальной [исходной спецификации](specification.md), затем добавляет R2 в следующей ветке того же checkout. Результат — накопительная `specification.md`, PR между двумя личными ветками и два человеческих review актуального diff. Node.js, OpenSpec и код калькулятора здесь не нужны.

## Подготовьте одну папку

```bash
git clone https://github.com/apolenkov/sdd-guide-credit-calculator-stage-2.git
cd sdd-guide-credit-calculator-stage-2
git status --short --branch
```

В общем эталоне организатор выдаёт доступ на чтение и отправку личных веток. Не отправляйте решение в `main`, не обходите её защиту и не сливайте учебный PR. Замените `your_login` своим GitHub-логином; для повторного прохождения добавьте одинаковый суффикс ко всем личным веткам.

Если дерево уже содержит неожиданные правки или нужное имя ветки занято, остановитесь и уточните папку/имя. Ничего не сбрасывайте и не используйте force push.

## Восстановите личный результат R1

1. Зафиксируйте источник baseline и создайте личную R1-ветку:

   ```bash
   git rev-parse origin/main
   git show origin/main:specification.md
   git switch -c course/your_login/stage-1-error-result
   ```

2. Измените `specification.md` точно в трёх местах:

   - в «Требования и сценарии» добавьте правило очистки предыдущего результата до «—» и указания ошибочного поля;
   - добавьте сценарий `120 000 ₽`, `0%`, `12 месяцев` → `10 000 ₽`, затем `1,5 месяца` → ошибка срока и «—»;
   - удалите решённый вопрос из «Открытых вопросов» и оставьте «Для данного упражнения открытых вопросов нет».

   Сохраните четыре исходных сценария. Заполните [происхождение позднего старта](transfer.md) фактическими URL, полным SHA `origin/main` и именем личной ветки; не подставляйте запомнённые значения.

3. Проверьте и сохраните R1:

   ```bash
   git diff --check
   git diff -- specification.md transfer.md
   git add specification.md transfer.md
   git diff --cached --check
   git diff --cached -- specification.md transfer.md
   git commit -m "docs: clarify result after invalid input"
   git status --short
   git rev-parse HEAD
   git push -u origin course/your_login/stage-1-error-result
   ```

   Перед R2 снова выполните `git status --short` и `git rev-parse HEAD`; дерево должно быть чистым, а SHA — фактическим последним коммитом R1. Сохраните этот SHA вне Git для PR и следующей ветки.

## Добавьте требование R2

Учебное решение: действие «Сбросить» возвращает сумму к `3 000 000 ₽`, ставку к `16%`, срок к `240 месяцам`, очищает ошибки и результат до «—» и не запускает расчёт. Повторный сброс сохраняет это состояние.

1. Создайте R2 от текущего принятого R1:

   ```bash
   git switch -c course/your_login/stage-2-reset
   ```

2. Добавьте правило и три сценария: сброс после успешного расчёта, сброс после ошибки и повторный сброс. Пять сценариев R1 должны сохраниться; итоговый договор содержит восемь сценариев.

3. Проверьте, сохраните и отправьте R2:

   ```bash
   git diff --check
   git diff course/your_login/stage-1-error-result -- specification.md transfer.md
   git add specification.md
   git diff --cached --check
   git diff --cached -- specification.md
   git commit -m "docs: specify form reset behavior"
   git push -u origin course/your_login/stage-2-reset
   git diff course/your_login/stage-1-error-result...HEAD -- specification.md transfer.md
   git rev-parse HEAD
   ```

4. Откройте PR с base `course/your_login/stage-1-error-result` и head `course/your_login/stage-2-reset`. Используйте [шаблон описания и вопросов](review/request.md). Общая `main` не является базой учебного PR.

Если точная учебная Jira-задача уже выдана, добавьте в неё ссылку на PR и полный SHA. Не создавайте случайный ключ/родителя и не пишите, что review получено, пока его нет.

## Получите два человеческих review

Сначала другой аналитик проверяет требования и восемь сценариев. После устранения его замечаний разработчик или архитектор проверяет реализуемость правила, сценариев и будущих тестов.

Каждое замечание примите и исправьте либо аргументированно отклоните в PR. После любого нового коммита оба человека подтверждают актуальный diff повторно. Автоматическая команда и ИИ не являются человеческим одобрением.

После первого полного цикла двух review можно выполнить необязательную [ИИ-предпроверку](ai/request.md) в этой же папке и R2-ветке. Если вы приняли правки ИИ, сделайте коммит, отправьте его в тот же PR и снова получите оба review уже нового diff. Если 2-ИИ пропущена, основной процесс остаётся полным.

Когда обсуждения разрешены и два подтверждения относятся к текущему head, сохраните ссылку и полный SHA. В общем эталоне закройте учебный PR без слияния и сохраните обе личные ветки. Если для технического walkthrough отзывы разрешено пропустить, прямо отметьте человеческую приёмку незавершённой.

## Продолжите R3 в этой же папке

Поздний старт не вводит новый обязательный clone на следующем шаге. Создайте `course/your_login/stage-3-reset-years` от принятой R2 и следуйте [ручной инструкции R3](https://apolenkov.github.io/customdev-learning/guides/stage-3.html): обновите `AGENTS.md`, инициализируйте native OpenSpec для OpenCode и поэтапно перенесите все восемь сценариев в активный Change. В этом checkout нет приложения; Apply и реализация запрещены.

[3-ИИ](https://apolenkov.github.io/customdev-learning/guides/stage-3-ai.html) создаёт отдельный `add-payment-summary` в `course/your_login/stage-3-ai-payment-summary` и отдельный PR с base `course/your_login/stage-3-reset-years`.

## Карта семи стабильных страниц

- [R1 — спецификация в Git](https://apolenkov.github.io/customdev-learning/guides/stage-1.html)
- [1-ИИ — помощь с R1](https://apolenkov.github.io/customdev-learning/guides/stage-1-ai.html)
- [R2 — сброс, PR и два review](https://apolenkov.github.io/customdev-learning/guides/stage-2.html)
- [2-ИИ — необязательная предпроверка](https://apolenkov.github.io/customdev-learning/guides/stage-2-ai.html)
- [R3 — ручной переход в OpenSpec](https://apolenkov.github.io/customdev-learning/guides/stage-3.html)
- [3-ИИ — отдельный `add-payment-summary`](https://apolenkov.github.io/customdev-learning/guides/stage-3-ai.html)
- [R4 — изолированный продуктовый Store](https://apolenkov.github.io/customdev-learning/guides/stage-3-star.html)

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
сценариев с текущим baseline, перечисли пробелы и предложи план с проверками.
Пока не меняй файлы или код, не создавай Change, не запускай Apply и не
называй read-only проверку реализацией новых функций.
```

Если SHA недоступен, дерево грязное или файлы не совпадают с передачей, остановитесь. Переход к Change, Apply и коду требует отдельного разрешения.
