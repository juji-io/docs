# **AI Chatbots vs. Non-AI Chatbots**

In general, chatbots are made to scale out human-human communications
(e.g., product marketing and customer support) through
automation. Depending on the underlying technologies used, today's
chatbots fall into two broad categories: Non-AI chatbots and AI
chatbots.

## **A Quick Comparison**

Non-AI chatbots focus on automating simple tasks (e.g., broadcasting
messages) with little intelligence, while AI chatbots focus on
automating tasks, including complex tasks that involve highly diverse
user interactions, with a human touch.  The table below summarizes the
key differences between the two and their suitable applications,
respectively.

<p align="center"><img src="../img/comparison-table.png" alt="Non-AI
vs. AI chatbots comparison table" width="650"/></p>

Juji Studio enables you to easily create powerful AI chatbots with
built-in machine intelligence. Your application can often help you
decide whether you need an AI chatbot. For example, if you need a
chatbot just to broadcast messages but ignore any user interactions
(e.g., user questions), you probably do not need an AI chatbot. On the
other hand, if you want your chatbot to interactively engage and help your
audience, e.g., answering user product inquiries while introducing 
products, then you need an AI chatbot.

## Conversation Capabilities

AI chatbots and non-AI chatbots differ greatly in their capabilities
in carrying on and managing conversations that involve natural
language (free-text) communications. The type of communications you
want to support helps you decide whether you need a non-AI or AI
chatbot.

### **Non-AI Chatbots**

Most non-AI chatbots are also known as "button bots", which drive a
fixed chat flow that requires users to click on a set of choice
buttons and move a "chat" forward as shown below.

<p align="center"><img src="../img/button-bot-pk-1.png" alt="an example of
button bot" width="650"/></p>

In such a flow, users are not allowed to interrupt or deviate from the
flow, let alone asking questions or making requests during the flow
(e.g., user questions are simply ignored). Such chatbots are suitable
for only very simple tasks during which user actions can be highly
anticipated (e.g., only a couple of choices to make) and users are
unlikely to deviate from a pre-defined chat flow. 

### **AI Chatbots**

In contrast, AI chatbots support a natural, fluid conversation during
which they can actively listen to users' natural language input,
allowing users to pose questions and deviate from a planned chat
flow. The following screenshot shows that a user poses a free-text
question instead of answering a chatbot's initial inquiry. The
chatbot was able to recognize the free-text question and responds to it
instantaneously. In addition, the chatbot remembers the conversation
context, and reasks the question.

<p align="center"><img src="../img/ai-bot-pk-1.png" alt="an example of
AI chatbot - task oriented" width="650"/></p>

<br>

In addition to supporting task-oriented chats (e.g., answering user
questions), AI chatbots are capable of social chitchats. Below is an
example showing a social chat between a chatbot and a user:

<p align="center"><img src="../img/free-text-chat.png" alt="an example of
AI chatbot - social chats" width="650"/></p>

