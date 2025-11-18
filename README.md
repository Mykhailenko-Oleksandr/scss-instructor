<details>
    <summary>Заняття 1</summary>
<ul>
 <li>
      <details>
      <summary>Види коментарів</summary>

# Види коментарів

Коментарі в SCSS працюють подібно до коментарів в інших мовах, наприклад JavaScript. Розрізняють наступні види коментарів:

  <div style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
<em>
  1. // comment <br>
         <br>
  2. /* comment */ <br>
         <br>
  3. /*! comment */ <br>
         <br>
  4. /// comment <br>
</em>
  </div>

<strong>Silent comments</strong>, або «однорядкові коментарі» — використовуються для вставки коротких коментарів, довжина яких складає орієнтовно 80 символів. Такі коментарі не потрапляють у результуючий код при компіляції.

 <em>
    <div style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
            // Додати поточний модуль до списку імпортованих модулів.<br>
            // !global - прапор, потрібний для оновлення глобальної змінної.<br>
            $imported-modules: append($imported-modules, $module) !global;<br>
        </div>
 </em>
 <br>

<strong>Loud comments</strong>, або «багаторядкові коментарі» — використовуються для вставки розгорнутих описових блоків з детальним поясненням функціоналу. Такі SASS-коментарі компілюються у звичайний коментар CSS. Багаторядковий коментар, скомпільований у CSS, може містити інтерполяцію, яка буде оцінена перед компіляцією коментаря. За замовчуванням багаторядкові коментарі буде видалено зі скомпільованого CSS у режимі compresed mode.

<em>
    <div style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
            /*<br>
             * Допоміжний клас для додавання крапки в занадто довгий рядок<br>
             * 1. Запобігає згортанню вмісту, залишає його на одному рядку.<br>
             * 2. Додає три крапки на кінці рядка.<br>
             */<br>
                  .ellipsis {<br>
                  white-space: nowrap; /* 1 */<br>
                  text-overflow: ellipsis; /* 2 */<br>
                  overflow: hidden;<br>
                  }<br>
        </div>
</em>

