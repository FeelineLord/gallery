Здравствуйте. Меня зовут Вадим. Это моё небольшое приложение для просмотра/сохранения фотографий, написанное на собственном коде без подключаемых пользовательских компонентов. В разработке использовался react + sass.

Основной функционал:

1. Загрузка фотографий lorem picsum с нормализацией размера. Для облегчения загрузки  размер загружаемых фотографий соответствует их размерам на странице. В режиме просмотра (при клике на фото) загружается изображение с размерами экрана вашего компьютера/телефона/планшета и сохранением пропорций. Поскольку изображения при стандартной сортировке выглядят как могильные плиты, реализована псевдорандомная сортировка, изображения разбиты на коллоны:

ширина экрана > 1367:
small: 7 колонн,
medium: 5 колонн,
large: 3 колонны.

ширина экрана между 1367 и 800:
small: 5 колонн,
madium: 4 колонны,
large: 2 колонны.

ширина экрана < 800:
small: 3 колонны,
medium: 2 колонны,
large: 1 колонна.

Опция смены размеров появляется при наведении на "images size", опция режима просмотра - при нажатии на любую картинку.

P.S: здесь была трудность. Чтоб добиться эффекта "разброса" изображений с 6-ю вариантами числа колонн, которые в сумме дают ширину монитора и разные paddings, пришлось попробовать реализацию разных идей. В итоге всё решилось довольно просто.

2. Работа через local storage. Все настройки и адреса "лайкнутых" фото находятся в браузерном объекте, сохраняя ваши действия после обновления страницы. Если Вы нашли  ошибку (у меня их не было, но я ведь джун), и у Вас ничего не работает, для продолжения просмотра очистите local storage или воспользуйтесь анонимным окном в браузере.

3. Смена темы оформления. Элементы первой я взял у себя же - из собственной игры, но мне понравилось, как она выглядит. Вторая, "облегчённая", светлая тема - в стандартных светлых цветах. Здесь трудностей не было.

4. Постраничная "пагинация". Во избежание ошибок Вы можете выбрать количество изображений/страниц, находясь только на 1й странице. Введите в инпут число от 50 до 100 на панели навигации. На остальных страницах он будет недоступен, ведь от этой опции напрямую зависит количество страниц. Изначально я "фетчил" 100 изображений, и при выборе не происходило повторного рендера, что неплохо оптимизировало приложение. Однако от этой идеи пришлось отказаться ввиду "потери" фотографий, которые при количестве на страницу меньше 100 просто терялись. Ограничение от 50 до 100 сделано в целях красоты и оптимальной нагрузки: меньше = пустой экран, больше = возможны лаги.

5. Реализована простая система хранения результатов выполнения fetch на стороне браузера. После успешной загрузки страницы с последующим переходом на другую страницу и возвратом на исходную Вы обнаружите, что загрузка изображений происходит быстрее. Обратите внимание: изменив images per page, Вы обнулите сохранённые данные.

6. Два «состояния». В первом можно найти только отсортированные "понравившиеся" фотографии. На странице со всеми изображениями можно нажать на "сердечко": если оно чёрное, то станет красным, и фото отправится на страницу "понравившиеся", но при этом останется и на главной. "Привилегированное" фото можно "дебафнуть" до обычного, нажав на красный лайк. В таком случае оно не будет отображаться на странице "liked". Переход осуществляется по ссылке в левом верхнем углу. До тех пор, пока Вы не выберете хотя бы одну фотографию, ссылка не будет доступна для перехода.

7. Приложение полностью адаптивное. Если у Вас есть время, посмотрите пожалуйста на разных разрешениях (от 320px). Поплыть не должно. НЕ ДОЛЖНО!

Замеченные и неисправленные недостатки:
- В режиме «просмотра» изображения грузятся размером чуть больше текущих соотношений сторон экрана пользователя. Это сделано для того, чтобы избежать "мыльной картинки" и "шума" при искусственном масштабировании средствами css. Следовательно, если открыть картинку на маленьком разрешении (mobile) и расширять экран до больших размеров (desktop), её качество будет падать. 
*Upd: решил с помощью debounce-функции замены url при ресайзе. Теперь изображения в view mode будут качественными на любых экранах.

- Попадаются одинаковые изображения с разными ID. Соответственно, стоило бы их отсеять, но для этого нужно иметь массив со всеми объектами. В случае нашего приложения это не затратно, однако если представить себе fetch большего количества картинок, такое решение стало бы печальным.

- При смене ссылок в view режиме изображение мигает, чем лупит по глазам. Бррр. Я даже не знаю как это исправить, ведь на localhost такого не было.

LINK: https://feelinelord.github.io/gallery/
