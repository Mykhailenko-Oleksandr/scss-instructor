<details>
<summary>Види коментарів</summary>

# Види коментарів

Коментарі в SCSS працюють подібно до коментарів в інших мовах, наприклад JavaScript. Розрізняють наступні види коментарів:

<p style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
 1.// comment </br>
 </br>
2./* comment */ </br>
 </br>
3./*! comment */ </br>
 </br>
4./// comment </br>
</p>

<strong>Silent comments</strong>, або «однорядкові коментарі» — використовуються для вставки коротких коментарів, довжина яких складає орієнтовно 80 символів. Такі коментарі не потрапляють у результуючий код при компіляції.

<p style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
    // Додати поточний модуль до списку імпортованих модулів.</br>
    // !global - прапор, потрібний для оновлення глобальної змінної.</br>
    $imported-modules: append($imported-modules, $module) !global;</br>
</p>

<strong>Loud comments</strong>, або «багаторядкові коментарі» — використовуються для вставки розгорнутих описових блоків з детальним поясненням функціоналу. Такі SASS-коментарі компілюються у звичайний коментар CSS. Багаторядковий коментар, скомпільований у CSS, може містити інтерполяцію, яка буде оцінена перед компіляцією коментаря. За замовчуванням багаторядкові коментарі буде видалено зі скомпільованого CSS у режимі compresed mode.

<p style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
    /*</br>
     * Допоміжний клас для додавання крапки в занадто довгий рядок</br>
     * 1. Запобігає згортанню вмісту, залишає його на одному рядку.</br>
     * 2. Додає три крапки на кінці рядка.</br>
     */</br>
          .ellipsis {</br>
          white-space: nowrap; /_ 1 _/</br>
          text-overflow: ellipsis; /_ 2 \*/</br>
          overflow: hidden;</br>
          }</br>
</p>

<strong>Very loud comments</strong> — якщо коментар починається з /\*!, він завжди буде включений у вивід CSS. Такий тип коментарів використовується для додавання тексту ліцензій, авторських прав тощо.

<p style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">/*! _decimal.scss | MIT License | gist.github.com/terkel/4373420</p>

<strong>SassDoc comments</strong> — кожна змінна, функція, міксин і плейсхолдер, призначені для повторного використання у проєкті, повинні бути задокументовані як частина глобального API за допомогою використання [SassDoc](http://sassdoc.com/

<p style="background: #383737ff; border-radius: 8px; padding-left: 10px;  padding-right: 10px;">
    /// Вертикальний ритм (інтерліньяж) для тексту, який використовується у всьому коді.</br>
    </br>
    /// @type Length</br>
    </br>
    $vertical-rhythm-baseline: 1.5rem;
</p>

<strong>SassDoc</strong> виконує дві основні задачі:

обходить стандартні коментарі, використовуючи систему анотації на основі всього, що є частиною відкритого або закритого API;

дозволяє створювати HTML-версію документації API за допомогою будь-якого інструменту генерування SassDoc (CLI tool, Grunt, Gulp, Broccoli, Node…).

</details>