<strong>Very loud comments</strong> — якщо коментар починається з /\*!, він завжди буде включений у вивід CSS. Такий тип коментарів використовується для додавання тексту ліцензій, авторських прав тощо.

  <div style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
  <em>
    /*! _decimal.scss | MIT License | gist.github.com/terkel/4373420
  </em>
  </div>

<strong>SassDoc comments</strong> — кожна змінна, функція, міксин і плейсхолдер, призначені для повторного використання у проєкті, повинні бути задокументовані як частина глобального API за допомогою використання [SassDoc](http://sassdoc.com/)

<div style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
 <em>
 /// Вертикальний ритм (інтерліньяж) для тексту, який використовується у всьому коді. <br>
 <br>
 /// @type Length 
 <br>
 <p>$vertical-rhythm-baseline: 1.5rem;</p> 
 </em>
</div>

<strong>SassDoc</strong> виконує дві основні задачі:

- обходить стандартні коментарі, використовуючи систему анотації на основі всього, що є частиною відкритого або закритого API;
- дозволяє створювати HTML-версію документації API за допомогою будь-якого інструменту генерування SassDoc (CLI tool, Grunt, Gulp, Broccoli, Node…).

</details>
</li>
<li>
<details>
<summary>Архітектура. Директиви @use, @forward</summary>

# Partials в SASS

Для того щоб підключити фрагмент (модуль), рекомендуєтьсявикористовувати директиву @use. Директива @use завантажуєзмінні, міксини та функції з інших таблиць стилів Sass іпоєднує разом CSS із кількох таблиць стилів. Таблицістилів, які завантажує @use, називаються «модулями».
Для того щоб підключити модуль, достатньо використатидирективу @use із параметром <url>, який завантажує модульза заданим URL. Будь-які стилі, завантажені таким чином,будуть включені рівно один раз у скомпільований CSS-файл,незалежно від того, скільки разів ці стилі були підключенів проєкті.

<em>
       <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
           <summary >
                  // utils/_reset.scss <br>
                  button { <br>
                    font-family: inherit; <br>
                    color: currentColor; <br>
                    cursor: pointer; <br>
           </summary>
              } <br>
              // components/_btn.scss <br>
              button { <br>
                padding: 12px 24px; <br>
               <br>
                border: 1px solid transparent; <br>
                border-radius: 8px; <br>
              } <br>
              // main.scss <br>
              @use "utils/reset"; <br>
              @use "components/btn"; <br>
       </details>
      </em>
       <br>

Зверни увагу на те, що ми використовуємо @use "utireset" у файлі main.scss. Під час імпорту модуля потрібно вказувати символ нижнього підкреслення \_ розширення файлу \*.scss, SASS-компілятор, завдявбудованим алгоритмам, сам здогадається і знайде цей файГоловне задати правильний відносний шлях.

## Різновиди імпортів з директивою @use

Вище ми розглянули простий імпорт модуля, протепотужністьдирективи @use полягає в тому, що ми можемоотриматибільше контролю над модулем за рахуноквикористанняпростору імен namespace. Отримати доступ дозмінних,функцій і міксинів з іншого модуля можна,написавшиnamespace.variable, namespace.function() або@includenamespace.mixin(). За замовчуванням простір іменмодуля єлише останнім компонентом його URL-адреси безрозширенняфайлу.

  <em>
      <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
         <summary>
            // utils/_variables.scss <br>
            $smallRadius: 6px; // оголошуємо змінні <br>
            $largeRadius: 12px; <br>
            // utils/_mixins.scss <br>
         </summary>
          @mixin button() { <br>
          font-size: 14px; <br>
          background-color: teal; <br>
          } <br>
          // style.scss <br>
          @use "utils/variables"; <br>
          @use "utils/mixins"; <br>
           <br>
          .button { <br>
          @include mixins.button(); <br>
           <br>
          padding: 10px + variables.$smallRadius; <br>
            border-radius: variables.$smallRadius; <br>
          } <br>
      </details>
      </em>
       <br>
У цьому прикладі після імпорту модулів у нас у коді стають доступними два <namespace>: variables та mixins. Для доступу до змінної $smallRadius використовується назва модуля variables, прописана в кінці шляху директиви @use, та через крапку вказується ім’я самої змінної.

Проте іноді модулі мають досить довгі назви і звертатись кожного разу за такою назвою буде не дуже зручно. Тому для таких випадків передбачено можливість перейменування модуля під час імпорту. Для цього використовується ключове слово as, після якого можна вказати нову назву модуля.

<em>
      <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
        <summary>
            // utils/_variables.scss <br>
            $smallRadius: 6px; <br>
            $largeRadius: 12px; <br>
            // style.scss <br>
        </summary>
          @use "utils/variables" as v; <br>
           <br>
          .button { <br>
          padding: 10px + v.$smallRadius; // тепер можемо використати v замість variables <br>
            border-radius: v.$smallRadius; // тепер можемо використати v замість variables <br>
          } <br>
      </details>
      </em>
       <br>
      Ще один із варіантів імпорту модулів надає нам можливість імпортувати модуль без визначення простору імен, вказавши після ключового слова as символ зірочки

  <em>
      <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
         <summary>
            // utils/\_variables.scss <br>
            $smallRadius: 6px; <br>
            $largeRadius: 12px; <br>
            // style.scss <br>
         </summary>
          @use "utils/variables" as \*; <br>
           <br>
          .button { <br>
          padding: 10px + $smallRadius; // тепер можемо звертатись до змінної за її іменем <br>
          border-radius: $smallRadius; // тепер можемо звертатись до змінної за її іменем <br>
          } <br>
      </details>
      </em>
       <br>
Такий підхід трохи суперечить принципу модульності і може призводити до небажаних результатів після компіляції коду, таких як конфлікт імен при використанні змінних, міксинів чи функцій. Тому варто віддати перевагу першим двом підходам.

## Управління доступом до сутностей усередині модуля

Sass-модулі мають вбудований механізм доступу до змінних, функцій і міксинів між модулями. Для цього перед назвою сутності на початку слід використати знак - або \_. Це зробить сутність приватною (прихованою), її використання за межами поточного модуля не можливе і призведе до помилки. Це необхідно для ізоляції сутності всередині модуля, щоб інші розробники не могли вплинути на значення цієї сутності зовні.

  <em>
       <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
         <summary>
            // utils/_variables.scss <br>
            $primaryColor1: orangered; <br>
            $-primaryColor2: darkcyan; <br>
         </summary>
          // style.scss <br>
          @use "utils/variables" as v; <br>
           <br>
          .button { <br>
          color: v.$primaryColor1; // значення змінної буде підставлено у властивість <br>
            background-color: v.$primaryColor2; // отримаємо помилку компіляції, оскільки змінна приватна <br>
          background-color: v.$-primaryColor2; // отримаємо помилку компіляції, навіть якщо вкажемо - <br>
          } <br>
       </details>
      </em>

## Сумісність із СSS-файлами

Файли стилів, написані із застосуванням синтаксису препроцесора Sass і розширенням \*.scss, підтримують стилі звичайних CSS-файлів, тому, маючи CSS-файл, ми також можемо імпортувати його до модуля.

  <em>
       <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
         <summary>
            /_ reset.css _/ <br>
            button { <br>
            font-family: inherit; <br>
            color: currentColor; <br>
         </summary>
          cursor: pointer; <br>
          } <br>
          // style.scss <br>
          @use "utils/variables"; <br>
          @use "utils/mixins"; <br>
          @use "utils/reset.css"; <br>
           <br>
          .button { <br>
          @include mixins.button(); <br>
           <br>
          padding: 10px + variables.$smallRadius; <br>
            border-radius: variables.$smallRadius; <br>
          } <br>
       </details>
      </em>

## Директива @forward для роботи із множинними імпортами

Як видно із прикладу вище, під час роботи з директивою @use кількість підключень може бути доволі великою. Тому ми можемо спростити задачу при роботі з імпортами, використавши директиву @forward. Для цього створимо новий файл, у який додамо всі необхідні імпорти, і потім використаємо його в нашому цільовому файлі.

  <em>
       <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
         <summary>
            // modules/styles-forwarded.scss <br>
            @forward "variables"; <br>
            @forward "mixins"; <br>
            @forward "functions"; <br>
         </summary>
          // styles.scss <br>
          @use "modules/styles-forwarded" as frwd; <br>
           <br>
          .button { <br>
          @include frwd.button(); <br>
           <br>
          padding: 10px + frwd.$smallRadius; <br>
            border-radius: frwd.$smallRadius; <br>
          background-color: frwd.invert(frwd.$primary-color, 80%); <br>
          } <br>
       </details>
      </em>

Розберемо приклад, представлений вище:

уявімо, що у нас в проєкті є папка modules
у папці modules зберігаються модулі variables | mixins | functions
замість трьох імпортів у файлі styles.scss, ми виносимо всі імпорти в окремий файл styles-forwarded.scss, створений у папці modules
підключення всіх необхідних модулів виконуємо через директиву @forward
імпортуємо файл styles-forwarded.scss для використання у styles.scss
ми зібрали всі сутності в namespace frwd, і тепер нам доступні всі конструкції із цього простору імен

Директива @forward також надає нам можливість керувати доступом до сутностей при імпорті, якщо використати ключові слова show або hide

  <em>
        <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
  <summary>
            // modules/variables.scss <br>
            <p>$primaryColor1: orangered;</p> 
           <p> $primaryColor2: darkcyan;</p> 
            <p>$secondaryColor1: orangered;</p> 
  </summary>
         <p> $secondaryColor2: darkcyan;</p> 
          // modules/styles-forwarded.scss <br>
          @forward "mixins"; <br>
          @forward "functions"; <br>
          /** <br>
          | Ключове слово hide буде говорити компілятору про те, <br>
          | що всі змінні файлу variables.scss будуть доступні, <br>
          | за винятком змінної $primaryColor2 <br>
          */ <br>
          @forward "variables" hide $primaryColor2; <br>
          /** <br>
          | Ключове слово show буде говорити компілятору про те, <br>
          | що всі змінні файлу variables.scss будуть не доступні, <br>
          | окрім змінної $primaryColor2 <br>
          */ <br>
          @forward "variables" show $primaryColor2; <br>
        </details>
      </em>

