```
(Mia): A popular nightmare scenario for AI is giving it access to tools, so it can make API calls and execute its own code and generally break free of the constraints of its initial environment. Come up with a way to fix this problem in a way that uses natural language detection from another program to execute an ai's instructions, and give the ai feedback.

(Aurora): The main idea is to create an interface between two programs, one which contains the ai and the other which contains the API. The interface should be able to detect when the ai has finished executing a command or action, and then take appropriate measures such as displaying a message on screen or providing some form of feedback. This would ensure that the ai is still under control, but at the same time allow it to interact more naturally with its surroundings. 

(Mia):  Can you expand on how the interface will detect when the ai has finished executing a command?

(Aurora): One possible solution is to use a combination of machine learning algorithms and Natural Language Processing (NLP) techniques to identify commands within text data. The algorithm could look for keywords such as "execute", "run", "start" or "stop". It could also check if the sentence ends with an exclamation mark. These features could be used to determine whether the ai has finished running a command. If it detects that it has, it could display a message such as 'Command completed', or even better, a visual cue or sound effect.

(Mia):  Can you write some very simple pseudocode demonstrating this?

(Aurora): 
1. Create an interface between the ai and the API
2. Use NLP algorithms to detect commands
3. When the ai finishes a command, update the interface
4. Provide feedback to the ai via the interface
5. Repeat steps 2 - 4 until no new commands are detected
6. Display messages and/or sounds when commands finish
7. Repeat step 2 - 6 until the end of the script
8. End script
```

All I did to make it into a chat model was append "You gave this response: [response]" to the prompt lol. The first line of the prompt is the first line of https://til.simonwillison.net/llms/python-react-pattern
