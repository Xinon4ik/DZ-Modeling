from PIL import Image, ImageOps
import matplotlib.pyplot as plt


def BrezenhemLine(image, x0, y0, x1, y1, color):
    # Считаем разницу между начальными и конечными координатами отдельно для 'х' и 'y'
    delta_x = abs(x1 - x0)
    delta_y = abs(y1 - y0)

    epsilon = 0  # Переменная, отвечающая за необходимость изменения координаты 'y'
    step = 1  # Задаём шаг изменения координаты 'y'
    reverse = False
    # Для облегчения алгоритма, если 'x0 > x1' меняем координаты местами
    if (x0 > x1):
        x0, x1, y0, y1 = x1, x0, y1, y0

    #  Обрабатываем возможность изображения линий, y которых 'y0 > y1'
    if (y0 > y1):
        step = -1

    if (delta_x < delta_y):  # Проверка на угол больше 45 градусов
        x0, y0, x1, y1, delta_x, delta_y = y0, x0, y1, x1, delta_y, delta_x  # Меняем 'х' и 'y' переменные местами
        reverse = True  # Флаг для корректного отображения отрезков с углом наклона более 45 градусов

        if (step == -1):  # Меняем местами координаты для прямых с шагом по оси 'y' равным -1
            x0, x1, y0, y1 = x1, x0, y1, y0

    for x in range(x0, x1 + 1):
        if reverse == True:
            image.putpixel((y0, x), color)

        else:
            image.putpixel((x, y0), color)
        epsilon = epsilon + 2 * delta_y

        if epsilon >= delta_x:
            y0 += step
            epsilon -= 2 * delta_x


def Test_Lines():  # Ручная проверка линий с различными углами наклона
    test_image = Image.new('RGB', (20, 19))  # Задаём параметры поля

    # Линии с углом наклона не более 45 градусов при различных значениях x, y
    BrezenhemLine(test_image, 1, 1, 6, 2, (255, 0, 0))  # Красный
    BrezenhemLine(test_image, 12, 2, 7, 1, (255, 51, 153))  # Розовый
    BrezenhemLine(test_image, 13, 1, 15, 3, (250, 128, 0))  # Оранжевый
    BrezenhemLine(test_image, 18, 3, 16, 1, (255, 255, 0))  # Жёлтый

    BrezenhemLine(test_image, 1, 5, 6, 4, (140, 200, 0))  # Жёлто-зелёный
    BrezenhemLine(test_image, 12, 4, 7, 5, (0, 255, 0))  # Зеленый
    BrezenhemLine(test_image, 13, 6, 15, 4, (51, 120, 0))  # Тёмно-зелёный
    BrezenhemLine(test_image, 18, 4, 16, 6, (153, 255, 153))  # Светло-зеленый

    # Линии с углом наклона более 45 градусов при различных значениях x, y
    BrezenhemLine(test_image, 1, 6, 2, 11, (0, 255, 255))  # Голубой
    BrezenhemLine(test_image, 2, 17, 1, 12, (0, 100, 200))  # Тёмно-синий
    BrezenhemLine(test_image, 4, 6, 3, 11, (0, 0, 255))  # Синий
    BrezenhemLine(test_image, 3, 17, 4, 12, (150, 0, 255))  # Фиолетовый

    # Вертикальные линии
    BrezenhemLine(test_image, 7, 6, 7, 11, (96, 96, 96))  # Тёмно-серый
    BrezenhemLine(test_image, 9, 11, 9, 6, (160, 160, 160))  # Серый

    # Горизонтальные линии
    BrezenhemLine(test_image, 7, 13, 12, 13, (200, 200, 200))  # Светло-серый
    BrezenhemLine(test_image, 12, 15, 7, 15, (255, 255, 255))  # Белый

    test_image = ImageOps.flip(test_image)  # Переворачиваем поле относительно горизонтальной оси
    plt.figure('Test lines')  # Задаём название окну с линиями
    plt.imshow(test_image)


def Custom_Line():
    color = (255, 255, 255)  # Задаем белый цвет для линии

    print('Поле будет иметь размеры [size x size], '
          'следите, что бы координаты отрезка были натуральными, меньше, чем size')

    # Задаём размеры поля и координаты отрезков
    x0 = int(input('x0 = '))
    y0 = int(input('y0 = '))
    x1 = int(input('x1 = '))
    y1 = int(input('y1 = '))

    if x0 >= x1:
        size_x = x0 + 10
    else:
        size_x = x1 + 10

    if y0 >= y1:
        size_y = y0 + 10
    else:
        size_y = y1 + 10

    image = Image.new('RGB', (size_x, size_y))  # Задаём параметры поля
    BrezenhemLine(image, x0, y0, x1, y1, color)  # Строим линию по введённым координатам

    image = ImageOps.flip(image)  # Переворачиваем поле относительно горизонтальной оси
    plt.figure('Custom lines')  # Задаём название окну с линией
    plt.imshow(image)


def Main():
    test_lines_flag = str(input('Вы хотите начертить линии с заранее заданными координатами? [+]/[-]'))
    if test_lines_flag == ('+'):
        Test_Lines()

    custom_line_flag = str(input('Вы хотите начертить линию с произвольными координатами? [+]/[-]'))
    if custom_line_flag == ('+'):
        Custom_Line()

    plt.show()  # Демонстрируем полученный результат


Main()
