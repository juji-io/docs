# **Design Tips: <br> Enable Quality Conversations**

When using AI chatbots to automate human interactions, not only should such AI chatbots carry out a conversation, but they should also engage their users in a quality and productive conversation. Here we share a set of design tips on how to design an AI chatbot that can deliver a quality conversation.

In case you are not sure what an AI chatbot is or why you need one,
check out this comparison on [AI chatbots vs. Non-AI
chatbots](../why-ai-chatbots).

## **Support Task Workflow and Social Chitchat**

Human-human conversations are always meant to be two-way
exchanges. Otherwise it is a monlogue. Similary, human-AI
conversations should also be two-way communication: both humans and AI
can take initiatives in such a conversation and work toward a common
goal. In particular, effective AI chatbots should be able to
accomplish specific tasks while delivering great social experiences at the
same time. Use the tips below to create an engageing AI chatbot with a
lot less time and effort than most of today's chat engines require
from users.

### Start w/ Chat Flow Outline

Building an AI chatbot is similar to writing a screenplay, which
should have a beginning, which equates to a welcome and set up, a second act, which takes you through the body of its content, and a third act, which transports you to a decision-based ending. The key to any good screenplay - and chatbot - is a clear through-line or narrative that takes you from beginning to end. Or to put it another way, when you get on a a bus you usually know where you're going. There's a reason for that.

Juji provides a set of chatbot templates, each of which has a clear narrative pathway, regardless of domain. We'd stronly recommend you start your journey into writing a chatbot by using one of these, if possible. If you're feeling ambitious and would rather skip the templat, always write a chatbot outline, just like a good screenwriter writes a beat sheet outline for her/his project. Of course in a chatbot, this will be more likely to involve dialogue, another critical part of both the screenwriter's and bot-writer's arsenal. Send your outline around for external feedback. You're almost certain to learn ways to improve it.

Below is a sample outline that is intended to create a chatbot
that can  chat with gamers about games.

<br>

<p align="center"><img src="../img/chat-outline.png" alt="chat-outline" width="650"/></p>

<br>

Here is a second sample outline, Here a chatbot helps customers make and manage restaurant reservations.

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
chatbot](../juji-studio/design) and add the marked items in the main chat flow.

<p align="center"><img src="../img/chat-outline-annotated.png" alt="annotated
sample chat outline" width="650"/></p>

Over time this process should become faster and faster as you become omre familar with the 'storytelling' aspects that Juji can handle so well. Indeed, many of our users say Juji is the best platform they have ever used not just becaise it has a complex built-in engine with an easy to understand UI but it also a very creative tool.

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
outline), and if they don't - according to the data - then you can adjust the topics until they do.

In particular, we recommend that you prepare answers to <a href="#" name="qa-types">**three types of user questions**</a> that can be anticipated.

* <a href="#help-guide">HELP Guide</a>
* <a href="#recip-q">Reciprocal Questions</a>
* <a href="#common-q">Common Sense Questions</a>

#### <a name="help-guide"></a>Prepare HELP Guide

No matter how smart your chatbot is, there's always something it's going to miss. To make
a conversation more efficient, transparent and effective, we recommend you
always prepare a `HELP` guide to make sure users know your chatbot's capabilities. By establishing its limits, you will be setting clear expectations with users, who will be more likely to stick with your chatbot if something goes awry. If a disappointment is a true surprise, users tend to take their leave, sharpish. And when they go, they have a habit of not coming back. So this is important stuff.

The best way to insure you're covered is to head for the Q&A dashboard, and add an entry with "Help"
in the `Question` column, and your help guide in the `Answer` column, and then click `Submit`. You can also do so by downloading the CSV file on
the Q&A board, filling in the entry related to `Help` in the CSV file, and then uploading the revised CSV file.

As part of the HELP guide, it is also critical to customize answers to the following two questions:

* **User request to chat with a human agent**. By default, this question is already in a chatbot's knowledge base. You may want to edit the system default response based on your situation. Just download the CSV file from the Q&A board and edit the answer to this question in the CSV file. Then rename and upload to save the entries to your chatbot.