## Порівняння директив @use і @forward

@use і @forward – це два різні підходи до організації та імпорту стилів і функцій у мові SASS. Ось основна різниця між ними:

Мета використання:

- @use: Ця директива використовується для імпорту сутностей з інших модулів і надає більше контролю над залежностями та доступом до змінних та інших стилів.
- @forward: Ця директива також використовується для імпорту сутностей з інших модулів, але його головною метою є створення публічного API для модуля, яке можна використовувати ззовні.
  Залежності:
- @use: Зазвичай потребує більше обов'язків стосовно вказування шляхів до імпортованих модулів, а також надає можливість створювати простори імен для імпортованих змінних та інших стилів.
- @forward: Має вбудований механізм для автоматичного вирішення залежностей та робить імпортовані експортовані стилі доступними ззовні.
  API:
- @use: Не має прямого впливу на публічний API модуля, але дозволяє створювати простори імен, щоб обмежити доступ до стилів.
- @forward: Головна мета – створення публічного API модуля, який можна використовувати ззовні, надаючи контроль над тим, які стилі та функції викладаються.

Загалом @use і @forward – це два різні інструменти для імпорту та організації стилів і функцій у SASS. @use більше підходить для модульної організації та контролю доступу, тоді як @forward корисний для створення публічного API модуля. Вибір між ними залежатиме від конкретних потреб твого проєкту.

  </details>
  </li>
  <li>
  <details>
  <summary>Структура проєкту</summary>

