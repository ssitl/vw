Примерный план:
---------------

- [ ] Определиться с форматами данных вирусов и других
  игровых артефактов (JSON). Записать это в файл.

	Вопросы (по игре/возможностям), чтобы думать про
	структуру вируса дальше.

	Список ВОЗМОЖНЫХ характеристик вируса на будущее:
	1. Размер "памяти". Ограничивает возможность написания
	"заумных логик". Например, путем ограничения количества
	условий в алгоритме.
	2. Поле зрения.
	3. Скорость (дальность) передвижения за 1 ход.
	По этим пунктам основной вопрос - нужны ли они, или будем
	делать все проще?

  !!!!!
  Для тестовой версии оставляем следующие параметры вируса:
  Имя игока (playerName)
  Название вируса (игрок может иметь несолько разных вирусов)

  Параметры отдельной клетки вируса:
  Здоровье (health)
  Сила атаки (attack/strength?)
  Защита (deffence?)

  x, y - соответствующие координаты на игровом поле.

	Дополнительные вопросы.
	1. Будет ли у игрока возможность распределять "хиты" по
	параметрам вируса? Т.е. дается 10 хитов, которые игрок
	распределяет по жизни/силе/атаке и т.д.

  !!!!!
  Для первой версии такой возможности нет

- [ ] Определить, какие нужны функции для их обработки
  и преобразования

	Для работы нам будут нужны основные функции:
	1. Определить общую картину вокруг (посмотреть/look)

  Входные параметры: id клетки. Функция так-же оперирует объектом "игровое поле".
  Возвращаемый результат: набор значений, описывающих обстановку в радиусе видимости для текущей клетки
    - количество клеток (своих/чужих/всего)
    - точка(набор точек), куда может "сходить врус", чтобы оказаться в месте с (минимальным/максимальным) количеством (своих/чужих/любых клеток). Текущая точка (в которой сейчас находится вирус так-же учитывается) в списке возможных "сходить", если подходит под одно из условий.

	2. Принять решение (решить/с английским туго)
	В этой функции выполняется алгоритм "логики" вируса в
	зависимости от обстановки вокруг.
  Входные параметры: "логика вируса", "обстановка в поле видимости" (результат работы функции "посмотреть" для кокретной клетки), id клетки. Данная функция так-же оперирует объектом "игровое поле".
  Возвращаемый результат: значения "вид действия" и, при необходимости, дополнительные параметры (место на игровом поле, куда сходить, какой вирус атаковать и т.д.)

	3. Выполнить действие (выполнить/act - и тут туго)
	Функция, собственно, выполняет действие - ходит /
	атакует / делится и прочее.
  Входные параметры: id клетки. Данная функция так-же оперирует объектом "игровое поле".
  Результат выполнения: соответствующие изменения в объекте "игровое поле".

	Я бы все эти 3 функции завернул в общую обертку (процесс/process),
	которая бы выполнялась над каждым элементом вируса.

- [ ] Определить минимальный HTTP API и как он должен
  работать
		
		В тестовой версии игры достаточно следующих экранов:
		
		*Стартовый

		Описание: отображает меню из двух кнопок
		(лаборатория/бой) + общуюу статистику.
		Функции:
			- показать главный экран: отображается две кнопки -
			лаборатория и бой и так-же отображается статистика по
			игрокам;
		Дополнительные функции:
			- получить статистику по игрокам;


		*Лаборатория*
		Описание: позволяет создавать или редактировать вирус. Под
		редактированием подразумеватся задать/сменить вирусу имя
		и загрузить алгоритм.
		Функции:
			- показать экран лаборатории:  отображается список
			вирусов игрока, кнопки создать, редактировать,
			загрузить алгоритм, сохранить и текстовое поле для
			ввода названия вируса;
		Дополнительные функции:
			- получить список вирусов игрока;
			- загрузить алгоритм от клиента на сервер;
			- записать новые данные по вирусу в БД;
			

		*Боевой*
		Опиание: на данном экране выбирается режим боя
		(песочница - со своими или "стандартными" вирусами или
		бой с игроком).
		Функции:
			- показать экран выбора режима: отображаются две
			кнопки - бой в песочнице и бой с игроком;
			- показать экран подготовки к бою (режим боя с
			игроком): выводится список всех вирусов игрока, где он
			может выбрать одного из них. Так-же отображается
			название вируса, который выбрал второй игрок или
			сообщение о том, что второй игрок еще не сделал свой
			выбор. Отображается кнопка "готов".
			- показать экран подготовки к бою (режим песочница):
			выводится список вирусов игрока + список "стандартных
			вирусов. Отображается кнопка "готов". 
			- показать экран самого боя: отображается несколько
			игровых полей через определенный срез времени,
			выводится информация о результатах боя.
		Дополнительные функции:
			- получить список вирусов игрока;
			- получить список стандартных вирусов;
			- получить результат боя ввиде срезов игрового поля;

- [ ] Реализовать функции для обработки данных
- [ ] Реализовать HTTP API для доступа к этим функциям
- [ ] Сформировать дальнейшие планы
