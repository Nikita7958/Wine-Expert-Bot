import telebot
from telebot import types

bot = telebot.TeleBot()


# @bot.message_handler(commands=['score'])
# def score(message):
#     markup3 = types.ReplyKeyboardMarkup()
#     btn1 = types.InlineKeyboardButton("понравился")
#     btn2 = types.InlineKeyboardButton("непонравился")
#     markup3.row(btn1, btn2)
#     bot.send_message(message.chat.id, 'Как тебе коктель? оцени "понравился" или "непонравился"', parse_mode=markup3)
#     if message.text == 'понравился':
#         bot.reply_to(message, "Вау! Я вижу что ты высокий ценитель, я запомню что тебе он  понраву.")
#         # f = open('I remember', 'w')
#
#         # bot.send_message(message.chat.id, f)
#     elif message.text == 'непонравился':
#         bot.send_message(message.chat.id, 'жаль')


@bot.message_handler(commands=['go', 'start'])
def go(message):
    markup = types.ReplyKeyboardMarkup()  # водим клавиатуру в функцию
    btn1 = types.InlineKeyboardButton("Да")  # создаём кнопку
    btn2 = types.InlineKeyboardButton("Нет")  # создаём кнопку
    markup.row(btn1, btn2)  # раставляем кнопки в ряду

    bot.send_message(message.chat.id, f'Здраствуй, {message.from_user.first_name},'
                                      f' не желаешь ли <b>чего-нибудь</b> выпить?', parse_mode='html',
                     reply_markup=markup)  # бот нам предлагаетвыбор ивыводит кнопки на экран
    bot.register_next_step_handler(message, get_alcohol)  # отпровляет бота на следующую функцию


def get_alcohol(message):
    if message.text == 'Да':  # если пользователь нажал да
        markup = types.ReplyKeyboardMarkup()  # водим клавиатуру в функцию
        btn1 = types.KeyboardButton("С алкоголем")  # создаём кнопку
        btn2 = types.KeyboardButton("Без алкоголя")  # создаём кнопку
        markup.row(btn1, btn2)  # раставляем кнопки в ряду
        bot.reply_to(message, "Чего тебе хочется?", reply_markup=markup)  # бот отпровляет сообщение
        bot.register_next_step_handler(message, get_answer_alcohol)

    elif message.text == 'Нет':
        bot.send_message(message.chat.id, f'Тогда до свидания, {message.from_user.first_name}')


def get_answer_alcohol(message):
    if message.text == 'С алкоголем':
        markup = types.ReplyKeyboardMarkup()
        btn1 = types.KeyboardButton("Крепкий")
        btn2 = types.KeyboardButton("Слабоалкогольный")
        markup.row(btn1, btn2)
        bot.reply_to(message, "Что ты предпочитаешь?", reply_markup=markup)
        bot.register_next_step_handler(message, Strong_and_NotStrong_alcohol)

    elif message.text == 'Без алкоголя':
        markup = types.ReplyKeyboardMarkup()
        btn1 = types.KeyboardButton("Молочный")
        btn2 = types.KeyboardButton("Не молочный")
        markup.row(btn1, btn2)
        bot.reply_to(message, "Что ты предпочитаешь?", reply_markup=markup)
        bot.register_next_step_handler(message, Not_alcohol)


def Strong_and_NotStrong_alcohol(message):
    markup = types.InlineKeyboardMarkup()

    if message.text == 'Крепкий':
        btn1 = types.InlineKeyboardButton("Манхетан", url='https://ru.inshaker.com/cocktails/38-manhetten')
        btn2 = types.InlineKeyboardButton('Зеленая фея', url='https://ru.inshaker.com/cocktails/408-zelenaya-feya')
        btn3 = types.InlineKeyboardButton('Олд фешен', url='https://ru.inshaker.com/cocktails/53-old-feshen')
        btn4 = types.InlineKeyboardButton('Май тай', url='https://ru.inshaker.com/cocktails/37-may-tay')
        btn5 = types.InlineKeyboardButton('Космополитен', url='https://ru.inshaker.com/cocktails/29-kosmopoliten')
        btn6 = types.InlineKeyboardButton('Б-52', url='https://ru.inshaker.com/cocktails/164-b-52')
        btn7 = types.InlineKeyboardButton('Лонг айленд айс ти',
                                          url='https://ru.inshaker.com/cocktails/35-long-aylend-ays-ti')
        btn8 = types.InlineKeyboardButton('Секс на пляже', url='https://ru.inshaker.com/cocktails/814-seks-na-plyazhe')
        btn9 = types.InlineKeyboardButton('Дайкири', url='https://ru.inshaker.com/cocktails/22-daykiri')
        btn10 = types.InlineKeyboardButton('Негрони', url='https://ru.inshaker.com/cocktails/55-negroni')
        btn11 = types.InlineKeyboardButton('Маргарита', url='https://ru.inshaker.com/cocktails/39-margarita')
        markup.row(btn1, btn2, btn3)
        markup.row(btn4, btn5, btn6)
        markup.row(btn7, btn8)
        markup.row(btn9, btn10, btn11)
        bot.reply_to(message, "Может быть, тогда тебе понравится что-нибудь из этого🍷", reply_markup=markup)

    elif message.text == 'Слабоалкогольный':
        btn1 = types.InlineKeyboardButton("Апероль Шприц", url='https://ru.inshaker.com/cocktails/1098-aperol-shprits')
        btn2 = types.InlineKeyboardButton('Мохито', url='https://ru.inshaker.com/cocktails/57-mohito')
        btn3 = types.InlineKeyboardButton('Джин тоник', url='https://ru.inshaker.com/cocktails/368-dzhin-tonik')
        btn4 = types.InlineKeyboardButton('Текила санрайз', url='https://ru.inshaker.com/cocktails/873-tekila-sanrayz')
        btn5 = types.InlineKeyboardButton('Беллини', url='https://ru.inshaker.com/cocktails/17-bellini')
        btn6 = types.InlineKeyboardButton('Пина колада', url='https://ru.inshaker.com/cocktails/89-pina-kolada')
        btn7 = types.InlineKeyboardButton('Мохито клубничный',
                                          url='https://ru.inshaker.com/cocktails/632-mohito-klubnichnyy')
        btn8 = types.InlineKeyboardButton('Отвертка', url='https://ru.inshaker.com/cocktails/52-otvertka')
        btn9 = types.InlineKeyboardButton('Том коллинз', url='https://ru.inshaker.com/cocktails/44-tom-kollinz')
        btn10 = types.InlineKeyboardButton('Пенициллин', url='https://ru.inshaker.com/cocktails/1086-penitsillin')
        btn11 = types.InlineKeyboardButton('Американо', url='https://ru.inshaker.com/cocktails/16-amerikano')
        markup.row(btn1, btn2, btn3)
        markup.row(btn4, btn5, btn6)
        markup.row(btn7, btn8)
        markup.row(btn9, btn10, btn11)
        bot.reply_to(message, "Может быть, тогда тебе понравится что-нибудь из этого🍷", reply_markup=markup)


