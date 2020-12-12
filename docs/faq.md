
# **Frequently Asked Questions**

## General Questions

<a name="!ai-vs-no-ai"></a>
### What are the differences between AI chatbots and non-AI chatbots?

Here is a [quick comparison](../why-ai-chatbots#a-quick-comparison) between the two.

<a name="!know-ai-chatbot"></a>
### How do I tell if my chatbot is an AI chatbot?

Use the quick test below to check if your chatbot has any AI in it. If your answer is "yes" to all questions below, your chatbot is definitely an AI chatbot.

* Can your chatbot interact with your audience naturally, e.g.,
  answering user natural language questions any time during a chat?

* Can your chatbot handle multi-step tasks with highly diverse (often
  non-linear) user paths that are difficult to numerate or anticipate?

* Can your chatbot bond with your audience through natural, social
  interactions?

* Can your chatbot learn insights of your audience from a chat and
  use such insights to help them in the chat in real time?

* Can your chatbot improve and learn from more user interactions over time?

<a name="!why-ai-chatbot"></a>
### Why do I need an AI chatbot?

Here is a [quick test](../why-ai-chatbots/#quick-test) to help you find out if you need an AI chatbot.(Spoiler Alert: You probably do.) 

<a name="!chat-length"></a>
### How long normally can a user chat with a Juji chatbot?

It depends on the purpose of your chatbot. An interview chatbot may chat with its users for a long period of time (e.g., 45
minutes), while an e-commerce chatbot may chat with its users for a couple of minutes to help resolve user issues. Please
check out [how to determine the optimal chat length](../chatbot-design-tips#optimal-chat-length).

<a name="!improve-chatbot"></a>
### How will my Juji chatbot improve over time? Does it get smarter if more people use it?

Your chatbot can improve over time for two reasons. First, it will be get smarter if you inject more knowledge into your chatbot. Second, it will also improve because Juji constantly improves its dialog library based on all Juji chatbot usage and behavior. In other words, more Juji chatbots are in action, the better all the Juji chatbots will get. Yes, Juji Chatbots have a network effect in play. Or with apologies to Alexandre Dumas. "All for one and one for all". But we don't do user-side training data, so that headache you don't have. 

<a name="!creation-time"></a>
### How long will it take to create an AI chatbot?

: This depends on the purpose of your chatbot. For example, if you
want to create an e-commerce chatbot that introduces products and
answer customer questions, it may take from a couple of hours to a few
days, during which most of the time will be spent on coming up and
entering the Q&A pairs. If you already have a list of Q&As and your
product list is short, it would then be rather fast. For example, it
would take just a few minutes to get the first version up and running
and then a couple of hours to fine-tune it if you wish to do so.

<hr>
<a name="!user-data"></a>
### How will Juji use the data collected from interviewees?
: Privacy is very important to us. Please refer to our privacy policy at https://juji.io/util/juji-privacy-policy.pdf.

<hr>
<a name="!contact-info-safety"></a>
### Will Juji keep a copy of user contact information and their responses? Will Juji retain rights to use them?

: Juji holds privacy at the very heart of our
product. We do not actively collect contact information from chatbot
users. It is up to chatbot creators to decide if such information is
to be collected. Although we keep chat logs, they are secured using
industry standard secure protocols. Regarding details of our use of
the data collected and other privacy concerns, please refer to our
privacy policy at https://juji.io/util/juji-privacy-policy.pdf.

<hr>
<a name="!cost"></a>
### How much does a chatbot cost?
: You can create as many chatbots as you want without being charged. It is also
  free for your chatbot to chat with as many people as you want, if you don't
  use Juji Premium features (e.g., customizing chatbot behavior based on natural
  language input or downloading chat reports). Subscription to Juji Premium
  starts at $25/month or $240/year, which includes up to 100 free chats per month.
  After that, each additional chat costs $0.1, the usage is billed monthly.  If you
  are from academia and intend to use Juji for academic research, please contact
  us at hello@juji.io for special discount.

## Design Questions

<hr>
<a name="!design-page"></a>
### What does `Design` do?
: This allows you to customize your chatbot, such as its persona and chatbot actions.

<hr>
<a name="!create-ai-chatbot"></a>
### How do I create an AI chatbot/AI helper/AI agent?
: On your dashboard, click on the **`+ AI Helper`** button to create a new chatbot. Please check [how to get started](https://docs.juji.io/)

<p align="center"><img src="../img/create-chatbot.png" alt="create a new chatbot" width="650"/></p>

<hr>
<a name="!project-name"></a>
### Will my users/audience see my project name?

: As shown below, your project name is internal to you, while the AI chatbot name is external to your audience.

<p align="center"><img src="../img/project-name-chatbot-name.png" alt="Project Name vs. Chatbot Name" width="650px"/></p>

<hr>
<a name="!change-persona"></a>
### How do I change chatbot persona?

: Click on **`Design`** on the left menu panel and then click on **`Chatbot Settings`**. On
this page, you can customize your chatbot persona. See [Customize Chatbot Persona](../design#chatbot-persona) for more details.

<p align="center"><img src="../img/change-persona.png" alt="change chatbot persona" width="650"/></p>

<hr>
<a name="!own-persona"></a>
### How can I define my own persona?

: Click on **`Design`** on the left menu pane, then click on the
**`Custom`** persona. You can then define your own custom
persona. More details are under [Customize Chatbot
Persona](../design#chatbot-persona).


<hr>
<a name="!persona"></a>
### Will the persona I choose affect the way s/he responds to users?
: Yes, different persona may have different responses depending on the context of the chat. Please check our publication regarding the [effect of chatbot personality](https://dl.acm.org/citation.cfm?id=3232077&dl=ACM&coll=DL).

<hr>
<a name="!persona-fit"></a>
### If I give you the type of audience and information I am after, can you help me choose a fitting persona?
: We can help you choose a fitting persona if you provide more information about the interview you would like to conduct.

<hr>
<a name="!customize-chat"></a>
### How do I customize a conversation?
: Click on **`Design`** on the left menu pane, you will see the design page. Mouse over any text bubble or click on it to edit or delete the text. You can also click on any **`+`** sign to add new conversation topic.

<hr>
<a name="!miss-my-q"></a>
### Why didn't my chatbot take my question?

My chatbot asks a question, such as "I can help you now. What can I help you with today?".  But when a user asks a question, the chatbot does not answer and I have to ask it again as shown below.

<p align="center"><img src="../img/wrong-q.png" alt="wrong chatbot question" width="350px"/></p>


: Juji chatbots send two types of messages, one is just a message without waiting for a user to respond, the other is a "true" request, which will wait for a user to respond. To take a user input, make sure your question is a "true" question. Check the card associated with your question and make sure it looks like T5 below instead of T6. A "true" request/question has a chat icon associated with the card (T5), while a plain message does not have it (T6).

<p align="center"><img src="../img/pseudo-q.png" alt="pseudo question" width="350px"/></p>

When you want your chatbot to send a true question, make sure you choose `Make a Request` option as shown below:

<p align="center"><img src="../img/design-topic-type.png" alt="add a
request" width="550"/></p>

<hr>
<a name="!remark"></a>
### What is a `Remark` or `Message`?
: A remark is a chatbot comment in conversation that does not require user input.

<hr>
<a name="!msg-vs-request"></a>
### What are the differences between a `Message` and a `Request`?
: A message or remark is a chatbot comment in conversation that does not wait for a user response. In contrast, when the chatbot asks a question or make a request, it will actively wait for the user to input the answer.

<hr>
<a name="!custom-topic"></a>
### What is a custom topic and how to write it?
: A custom topic allows you to customize the way you would like the bot to respond to users' inputs. Topics are the primary building blocks of the chatbot's conversation. The [concept page](concept.md) of the Juji documentation provides detailed explanation on how to write a topic.

<hr>
<a name="!custom-response"></a>
### How can I customized the chatbot's response to participants' answers in open-ended questions?
: You can use both [Juji Studio](../juji-studio) or [Juji IDE](../juji-ide) to customize chatbot responses. Also check out [Chatbot Design](../design) for specifics.

<hr>
<a name="!mostly-choices"></a>
### Does the chatbot work with interview questions which have primarily choice answers, and need only the chatbot's help to draw out responses for those who select “other” in their multiple choice answer?
: Yes, we support choice questions, open-ended questions, and other types of questions. Although we recommend our users to take advantage of our AI powered conversation skills and personality analysis by using open-ended questions, our chatbot works perfectly in chat with primarily choice questions. The AI chatbot can be easily set up to collect extra responses when interviewee select "other" in a multiple choice question.

<hr>
<a name="!add-q"></a>
### How do I add a question?
: Click on **`Design`** on the left menu pane, you can add a question by clicking any **`+`** sign then choosing the question type.

<hr>
<a name="!multi-choice"></a>
### How to add a multiple choice (checkboxes) question?
: On the “Design” page of your chatbot, you can add a multiple choice question by first clicking the “+” sign then choosing “Checkboxes” in the popup menu.

<hr>
<a name="!single-choice"></a>
### How to add a single choice (radio buttons) question?
: On the “Design” page of your chatbot, you can add a single choice question by first clicking the “+” sign then choosing “Radio buttons” in the popup menu.

<hr>
<a name="!followup"></a>
### What is a follow-up request?
: A follow-up request is where a chatbot asks a question to deepen a conversation based on a user's answer to the previous question (i.e., parent question). For example, a follow-up question may be used to probe further (e.g., `What features do you dislike most?`) if a user's answer to the previous question (e.g., `How do you like the lipstick so far`) contains negative or positive sentiment (see how to easily [detect user sentiment](../design#sentiment-detection) in a chat). Unlike a reguar question, a follow-up question is often conditioned up user responses to a previous question.

<hr>
<a name="!followup-vs-reg"></a>
### What are the differences between a follow-up request or a request I added using the round green `+` button)?
### When should I add a follow-up request?
### Should I add a follow-up or a regular request?

: It is quite simple to test whether you need a follow-up or just a regular request. A follow-up request is always conditioned upon one or more other requests. The follow-up request will not be activated if such a condition is not met during a chat. In contrast, a regular request added using the green round **`+`** button will be activated unconditionally as the chat flows to it. In other words, if you want your chatbot to always make a request regardless what happened in a chat, you will add a regular request. Otherwise, you will add a follow-up request that will depend on certain conditions, e.g., particular user responses to a chatbot question.

<hr>
<a name="!capture-emoji"></a>
###How can I capture a user's emoji like "thumbs up" and respond to it using an emoji?

: In Juji, you can capture user emoji input in two ways. One is to capture the keyboard input of an emoji. For example, the keyboard input for the smiling face emoji is :-). To capture such a smiling face input and respond to it with a same emoji, you can create a trigger that uses `matches` pattern and then respond to this pattern using the keyboard input:

<p align="center"><img src="../img/handle-emoji-1.png" alt="Handle Emoji" width="450px"/></p>

: Here is the chat result that shows a user's emoji input and the corresponding chatbot emoji response:

<p align="center"><img src="../img/handle-emoji-1-result.png" alt="Handle Emoji Result" width="550px"/></p>

: Another way of capturing emojis is to directly copy and paste an emoji into a pattern as shown below (note that you must quote the emoji):

<p align="center"><img src="../img/handle-emoji-2.png" alt="Handle Emoji" width="450px"/></p>

: Here is the chat result that shows a user's emoji input and the corresponding chatbot emoji response:

<p align="center"><img src="../img/handle-emoji-2-result.png" alt="Handle Emoji Result" width="550px"/></p>

: In addition, Juji's built-in dialogs automatically handle many types of emojis. If you just want to use Juji default responses to user emojis, you don't need to do anything. The example below shows such a default Juji response to a user's frowning face emoji.

<p align="center"><img src="../img/default-emoji-response.png" alt="Handle Emoji Result" width="550px"/></p>

<hr>
<a name="!question-number"></a>
###How many questions should I put in so my chatbot can function reasonably smart?

: This depends on your chatbot application. Applications that involve
much knowledge especially complex knowledge may need many more
questions than others. Here is a practical way to [anticipate the
types of questions](../chatbot-design-tips#prepare-qa-list-and-chitchats)
your chatbot should handle. This list helps you jumpstart the smarts
of your chatbot.

<hr>
<a name="!faq-id"></a>
### Why do I need the ID column in my Q&A CSV file? Can I delete it? Do I have to use the IDs given to me?

: The ID column is used to "index" the Q&A list so your chatbot knows how various questions are related to each other. For example, the questions with the same ID indicate that these questions share the same answer so you don't need to repeat the answers in the CSV entries.

: The ID column must be kept in the CSV file. You can change the
values in the ID column to whatever text labels you want to use. We in
fact encourage you to use labels that you can remember to facilitate
Q&A management. After you make such changes, make sure you choose the
`Replace` option when you upload the changed CSV file. See [more tips](../design#qa-tips) on defining IDs.

<hr>
<a name="!confirm-unanswered-anser"></a>
### Why do I always need to confirm the answers to the unanswered user questions on my Q&A dashboard? Can my chatbot learn itself? Why didn't my chatbot automatically learn new Q&As?

: In the background, your chatbot is indeed learning constantly based on its interactions with users. Like any machine learning, self-learning however may be erroneous (still remember the [infamous chatbot Tay](https://en.wikipedia.org/wiki/Tay_(bot))?). To avoid such mistakes, Juji currently uses human-in-the-loop learning, which requires that a human verifies the learned results before adopting them.

: Here is an example where self-learned results may be
problematic. Consider the chat below between a user and a chatbot,
selling products that cure fleas.  Since the chatbot could not find an
answer to the user's question, it shows several potentially matched
questions. Although the user didn't see the answer she seeks, she is
interested in the answer regarding pet use anyway. So she clicks on the
suggested question (option 1) and views the answer.

<p align="center"><img src="../img/wrong-qa-1.png" alt="Wrong Matched QA" width="550px"/></p>

: Through this user interaction, the chatbot learns that the two
questions `Can I use your product for my kids` and `Can I use your
product for my pets?` are somewhat related to each other. It then
lists the latter as the top-matched one on the Q&A dashboard:

<p align="center"><img src="../img/wrong-qa-2.png" alt="Wrong Matched QA" width="550px"/></p>

: However, the chatbot cannot really determine whether these two
questions are close enough to share the same answer. In this case, it
might be very problematic if just making the two questions share the
same answer simply based on the user interaction. Such determination
is often highly domain dependent (e.g., the type of products being
sold), the chatbot needs to be taught explicitly. Hence Juji requires
that a human manually verifies whether a matched question is indeed a
good match to avoid potential mistakes. This will keep a chatbot's
knowledge base clean, and hopefully free of errors.

<hr>
<a name="!faq-q-variation"></a>
###How many question variations or expressions should I put in when preparing Q&A?

: You can start with just one expression per question. Juji has a rich question library that will automatically augment a question you put in. Additionally, Juji chatbots always try to recommend similar questions if it could not find a well matched question during a chat. You can also use the [Q&A dashboard](../design#customize-qa-and-fallback) to monitor and improve the Q&A capabilities of your chatbot incrementally.

: Below is an example showing that a chatbot recommends similar questions when a highly matched question could not be found.

<p align="center"><img src="../img/recommend-questions.png" alt="Recommend similar questions" width="650"/></p>

<hr>
<a name="!overlap-topics"></a>
### Why do I see overlapped topic cards or cannot add follow-ups?

: One of the most probable reasons is that you are editing the same
chatbot in multiple windows/tabs or several people are using the same
account. In these parallel sessions, you might have been editing
different parts of the chatbot flow and conflicts were created and
could not be reconciled. While we will prevent multiple sessions to be
active at the same time in the near future, please check to make sure
you have only one window/tab open for one chatbot at a time.


<hr>
<a name="!faq-not-updated"></a>
### Why cannot my chatbot answer any questions even after I uploaded my Q&A CSV file?

: If this occurs, please double check the Q&A CSV file you
uploaded. Make sure that all the Q&As are entered in the CSV following
the [required format](../design#customize-qa-and-fallback).

<hr>
<a name="!disable-chatbot"></a>
###How do I suspend/pause/stop/disable a chatbot? I don't want to delete my chatbot but I want to pause it.
###How do I set up "out of office" for my chatbot?

: This is quite easy to do on Juji. Just follow these steps to
[suspend a chatbot](../design#suspend-chat).

<hr>
<a name="!similar-vs-contains"></a>
###What is the difference between 'contains-keywords` and `is-similar-to` trigger?
### When should I use `contains-keywords` vs. `is-similar-to` trigger to guide my chatbot?

: To decide which type of trigger to use, please check out [this tip](../chatbot-design-tips-advanced#use-proper-chatbot-trigger) on the differences of the two and which one you should use.

<hr>
<a name="!choice-vs-free-text"></a>
###When should I use a choice question vs. a free-text question?
###How should I decide a choice question vs. a free-text question?

: These two questions normally elicit different types of
information. One (choice) is more structured than the other
(free-text). Check out [this design tip](../chatbot-design-tips-advanced#use-proper-chatbot-request) to
choose one to deliver the best user experience.
<hr>
<a name="!preview"></a>
### What does `Preview` do?
: The **`Preview`** page allows you to test your chatbot before you deploy it to meet your audience.

<hr>
<a name="!preview-start-again"></a>
### My chat starts over again when I return to the `Preview` page
: This is the expected behavior. “Preview” page is set up for user to tests their designed chats in different scenarios. When refreshed or returning to the “Preview” page from elsewhere, it will restart the chat.

## Deployment Questions

<hr>
<a name="!deploy-page"></a>
### What does `Deploy` do?
: This allows you to deploy your chatbot to meet your audience. For example, you can get a web URL and send it out with your email, or you can embed the URL on your website to meet with your website visitors.

<hr>
<a name="!deploy"></a>
### How do I deploy my chatbot?
: Click on **`Deploy`** on the left menu pane to go to the release page. Then choose your deployment type. For more details, check out various [deployment functions](../release).

<hr>
<a name="!where-deploy"></a>
### Should I create a chatbot on Facebook Messenger or on my website

: If you maintain a Facebook page or group and use this channel to
engage with your target audience frequently, we recommend that you deploy a
chatbot to your Facebook Messenger that attaches to your Facebook page
or group. A Facebook Messenger chatbot has several advantages over a web-based deployment:

: * Easy to deploy
: * Easy to personalize a chat for an opt-in user
: * Can be synced with Facebook posts or ads
: * Native to any mobile devices
: * Always on

<hr>
<a name="!deploy-to-web"></a>
### How do I deploy the chat to my website?
: Go to “Deploy” page, choose web deployment to get the URL. You can then embed the URL into an iframe on your website.

<hr>
<a name="!after-deploy"></a>
### After I deploy my chatbot, what should I do then?

: One wise chatbot developer says that raising a chatbot is similar to
raising a child, you should monitor your chatbot and feed your chatbot
with new knowledge periodically to improve it and help it grow. Juji
provides you with dashboards to [monitor the Q&A
status](../design#customize-qa-and-fallback) as well as [monior the
audience interaction](../reports) with your chatbot.

: We strongly recommend that you check your chatbot via the dashboards
periodically. If you don't have time to do so, you may want to hire a
professional (e.g., a chatbot agency) who can help you monitor and
maintain your chatbot.

<hr>
<a name="!vs-survey"></a>
### How to use Juji chatbot with Qualtrics or Survey Monkey?
### How to use Juji chatbot with other survey software?
: You can include Juji chatbot's Web deployment link in your survey messages. Alternatively, you can include third-party survey link in Juji chatbot's messages.

<hr>
<a name="!completion-code"></a>
### I want a completion code for Mechanical Turk. How do I get a completion code?
: In the `Wrap-up` topic, if you choose to end the chat, you have an option to  choose whether or not you want to display a completion code that is unique for every end-user when the conversation ends.

<hr>
<a name="!no-identity-info"></a>
### I don't want to collect any identifying information such as email addresses or last names
: On the web deployment, you can choose whether or not you want to collect email and/or last name from your chatbot end-users. The first name is mandatory for the chatbot to properly address the user in conversation.

<hr>
<a name="!247-chat"></a>
### Does my deployed chatbot operate 24/7?
: Certainly. Your chatbot is alive 24x7.

<hr>
<a name="!update-live"></a>
### Will we be able to go into the chatbot at any time and make changes after it goes live?


: Yes, Juji Studio allows you to do so very easily and quickly. Check out the instructions under [Design](../design).

## Reporting Questions

<hr>
<a name="!reports-page"></a>
### What does `Reports` do?
### What do the results look like?
### What do I get?
### What results do I get?
: The **`Reports`** page displays multiple types of information gathered by your chatbot, such as chat stats, responses from each user, personality analysis, and overall response summaries.

<hr>
<a name="!dont-see-results"></a>
### I don't see results of my chat
: Only the participation in a released(deployed) chat will show up in the results page. Participation in a preview chat will not be stored as results. For Web deployment, test mode is another option for testing. Comparing with testing on the `Preview` page, the participation on the test mode link can be viewed on the `Results` page.

<hr>
<a name="!download-results"></a>
### Can I download the conversation results?
: Yes. They can be downloaded as CSV files by clicking the download CSV icon next to the corresponding result type. See [export data to CSV](../reports#export-audience-data) for more details.

<hr>
<a name="!sync-w-crm"></a>
### What capabilities will we have to sync to SalesForce or Marketo?

: Currently you can export all your chat data to a CSV file, which can
then be easily imported into third-party applications, such as
SalesForce and Marketo. Check out [how to eport to CSV](../reports#export-audience-data). If you have specific data-export requirements, please feel free to write to us (support@juji.io).
