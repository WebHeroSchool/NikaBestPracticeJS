# JS Best Practice Guide

## 1. Используйте === для сравнения

Оператор == в действительности не сравнивает объекты, а пытается привести их к одному типу. К примеру, в выражении 5 == '5', строка справа конвертируется в число, и только потом сравнивается. Тогда как ===(!==) не делает такого преобразования. Использование сравнения с преобразованием типов может привести к непредвиденным проблемам, связанным с особенностями конвертации разных типов. Например, Объекты String имеют тип Object, а не String.
    
## 2. Не используйте new Object()

    Используйте {} вместо new Object()
    Используйте "" вместо new String()
    Используйте 0 вместо new Number()
    Используйте false вместо new Boolean()
    Используйте [] вместо new Array()
    Используйте /()/ вместо new RegExp()
    Используйте function (){} вместо new Function()
 Сокращайте!

## 3. Размещайте ваш скрипт в конце страницы
Если у вас имеются файлы JS, единственная цель которых – добавление какой-то функциональной возможности (например, после нажатия кнопки), то вперед, разместите эти файлы внизу, сразу перед закрывающим тегом body. Это безусловно относится к устоявшейся практике.

## 4. Объявляйте переменные снаружи от цикла For

При выполнении длинных циклов «for» не создавайте дополнительной нагрузки на движок. Например:

### Неудачный вариант
    for(var i = 0; i < someArray.length; i++) {
        var container = document.getElementById('container');
        container.innerHtml += 'my number: ' + i;
        console.log(i);
     } 
Обратите внимание, как нам необходимо определять длину массива при каждой итерации и как мы каждый раз обходим DOM для получения элемента с id "container" – очень неэффективно!

### Удачный вариант
    var container = document.getElementById('container');
     for(var i = 0, len = someArray.length; i < len;  i++) {
        container.innerHtml += 'my number: ' + i;
        console.log(i);
     }
## 5. Не передавайте строку в "SetInterval" или "SetTimeOut"
### Рассмотрим следующий код:
    setInterval(
     "document.getElementById('container').innerHTML += 'My new number: ' + i", 3000
     );
Этот код не только неэффективен, но и возникает огромный риск, связанный с нарушением информационной безопасности. Никогда не передавайте строку в "SetInterval" или "SetTimeOut". Вместо этого передавайте имя функции.

    setInterval(someFunction, 3000);
## 6. Имеется длинный список переменных? Уберите ключевое слово "Var" и используйте вместо него запятые.
    var someItem = 'some string';
    var anotherItem = 'another string';
    var oneMoreItem = 'one more string';

### Более удачный вариант
    var someItem = 'some string',
        anotherItem = 'another string',
        oneMoreItem = 'one more string';
## 7. Всегда, всегда используйте точки с запятой
Технически в большинстве браузеров опускание «;» сойдет вам с рук. 

Тем не менее, это очень плохая практика, в результате использования которой потенциально могут возникнуть гораздо более крупные и тяжелые для обнаружения проблемы.
## 8. Не объявляйте ненужные переменные
При каждом объявлении переменных, браузер должен выделить пространство памяти для них. Следовательно, чтобы уменьшить использование памяти, необходимо сократить количество объявления переменных.
## 9.Избегайте глобальных переменных 
Глобальных переменных стоит избегать по нескольким причинам. 

Во-первых, их легко переписать в различных местах кода, потому что они везде доступны. Во-вторых, они могут переписывать объект window, так как являются свойствами объекта window.

Две эти проблемы затрудняют восприятие кода. Следовательно, стоит определять локальные переменные настолько часто, насколько это возможно, используя ключевые слова var, let илиconst.

Переменные, определенные с var, доступны на том уровне, на котором они определены, и ниже, до того, как они будут определены. 
## 10. Переменные и константы должны быть наверху

Объявление переменных и вверху файла делает код чище. Также это помешает случайно ссылаться на переменные, объявленные с let или const до того, как они будут определены. 

Если strict mode выключен, мы также избегаем создания глобальных переменных и случайного повторного объявления. Большинство текстовых редакторов отлавливает повторные объявления, но вероятность пропустить их остается. 