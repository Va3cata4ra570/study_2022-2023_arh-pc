---
## Front matter
title: "Отчёта по лабораторной работе 9"
subtitle: "Программирование цикла. Обработка аргументов командной строки."
author: "Дион Гонсан Седрик Мишель"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=trueЗырянов Артём Алексеевич	НБИбд-01-22

  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Приобретение навыков написания программ с использованием циклов и обработкой аргументов командной строки.

# Задание

1. Изучите примеры программ

2.  Напишите программу, которая находит сумму значений функции f(x) для x = x1, x2
, ..., xn, т.е. программа должна выводить значение f(x1) + f(x2)+...+f(xn). Значения x передаются как аргументы. Вид функции f(x)
выбрать из таблицы 9.1 вариантов заданий в соответствии с вариантом, полученным при выполнении лабораторной работы № 7. Создайте исполняемый файл и проверьте его работу на нескольких наборах x.

3. Загрузите файлы на GitHub.

# Теоретическое введение

Стек — это структура данных, организованная по принципу LIFO («Last In
— First Out» или «последним пришёл — первым ушёл»). Стек является частью
архитектуры процессора и реализован на аппаратном уровне. Для работы со
стеком в процессоре есть специальные регистры (ss, bp, sp) и команды.
Основной функцией стека является функция сохранения адресов возврата
и передачи аргументов при вызове процедур. Кроме того, в нём выделяется
память для локальных переменных и могут временно храниться значения регистров.

Для организации циклов существуют специальные инструкции. Для всех инструкций максимальное количество проходов задаётся в регистре ecx. Наиболее
простой является инструкция loop. Иструкция loop выполняется в два этапа. Сначала из регистра ecx вычитается
единица и его значение сравнивается с нулём. Если регистр не равен нулю,
то выполняется переход к указанной метке. Иначе переход не выполняется и
управление передаётся команде, которая следует сразу после команды loop.

# Выполнение лабораторной работы


1. Создайте каталог для программам лабораторной работы № 9, перейдите в
него и создайте файл lab9-1.asm

2. Введите в файл lab9-1.asm текст программы из листинга 9.1. 
Создайте исполняемый файл и проверьте его работу. (рис. [-@fig:001], [-@fig:002])

![Файл lab9-1.asm](image/1.png){ #fig:001 width=70%, height=70% }

![Работа программы lab9-1.asm](image/2.png){ #fig:002 width=70%, height=70% }

3. Данный пример показывает, что использование регистра ecx в теле цилка
loop может привести к некорректной работе программы. Измените текст программы добавив изменение значение регистра ecx в цикле:
Создайте исполняемый файл и проверьте его работу. Какие значения принимает регистр ecx в цикле? 
Соответствует ли число проходов цикла значению N, введенному с клавиатуры? (рис. [-@fig:003], [-@fig:004])

Программа запускает бесконечный цикл при нечетном N и выводит только нечетные числа при четном N.

![Файл lab9-1.asm](image/3.png){ #fig:003 width=70%, height=70% }

![Работа программы lab9-1.asm](image/4.png){ #fig:004 width=70%, height=70% }

4. Для использования регистра ecx в цикле и сохранения корректности работы
программы можно использовать стек. Внесите изменения в текст программы
добавив команды push и pop (добавления в стек и извлечения из стека) для
сохранения значения счетчика цикла loop. Создайте исполняемый файл и проверьте его работу. 
Соответствует ли в данном случае число проходов цикла значению N введенному с клавиатуры? (рис. [-@fig:005], [-@fig:006])

Программа выводит числа от N-1 до 0, число проходов цикла соответсвует N.

![Файл lab9-1.asm](image/5.png){ #fig:005 width=70%, height=70% }

![Работа программы lab9-1.asm](image/6.png){ #fig:006 width=70%, height=70% }

5. Создайте файл lab9-2.asm в каталоге ~/work/arch-pc/lab09 и введите в него
текст программы из листинга 9.2.
Создайте исполняемый файл и запустите его, указав аргументы. (рис. [-@fig:007], [-@fig:008])
Сколько аргументов было обработано программой?

Программа обработала 5 аргументов.

![Файл lab9-2.asm](image/7.png){ #fig:007 width=70%, height=70% }

![Работа программы lab9-2.asm](image/8.png){ #fig:008 width=70%, height=70% }

6. Рассмотрим еще один пример программы которая выводит сумму чисел,
которые передаются в программу как аргументы. (рис. [-@fig:009], [-@fig:010])

![Файл lab9-3.asm](image/9.png){ #fig:009 width=70%, height=70% }

![Работа программы lab9-3.asm](image/10.png){ #fig:010 width=70%, height=70% }

7. Измените текст программы из листинга 9.3 для вычисления произведения
аргументов командной строки. (рис. [-@fig:011], [-@fig:012])

![Файл lab9-3.asm](image/11.png){ #fig:011 width=70%, height=70% }

![Работа программы lab9-3.asm](image/12.png){ #fig:012 width=70%, height=70% }

8. Напишите программу, которая находит сумму значений функции f(x) для x = x1, x2
, ..., xn, т.е. программа должна выводить значение f(x1) + f(x2)+...+f(xn). Значения x передаются как аргументы. Вид функции f(x)
выбрать из таблицы 9.1 вариантов заданий в соответствии с вариантом, 
полученным при выполнении лабораторной работы № 7. 
Создайте исполняемый файл и проверьте его работу на нескольких наборах x.
(рис. [-@fig:013], [-@fig:014])

для варивнта 10 f(x) = 5(2+x)

![Файл lab9-4.asm](image/13.png){ #fig:013 width=70%, height=70% }

![Работа программы lab9-4.asm](image/14.png){ #fig:014 width=70%, height=70% }


# Выводы

В заключение, это позволило нам освоить работу со стеком, циклом и аргументами в ассемблере Nasm.

# Список литературы{.unnumbered}

1. [Расширенный ассемблер: NASM](https://www.opennet.ru/docs/RUS/nasm/)