As shown above, the chatbot can recognize user input and carry on a
conversation naturally. Juji provides a dialog library that contains
thousands of [built-in mini conversations](../design#built-in-dialog),
which can be directly used to support various social chitchats.

## People Insights from Chat

Having a conversation is a natural way to get to know a person and use
the understanding to best help the person. Since chatbots aim at
scaling out human-human communications, ideally chatbots should get to
know their users and use such knowledge to best help their users. The
level of understanding about your audience that you want to obtain
can also help you decide whether you need a non-AI or AI chatbot. 

### **Non-AI Chatbots**

Since non-AI chatbots typically do not interpret users' natural
language expressions, their understanding of users is often
limited. For example, their understanding of users is limited at
eliciting users' choices or preferences from button selections as
described above. Extracting richer information or implicit meanings
from natural language expressions is not part of the user
understanding process in non-AI chatbots. 

### **AI Chatbots**

On the other hand, AI chatbots can interpret users' free-text
expressions, which enable them to gain a deeper understanding of
users. The example shown below indicates that not only does an AI
chatbot understand that a user dislikes the movie in question, but it
is also able to gather the rationale behind the user's negative
sentiment.

<p align="center"><img src="../img/people-insights-1.png" alt="an example of
AI chatbot for interpreting user input" width="650"/></p>

Furthermore, a capable AI chatbot can read between the lines and
automatically infer deep people insights from a chat. For example,
such a chatbot may infer a user's implicit needs and wants, who is
family-oriented and family safety is the top priority. It can then use
such insights to personalize the service, such as recommending
products or services that meet the needs of the family. Similarly, an
AI chatbot may infer that a user is impulsive and a quick decision
maker, the chatbot may remind the user of checking facts before making
a decision. Below shows two examples where a chatbot "coaches" two
different candidates to do their best in an interview based on their
unique characteristics.

<p align="center"><img src="../img/people-insights-2.png" alt="an example of
AI chatbot inferring user intent and characteristics" width="550"/></p>


## **Quick Test**

There are many hypes and hopes about AI chatbots. If you are wondering whether you need an AI chatbot, a quick test below may help you make a decision. Additionally, there are many chatbot platforms out but not all of them can make AI chatbots. If you decide to make an AI chatbot, use the second test below to help you find the right chatbot platform that can live up to your expectations.

### **Do I Need AI Chatbot**

As described above, the differences between non-AI and AI chatbots are
their abilities to engage with humans, glean human insights from a
chat, and personalize such engagements. If you are still unsure which
type of chatbot you need, you can use the following quick test to
determine whether you need an AI chatbot.

* Do you want your chatbot to interact with your audience, e.g.,
  answering user free-text questions any time during a chat?

* Do you want your chatbot to handle multi-step tasks with highly diverse
  user paths that are difficult to numerate or anticipate?

* Do you want your chatbot to bond with your audience through social
  interactions and handle exceptions gracefully?

* Do you want your chatbot to learn insights of your audience from a chat and
  use such insights to help them in the chat?

* Do you want your chatbot to improve and learn over time?

If your answer is **`yes`** to **any** of the above questions, you
need an AI chatbot. Additionally, you can use the above questions to
evaluate whether a chatbot is an AI chatbot and its capabilities.  

### **Which AI Chatbot Platform to Use?** <a name="right-platform"></a>

This seems like a difficult question to answer especially for people who are not an AI expert. There is in fact a simple test to evaluate AI chatbot platforms: 

!!! question "Does the platform use its own chatbot to serve its own business?"
    In other words, do they trust their own product enough to dogfood it?

If the answer to the above question is `yes`, ask:

!!! question "How do you like your interaction with the featured chatbot?"
    Concretely, ask the following:

    * Whether and how well does it understand your free-text input?
    * Whether and how well does it address your questions and handle your interruptions?
    * Whether and how well does it help you achieve your task?

    Keep in mind that this is perhaps one of their better chatbots.  

If the answers to the above questions are all positive, ask:

!!! question "How fast can you use the platform to create a simple AI chatbot yourself?" 
    Just make a simple chatbot to demonstrate the following:

    * Ask an open-ended question to greet a user - (e.g., `How are you doing?`)
    * Present a piece of information (e.g., introducing a product)
    * Ask user opinion after presenting the information
    * Ask a general question before responding to chatbot greeting
    * Ask a question about the presented information before giving your own opinion

If the platform does not allow you to DIY the simple AI chatbot as above, ask:

!!! question "How long will take the platform provider to do it for you?"

If the answers to all the above questions are positive, there is definitely a good sign that the platform is an AI chatbot platform. You can then make a decision based on additional factors, such as ease-of-use and pricing of the platform.

## **What's Next**

Ready to create your own AI chatbot? Check out these [design tips](../chatbot-design-tips) for creating super helpful and user-pleasing AI chatbots to help you scale your business and delight your audience. 
