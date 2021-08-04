  # Отступы и форматирование

-   Используйте 4 пробела, а не табуляцию.
-   Файл должен заканчиваться на один символ переноса строки, но не должен заканчиваться на пустой строке (два символа переноса строки).    
-   Отступы всех `do`/`while`/`for`/`if`/function должны составлять 4 пробела.    
-   `or`/`and`  в  `if`  должны быть обрамлены круглыми скобками (). 
    ```lua
    if (a == true and b == false) or (a == false and b == true) then
        <...>
    end -- хорошо
    
    if a == true and b == false or a == false and b == true then
        <...>
    end -- плохо
    
    if a ^ b == true then
    end -- хорошо, но не явно
    ```    
- Не используйте конкатенацию для конвертации в строку или в число (вместо этого воспользуйтесь  `tostring`/`tonumber`).
    ```lua
    local a = 123
    a = a .. ''
    -- плохо
    
    local a = 123
    a = tostring(a)
    -- хорошо
    
    local a = '123'
    a = a + 5 -- 128
    -- плохо
    
    local a = '123'
    a = tonumber(a) + 5 -- 128
    -- хорошо
    ```
-   Постарайтесь избегать несколько вложенных  `if`  с общим телом оператора.
    ```lua
    if (a == true and b == false) or (a == false and b == true) then
        do_something()
    end
    -- хорошо
    
    if a == true then
        if b == false then
            do_something()
        end
    if b == true then
        if a == false then
            do_something()
        end
    end
    -- плохо
    ```
-   Избегайте множества конкатенаций в одном операторе, лучше использовать  `string.format`.
    ```lua
    function say_greeting(period, name)
         local a = "good  " .. period .. ", " .. name
    end
    -- плохо
    
    function say_greeting(period, name)
        local a = string.format("good %s, %s", period, name)
    end
    -- хорошо
    
    local say_greeting_fmt = "good %s, %s"
    function say_greeting(period, name)
        local a = say_greeting_fmt:format(period, name)
    end
    -- лучше всего
    ```
-   Используйте  `and`/`or`  для указания значений переменных, используемых по умолчанию,
    ```lua
    function(input)
        input = input or 'default_value'
    end -- хорошо
    
    function(input)
        if input == nil then
            input = 'default_value'
        end
    end -- нормально, но избыточно
    ```
-  не используйте `else` если в блоке`if` вы вызываете `return`.
    ```lua
    if a == true then
        return do_something()
    end
    do_other_thing() -- хорошо
    
    if a == true then
        return do_something()
    else
        do_other_thing()
    end -- плохо
    ```
- не следует вставлять пробелы между именем функции и открывающей круглой скобкой, но аргумент необходимо разделять одним символом пробела
    ```lua 
    function name (arg1,arg2,...)
    end -- плохо
        
    function name(arg1, arg2, ...)
    end -- хорошо
    ```
- добавляйте пробел после маркера комментария
    ```lua
  while true do -- встроенный комментарий
      -- комментарий
      do_something()
  end
  --[[
  многострочный
  комментарий
  ]]--
    ```
- вставляйте пробелы до и после оператора.
     ```lua
  local thing=1
  thing = thing-1
  thing = thing*1
  thing = 'string'..'s'
  -- плохо

  local thing = 1
  thing = thing - 1
  thing = thing * 1
  thing = 'string' .. 's'
  -- хорошо
     ```
 - добавляйте пробел после запятых в таблицах.
    ```lua
    local thing = {1,2,3}
    thing = {1 , 2 , 3}
    thing = {1 ,2 ,3}
    -- плохо
    
    local thing = {1, 2, 3}
    -- хорошо
    ```
