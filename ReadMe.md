В скриптовых файлах содержится программа для работы с прибором 34 для Т-15.
## Установка параметров прибора
Файл: config.json 
* data - сегодняшнее число (чтобы структурировать собираемые данные). Папка с этим числом создастся сама.
* amplitude_range - амплитудная калибровка, число от 0 до 2:
    * 0: -0.5..+0.5 В
    * 1: -0.1..+0.9 В
    * 2: -0.9..+0.1 В
* trigger_lvl - установка уровня запуска в вольтах. Может принимать отрицательные значения.
* trigger_ch - установка канала, по которому будет срабатывать триггер. По умолчанию - "ch1".
##Подключение к прибору
Файл - Connecting.py 

Нужно просто запустить один раз, при включении прибора. Если ошибок не выскочило, все должно работать. Если выскочило, то лучше запустить из web-интерфейса. 
После запуска из web-интерфейса всеми остальными скриптами можно пользоваться независимо.

## Запись данных
Производится в два этапа

1)) Файл Start_recording.py
- Задать shot_N - разряд, который собираетесь записать. 
- Задать N_pages_set - количество страниц, которые собираетесь записать.
- Запустить Start_recording

2)) Файл Stop_recording.py
- Ввести номер разряда и запустить.
- Если записалось столько страниц, сколько просили, он остановит ожидание триггера и запишет все данные в файл. 
- Если записалось меньше страниц, чем просили, программа спросит, останавливать ли запись. 
    * Если ожидание триггера надо остановить и записать все полученные данные в файл - введите 1.
    * Если нужно продолжить ожидание триггера и запись данных в оперативную память, введите 0.
    
Когда ожидание триггера остановлено - появится сообщение: "Ожидание триггера остановлено". Если такого сообщения нет, то что-то 
пошло не так, но это не страшно. В файл данные он записал, а остановка триггера не обязательна для того, чтобы снова запустить запись данных.

Чтобы записать следующий разряд токамака, надо заново запустить файл Start_recording и далее по списку.

## Вывод данных на экран 
* Для вывода сырых данных сигналов - файл Viewer_data.py. 
    * Написать номер разряда, запустить файл.
    * Выводит N картинок по 8 графиков в каждом, где N = N_page // 50 + 1, N_page - кол-во записанных страниц.
    
* Для вывода сигналов в фотоэлектронах - файл To_phe_and_time_evolution.
    * Написать номер разряда, запустить. 
    * Выводит 8 картинок. По оси x - время, посчитанное с той дельтой комбископа, которую мы определили в чт.