def Not_alcohol(message):
    markup = types.InlineKeyboardMarkup()
    if message.text == 'Молочный':
        btn1 = types.InlineKeyboardButton("Молочный коктейль",
                                          url='https://eda.ru/recepty/napitki/molochnij-koktejl-29064')
        btn2 = types.InlineKeyboardButton('коктейль с бананом',
                                          url='https://eda.ru/recepty/napitki/molochnij-koktejl-s-bananom-37433')
        btn3 = types.InlineKeyboardButton('Клубничный  коктейль',
                                          url='https://eda.ru/recepty/napitki/klubnichnij-molochnij-koktejl-28186')
        btn4 = types.InlineKeyboardButton('Бананово  коктейль',
                                          url='https://eda.ru/recepty/napitki/bananovo-molochnyy-kokteyl-32264')
        btn5 = types.InlineKeyboardButton('Вишневый  коктейль с какао',
                                          url='https://eda.ru/recepty/napitki/vishnevij-molochnij-koktejl-s-kakao-24138')
        btn6 = types.InlineKeyboardButton('Коктейль с яблоком',
                                          url='https://eda.ru/recepty/napitki/molochnij-koktejl-s-jablokom-50206')
        markup.row(btn1, btn2)
        markup.row(btn3, btn4)
        markup.row(btn5, btn6)
        bot.reply_to(message, "Может быть, тогда тебе понравится что-нибудь из этого🥤", reply_markup=markup)

    elif message.text == 'Не молочный':
        btn1 = types.InlineKeyboardButton("Атланта",
                                          url='https://eda.ru/recepty/napitki/bezalkogolnij-koktejl-atlanta-45331')
        btn2 = types.InlineKeyboardButton('Шмель',
                                          url='https://eda.ru/recepty/napitki/bezalkogolnij-koktejl-shmel-51661')
        btn3 = types.InlineKeyboardButton('Стеклянная весна',
                                          url='https://eda.ru/recepty/napitki/bezalkogolnye-kokteyli-steklyannaya-vesna-92484')
        btn4 = types.InlineKeyboardButton('Мохито безалкогольный',
                                          url='https://eda.ru/recepty/napitki/mohito-bezalkogolnij-28074')
        btn5 = types.InlineKeyboardButton('Безалкогольный глинтвейн',
                                          url='https://eda.ru/recepty/napitki/bezalkogolnij-glintvejn-31015')
        btn6 = types.InlineKeyboardButton('Безалкогольный апельсиново-клюквенный пунш',
                                          url='https://eda.ru/recepty/napitki/bezalkogolnij-apelsinovo-kljukvennij-punsh-20378')
        markup.row(btn1, btn2, btn3)
        markup.row(btn4)
        markup.row(btn5)
        markup.row(btn6)
        bot.reply_to(message, "Может быть, тогда тебе понравится что-нибудь из этого🥤", reply_markup=markup)

@bot.message_handler(commands=['help'])
def Help(message):
    bot.send_message(message.chat.id,
                     f"<b>Привет!👋 {message.from_user.first_name}</b>, этот бот поможет тебе выбрать напиток "
                     f"для приятного время препровождения. "
                     "Если хочешь <b>начать</b> напиши /go.", reply_markup='html')
    bot.register_next_step_handler(message, go)

@bot.message_handler()
def shall_we_start(message):
    bot.send_message(message.chat.id, 'Давай начнём с начала')
    bot.register_next_step_handler(message, go)



bot.polling(none_stop=True)
