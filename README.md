# NeonGame
Игра-платформер на Unreal Engine 4
- Овчинникова Алина 
- hebgehogg@gmail.com
- тел: +7(950) 446-12-02

### Версия 4.25.3


# Design doc

### Concept: 

Platforms: Windows.  
Technologies: Unreal Engine 4.  
Languages:  английский.  
Genre: 3D platformer.  
Emotions: снятие стресса после работы/учебы (убийство времени).  
Rating:  7+ (E — Everyone).  
User Number:  single-player.  
Gameplay time:  около 20 минут.  
Maine mechanic:  собирать очки, для побития рекорда.  
Setting:  постоянное увеличение скорости.  
Goal: побить свой же рекорд (или установить новый), собрав как можно больше очков.  


### Mood: 

![Mood](https://github.com/hebgehogg/NeonGame/blob/main/photos/Visual%20references.jpg)


### Setting: 

Визуальная часть игры имитирует туннель, в котором игрока ждет куча препятствий и враги.  
Сеттинг мрачный, но как было показано в пункте "Mood", он разбавлен неоновыми элементами - это и есть фишка дизайна, это придает особое настроение.  
Процедурная генерация мира создается при помощи уникально сбалансированного алгоритма, который создан эмпирическим путем.
Игра завлекает своей концепцией - очки собирать в процессе становится труднее, тк скорость бега увеличивается.  
Также в игре есть звуки сбора бонусов и бустов, чтобы игрок понимал, что он "подобрал" объект.   


### Game Character: 

Персонаж - стандартнвая фигурка из UE4.  
Камера установлена от 3 лица.  
Персонаж имеет взаимодейсивия с объектами на карте - врагами, препядствиями, очками и бонусами, а также с самой картой.  
Описание управления и уровней будет ниже.  


### Interface: 

> Окно открывающиеся при входе  

![Окно](https://github.com/hebgehogg/NeonGame/blob/main/photos/StartGame.png)

> Окно паузы  

![Окно](https://github.com/hebgehogg/NeonGame/blob/main/photos/Paused.png)

> Окно окончания игры  

В игре сохраняется ваш лучший счет.  

![Окно](https://github.com/hebgehogg/NeonGame/blob/main/photos/GameOver.png)


### Gameplay map: 

![Gameplay map](https://github.com/hebgehogg/NeonGame/blob/main/photos/Gameplay%20map.jpg)

### Balance:

| Свойство | Характеристика |
| ------------- |:------------------:|
| Скорость передвижения игрока | 600-1500 |
| Шанс спавна бустов | 1 |
| Шанс спавна врагов | 10% |
| Шанс спавна очков (coins) | 50%, если блок не занят.|
| Количество жизней персонажа | 17% |
| Количество уровней | бесконечно |

* В 1 ряд нельзя спавнить 3 высоких блока.

* Если спавнится враг, то он 1 на ряду.

* Блок лавы не может спавнится рядом и с высоким блоком, рядом с лавой могут быть только низкие блоки.

* В "дыре" между блоками не может спавиниться ничего.

* На 1 месте не может спавнится несколько объектов.

### Level design: 

Каждый новый уровень - это увеличение скорости, которая начинается с 600 и увеличивается до 1500 с каждой секундой.  
Эта механика раскрывает суть геймплея - не застаить игрока "скучать", постоянно повышая сложность.  
На каждом уровне есть "Coins', чем больше их собрал игрок - тем лучше, в игре для этого добавлен счетчик который выводит все на экран.  
Лучший счет запоминается - хранится у пользователя на устройстве.  
Все отображено в интерфейсе.  

![Level design](https://github.com/hebgehogg/NeonGame/blob/main/photos/LevelDesign.png)

Чтобы не нагружать ПК, после прохода блока персонажем - он удаляется. (максимум 10  блоков на карте)  
Тот же механизм работает с объектами на карте.  

![Level design](https://github.com/hebgehogg/NeonGame/blob/main/photos/Destroy.png)


# Levels

Уровни генерируются процедурно:  
Платформы генерируются постоянно - максимум на карте может быть 10 платформ, платформы которые прошел игрок - удаляются.
Генирация предметов происходит по средстам рандома, каждый элемент генерируется отдельно.  
Про генерацию очков/блоков/бустов/врагов написано ниже.    
Видимость на 10 блоков.  
Мышка всегда видна, чтобы управление в меню было достунпным.  

Чтобы персонаж не умирал в случае спавна блока перед ним в начале игры, была добавлена проверка "если герой на 1 платформе (в начале) то отрисовка с 10 блока".  

![Levels](https://github.com/hebgehogg/NeonGame/blob/main/photos/%D0%9F%D1%80%D0%B5%D0%B4%D0%BC%D0%B5%D1%82%D1%8B.png)



# Управление

В игре есть 3 дорожки, переход между ними было решено сделать как в SF (дискретное передвижение), как мне кажется в ранере при повышенной скорости эта самая удобная механника передвижения.  

> Управление адаптировано под любого пользователя: для геймеров на WASD, для обычного пользователя на стрелочки.

![Управление](https://github.com/hebgehogg/NeonGame/blob/main/photos/management.jpg)

> Алгоритм перехода с дорожки на дорожку:

![Управление](https://github.com/hebgehogg/NeonGame/blob/main/photos/%D0%A3%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5.png)

# Блоки

> Блок из которых генерируется карта 

Точка отсчета спавна задана при помощи элемента Arrow, она задает вектор спавна. Спавн происходит в цикле от 1 до 10, блоки которые прошел перонаж удаляютя.  

![Блок](https://github.com/hebgehogg/NeonGame/blob/main/photos/MainBlock.png)

> Пустой блок

Пустой блок, словно "дыра вниз" создается при помощи "скрытия из виду" блока описаного выше.

> Высокий блок - блок через который нельзя перепрыгнуть - при соприкосновении "убивает" персонажа.  

![Блок](https://github.com/hebgehogg/NeonGame/blob/main/photos/Big.png)

> Низкий блок - блок через который можно перепрыгнуть - при соприкосновении "убивает" персонажа.  

![Блок](https://github.com/hebgehogg/NeonGame/blob/main/photos/Low.png)

> Лава - блок через который можно перепрыгнуть только на скорости - при соприкосновении "убивает" персонажа.  

![Блок](https://github.com/hebgehogg/NeonGame/blob/main/photos/Magma.png)


# Бонусы (Coins) - анимированные

Основная чель игры - собрать бонусы, макет представлен ниже:

![Бонусы](https://github.com/hebgehogg/NeonGame/blob/main/photos/Coin.png)

> Алгоритм сбора очков:

Очки накапливаются в переменной, с помощью нее выводятся на экран.

![Бонусы](https://github.com/hebgehogg/NeonGame/blob/main/photos/GetCoins.png)

# Бусты - анимированные

Бусты нужны для разнообразия геймплея, я добавла 3 разновидности бустов, для среднего времени гейплея это достаточно, тк они генерируются с определенным шансом, они не успеют "надоесть".

> Буст Х2 - буст увиличивающий собр монеток в 2 раза.  

![Блок](https://github.com/hebgehogg/NeonGame/blob/main/photos/BonusMultiScore.png)

> Буст замедляюзий врагов на карте.  

![Блок](https://github.com/hebgehogg/NeonGame/blob/main/photos/BonusSlowTime.png)

> Буст позволяющий проходить через стены.  

![Блок](https://github.com/hebgehogg/NeonGame/blob/main/photos/BonusWalkTHWalls.png)


# Движущийся объект - враг

Передвигается слева на прво, скорость передвижения задается рандомно, промежуток подобран эмпирическим путем.

![Враг](https://github.com/hebgehogg/NeonGame/blob/main/photos/Enemy.png)

> Передвижение врага:

![Враг](https://github.com/hebgehogg/NeonGame/blob/main/photos/MoveEnemy.png)


# Конец игры 

Наступает когда игрок натыкается на препядствие, врага или падает с платформы.

![Конец игры ](https://github.com/hebgehogg/NeonGame/blob/main/photos/Death.png)

Была использована именно функция, поскольку нам нужно использовать внешние переменные, а при использовании макроса он на этапе препроцессинга оставляет только токены, но нет типов, переменных, функций, блоков кода, то есть, правила видимости функций и переменных для макросов не работают.

# Оформление дизайна

Все блоки, заставки и картинки были нарисованы и смоделированы мной.  
Ссылок на авторов нет, так как ничего не заимствовано.  

# Ссылки на вспомогательные материалы

Документация по UE4: https://docs.unrealengine.com/en-US/index.html  
Процедурная генерация (hubr): https://habr.com/ru/post/353526/



