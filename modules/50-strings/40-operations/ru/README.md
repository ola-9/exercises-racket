
### Получение отдельных символов и подстрок

Получить элемент строки, зная его индекс, можно с помощью функции `string-ref`. Если указанный индекс выйдет за границы строки, то вычисление завершится с ошибкой.

```scheme
 (string-ref "apple" 3) ; #\l
 (string-ref "apple" 5)
 ; string-ref: index is out of range
 ;   index: 5
 ;   valid range: [0, 4]
 ;   string: "apple"
 ;   context...
```

Взятие же *подстроки* выглядит так:

```scheme
; индексы:  01234
(substring "Apple" 2)   ; "ple"
(substring "Apple" 1 3) ; "pp"
(substring "Apple" 10 20)
; substring: starting index is out of range
;   starting index: 10
;   valid range: [0, 5]
;   string: "Apple"
;   context...
```

Заметьте, что `(substring s n)` выделяет подстроку от символа с индексом `n` и до конца исходной строки `s`. А вот `(substring s n m)` выделяет подстроку от индекса `n` до индекса `m`, не включая последний! Такое исключение правой границы встречается довольно часто в программировании. И, как и в случае `string-ref`, Racket следит, чтобы индексы не вышли за границы.

### Конкатенация строк

Соединить несколько строк в одну или, как ещё говорят, *сконкатенировать*, можно с помощью функции `string-append`:

```scheme
(string-append "Hello, " "World!") ; "Hello, World!"
(string-append "foo")              ; "foo"
(string-append "b" "a" "r")        ; "bar"
```

### Модуль `racket/string`

В поставку Racket входит модуль `racket/string`, предоставляющий большое количество полезных, но более специфических, чем простая конкатенация, функций.

> Обычно этот модуль подключать не приходится, потому что `#lang racket` делает это автоматически.

Например, функция `string-join` из этого модуля может просто сконкатенировать все строки из заданного списка, добавив между строками строку-разделитель, а ещё способна добавить что-нибудь в начало получаемого текста, в его конец и даже перед последним присоединяемым элементом! На это стоит посмотреть:

```scheme
(string-join (list "a" "b" "c")) ; "a b c" - разделитель, это пробел

(define (greet names)
 (string-join
  names ", "
  #:before-first "Hello, "
  #:before-last " and "
  #:after-last "!"))

(greet (list "Bob"))               ; "Hello, Bob!"
(greet (list "Bob" "Tom"))         ; "Hello, Bob and Tom!"
(greet (list "Bob" "Tom" "Alice")) ; "Hello, Bob, Tom and Alice!"
```

Узнать больше об этой функции и познакомиться с другими функциями модуля вы сможете в [документации](https://docs.racket-lang.org/reference/strings.html#%28mod-path._racket%2Fstring%29).