* **Default response to any unrecognized user input**. You can edit the <a href="https://juji.io/docs/juji-studio/design/" target="_blank">**default response to unknown user input**</a> as part of the [conversation parameters](../design#conversation-parameters). You can also add randomized choices to more specific fallbacks.

You can handle other help questions, but be careful not to overwhelm the user, who can always go to the FAQ if s/he needs specific questions answered at any time during the conversation.


#### <a name="recip-q"></a>Prepare Answers to Reciprocal Questions

Users often ask 'reciprocal questions', which are triggered by bot questions like `what is your favorite
color` Chatbot creators should anticipate that users won't answer, except with a 'reciprocal question' of their own, so it's wise to prepare the chatbot to handle these 'comebackers'. Not surprisingly, there are Juji topics that can help make this easy for you.

#### <a name="common-q"></a>Prepare Answers to "Common Sense" Questions

Users engage better with chatbots that can can answer simple, "common sense" questions related to the duties of the
chatbot, or even vaguely more connected 'common-snese questions. For example, if a chatbot is used to greet online customers
for an e-commerce business, it should be able to answer questions about the price and availability of the products sold online. Similarly, if a chatbot is used to
onboard customers for an application, it should answer questions about the benefits and features of the application.

All the Q&As can be entered in a CSV file or directly in the table on
the `Q&A Board` page. Please refer to [Customize
Q&A](../juji-studio/design#customize-qa-and-fallback) for more details on how to
add/edit Q&As.

<p align="center"><img src="../img/design-qa.png" alt="define Q&As" width="650"/></p>

## **Balance Business Goals and User Experience**

Businesses use chatbots to scale out human-human communications and
optimize business outcomes (e.g., improving customer satisfaction
while reducing cost). To achieve this goal, it is important to design
a chatbot that can balance getting the job done with
user experience, also known as 'having fun'.  Getting this balance just right is a critical step, but we try to make it easy with just the few key tips below.

### Mix Messages and Requests

Juji AI chatbots can send two types of messages (check out [chatbot
design](../juji-studio/design)). One type is a plain chatbot **message** that ignores
user input. The other is a chatbot **request** that waits for user input
and responds to it. If a chatbot sends too many messages that ignore
user input, it feels like a monologue instead of a
dialog, or conversation. If a chatbot asks too many questions, it feels like an
interrogation instead of a discussion. So, just like all good things, a little moderation and balance is required. Mix up the message and requestes. Edit your work on the fly. If you find your bot is sounding too interogative, make some adjustments. And remember. rewriting is a lot more fun than getting that first draft down (although that's must too). If you hit the sweet spot you've got yourself a
*mixed-initiative conversation*.  Pat yourself on the back for creating a very humanlike conversation.

### The Role of Delays

Chatbot messages can be delayed in 1s increments. (you can set `delay` in [topic
settings](#topic-settings). Delays seem natural and real, as if the bot is choosing its response wisely (even though it's already loaded up by the bot in a matter of a few milliseconds. The second and more creative reason for a delay is that it imparts drama at key moment in the course of a chatbot through-line. For example, if the expected response to a given user question is personal, profound, or in some way critical to the chatbot's narrative, take your time giving the bot's response and add a little drama to the proceedings. You can also test the amount of delay that works for a given situation.

**IMPORTANT TIP:** If you intend to have your chatbot wait for a user input and respond to it before moving on, make sure you choose `Make a Request`. Otherwise, your chatbot simply ignores any user input even if the message is worded like a question. As the example shown below, T6 will not wait for a user's input but T5 will. Note the chat icon appearing on T5, indicating T5 is a "true" question.

<p align="center"><img src="../img/pseudo-q.png" alt="Pseudo question" width="350"/></p>

### Mix In Different Types of Requests.

Juji AI chatbots support several types of requests, e.g., choice-based
and free-text requests. While choice-based questions are quick and
easy for users to answer, they gather limited information for
a chatbot to act upon. Moreover, choice-based answers can be easily
"cheated" (e.g., a user simply makes a random choice without even
reading the request). On the other hand, free-text questions,
especially open-ended questions, can often garner rich and meaningful
responses, but they take more time and effort for users to respond. We want users to want to respond fully. The character and personality of the bot can be absolutely critical in that regard.

### A 2:3 Ratio

To keep users engaged over the course of a chat narrative be sure mix choice-based and free-text requests. Our research shows that the optimium ratio is 2:3, with two (2) choice questions for every three (3) free-text inquiries. We have found that proportion normally works very well.

### The Yes-No Question Is Not Always Your Friend

We also encourage the use of open-ended chatbot inquiries (e.g., `How do you feel about the movie`) instead of simple yes-no questions (e.g., `Do you like the movie`), which open the bot up to a not particularly useful mono-syllabic answer. Bots engage users when users feel engaged enough to text into the bot, but users do not like the question `why?` following a yes/no question which should have been avoided in the first place. The golden rule here is that user engagement is everything.

### Use Proper Juji Built-in Dialog

As mentioned in the [design](../juji-studio/design) section, Juji provides a rich
set of [built-in, mini conversations](../juji-studio/design#built-in-dialog). These
built-in dialogs automatically handle highly diverse, potentially
complex user expressions. Such dialogs deliver great conversation experience
without requiring much customization. And as Juji grows so does the library of built-in conversational snippets, making your life even easier with Juji.

Since Juji uses the request label (see how to [write a good label](../chatbot-design-tips-advanced#give-sensible-labels)) to find the matched built-in dialog, its up to label selecction to find the built-in that's right for you. That's why we always recommend testing out the built-ins against your label until you find the built-in that works for your conversational outline and structure. Don't spend hours on this, but at least get the responses to the point where they're accurate enough to be effective.=, and if you want to improve them, you can add variations that go into the Juji brain bank, so it's a win-win.

<p align="center"><img src="../img/search-a-topic.png" alt="search a
topic" width="550"/></p>

### Detecting Gibberish

`akjds;laksdjfsl;kdjfa;lskdjf` When a Juji chatbot sees that in response to a pretty straightforward question, it can detect that its gibberish and respond in a way that helps the user return to a more motivated place, if that's possible. Even  person with a less-than-goldfish length attention span will appreciate the bot's good intentions, and after adding some more gibberish may be silently impressed that here was a bot that kind of understood their idea of a joke rather than deliver some completely robotic fallback like "I'm still learning. Run your answer by me again." Juji bots like to learn but `akjds;laksdjfsl;kdjfa;lskdjf` is definitely not on the curriculum.

Juji regards "non-answers" the sanme way as it treats `asdfasdfouywer9uw09eru1` The classic non-answer is `I don't know` Using the gibberish detection workflow you can decide whether to accept an non-answer response as shown below.

<p align="center"><img src="../img/topic-setting-1.png" alt="Topic
Setting 1" width="650"/></p>

You can also control the required length of any given user response and also indicate whether a chatbot request is required
to answer or not. Be careful with these settings. They are global and can have a major impact on the functionality of your Juji Chatbot.

### Optimal Chat Length

Although Juji AI chatbots can engage users in a very lengthy
conversation (e.g., the longest was 3.5 hours), engaging someone in a
conversation requires much time and mental effort, for both visitor and creator. The rule of thumb here should be, make the chatbot as short as it can be get its job done. If you're keeping a user on the bot for 5 minutes you are doing very well, so don't push your luck unless your use case requires it. If you're seeking out free-text information, and your bot's character and dialogue is managing to ellicit a ton of free text responses that are worthwhile, 10-12 minutes is probably your limit.  If your
chatbot is intended to conduct lengthy interviews, try to keep it within 45 minutes.

## **Create Natural and Engaging Conversations**

The tips listed below help power chatbot to deliver a natural, humanlike
conversation experience that can best engage with your target audience.

### Paraphrase Messages and Requests

To make a chatbot sound more natural, define variations of your line or 'paraphrases' as we call them at Juji for any given a chatbot
message or a request. For example, if your chatbot says 'hello' to your
audience everyday, you might want your chatbot to change it up on a randomized basis to
avoid sounding repetitive, and robotic. This can be easily done by adding paraphrases
to the 'hello' message. Below indicates the use of the green "+" to add
paraphrases to a chatbot message:

<p align="center"><img src="../img/add-paraphrases-remark.png" alt="paraphrase a message" width="550"/></p>

Similarly, a chatbot may need to repeat a question/request if a user
does not comply to it. In such a case, you want to add different forms of the question prompt like a person would IRL. Repetitive is a great giveaway of robotic conversation, and people, who like their bots to be just like them, hate it. Juji also enables another humanlike element. When giving a request first time, the chatbot
will naturally set out the context and rationale for its request. On subsequent asks of the tame question, the chatbot will omit these contextual elements (because the user is already aware of them) and in so doing will sound natural and relaxed.

Here's am example of paraphrasing a request in action, showing the initial contextually sound phrasing of a chatbot request. Since this message is quite a mouthful, avoiding it on a second or subsequent ask would b very valuable

<p align="center"><img src="../img/initial-msg.png" alt="Initial Message" width="650"/></p>.

Here is the paraphrase (shorter version) of the same message above and will be used by the chatbot to repeat the question if needed. Always check the box "only for reasking" with your follow-up versions fo the same question, so Juji doesn't randomly choose the shorter, de-contextualized version as the randomized first choice, thereby confusing the user.

<p align="center"><img src="../img/reasking-msg.png" alt="Reasking Message" width="650"/></p>

You can decide how many of your versions are for reasking, and therefore create a range of questions which is deep and expressive.

<p align="center"><img src="../img/paraphrase-a-question-2.png" alt="chatbot design tip: defining a list of re-asking expressions for a question" width="650"/></p>

The screenshot below shows how question paraphrases are used in a chat.

<p align="center"><img src="../img/paraphrase-a-question-demo.png" alt="chatbot design tip: a chatbot asks a question using different expressions: first time vs. second time." width="650"/></p>

### Personalize Messages and Requests

Personalized messages and requests make users feel more special and keeps them engaged. There are two simple ways to make a
chatbot message or requested personalized.

* **Address users by their first name occasionally during a chat**.

The function  `(user-first-name)` can be inserted into any chatbot message to make users feel that chatbot is paying attention to them. Everyone likes the personal touch. Don't overuse the first name function in your conversation. It can go from caring to creepy kind of quickly. A quick read-out loud will set the alarm bells ringing if you've gone too far.

<p align="center"><img src="../img/user-first-name-func.png" alt="call user by his or her first name function (user-first-name)" width="650"/></p>

* **Repeat what a user says in a chatbot response**. This is another "make the user feel heard" approach. Here's how

	1. Define a `contains-keywords` trigger
	2. `STORE MATCHED INPUT` into a custom attribute (e.g., `like-protein`)
	3. Insert the attribute into chatbot response using a function. (e.g., `(get-user-attribute-as-string "like-protein")`

<p align="center"><img src="../img/design-repeat-words.png" alt="Repeat user words" width="450"/></p>

Below is how the chat should play out:

<p align="center"><img src="../img/preview-repeat-words.png" alt="Preview the repeat of user words" width="650"/></p>

Again, it's important not to go overboard with the repeat-backs, or what sounded supportive can quickly become tiresome, and possibly even disingenuous. (Both the former are conversation killers in real life so you can imagine how an automated chatbot will fair having to deal with this kind of repetition).

* **Echo a user's feelings in a chatbot response**.

Acknowledging user feelings, and making clear you understand them are the dual elements of empathy (Empathy is made up of 'cognitive empathy' which is understanding a person's concerns or predicament, which is a pre-requisite of 'affective empathy' which is the expressed concern to 'show' the person that you (or in this case the bot) can demonstrate its understanding. In other words it's a very important device, and here's how to build it. When your customizing your bots responses;

  	1. Define a `contains-sentiment` trigger
  	2. Create a corresponding chatbot response based on the detected sentiment

<p align="center"><img src="../img/design-ack-sentiment.png" alt="Ack user sentiment" width="450"/></p>

And here's the chat as it would play out

<p align="center"><img src="../img/preview-ack-sentiment.png" alt="Preview how to ack user sentiment" width="650"/></p>

Used judiciously, this feature is a very important way of imprinting the empathetic nature of Juji on its users. It's worth noting that empathy is a profund and very transferable human trait, that is foundational to personality. It is often known as a "super trait", and its central to Juji's approach.

### Determine Chatbot Default Response

We've established that no chatbot is perfect. Before you came to Juji, you may have felt that you were never going to find a bot engine that was close enough.  To
cope with unrecognizable user input, Juji provides many built-in dialogs. However, these built-in chatbot responses may not be suitable
for your chatbot applications, so you can build your own. For example, if a user asks about the weather at a given location, such as `What's the weather like in San Jose`. The default, built-in chatbot response would be like: `I am not a weather bot. You may want to check with weather.com`. However, if you are
building a weather chatbot, such a response wouldn't be right at all.

So go ahead and override Juji's built-in chatbot responses with your own. Simple go to the `Chatbot Settings` page (the right hand tab on the `Design` ) to define this new default response:

<p align="center"><img src="../img/chatbot-settings-defaultresponse.png"
alt="chatbot default response to unknown user input" width="650"/></p>

In the above example, the default response that you entered will then
be used instead of Juji built-in default responses.

### Chatbot Refresh Rate

Juji is structured so it can essentially talk forever if prompted. By default, though, the bot restarts fresh every 60 minutes. If your bot is a long interview, you might want set the refresh rate a little longer, because it's unlikely that the user will want to start over with the same interview. That wouold be odd. You can set the `refresh rate` by scrolling down `chatbot settings` situated as the right tab of the `design` screen.

<p align="center"><img src="../img/chatbot-settings-refresh.png"
alt="set up a chatbot refresh rate" width="650"/></p>

## **Ensure Conversation Quality**

Like in a natural conversation, humans rarely follow a pre-defined
conversation flo, and tend to digress, because we're all - to a greater or lesser extent - creative, spontaneous, or very occassionally in a bad mood and non-cooperative. To
engage users in a quality conversation, a smart chatbot should be able to anticipate user digressions and handle them just right. Getting this right in most engines is a time-consuming feat, but in Juji we've taken the human approach, analyzed milions of human-chatbot conversations and boiled down the number of digressions to those most commonly used (and that make up about 95% of most digressive interactions). Digressions are most likely as non-dequitor responses to questions, particularly open-end questions.

Here are just a few examples, some of which are already covered.

* Gibberish user input (e.g., "aasfa asfs fa")
* "I don't know" input
* User excuses  (e.g., "this question is too hard for me")
* User clarification (e.g., "What do you mean?")
* User asks to alter chat flow (e.g., "skip")
* User asks an irrelevant question. (Do you think a blue shirt was right for today?)
* User comments on the question (e.g., "this is a strange question")
* Mono-syllabic or lazy input (e.g., "good").

Not only must a chatbot respond to each type of user digression properly,
but it must also decide how to continue a conversation. For example,
if a chatbot asks a non-required question, it should not re-ask the
question if a user asks to skip the question.

To help chatbot designers handle diverse user digressions, Juji offers
a rich, built-in fallback conversation library that automatically
detects many types of user digression and figures out how to handle
each type properly. Chatbot designers can leverage the fallback
library directly but still have the flexibility to turn on/off specific
digression handlers using the chatbot settings as shown below.

<p align="center"><img src="../img/handling-user-digressions.png"
alt="Settings for turning on or off different user digression handling
" width="650"/></p>

Next we use more concrete examples to explain how Juji handles several
common types of user digressions to ensure conversation quality.

### Handling User Excuses to Open-Ended Questions

<p align="center"><img src="../img/topic-setting-2.png" alt="Topic
Setting 2" width="650"/></p>

Being human, users may also give "excuses" or intentionally dodge a question. Take this example. Let's assume
that a chatbot asks a user "What's the top challenge you face?".  One
user may respond "I don't really know since I have many challenges."
while another user may state "That's tough to answer." Both get us nowhere. There are countless examples of "nowhere" responses like this, which need carefully constructed responses to reinvigorate the discussoin (Bot are just like humans in that regard. If a conversation is flagging, we use similar devices to get the confab back on the rails. At Juji, we do this by detecting the type of user response, and giving a suitable comeback. If a question is deemed optional but was answered anyway, we just tell the user not to worry and move on.

Below shows Juji's handling of several user excuses.

* Example 1: Too personal
<p align="center"><img src="../img/handling-user-excuse-1.png"
alt="Handling a user excuse: this is very personal" width="650"/></p>

* Example 2: No matched answer
<p align="center"><img src="../img/handling-user-excuse-2.png"
alt="Handling a user excuse: don't know how to answer the question"
width="650"/></p>

* Example 3: Too hard
<p align="center"><img src="../img/handling-user-excuse-3.png"
alt="Handling a user excuse: the question is too hard to answer"
width="650"/></p>

A chatbot designer can enable/disable Juji's auto excuse handling by
going to the "Chatbot Settings" tab, and check on/off the box labeled
"Handles a user's various excuses not answering a question" under
"Fallback handling".

### Handling User Clarification Questions

Just like in any conversations, a user might not fully understand a
chatbot's question or find the question unclear. When this occurs, the
user may seek clarification with a "Clarification Question". Here are a few examples of how to create a seamless clarification strategy.

<p align="center"><img src="../img/handling-user-clarification.png"
alt="Handling a user's clarification question: what would you like to
know about me" width="650"/></p>

Here is another example, a chatbot asks "What's the top challenge you
face?" A user may ask a clarification question "What kind of
challenges are you referring to?" or "What do you mean?".

Since it is hard to anticipate what a user's clarification question
might be and pre-train a chatbot to handle all possible clarification
expressions, one of the easiest ways for a chatbot to handle user
clarification questions is to paraphrase a question in multiple ways.
This would help a user better understand the question.

Using the first example mentioned above, the chatbot may paraphrase
the question as following:

* Could you describe yourself in three key phrases?
* Could you say a bit about the type of work you do?
* Could you say a bit about yourself, e.g., the kind of gamer you are?

Make the paraphrases more specific and the specifics can be determined by the conversation context (e.g., a conversation with job candidates vs. employees vs. gamers).  Should the chatbot just start with a more specific question? Our tip would be keeping the initial asking broad because you never know what kind of answers people may come up with.  You can always design paraphrases to be more specific to handle user clarification questions.

You can paraphrase a question easily with Huhi, so your attempts to help a user get the clarity s/he needs will feel natural, friendly and human. As a chatbot
designer, you just need to design a chatbot question with severa alternatives (see <a
href="https://juji.io/docs/quality-chatbot-design-tips/#paraphrase-messages-and-requests">paraphrase
a chatbot question</a>) and Juji takes care of the rest, with the help of our ever-growing built-in library that captures, among many other things, those pesky clarification questions. By reprhasing your chatbot's question, calmly and naturalistically, we are far more likely to keep the chat going, once the user feels more comfortable moving forward with a useful response that helps her/hiim and Juji. One last note on this area. Juji is designed to be a very cooperative chatbot, which thrives on teamwork with the user. That teamwork makes for better responses and greater user loyalty.

## **Preview Chatbot Often When Building**

Most of Juji's myriad of features aren't activated until you preview your bot, and sometimes there's a mismatch between your entry and how Juji responds. The more you preview as you design, the more you'll be able to adjust your input in a way that Juji can understand. None of this is any more than trial and error. Finally, if you like what you've got but haven't been able to get out of a conflict with the AI, go ahead and clone what you have (or take a copy of the text version of the bot) so you have a record of the copy you like. It's very likely that the solution will enable you to keep most if not all your creativity intact.

## Periodically Change Up Your Chatbot's Conversation

Unless you're calling a particularly rigid call center, humans have a tendency to vary their scripts with some ad-libs. You should consider doing the same with your chatbot. Clients have a tendency to say "done and dusted", when their chatbot is in production, but continuing to improve and vary it keeps it feeling more alive, which for a blob of spinning electrons is always a good idea. The moral of the story is don't be afraid to go in and adjust the story. You should definitely do this is some part of the flow isn't working, according to the conversation data, but even if everything's feeling great, changing it up to keep it fresh is also a great idea. One word of caution though. Don't undermine it at its core. In other words, don't throw out the bot with the bathwater.

## **What's Next**

Want to power up your chatbot and get some more magic going? Juji has
you covered. Dig deeper into [advanced design tips](../chatbot-design-tips-advanced) or **[Juji IDE](../juji-ide)**.
