# Chatbot-response-using-python
A simple chatbot with python


main.py

import re

import long_responses as long

def

message_probability(user_message,

recognised_words,

single_response=False,

required_words=[]):

message_certainty = 0

has_required_words = True

# Counts how many words are present in each predefined message

for word in user_message:

if word in recognised_words:

message_certainty += 1

# Calculates the percent of recognised words in a user message

percentage = float(message_certainty) / float(len(recognised_words))

for word in required_words:

if word not in user_message:

has_required_words = False

break

if has_required_words or single_response:

return int(percentage*100)

else:

return 0

def check_all_messages(message):

highest_prob_list = {}

def response(bot_response,list_of_words,single_response=False, required_words=[]):

nonlocal highest_prob_list

highest_prob_list[bot_response]=message_probability(message,list_of_words,single_response,re

quired_words)

# Response ----------------------------------------------------------------

response('Hello!',['hello','hi','sup','hey','heyo'],single_response=True)

response('I\'m doing fine,and you?', ['how','are','you','doing'], required_words=['how'])

response('Thank you!', ['i','love','code','palace'], required_words=['code','palace'])

#long responses

response(long.R_EATING, ['what','you','eat'], required_words=['you','eat'])

response(long.R_ADVICE,['give', 'me', 'a','advice'], required_words=['give','advice'])

response(long.R_COMPUTER,['who','is','the','father','of','the','computer'],

required_words=['father','computer'])

best_match = max(highest_prob_list, key=highest_prob_list.get)

#print(highest_prob_list)

return long.unknown() if highest_prob_list[best_match] < 1 else best_match

def get_response(user_input):

split_message = re.split(r'\s+|[,;?!.-]\s*', user_input.lower())

response = check_all_messages(split_message)

return response

# Testing the response system

while True:

print('Bot: ' + get_response(input('You: ')))

long_responses.py

import random

R_EATING = "I don't like eat anything because I'm a bot obviously!"

R_ADVICE = "Whether it's a new challenge or a difficult task, keep pushing yourself to do

better and never setbacks discourage you."

R_COMPUTER = "The father of the computer is Charles Babbage,who is credited with

designing and building the first mechanical computer in the 19th century."

def unknown():

response = ['Could you please re-phrase that?',

"...",

"Sounds about right",

"What does that mean?"][random.randrange(4)]

return response


