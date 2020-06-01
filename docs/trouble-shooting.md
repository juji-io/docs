# **Trouble Shooting**

Although [Juji Studio](../juji-studio) has made the customization and
management of a chatbot radically simple, you may still encounter
issues during such a process. Below we list commonly encountered
issues reported by chatbot designers and the solutions to resolve such
issues.

## **My chatbot didn't wait for user responses after asking a question**

### **Description**

I want to customize my chatbot to ask follow-up questions based on
user input. As shown in the screenshot below, for example, my chatbot
first asks a user `what's your favorite color`.

<p align="center"><img src="../img/ask-q-pseudo-1.png" alt="a chatbot asks
a question" width="650px"/></p>

If a user's choice is `red`, my chatbot will ask
a follow-up question `could you give me an example object that has the
red you like`. See the screenshot below.

<p align="center"><img src="../img/ask-q-pseudo-2.png" alt="a chatbot asks
a question" width="650px"/></p>

When I preview my chatbot, the chatbot did ask the question. However,
it didn't wait for a user to answer the follow-up question and just
continued. See below my screenshot.

<p align="center"><img src="../img/skipped-user-answer.png" alt="a chatbot asks
a question" width="650px"/></p>


### **Trouble Shooting**

The common cause that your chatbot does not wait for a user to
answer its question is that the question is not defined properly as a "true"
question. 

Juji chatbots send two types of messages, one is just a message
without waiting for a user to respond, the other is a request, a
"true" question that will wait for a user to respond before advancing
a chat. If you have designed your chatbot to ask a question and elicit
user responses, make sure your question is a "true" question.

Using the above example, the question expression is included as part
of the `Quick acknowledgement`, which only sends a message
without waiting for any user response (see Customize THEN Actions in
[chatbot design](../design)). To ask a follow-up question as intended,
you will need to add a `Follow-up Request` as shown below:

<p align="center"><img src="../img/create-a-request.png" alt="Create a
follow-up request step 1" width="650px"/></p>

<p align="center"><img src="../img/created-request.png" alt="a
follow-up request is created" width="650px"/></p>

<p align="center"><img src="../img/created-request-content.png"
alt="the content of a created follow-up request for asking a question" width="650px"/></p>

The created follow-up request `T6` is a "true" question and wait for a
user's response before continuing a conversation. See the screenshot
below.

<p align="center"><img src="../img/allowed-user-answer.png"
alt="a follow-up question is asked and a user response is given" width="650px"/></p>

To check whether a chatbot is asking a "true" question, you can always
check the card associated with the message containing your question
expression. See two cards T5 and T6 shown in the screenshot below. A
"true" request/question has a chat icon associated with the card (T5),
while a plain message does not have it (T6).

<p align="center"><img src="../img/pseudo-q.png" alt="pseudo question" width="350px"/></p>

When you want your chatbot to ask a true question, make sure you
choose `Make a Request` option as shown below:

<p align="center"><img src="../img/design-topic-type.png" alt="add a
request" width="550"/></p>


## **Image does not show up in Facebook**

### **Description** I created a Facebook Messenger bot. In my chatbot,
I created a Facebook Media message, which includes an image URL. I got
my image URL on the internet by using "Copy image address". I can see
the display of the image inside my Juji design page but the image did not
show up in the Facebook Messenger chat window.


### **Trouble Shooting**

While you can view an image in Juji, Facebook Messenger may not always
support the display of such an image. When this happens, there are a
couple of ways to get around it.

First, you can try to get the image URL from a different way. For
example, click on the image you want to include, then right click on
the image to choose "Copy image address". Depending on where you "Copy
image address", the URL may come with much information and such
information may not be taken by Facebook Messenger. So if you can get
to the image itself and its image URL, use that URL instead.

Second, you can always download the image and then upload it to
Facebook (anywhere in a Facebook, it could be a page you created or
your own page). Then use "Copy image address" to get its URL. Because
now Facebook is hosting the image, the chance for Facebook Messenger
to display it properly is higher.

Of course it is always your responsibility to make sure that you have
the proper rights to use an image in your chatbot.

