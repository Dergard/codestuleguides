## Отступы и форматирование

+ 4 пробела вместо табуляции
+ файл должен заканчиваться на один символ переноса строки, но не должен заканчиваться на пустой строке (два символа переноса строки)
+ Отступы всех do/while/for/if/function должны составлять 4 пробела.
+ or/and в if должны быть обрамлены круглыми скобками ():
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
+ Не используйте конкатенацию для конвертации в строку или в число (вместо этого воспользуйтесь tostring/tonumber)

```lua
local a =  123

a **=** a **..**  ''

-- плохо

**local** a **=**  123

a **=**  **tostring****(**a**)**

-- хорошо

**local** a **=**  '123'

a **=** a **+**  5  -- 128

-- плохо

**local** a **=**  '123'

a **=**  **tonumber****(**a**)**  **+**  5  -- 128

-- хорошо

<![if !supportLists]>· <![endif]>Постарайтесь избегать несколько вложенных if с общим телом оператора:

**if**  **(**a **==**  **true**  **and** b **==**  **false****)**  **or**  **(**a **==**  **false**  **and** b **==**  **true****)**  **then**

do_something**()**

**end**

-- хорошо

**if** a **==**  **true**  **then**

**if** b **==**  **false**  **then**

do_something**()**

**end**

**if** b **==**  **true**  **then**

**if** a **==**  **false**  **then**

do_something**()**

**end**

**end**

-- плохо

<![if !supportLists]>· <![endif]>Избегайте множества конкатенаций в одном операторе, лучше использовать string.format

**function** say_greeting**(**period**,** name**)**

**local** a **=**  "good  "  **..** period **..**  ", "  **..** name

**end**

-- плохо

**function** say_greeting**(**period**,** name**)**

**local** a **=**  **string.format****(**"good %s, %s"**,** period**,** name**)**

**end**

-- хорошо

**local** say_greeting_fmt **=**  "good %s, %s"

**function** say_greeting**(**period**,** name**)**

**local** a **=** say_greeting_fmt:format**(**period**,** name**)**

**end**

-- лучше всего

<![if !supportLists]>· <![endif]>Используйте and/or для указания значений переменных, используемых по умолчанию

<![if !supportLists]>· <![endif]>**function****(**input**)**

<![if !supportLists]>· <![endif]> input **=** input **or**  'default_value'

<![if !supportLists]>· <![endif]>**end**  -- хорошо

<![if !supportLists]>· <![endif]>

<![if !supportLists]>· <![endif]>**function****(**input**)**

<![if !supportLists]>· <![endif]>  **if** input **==**  **nil**  **then**

<![if !supportLists]>· <![endif]> input **=**  'default_value'

<![if !supportLists]>· <![endif]>  **end**

<![if !supportLists]>· <![endif]>**end**  -- нормально, но избыточно

операторов if и возврата:

if a == true then

return do_something()

end

do_other_thing() -- хорошо

if a == true then

return do_something()

else

do_other_thing()

end -- плохо

Использование пробелов:

не следует вставлять пробелы между именем функции и открывающей круглой скобкой, но аргумент необходимо разделять одним символом пробела

function name (arg1,arg2,...)

end -- плохо

function name(arg1, arg2, ...)

end -- хорошо

добавляйте пробел после маркера комментария

while true do -- встроенный комментарий

-- комментарий

do_something()

end

--[[

многострочный

комментарий

]]—

примыкающие  конструкции

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

добавляйте пробел после запятых в таблицах

local thing = {1,2,3}

thing = {1 , 2 , 3}

thing = {1 ,2 ,3}

-- плохо

local thing = {1, 2, 3}

-- хорошо

используйте пробелы в определениях ассоциативного массива по сторонам от знаков равенства и запятых

return {1,2,3,4} -- плохо

return {

key1 = val1,key2=val2

} -- плохо

return {

1, 2, 3, 4

key1 = val1, key2 = val2,

key3 = vallll

} -- хорошо

также можно применить выравнивание:

return {

long_key  = 'vaaaaalue',

key  = 'val',

something = 'even better'

}

также можно добавлять пустые строки (не слишком часто) для выделения групп связанных функций. Пустые строки не стоит добавлять между несколькими связанными программами в одну строку (например, в формальной реализации)

не слишком часто можно добавлять пустые строки в коде функций, чтобы отделить друг от друга логические части

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

Удаляйте символы пробела в конце файла (они категорически запрещаются)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUwOTk0MjQ0OCw0OTE0MTQxMTAsLTEwNz
YwNDk2OTFdfQ==
-->