-   используйте пробелы в определениях ассоциативного массива по сторонам от знаков равенства и запятых.
    ```lua
    return {1,2,3,4} -- плохо
    return {
        key1 = val1,key2=val2
    } -- плохо
      
    return {
        1, 2, 3, 4
        key1 = val1,
        key2 = val2,
        key3 = vallll
    } -- хорошо
      
    --также можно применить выравнивание:      
    return {
        long_key  = 'vaaaaalue',
        key       = 'val',
        something = 'even better'
    }
    ```
- Добавляйте пустые строки (не слишком часто) для выделения групп связанных функций. Пустые строки не стоит добавлять между несколькими связанными программами в одну строку (например, в формальной реализации)
    ```lua
        if thing then
            -- ...что-то...
        end
        function derp()
            -- ...что-то...
        end
        local wat = 7
        -- плохо
        
        if thing then
            -- ...что-то...
        end
        
        function derp()
            -- ...что-то...
        end
        
        local wat = 7
        -- хорошо
    ```
- Удаляйте символы пробела в конце файла (они категорически запрещаются).       

# Недопущение глобальных переменных

Следует избегать глобальных переменных. В исключительных случаях используйте переменную  `_G`  для объявления, добавьте префикс или таблицу вместо префикса:
```lua
   function bad_global_example()
   end -- глобальная, очень-очень плохо
   function good_local_example()
   end
   _G.modulename_good_local_example = good_local_example -- локальная, хорошо
   _G.modulename = {}
   _G.modulename.good_local_example = good_local_example -- локальная, лучше
```
Всегда добавляйте префиксы во избежание конфликта имен

# Именование

-   имена переменных/»объектов» и «методов»/функций `snake_case`
    ```lua
    some_longnamed_variable = 123
    ```
-   имена «классов»: CamelCase
-   частные переменные/методы (в будущем параметры) объекта начинаются с символа подчеркивания  `<object>._<name>`. Избегайте  `local  function  private_methods(self)  end`
-   логическое именование приветствуется  `is_<...>`,  `isnt_<...>`,  `has_`,  `hasnt_`.
-   для «самых локальных» переменных: -  `t`  для таблиц -  `i`,  `j`  для индексации -  `n`  для подсчета -  `k`,  `v`  для получения из  `pairs()`  (допускаются,  `_`  если не используются) -  `i`,  `v`  is what you get out of  `ipairs()`  (допускаются,  `_`  если не используются) -  `k`/`key`  для ключей таблицы -  `v`/`val`/`value`  для передаваемых значений -  `x`/`y`/`z`  для общих математических величин -  `s`/`str`/`string`  для строк -  `c`  для односимвольных строк -  `f`/`func`/`cb`  для функций -  `status,  <rv>..`  или  `ok,  <rv>..`  для получения из pcall/xpcall -  `buf,  sz`  – это пара (буфер, размер) -  `<name>_p`  для указателей -  `t0`.. для временных отметок -  `err`  для ошибок
-   допускается использование сокращений, если они недвусмысленны, и если вы документируете их (или они слишком распространены).
-   глобальные переменные пишутся ЗАГЛАВНЫМИ_БУКВАМИ. Если это системная переменная, для определения используется символ подчеркивания (`_G`/`_VERSION`/..)
-   именование модулей – с помощью snake_case (избегайте подчеркивания и дефисов) - „luasql“, а не „Lua-SQL“
-   `*_mt`  и  `*_methods`  определяют метатаблицу и таблицу методов

## 

Идиомы и шаблоны

Всегда пользуйтесь круглыми скобками при вызове функций, за исключением множественных случаев (распространенные идиомы в Lua):

-   функции  `*.cfg{  }`  (`box.cfg`/`memcached.cfg`/..)
-   функция  `ffi.cdef[[  ]]`

Избегайте конструкций такого типа:

-   <func>“<name>“ (особенно избегайте require“..“)
-   `function  object:method()  end`  (используйте  `function  object.method(self)  end`)
-   не вставляйте точку с запятой в качестве символа-разделителя в таблице (только запятые)
-   точки с запятой в конце строки (только для разделения нескольких операторов в одной строке)
-   старайтесь избегать создания ненужных функций (closures/..)

