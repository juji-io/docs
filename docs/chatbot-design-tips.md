# **Designing AI Chatbots: Best Practices**

In this section, we share tips on designing AI chatbots
that can:

* Actively listen to users and provide timely help any time during a chat

* Read between the lines to infer users' implicit needs and wants

* Keep track of context to carry on a natural, fluent conversation

* Personalize guidance or service to act as humans' best helpers

## **Support Tasks and Social Chitchat**

Effective AI chatbots should be able to accomplish specific tasks and
deliver delightful social experience at the same time. Use the tips
below to create such an AI chatbot with minimum time and effort.

### Start with a Chat Outline

Building an AI chatbot is similar to writing a screenplay, which
should have a beginning, body, and end. Moreover, it should have a
clear conversation objective that can guide the chatbot's to drive a
dialog and achieve the objective. 

We strongly recommend that creating a chat outline using a text
editor, such as a Google doc. Google doc allows collaborative editing,
which let your colleagues or clients alike help you polish
the outline.

Below is a sample chat outline:
<br>
<p align="center"><img src="/img/chat-outline.png" alt="add a
topic buttons" width="650"/></p>

Once the outline is ready, mark each item as a chatbot message
(requiring no user input) or chatbot request (requiring user
input). Based on the markings, you can then create a chatbot and add
the marked items in the main chat flow.

### Prepare Q&A List

To deliver a superior user experience, an AI chatbot should
handle user inquiries or comments falling outside the main chat flow
*anytime* during a chat. We recommend that chatbot creators
prepare answers to three types of user questions that can be
anticipated. All the Q&As can be entered in a CSV file or directly in
the table on the `Q&A Board` page.

<p align="center"><img src="/img/design-qa.png" alt="define Q&As" width="650"/></p>

#### Prepare Answers to Reciprocal Questions

Users often ask reciprocal questions, such as `what is your favorite
color` when asked the same question by a chatbot. One should
anticipate such user behavior and prepare the chatbot to handle such
reciprocal questions.

#### Prepare `HELP` Guide

To make a conversation more efficient and transparent, we recommend to
prepare a `HELP` guide, an answer to a user's request for help. This
will help users figure out what they can or cannot do with the
chatbot. It will also reduce user frustrations and
help the chatbot better guide a user behavior. 

#### Prepare Answers to "Common Sense" Questions

Users will enjoy interacting with a chatbot more, if the chatbot can
answer simple, "common sense" questions related to the duties of the
chatbot. For example, if a chatbot is used to greet online customers
of an e-commerce business, it should answer questions about the price
and availability of the products. Similarly, if a chatbot is used to
onboard customers for an application, it should answer questions about
the application.

## **Create Natural and Engaging Conversations**

The tips listed below help power chatbot to deliver a natural
conversation experience that can best engage with target audience.

### Mix Messages and Requests

