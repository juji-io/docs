# **Making AI Chatbots: <br> Best Practices**

Based on our 18+ years of experience for designing and developing
conversational AI (AI chatbots), here we share a set of design tips
for making practical AI chatbots that can truly help human users and
personalize their help in real-world applications.

In case you are not sure what an AI chatbot is or why you need one,
check out this comparison on [AI chatbots vs. Non-AI
chatbots](../why-ai-chatbots).

## **Support Tasks and Social Chitchat**

Effective AI chatbots should be able to accomplish specific tasks and
deliver delightful social experience at the same time. Use the tips
below to create such an AI chatbot with minimum time and effort.

### Start w/ Chat Flow Outline

Building an AI chatbot is similar to writing a screenplay, which
should have a beginning (Welcome), body, and end (Wrap up). Moreover,
it should have a clear conversation objective that can guide the
chatbot's to drive a dialog and achieve the objective.

Juji provides a set of chatbot templates, each of which always
includes a Welcome and Wrap-up. We strongly recommend that you first
create a **chat outline**, which defines a chat flow that your chatbot
will use to guide a conversation with a target audience. You can use
your favorite text editor, such as Word and Google Doc to edit such an
outline in a plain text format. Online editing tools, like Google doc, allow
collaborative editing, which let your teammates or clients help you
polish the outline.

Below is a sample outline that is intended to create a chatbot
that can  chat with gamers about games.  
<br>
<p align="center"><img src="../img/chat-outline.png" alt="chat-outline" width="650"/></p>

<br>

Here is another sample outline that aims at creating a chatbot that
helps make restaurant reservations as well as manage reservations.

<br>

<p align="center"><img src="../img/chat-outline-2.png" alt="another
sample chat outline" width="650"/></p>

<br>

### Draw Conversation Graph

As shown in the above outline, chat topics may be conditioned upon
previous chat topics. For example, topics `T2`, `T3`, and `T4` follow up to
one branch of `T1` (`New Booking`), while topics `T5` and `T6`
follow the other branch of `T1` (`Manage Booking`). Since Juji
AI chatbots support arbitrarily complex conversations that may include
complex depencies, it is always a good idea to draw the underlying
**conversation graph** to layout various dependencies. Below is the
corresponding conversation graph representing the restaurant
reservation chatbot mentioned above.

<p align="center"><img src="../img/chat-outline-2-graph.png" alt="another
sample chat outline" width="650"/></p>

