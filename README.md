# hakaton
import telebot
import random
import os
from conflic import token
bot = telebot.TeleBot(token)

# Handle '/start' and '/help'
@bot.message_handler(commands=['help', 'start'])
def send_welcome(message):
    bot.reply_to(message, """\
Hi there, I am EchoBot.
I am here to echo your kind words back to you. Just say anything nice and I'll say the exact same thing to you!\
""")
    
@bot.message_handler(commands=['craft'])
def send_craft(message):
    photo_name = random.choice(os.listdir('photos'))
    with open(f'photos/{photo_name}', 'rb') as f:  
        bot.send_photo(message.chat.id, f) 

# Handle all other messages with content_type 'text' (content_types defaults to ['text'])
@bot.message_handler(func=lambda message: True)
def echo_message(message):
    bot.reply_to(message, message.text)


bot.infinity_polling()

token = '7572848821:AAESz485YSaQCQqZWTCz7aFtBvSH98wiGUk'