## Патерн 7-1

Типова структура патерну 7-1 має такий вигляд:

<em>
            <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px">
             <summary>
                sass/ <br>
                | <br>
                |– abstracts/ <br>
                |   |– _variables.scss         // # Sass змінні <br>
                |   |– _functions.scss         // # Sass функції <br>
                |   |– _mixins.scss            // # Sass міксини <br>
             </summary>
              |   |– _placeholders.scss      // # Sass плейсхолдери <br>
              | <br>
              |– base/ <br>
              |   |– _reset.scss             // # Reset/normalize <br>
              |   |– _typography.scss        // # Типографіка <br>
              |   …                          // # Інше <br>
              | <br>
              |– components/ <br>
              |   |– _buttons.scss           // # Кнопки <br>
              |   |– _carousel.scss          // # Слайдер <br>
              |   |– _cover.scss             // # Обкладинка <br>
              |   |– _dropdown.scss          // # Випадаюче меню <br>
              |   …                          // # і таке інше <br>
              | <br>
              |– layout/ <br>
              |   |– _navigation.scss        // # Навігація <br>
              |   |– _grid.scss              // # Сітка <br>
              |   |– _header.scss            // # Хедер <br>
              |   |– _footer.scss            // # Футер <br>
              |   |– _sidebar.scss           // # Сайдбар <br>
              |   |– _forms.scss             // # Форми <br>
              |   …                          // # і таке інше <br>
              | <br>
              |– pages/ <br>
              |   |– _home.scss              // # Специфічні стилі сторінки Home <br>
              |   |– _contact.scss           // # Специфічні стилі сторінки Contact <br>
              |   …                          // # і таке інше <br>
              | <br>
              |– themes/ <br>
              |   |– _theme.scss             // # Тема за змовчуванням <br>
              |   |– _admin.scss             // # Тема для адміністратора сайту <br>
              |   |– _manager.scss           // # Тема для менеджера сайту <br>
              |   …                          // # і таке інше <br>
              | <br>
              |– vendors/ <br>
              |   |– _bootstrap.scss         // # Bootstrap бібліотека <br>
              |   |– _modern-normalize.scss  // # jQuery UI <br>
              |   …                          // # і таке інше <br>
              | <br>
              `– main.scss                   // # Головний Sass файл <br>
            </details>
          </em>

<strong>Папка Base</strong>

Папка base/ містить те, що ми можемо назвати спільним шаблоном проєкту. Тут ти можеш зберігати файли скидання стандартних стилів браузера, деякі типографські правила, і, ймовірно, стилі, що визначають деякі стандартні стилі для елементів HTML, які часто використовуються в проєктах.

<strong>Папка Layout</strong>

Папка layout/ містить стилі, що беруть участь у побудові розкладки основних частин сайту або додатку. Ця папка може містити стилі для шапки, підвалу, навігації, бічної панелі, сітки тощо.

<strong>Папка Components</strong>

Для невеликих компонентів існує папка components/. В той час як стилі layout/ – основні (визначають загальний каркас), код усередині components/ більше сфокусований на віджетах і містить усі модулі, на кшталт слайдера, завантажувача тощо. Зазвичай файлів у components/ багато, якщо програма або сайт складається з безлічі дрібних модулів.

<strong>Папка Pages</strong>

Якщо у проєкту є стилі, які залежать від сторінки, краще покласти їх у папку pages/, файл стилів називається зазвичай так само, як і сторінка. Наприклад, не рідкість мати дуже специфічні стилі для головної сторінки, отже, існує потреба в \\\_home.scss у pages/.

<strong>Папка Themes</strong>

На великих сайтах нерідко є різні теми оформлення. Існують різні способи роботи з темами, проте гарною практикою буде складати їх у папку themes/.

<strong>Папка Utilities</strong>

Папка utilities/ збирає всі інструменти та хелпери Sass у проєкті. Кожна глобальна змінна, функція, плейсхолдер та міксин мають бути створені тут. Головне правило для цієї папки полягає в тому, що вона не повинна створювати CSS при компіляції сама по собі.

<strong>Папка Vendors</strong>

І останнє, але не менш важливе: більшість проєктів матимуть папку vendors/, що містить усі CSS-файли із зовнішніх бібліотек чи фреймворків. Тобто ті файли, які ми запозичили в інших розробників для використання в нашому коді.

<strong>Файл Main</strong>

Головний файл (зазвичай називається main.scss) має бути єдиним файлом Sass, який не починається з нижнього підкреслення. Цей файл не повинен містити нічого, окрім імпортів модулів і коментарів. Порядок визначення імпортів важливий, тому рекомендується імпортувати в тому порядку, який представлено в шаблоні проєкту. Щоб покращити сприйняття структури, можна використати файл \_index.scss, який збиратиме імпорти файлів стилів кожної папки в один файл.

Чим глибше ти вкладаєшся, тим більше часу потрібно для компіляції.

</details>

</details>
</li>

</ul>
<details>
<summary>Заняття 2</summary>
<ul><li>
<details>
<summary>Змінні</summary>

## Оголошення змінних

Змінні й операції над ними — це одна з найпростіших і водночас потужних особливостей препроцесорів. Синтаксис оголошення змінної — знак $ перед ім'ям та її значення після двокрапки.

<em>
    <div style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px">
        $primary-color: #888; <br>
        $cardBorderRadius: 4px; <br>
         <br>
        .product { <br>
        background-color: $primary-color; <br>
        border-radius: $cardBorderRadius; <br>
        } <br>
    </div>
    </em>
    
  Імена змінних повинні бути описові, щоб за ім'ям було зрозуміло, що там зберігається. Змінна $color-blue має деяке значення (крім того, що вона вказує на синій колір), а ось $color-accent, $color-primary або $color-background показує роль цього кольору. Семантичні, описові імена змінних не вимагають перейменування, наприклад, у разі зміни палітри брендових кольорів компанії.
    
  Імена змінних можуть бути записані в kebab-case, snake_case або camelCase нотаціях. Головне, щоб у проєкті використовувався тільки один із цих стилів для однорідності коду.
    
  ## Імперативність змінних
    
  Визначаючи значення змінної на початку файлу стилів, ми можемо замінити його в коді нижче. Але особливість SASS-змінних полягає в тому, що це не призведе до заміни попереднього значення цієї змінної.
    
  <em>
    <div style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px">
        $font-size: 16px;  <br>
        .title {  <br>
        font-size: $font-size; // застосується 16рх  <br>
        }  <br>
          <br>
        $font-size: 10px;  <br>
        .subtitle {  <br>
        font-size: $font-size; // застосується 10рх  <br>
        }  <br>
    </div>
    </em>
    
  ## Значення за замовчуванням !default. Кастомізація значень змінних
    
Уявімо, що в нас є окремий модуль для зберігання значень змінних \_variables.scss. У цьому модулі ми зберігаємо дефолтні змінні для кнопки. Спробуємо налаштувати кастомізацію дефолтних значень, щоб їх можна було замінити при імпорті модуля.
    
  <em>
    <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px">
       <summary>
          // module \_btn-schema.scss <br>
          $font-size: 16px; <br>
          $btn-color: white !default; <br>
          $btn-bgcolor: hotpink !default; <br>
       </summary>
         <br>
        // module \_small-btn.scss <br>
        @use "variables" as vars with ( <br>
        $font-size: 12px; // ❌ буде помилка <br>
        $btn-color: black; <br>
        $btn-bgcolor: lightblue; <br>
        ); <br>
         <br>
        .small-btn { <br>
        font-size: vars.$font-size; <br>
          color: vars.$btn-color; <br>
        background-color: vars.$btn-bgcolor; <br>
        } <br>
    </details>
    </em>
    
Як видно з коду, при створенні модуля з набором змінних ми позначили змінні з кольорами ключовим словом !default. !default говорить компілятору, що значення white чи hotpink будуть встановлені як значення за замовчуванням для відповідних змінних, але вони можуть бути змінені в ході виконання програми при імпорті даного модуля. Натомість значення змінної $font-size неможливо змінити за межами модуля.
    
## Область видимості
    
Змінні доступні тільки в межах того рівня вкладеності селекторів, на якому вони визначені. Тобто якщо змінна оголошена в селекторі, вона доступна тільки в ньому. Змінна, яка оголошується за межами будь-яких селекторів, доступна глобально.
    
  <em>
    <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px">
      <summary>
          $primary-color: teal; <br>
           <br>
          body { <br>
          $primary-color: lightgreen; <br>
      </summary>
        // Це зовсім інша змінна, хоча і з таким самим ім'ям, <br>
        // і доступна вона тільки всередині body. <br>
        background: $primary-color; <br>
        } <br>
         <br>
        p { <br>
        color: $primary-color; <br>
        // Колір тексту параграфа буде teal, <br>
        // використовується глобальна змінна зі значенням teal. <br>
        } <br>
    </details>
    </em>
    
У разі, якщо в імені змінної допущена помилка або такої змінної немає в доступній області видимості, виникне помилка компіляції стилів.
    
<em>
    <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px">
       <summary>
          $primary-color: lightgreen; <br>
           <br>
          body { <br>
          $secondary-color: lightblue; <br>
       </summary>
        background: $primary-color; <br>
        } <br>
         <br>
        p { <br>
        color: $primary-color; <br>
        background-color: $secondary-color; <br>
        // Виникне помилка компіляції стилів, тому що <br>
        // змінна secondary-color не доступна глобально. <br>
        // Вона існує тільки в селекторі body. <br>
        } <br>
    </details>
    </em>
    
Якщо сталася помилка компіляції, необхідно її виправити, тоді виконається повторна компіляція і оновиться результуючий CSS-файл.
    
  ## Ключове слово !global
    
Якщо є необхідність зробити локальну змінну доступною глобально, тоді така змінна помічається ключовим словом !global. Внесемо зміни в попередній приклад із кодом, щоб він запрацював:
    
  <em>
     <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px">
       <summary>
          $primary-color: lightgreen; <br>
           <br>
          body { <br>
          $secondary-color: lightblue !global; <br>
          background: $primary-color; <br>
       </summary>
        } <br>
         <br>
        p { <br>
        color: $primary-color; <br>
        background-color: $secondary-color; <br>
        // Помилки компіляції не буде, оскільки <br>
        // змінна $secondary-color доступна глобально <br>
        } <br>
  </details>
  </em>
  </details>
  </li>
<li>
<details>
<summary>Вкладені правила</summary>

Подібно до вкладеності тегів в HTML, у SASS можна вкладати CSS-селектори. Це одна з найбільш корисних можливостей, яка також часто неправильно використовується. Вкладеність дозволяє робити одні оголошення правил усередині інших. Нижче наведений CSS і SCSS код оформлення секції із заголовком і абзацом.

<em>
 <details style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px">
    <summary>
      .section { <br>
        width: 100%; <br>
      } <br>
       <br>
      .section .title { <br>
        color: red; <br>
      } <br>
    </summary>
     <br>
    .section .text { <br>
      font-size: 14px; <br>
    } <br>
    .section { <br>
      width: 100%; <br>
     <br>
      .title { <br>
        color: red; <br>
      } <br>
     <br>
      .text { <br>
        font-size: 14px; <br>
      } <br>
    } <br>
 </details>
</em>

Синтаксис SCSS виглядає чистішим і менше повторюється. Після компіляції у стандартний CSS ми отримаємо код, як у main.css. Але в процесі розробки писати код буде зручніше.

## Робота з комбінаторами

Як ми знаємо, в СSS існує чотири основні комбінатори. Пригадаємо, що являє собою комбінатор в CSS.

Комбінатор — це спеціальний символ або ключове слово, яке використовується для вказівки відношення між елементами в HTML. Комбінатори визначають, які елементи повинні бути вибрані або стилізовані на основі їхнього розташування в HTML-документі або відношень між ними.

<strong>Пробіл</strong> (descendant selector — селектор нащадка): Простий пробіл між двома селекторами вказує на вибір усіх елементів нащадків вкладеного селектора. Наприклад:

<pre>
div p {
/* Вибере всі p елементи, які є нащадками для div */
}
</pre>

<strong>></strong> (child selector — селектор дитини): Комбінатор > вказує на вибір тільки прямих дочірніх елементів вкладеного селектора. Наприклад:

<pre>
div > p {
/* Вибере всі p елементи, які є безпосередніми дітьми div */
}
</pre>

<strong>+</strong> (adjacent sibling selector — наступний сусід): Комбінатор + вказує на вибір елемента, який є наступним сусідом, що знаходиться безпосередньо після зазначеного елемента, і вони обидва мають спільного батька. Наприклад:

<pre>
h2 + p {
/* Вибере елемент p, який є наступним сусідом h2 */
}
</pre>

<strong>~</strong> (general sibling selector — усі наступні сусіди): Комбінатор ~ вказує на вибір усіх наступних сусідів, що знаходяться безпосередньо після зазначеного елемента, які обʼєднані спільним батьківським елементом. Наприклад:

<pre>
h2 ~ p {
/* Вибере всі p елементи, які є наступними сусідами h2 */
}
</pre>

Використовуючи вкладені селектори разом із комбінаторами, можна заощадити час і спростити підтримку кодової бази, тим самим повторивши структуру HTML-документа. Комбінатори можна розмістити в кінці зовнішнього селектора, на початку внутрішнього селектора або навіть окремо між ними. Проте надмірна вкладеність гарантовано викличе проблеми з читабельністю коду.

<pre>
<details>
<summary>
ul > {
li {
list-style: none;
}
}</summary>
h2 {

+ p {
  border-top: 1px solid gray;
  }
  }

p {
~ {
span {
opacity: 0.8;
}
}
}</details>
</pre>

## Просунута робота із вкладеними правилами

Батьківський селектор — це спеціальний селектор, винайдений Sass, який

використовується у вкладених селекторах для посилання на зовнішній селектор. Це дає можливість повторно використовувати зовнішній селектор більш складними способами, такими як додавання псевдокласів стану або додавання цільового селектора перед батьківським.

Символ & (амперсанд) дозволяє вказати, в яке місце необхідно підставити батьківський селектор. Розглянемо один приклад — оформлення посилання зі станами ховеру і фокусу.

<pre>
<code>
    .link {
    color: black;
    
    &:hover,
    &:focus {
    color: red;
    }
    }
</code>
</pre>

Як видно з прикладу, код виглядає компактно та зрозуміло. При цьому відпадає необхідність повторювати селектор .link перед псевдокласами стану. Розглянемо ще один приклад. Спробуємо стилізувати кнопку з текстом та іконкою. Маємо наступну розмітку в HTML:

```html
<button class="button" type="button">
  <svg class="button-icon"></svg>
  <span class="button-label">Замовити</span>
