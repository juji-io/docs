
# **Customize Chatbot Settings**

In addition to customizing the main chat flow and the Q&A list, one
can also customize various chatbot settings, including the name of the project.

## Project Name

You can edit the `name` of your project by mouse hovering the project
name and then click on the `pencil` button.

<p align="center"><img src="https://juji.io/docs/img/chatbot-settings.png" alt="chatbot settings" width="650"/></p>

## Chatbot Persona

To personalize your chatbot, you can choose a stock persona or define a custom persona.

<p align="center"><img src="https://juji.io/docs/img/chatbot-settings-1.png" alt="chatbot settings" width="650"/></p>

<br>

To define a custom persona, click on the `Custom` persona icon as shown below. You can then upload your persona photo, give your custom persona a name, and enter a short bio. Once you are done, click on the green check mark to save it.

<p align="center"><img src="https://juji.io/docs/img/custom-chatbot-persona.png" alt="define a custom persona" width="650"/></p>

## Display Control

You can customize various chat display parameters to affect how a
chat or chat window appears.

<p align="center"><img src="https://juji.io/docs/img/display-control.png" alt="define a custom persona" width="650"/></p>

### Display control by number of words

When a chatbot sends a long message (by default 50 or more words), you
may wish to give users some time to read and digest the message before
moving on. In this case, the message will be automatically displayed
with a "More" button. Whenever a user has finished reading the message and is ready to move on, s/he will just click on the "More" button to move
on. You can change the default (50) to decide what would be considered
a long message.

<p align="center"><img src="https://juji.io/docs/img/display-control-example.png" alt="define a custom persona" width="650"/></p>

### Enable/Disable Progress Bar

When a chatbot is used to perform a certain task that has a definite
beginning and end, such as conducting an interview/survey, onboarding a user, or
taking an application, you may want to display a progress bar so the users would know where they are in the process. You can turn on or off the progress bar as needed.

<p align="center"><img src="https://juji.io/docs/img/chat-progress-bar.png" alt="chatbot settings" width="650"/></p>

### Enable/Disable User Feedback

Currently a chatbot can receive a user's feedback while it answers the
user's questions. You can enable/disable whether to receive a user's
feedback. It supports two types of user feedback, the first type is
just a quick "thumbs up" or "thumbs down" feedback, while the other
also takes additional comments in addition to a thumbs up or
down. Flip the toggle to enable it and then click on one of them to select which type of user feedback to receive.

<p align="center"><img src="https://juji.io/docs/img/user-feedback-settings.png" alt="chatbot settings" width="650"/></p>

## User Input Control

Under the section called "Input Control", you can turn on or off the spelling checker. Currently, the spelling checker auto-corrects the words that are not
in its directionary while providing users with a chance to revert the auto
correction.

<p align="center"><img src="https://juji.io/docs/img/input-control.png" alt="chatbot settings" width="650"/></p>

Once the spelling checker is turned on, you can add unusual words or
phrases to the existing dictionary so the use of such words/phrases
will not be auto-corrected.

## Customize Conversation Tempo

Customize the pace and duration of a conversation by following parameters.

<p align="center"><img src="https://juji.io/docs/img/conversation-tempo.png" alt="chatbot settings" width="650"/></p>

### **Conversation pace**

You can speed up or slow down a chatbot transitions from one topic to the next.


### **Messsage pace**

You can speed up or slow down a chatbot transitions from one message to the next.

### **Refresh duration**

You can also control how frequently a chatbot auto starts itself from
the beginning. In certain situations, you wish a chatbot to start more
frequently (e.g., an e-commerce chatbot) than others (e.g., an
interview chatbot) to make sure that users can accomplish their tasks
without starting over again.

## Response Control

Customize the following parameters to control how chatbot would handle
particular type of user responses.

<p align="center"><img src="https://juji.io/docs/img/response-control.png" alt="chatbot settings" width="650"/></p>

### **Minimal response length**

This is a short cut for you to control the minimal number of words a
user must provide to a chatbot request. This parameter sets the
default for *all* questions in your chatbot. You can customize the response length for a specific chabot question/request in the **Topic Settings** (see [customize topic settings](../customize-main-chat-flow#Customize-Topic-Settings).

### **Handling unknown user input**

This section allows you to control a chatbot's behavior when the chatbot does not recognize a user question or input. Currently, Juji provides several options for you to handle such a situation.

<p align="center"><img src="https://juji.io/docs/img/handling-unknown-user-input.png" alt="chatbot settings" width="650"/></p>

* Provide a default message. Juji has a built-in message to handle this. You can enter a custom message here to suit your context, e.g., providing a URL, an email, or a phone number to access a human agent.

* Provide email notification. If you enable this function, your chatbot will automatically elicit an email address, first name, and last name from a user when it cannot answer a user's question. It will then automatically email the question along with the answer to the user once the answer becomes available (e.g., an answer is submitted via the Q&A board).

<p align="center"><img src="https://juji.io/docs/img/customize-email-template.png" alt="chatbot settings" width="650"/></p>

### **Fallback handling**

This allows you to control what kind of
    fallback handling is desired for your chatbot. Juji provides a
    rich list of fallback handling functions to manage user input that
    is outside of your chatbot script. From our experience, users
    often deviate from your chatbot script and start a side
    talkng. These fallback handling functions enable your chatbot to
    handle user-initiated side talking gracefully and also keep the
    chat on track. 

<p align="center"><img src="https://juji.io/docs/img/handling-fallbacks.png" alt="chatbot settings" width="650"/></p>

## Collaboration Notes

In a situation where multiple people may co-design a chatbot, one can leave a note for each topic or the overall Q&A settings so their colleagues can understand the rationale of the design. In this section, one can customize the messages regarding the Q&A set up. The note will appear as a bubble next to the "Q&A board".

<p align="center"><img src="https://juji.io/docs/img/custom-qna-note.png" alt="chatbot settings" width="650"/></p>


<p align="center"><img src="https://juji.io/docs/img/qna-note-display.png" alt="chatbot settings" width="650"/></p>


## What's Next

Once a chatbot is ready, you can deploy it onto a website or a
Facebook page. Please check out [**Chatbot Deployment**](../release)
to deploy your AI chatbot. If you wish to further customize your chatbot, such as its [**main chat flow**](../customize-main-chat-flow) or [**capabilities to handle QnA**](../customize-qa), you can continue doing so. 