## 

Модули

Не начинайте создание модуля с указания лицензии/авторов/описания, это можно сделать в файлах LICENSE/AUTHORS/README соответственно. Для написания модулей используйте один из двух шаблонов (не используйте  `modules()`):

local M = {}

function M.foo()
...
end

function M.bar()
...
end

return M

или

local function foo()
...
end

local function bar()
...
end

return {
foo = foo,
bar = bar,
}

## 

Комментирование

Пишите код так, чтобы его не нужно было описывать, но не забывайте о комментировании. Не следует комментировать Lua-синтаксис (примите, что читатель знаком с языком Lua). Постарайтесь рассказать о функциях, именах переменных и так далее.

Многострочные комментарии: используйте соответствующие скобки (`--[[  ]]--`) вместо простых (`--[[  ]]`).

Комментарии к доступным функциям (??):

--- Копирование любой таблицы (поверхностное и глубокое)
-- * deepcopy: копирует все уровни
-- * shallowcopy: копирует только первый уровень
-- Поддержка метаметода __copy для копирования специальных таблиц с метатаблицами
-- @function gsplit
-- @table         inp  оригинальная таблица
-- @shallow[opt]  sep  флаг для поверхностной копии
-- @returns            таблица (копия)

## 

Тестирование

Используйте модуль  `tap`, чтобы написать эффективные тесты. Пример файла с тестом:

#!/usr/bin/env tarantool

local test = require('tap').test('table')
test:plan(31)

do -- check basic table.copy (deepcopy)
    local example_table = {
        {1, 2, 3},
        {"help, I'm very nested", {{{ }}} }
    }

    local copy_table = table.copy(example_table)

    test:is_deeply(
        example_table,
        copy_table,
        "checking, that deepcopy behaves ok"
    )
    test:isnt(
        example_table,
        copy_table,
        "checking, that tables are different"
    )
    test:isnt(
        example_table[1],
        copy_table[1],
        "checking, that tables are different"
    )
    test:isnt(
        example_table[2],
        copy_table[2],
        "checking, that tables are different"
    )
    test:isnt(
        example_table[2][2],
        copy_table[2][2],
        "checking, that tables are different"
    )
    test:isnt(
        example_table[2][2][1],
        copy_table[2][2][1],
        "checking, that tables are different"
    )
end

<...>

os.exit(test:check() and 0 or 1)

После тестирования кода вывод будет примерно таким:

TAP version 13
1..31
ok - checking, that deepcopy behaves ok
ok - checking, that tables are different
ok - checking, that tables are different
ok - checking, that tables are different
ok - checking, that tables are different
ok - checking, that tables are different
...

## 

Обработка ошибок

Принимайте разнообразные значения и выдавайте строго определенные.

В рамках обработки ошибок это означает, что в случае ошибки вы должны предоставить объект ошибки как второе возвращаемое значение. Объектом ошибки может быть строка, Lua-таблица или cdata, в последнем случае должен быть определен метаметод  `__tostring`.

В случае ошибки нулевое значение  `nil`  должно быть первым возвращаемым значением. В таком случае ошибку трудно игнорировать.

При проверке возвращаемых значений функции проверяйте сначала первый аргумент. Если это  `nil`, ищите ошибку во втором аргументе:

local data, err = foo()
if not data then
    return nil, err
end
return bar(data)

Если производительность вашего кода не имеет первоочередное значение, постарайтесь избегать использования более двух возвращаемых значений.

В редких случаях  `nil`  можно сделать возвращаемым значением. В таком случае можно сначала проверить ошибку, а потом вернуть значение:

local data, err = foo()
if not err then
    return data
end
return nil, err
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxOTE0MTg0NSwxOTI3Mjc3Mzk2LDQ5MT
QxNDExMCwtMTA3NjA0OTY5MV19
-->