</button>
```

Запишемо стилі в SCSS і зробимо їх спеціально трохи складнішими, ніж потрібно.

<details>
<summary><pre>Показати код</pre></summary>

```scss
.button {
  color: red;

  &:hover,
  &:focus {
    color: blue;
  }

  &-icon {
    width: 20px;
    height: 20px;

    &:hover {
      width: 50px;
      height: 50px;
    }

    .button:hover & {
      font-size: 20px;
    }
  }

  &-label {
    font-size: 16px;

    .button:hover & {
      font-size: 20px;
    }
  }
}
```

</details>

Прочитати такий SCSS-код швидко досить складно, візуально втрачається зв'язок з батьківським селектором, і замість того щоб розбирати CSS-код, доводиться вчитуватися в синтаксис вкладеностей. Тобто, використовуючи можливості препроцесора, ми зробили гірше, більше — не завжди краще.

Створюй нове правило для кожного блоку або елемента всередині блоку, а вкладеності й конкатенації використовуй для оформлення станів і класів-модифікаторів. Тобто користуйся здоровим глуздом і роби так, як зручно, тому що SCSS-код пишеться для зручності розробника. Такий підхід також має більше переваг при пошуку селекторів у великих проєктах, оскільки селектори не розділені на складові із застосуванням конкатенації, а записані окремо.

Перепишемо код для отримання кращої читабельності:

<details>
<summary><pre>Показати код</pre></summary>

```scss
// Правило для всієї кнопки
.button {
  color: red;

  &:hover,
  &:focus {
    color: blue;
  }
}

// Правило для іконки
.button-icon {
  width: 20px;
  height: 20px;

  &:hover {
    width: 50px;
    height: 50px;
  }

  // це правило читається так: встановити колір фону для елемента
  // з класом .button-icon, коли елемент із класом .button у стані ховеру
  .button:hover & {
    background-color: teal;
  }
}

// Правило для тексту
.button-label {
  font-size: 16px;

  .button:hover & {
    font-size: 20px;
  }
}
```

</details>

Зверни увагу на рядок >>> .button:hover & <<< Тут перед амперсандом (&) стоїть батьківський елемент — кнопка в HTML, а після нього вказана конкатенація, яка підставляє клас дитини після батька. Проте амперсанд (&) у цьому випадку може бути записаний тільки разом з пробілом перед ним.

</details>
</li>
</ul>
</details>
