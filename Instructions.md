# Today's Instructions
**NB: Use [Chatgpt](https://chatgpt.com/) for generating the data only.**
1. Use Chatgpt to generate a `JSON` with up to **100** `sample medical/disaster preparedness data` based on the questions you made yesterday.
2. Save that data to a file called `sample_data.json`.
3. Using the code below and `Visual Studio Code` or [Google Colab](https://colab.research.google.com/) write a simple Chatbot that utilizes that information.
**NB: THE CODE BELOW WILL NOT WORK AND NEEDS TO BE ADJUSTED TO WORK FOR YOU.**

## The code to use:
```python
import json
import pandas as pd
import random

# Load JSON Data
with open ('location/of/data.json') as file:
    data = json.load(file)
    
# Create a DataFrame
df = pd.DataFrame(data)

# Global variable to store the bot's name
bot_name = "Bot"

def chat(user_input):
    global bot_name

    # Check if the user wants to quit
    if user_input.lower() == 'quit':
        print(f"{bot_name}: Goodbye!\n")
        return False
    
    # Check if the user wants to see the data
    elif user_input.lower() == 'data':
        print(f"{bot_name}: Here is the data.")
        print(df.to_string())
        return True
    
    # Check if the user needs help
    elif user_input.lower() == 'help':
        print(f"{bot_name}: Here are the commands you can use:")
        print("Type 'quit' to end the chat.\nType 'data' to see the data.\nType 'help' for help.\nType 'settings' to change the settings.")
        return True
    
    # Check if the user wants to change the settings
    elif user_input.lower() == 'settings':
        print(f"{bot_name}: Here are the settings you can change:")
        print("Type 'change name' to change the name of the bot.")
        return True
    
    # Check if the user wants to change the name of the bot
    elif user_input.lower() == 'change name':
        new_name = input(f"{bot_name}: What would you like to change the name to? ")
        bot_name = new_name
        print(f"{bot_name}: The name has been changed to {new_name}.")
        return True
    
    # Find a response
    else:
        # Find the response
        response = df['responses'].loc[df['keywords'] == user_input]
        
        # Check if there is a response
        if len(response) == 0:
            print(f"{bot_name}: I do not understand that.")
        else:
            print(f"{bot_name}: {response.iloc[0]}")
        return True
    
def chat_bot():
    print(f"{bot_name}: Welcome to the Chatbot! How can I help you?")
    print(f"{bot_name}: Type 'help' for help.\n")
    chatting = True
    while chatting:
        user_input = input("You: ")
        chatting = chat(user_input)
        
chat_bot()
```
