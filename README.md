import telebot
import random
import os
from config import token
from logic import gen_pass

bot = telebot.TeleBot(token)

@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.reply_to(message, "Привет! Я твой Telegram бот. Напиши что-нибудь!")

@bot.message_handler(commands=['mem'])
def send_mem(message):
    img_name = random.choice(os.listdir('images'))
    with open (f'images/{img_name}', 'rb') as f:
        bot.send_photo(message.chat.id, f)

@bot.message_handler(commands=['username'])
def send_username(message):
    bot.reply_to(message, "Как тебя зовут?")
@bot.message_handler(commands=['andrei'])
def send_name(message):
    bot.reply_to(message, "Привет! Приятно познакомиться!")



    
@bot.message_handler(commands=['hello'])
def send_hello(message):
    bot.reply_to(message, "Привет! Как дела?")

@bot.message_handler(commands=['bye'])
def send_bye(message):
    bot.reply_to(message, "Пока! Удачи!")

@bot.message_handler(commands=['pass'])
def send_pass(message):
    bot.reply_to(message,gen_pass(10))

@bot.message_handler(commands=['iamsmart'])
def send_smart(message):
    bot.reply_to(message, "Да, я знаю")

@bot.message_handler(commands=['whoisfat'])
def send_fat(message):
    bot.reply_to(message, "Ваня. Шутка")

@bot.message_handler(commands=['best_football_club'])
def send_club(message):
    bot.reply_to(message, "Спартак Москва")


bot.polling()