Juji AI chatbots can send two types of messages (check out [chatbot
design](/design)). One type is a plain *chatbot message* that ignores
user input. The other is a *chatbot request* that waits for user input
and responds to it. If a chatbot sends too many messages that ignore
user input, it feels like a monologue (or chatbot spam) instead of a
dialog. If a chatbot asks too many questions, it feels like an
interrogation instead of conversation. Thus, an AI chatbot should
support a balanced asking and answering questions, also known as a
*mixed-initiative conversation*.  When writing a chat outline, mix the
use of chatbot messages (don't require user responses) and requests
(requiring user responses).


In addition, if you use multiple chatbot messages in a row, you may
want to add `delay` time (you can set it in [topic
settings](#topic-settings) between them to time each message so they
do not rush out too quickly one after another.

**IMPORTANT TIP:** If you intend to have your chatbot wait for a user input and respond to it before moving on, make sure you choose `Make a Request`. Otherwise, your chatbot simply ignores any user input even if the message is worded like a question. As the example shown below, T6 will not wait for a user's input but T5 will. Note the chat icon appearing on T5, indicating T5 is a "true" question. 

<p align="center"><img src="/img/pseudo-q.png" alt="Pseudo question" width="350"/></p>

### Paraphrase Messages and Requests

To make a chatbot sound more natural, define paraphrases for a chatbot
message or a request. For example, if your chatbot says hello to your
audience everyday, you want your chatbot to say something differnt to
avoid repeatitiveness. This can be easily done by adding paraphrases
to the hello message. Below indicates the use of the green "+" to add
paraphrases to a chatbot message:

<p align="center"><img src="/img/add-paraphrases-remark.png" alt="add a
topic buttons" width="550"/></p>

Similarly, a chatbot may need to repeat a question/request if a user
does not comply to it. In such a case, you want to add paraphrases of
the request, so your chatbot does not repeat the request using the
same phrase. Moreover, when giving a request first time, the chatbot
should give more information, such as the rationale of the
request. When repeating this request, the chatbot however should not
repeat everything to sound robotic.

Below is an example showing the initial phrase of a chatbot request. Since this message is long, it would not be used by the chatbot to repeat the question:

<p align="center"><img src="/img/initial-msg.png" alt="Initial Message" width="650"/></p>

Here is a paraphrase (shorter version) of the same message above and will be used by the chatbot to repeat the question if needed:

<p align="center"><img src="/img/reasking-msg.png" alt="Reasking Message" width="650"/></p>

### Personalize Messages and Requests

Personalized messages make users feel being heard and more willing to
be engaged or stay engaged. There are two simple ways to make a
chatbot message more personable:

* **Address users by their first name occasionally during a chat**. The function
  `(user-first-name)` can be inserted into any chatbot message to make
  a user feel that the chatbot is paying attention to him/her.


<p align="center"><img src="/img/user-first-name-func.png" alt="call user by name" width="650"/></p>

* **Repeat what a user says in a chatbot response**. The example below
  shows that the chatbot repeats the user's word and makes the user
  feel being heard.
  
	1. Define a `contains-keywords` trigger
  
	2. `STORE MATCHED INPUT` into a custom attribute (e.g., `like-protein`)
  
	3. Insert the attribute into chatbot response using a function
  (e.g., `(get-user-attribute-as-string "like-protein")`

<p align="center"><img src="/img/design-repeat-words.png" alt="Repeat user words" width="450"/></p>

<br>
Below is how the chat is like:

<p align="center"><img src="/img/preview-repeat-words.png" alt="Repeat user words" width="650"/></p>

* **Echo a user's feelings in a chatbot response**. The example below
  shows how the chatbot acknowledges the user's feelings.

  	1. Define a `contains-sentiment` trigger

  	2. Create a corresponding chatbot response based on the detected sentiment

<p align="center"><img src="/img/design-ack-sentiment.png" alt="Ack user sentiment" width="450"/></p>

<br>
Here is how the chat is like:

<p align="center"><img src="/img/preview-ack-sentiment.png" alt="Ack user sentiment" width="650"/></p>

## **Give Sensible Labels**

The label of a free-text request is used for multiple purposes. It is
used to summarize the topic (see the topic card on the left panel) and
also used to index user answers to the request in an
audience report.

More importantly, it is used to find a matched Juji built-in topic to
handle user responses to the request. For example, Juji has a built-in
topic that handles diverse user responses to the request `What are
your hobbies`. To find such a built-in topic, Juji uses the entered
label. Giving a sensible lable thus can better help Juji find the
right built-in conversation topic, which can then handle diverse user
responses on that topic with no or little customization required.  

## **Preview Chatbot Often**

Since an AI chatbot can exhibit complex conversation behavior, we
strongly recommend that you preview your AI chatbot frequently during
the customization process. This will also help you revert your
customizations if needed before going too far, since `undo` is
not supported at this moment.

If you need to undo the designs made, you may want to use the `clone`
function to clone a chatbot first before undoing the designs. This way
you will always have a copy of what you have made.

## **What's Next**

Want to power up your chatbot-fu and get some more magic going? Juji has you covered. Dig deeper into **[Juji IDE](/juji-ide)**.