Once the outline is ready, you can then mark each item as a chatbot
`message` (requiring no user input) or chatbot `request` (requiring
user input). Below is the above sample outline with markings
highlighted in yellow. This avoids [unnecessary
mistakes](#mix-messages-and-requests) during a chatbot making
process. Based on the markings, you can then [create a
chatbot](../design) and add the marked items in the main chat flow.

<p align="center"><img src="../img/chat-outline-annotated.png" alt="annotated
sample chat outline" width="650"/></p>

### Prepare Q&A List and Chitchats

As shown next to the conversation graph, one can also define a list of Q&As
or social chitchat topics *independent* of the main chat
outline. These Q&As and social chitchats can be invoked *anytime*
during a chat to answer user inquiries or handle user comments falling
outside the main chat flow. Not only does this capability deliver a
superior user experience, but it also makes a conversation more
natural and useful (e.g., providing instantaneous responses to user
inquiries). Additionally, Juji AI chatbots automatically tracks and manages a
conversation context, including topic switches (e.g., switching from a
topic in the main outline to a Q&A or social chitchat). They will
always bring users back on track (i.e., the topics in the main
outline).

In particular, we recommend that you prepare answers to <a href="#" name="qa-types">**three types of user questions**</a> that can be anticipated.

: * <a href="#help-guide">HELP Guide</a>

: * <a href="#recip-q">Reciprocal Questions</a>

: * <a href="#common-q">Common Sense Questions</a>

#### <a name="help-guide"></a>Prepare HELP Guide

No matter how smart your chatbot is, it cannot do everything. To make
a conversation more efficient and transparent, we recommend that you
always prepare a `HELP` guide to inform users what your chatbot can
do. This will help users figure out what they can or cannot do with
the chatbot. It will also reduce user frustrations and help the
chatbot better guide a user behavior.

You can go to the Q&A dashboard and directly add an entry with "Help"
in the `Question` column, and your help guide in the `Answer` column,
and then click `Submit`. You can also do so by downloading the CSV file on
the Q&A board, filling in the entry related to `Help` in the CSV file,
and then uploading the revised CSV file.

As part of the HELP guide, it is also valuable to customize answers to the following two questions:

* **User request to chat with a human agent**. By default, this question is already in a chatbot's knowledge base. You may want to edit the system default response based on your situation. Just download the CSV file from the Q&A board and edit the answer to this question in the CSV file. Then upload. 

* **Default response to any unrecognized user input**. You can edit the <a href="https://docs.juji.io/design#default-response" target="_blank">**default response to unknown user input**</a> as part of the [conversation parameters](../design#conversation-parameters).


#### <a name="recip-q"></a>Prepare Answers to Reciprocal Questions

Users often ask reciprocal questions, such as `what is your favorite
color` when asked the same question by a chatbot. One should
anticipate such user behavior and prepare the chatbot to handle such
reciprocal questions.

#### <a name="common-q"></a>Prepare Answers to "Common Sense" Questions

Users will enjoy interacting with a chatbot more, if the chatbot can
answer simple, "common sense" questions related to the duties of the
chatbot. For example, if a chatbot is used to greet online customers
of an e-commerce business, it should answer questions about the price
and availability of the products. Similarly, if a chatbot is used to
onboard customers for an application, it should answer questions about
the application.

All the Q&As can be entered in a CSV file or directly in the table on
the `Q&A Board` page. Please refer to [Customize
Q&A](../design#customize-qa-and-fallback) for more details on how to
add/edit Q&As.

<p align="center"><img src="../img/design-qa.png" alt="define Q&As" width="650"/></p>

## **Balance Business Goals and User Experience**

Businesses use chatbots to scale out human-human communications and
optimize business outcomes (e.g., improving customer satisfaction
while reducing cost). To achieve this goal, it is important to design
a chatbot that can balance the accomplishment of business tasks and
user experience.  

### Mix Messages and Requests

Juji AI chatbots can send two types of messages (check out [chatbot
design](../design)). One type is a plain chatbot **message** that ignores
user input. The other is a chatbot **request** that waits for user input
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

<p align="center"><img src="../img/pseudo-q.png" alt="Pseudo question" width="350"/></p>

### Mix Different Types of Requests

Juji AI chatbots support several types of requests, e.g., choice-based
and free-text requests. While choice-based questions are quick and
easy for users to answer, they gather limited information for
businesses to act upon. Moreover, choice-based answers can be easily
"cheated" (e.g., a user simply makes a random choice without even
reading the request). On the other hand, free-text questions
especially open-ended questions often elicit rich and meaningful
responses, but they take more time and effort for users to respond. In
addition, Juji has built-in [gibberish
detection](#ensure-quality-of-user-input) to prevent gibberish
responses.

To make users stay engaged without feeling too tired, it is a good
practice to mix choice-based and free-text requests in a chat. From
our experience, maintaining a 2:3 ratio, 2 choice questions and 3
free-text inquiries, normally works well. We also encourage the use of
open-ended chatbot inquiries (e.g., `How do you feel about the movie`)
instead of simple yes-no questions (e.g., `Do you like the movie`). The
former can elicit in-depth often unanticipated responses and make a
conversation more lively, while latter may end a chat prematurely. If
you have to use a yes-no question (e.g., collecting a definite yes-no
answer), you may want to add a follow-up `Why` free-text question to
elicit the rationale behind user responses.   

### Use Proper Juji Built-in Dialog

As mentioned in the [design](../design) section, Juji provides a rich
set of [built-in, mini conversations](../design#built-in-dialog). These
built-in dialogs automatically handle highly diverse, potentially
complex user expressions. Such dialogs deliver great conversation experience
without requiring much customization.

Since Juji uses the request label (see how to [give a good label](../chatbot-design-tips-advanced#give-sensible-labels)) to find the matched built-in dialog, such match is not always correct. For example, your chatbot is supposed to ask a yes-no question, such as `Would you like to take a test drive?`. Juji may not always match such a question with the built-in dialog that handles yes-no question.

<p align="center"><img src="../img/example-topic-1.png" alt="display of a retrieved built-in dialog" width="650"/></p>

We thus strongly recommend that you always check the retrieved built-in dialog to see if it is what you want. If the retrieved built-in dialog is incorrect, use the search button to find a better matched Juji built-in dialog. Using a proper built-in dialog not only supports a better conversation experience, but also reduces your effort of customizing a chatbot. 

<p align="center"><img src="../img/search-a-topic.png" alt="search a
topic" width="550"/></p>


### Optimal Chat Length

Although Juji AI chatbots can engage users in a very lengthy
conversation (e.g., the longest was 3.5 hours), engaging someone in a
conversation requires much time and mental effort. It is thus a good
practice to keep a chat at a certain length to keep your audience
engaged while completing intended tasks.

From our experience, a chat should be kept below 5 minutes if your
chatbot does not have much interesting content or topics to
discuss. If your chatbot poses questions and engage users in free-text
discussions, making a chat between 10-12 minutes enables your chatbot
to bond with your audience but without wearing them out. If your
chatbot is intended to conduct lengthy interviews, try to keep it
within 45 minutes.

If you need to gather certain amount of information from your audience
before your chatbot can help them, dividing a long chat into multiple
shorter chats is always more effective. For example, instead of
chatting with a user 30 minutes at once, see if you can make your
chatbot engage with a user 10 minutes every day for 3 days.


## **Create Natural and Engaging Conversations**

The tips listed below help power chatbot to deliver a natural
conversation experience that can best engage with target audience.

### Paraphrase Messages and Requests

To make a chatbot sound more natural, define paraphrases for a chatbot
message or a request. For example, if your chatbot says hello to your
audience everyday, you want your chatbot to say something differnt to
avoid repeatitiveness. This can be easily done by adding paraphrases
to the hello message. Below indicates the use of the green "+" to add
paraphrases to a chatbot message:

<p align="center"><img src="../img/add-paraphrases-remark.png" alt="paraphrase a message" width="550"/></p>

Similarly, a chatbot may need to repeat a question/request if a user
does not comply to it. In such a case, you want to add paraphrases of
the request, so your chatbot does not repeat the request using the
same phrase. Moreover, when giving a request first time, the chatbot
should give more information, such as the rationale of the
request. When repeating this request, the chatbot however should not
repeat everything to sound robotic.

Below is an example showing the initial phrase of a chatbot request. Since this message is long, it would not be used by the chatbot to repeat the question:

<p align="center"><img src="../img/initial-msg.png" alt="Initial Message" width="650"/></p>

Here is a paraphrase (shorter version) of the same message above and will be used by the chatbot to repeat the question if needed:

<p align="center"><img src="../img/reasking-msg.png" alt="Reasking Message" width="650"/></p>

Below shows another example with a question expression for the
first-time use and a list of re-asking expressions. Note the checkbox
"Reasking Message". You can use this checkbox to control whether a
question expression should be used for asking the question first time
or re-asking. If it is unchecked, a question expression is used to ask a
user first time when such a question is posed.

<p align="center"><img src="../img/paraphrase-a-question-1.png" alt="chatbot design tip: defining an initial expression for a question" width="650"/></p>

If it is checked, it means that the associated
expression will ONLY be used when a chatbot re-asks the question but
not the first time.

<p align="center"><img src="../img/paraphrase-a-question-2.png" alt="chatbot design tip: defining a list of re-asking expressions for a question" width="650"/></p>

If the box is not checked for **any** of the question expressions, then
every expression can be used for initial asking and re-asking. So it
is the best practice to define a list of expressions for re-asking
(normally abbreviated, shorter expressions) by checking the box but
leave certain expressions (complete, longer expressions) for initial asking.

The screenshot below shows how question paraphrases are used in a chat.

<p align="center"><img src="../img/paraphrase-a-question-demo.png" alt="chatbot design tip: a chatbot asks a question using different expressions: first time vs. second time." width="650"/></p>


### Personalize Messages and Requests

Personalized messages make users feel being heard and more willing to
be engaged or stay engaged. There are two simple ways to make a
chatbot message more personable:

* **Address users by their first name occasionally during a chat**. The function
  `(user-first-name)` can be inserted into any chatbot message to make
  a user feel that the chatbot is paying attention to him/her.


<p align="center"><img src="../img/user-first-name-func.png" alt="call user by his or her first name function (user-first-name)" width="650"/></p>

* **Repeat what a user says in a chatbot response**. The example below
  shows that the chatbot repeats the user's word and makes the user
  feel being heard.
  
	1. Define a `contains-keywords` trigger
  
	2. `STORE MATCHED INPUT` into a custom attribute (e.g., `like-protein`)
  
	3. Insert the attribute into chatbot response using a function
  (e.g., `(get-user-attribute-as-string "like-protein")`

<p align="center"><img src="../img/design-repeat-words.png" alt="Repeat user words" width="450"/></p>

<br>
Below is how the chat is like:

<p align="center"><img src="../img/preview-repeat-words.png" alt="Preview the repeat of user words" width="650"/></p>

* **Echo a user's feelings in a chatbot response**. The example below
  shows how the chatbot acknowledges the user's feelings.

  	1. Define a `contains-sentiment` trigger

  	2. Create a corresponding chatbot response based on the detected sentiment

<p align="center"><img src="../img/design-ack-sentiment.png" alt="Ack user sentiment" width="450"/></p>

<br>
Here is how the chat is like:

<p align="center"><img src="../img/preview-ack-sentiment.png" alt="Preview how to ack user sentiment" width="650"/></p>

### Determine Chatbot Default Response

No chatbot is perfect and can understand every user input. To
cope with unrecognizable user input, Juji provides many built-in
dialogs. However, these built-in chatbot responses may not be suitable
for your chatbot applications. For example, if a user asks about the
weather of a location, such as `What's the weather like in San Jose`. The default,
built-in chatbot response would be like: `I am not a weather
bot. You may want to check with weather.com`. However, if you are
building a weather chatbot, such a response might not be proper.

To override Juji built-in chatbot responses, you can define your own
default chatbot responses to anything it cannot recognize. You can go
to `Chatbot Settings` page (under `Design` menu) to define this defaul response: 

<p align="center"><img src="../img/chatbot-settings-defaultresponse.png"
alt="chatbot default response to unknown user input" width="650"/></p>


In the above example, the default response that you entered will then
be used instead of Juji built-in default responses.

### Periodically Refresh Chatbot

Just like a person, your chatbot may not want to engage with anyone in
a never-ending conversation. For example, if a chatbot is intended to
conduct an interview, it should end after the interview is
done. Similarly, if a chatbot is intended to help users in an
e-commerce situation, it may want to be refreshed from time to time so
users can be helped from the start (like re-entering a store).

By default, a Juji chatbot will be refreshed (restarted) every 60
minutes after it chats with a person. However, this refresh rate may
be different depending on your chatbot tasks. For example, if your
chatbot is conducting an interview that normally lasts for 45 minutes,
we recommend that you set the refresh rate to every 180 minutes
because your audience may not finish their interviews and want to
continue after 60 minutes. They certainly do not want to start it over
again. To set the refresh rate, you can go to the `Chatbot Settings`
page:

<p align="center"><img src="../img/chatbot-settings-refresh.png"
alt="set up a chatbot refresh rate" width="650"/></p>

## **Ensure Conversation Quality**

Like in a natural conversation, humans rarely follow a pre-defined
conversation flow because humans are creative and spontaneous. To
engage users in a quality conversation, a smart chatbot
should be able to anticipate user digressions and handle such
digressions accordingly. 

From millions of human-chatbot conversations, we have identified
several types of user digressions, especially when open-ended
questions are involved in a conversation:

* Gibberish user input (e.g., "aasfa asfs fa")
* "I don't know" input
* User excuses  (e.g., "this question is too hard for me") 
* User clarification (e.g., "What do you mean?")
* User asks to alter chat flow (e.g., "skip")
* User asks an irrelevant question
* User comments on the question (e.g., "this is a strange question")
* Thin input (e.g., "good")

Not only must a chatbot respond to each type of user input properly,
but it must also decide how to continue a conversation. For example,
if a chatbot asks a non-required question, it should not re-ask the
question if a user asks to skip the question. To help chatbot
designers handle diverse user digressions, Juji offers a rich built-in
fallback conversation library that automatically detects the type of
user digression and figures out how to handle it properly. Chatbot
designers can leverage the fallback library directly but still have
the freedom to turn on/off specific digression handlers using the
chatbot settings as shown below.

<p align="center"><img src="../img/handling-user-digressions.png"
alt="Settings for turning on or off different user digression handling
" width="650"/></p>

Next we use more concrete examples to explain how Juji handles several
common types of user digressions to ensure conversation quality.

### Handling Gibberish and "I don't know" User Input

Users may intentionally or unintentionally test a chatbot by feeding
the chatbot with non-sense or gibberish input. Juji has built-in
functions to automatically detect such input. Moreover, users may take
an easy way out by responding with `I don't know`. In such a case, a
chatbot can be configured to accept or not accept such user
responses. For example, if a discussion is about a user's knowledge,
such a response should be acceptable. On the other hand, if the
discussion is about a user's opinion, such a response may not be
acceptable since s/he can always come up with an
opinion.

You can customize gibberish detection or decide whether to permit user
`I don't know` response in a topic setting as shown below.

<p align="center"><img src="../img/topic-setting-1.png" alt="Topic
Setting 1" width="650"/></p>


<p align="center"><img src="../img/topic-setting-2.png" alt="Topic
Setting 2" width="650"/></p>

As shown above, you can also control the required length of a
user response and also indicate whether a chatbot request is required
to answer or not. 

### Handling User Excuses to Open-Ended Questions

Users may also give excuses or intentionally dodge a question. Assume
that a chatbot asks a user "What's the top challenge you face?".  One
user may respond "I don't really know since I have many challenges."
while another user may state "This is too hard for me to answer."

To simplify a conversation designer's task of anticipating diverse
user excuses, Juji has a built-in library that captures a number of
common user excuse expressions. During a conversation, Juji will
automatically detect a user excuse expression and respond to it
accordingly. If a question is optional, Juji will also inform a user
that the question is optional and the user can skip it if s/he wishes
to.

Below shows Juji's handling of several user excuses. 

<p align="center"><img src="../img/handling-user-excuse-1.png"
alt="Handling a user excuse: this is very personal" width="650"/></p>


<p align="center"><img src="../img/handling-user-excuse-2.png"
alt="Handling a user excuse: don't know how to answer the question"
width="650"/></p>


<p align="center"><img src="../img/handling-user-excuse-3.png"
alt="Handling a user excuse: the question is too hard to answer"
width="650"/></p>

### Handling User Clarification Questions to Open-Ended Questions

Just like in any conversations, a user might not fully understand a
chatbot's question or find the question unclear. When this occurs, the
human user may ask a clarification. For example, when a chatbot asks
"What's the top challenge you face?" A user may ask a clarification
question "What kind of challenges are you referring to?" or "what do
you mean".

Since it is hard to anticipate precisely what a user's clarification
question might be and pre-train a chatbot to handle all possible
clarification expressions, Juji enables you to use a simple
approach. As a chatbot designer, you just need to design a chatbot
question with several alternative question expressions (see <a href="https://juji.io/docs/chatbot-design-tips/#paraphrase-messages-and-requests">paraphrase
a chatbot question</a>). Juji will take care of the rest. This is
because Juji has a built-in library that captures the most common
user clarification questions. During a conversation, if Juji
automatically detects a user clarification expression, it will then
rephrase the question using an alternative question expression. This
way, a user gets a chance to re-interpret the question. 

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

Want to power up your chatbot and get some more magic going? Juji has
you covered. Dig deeper into [advanced design tips](../chatbot-design-tips-advanced) or **[Juji IDE](../juji-ide)**.

