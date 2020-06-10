# How to Write a Script from Scratch

Advanced chatbot designers may want to edit the REP scripts directly, since a Juji chatbot's full power can be accessed through the script. Whereas Juji Studio only supports limited chatbot capabilities.

A script usually consists of the following sections:

* [namespace declaration](#declare-namespace): declare the namespace of your chatbot and its dependencies;
* [question definitions](#define-questions): define questions the chatbot will ask;
* [gui definitions](#define-questions): define gui forms the chatbot will use;
* [topic definitions](#define-topics): define topics the chatbot will use;
* [chat configuration](#configurate-chat): configurate the chatbot to your preferrence.

## Declare Namespace

To start writing a script, you need to have a [namespace](reference.md#namespace) that the chatbot will live in. This namespace needs to be generated from the Juji system. The easiest way is to create an release and use its namespace. One way to find such namespace is through the [IDE](juji-ide.md#code-editor). For the purpose of this tutorial, we will use the imaginary `juji-doc-random0.eng1.juji.web1` namespace.

Once you have your namespace, you can start your script by declaring the namespace:
```clojure
(ns juji-doc-random0.eng1.juji.web1
 (:require [other-namespace-1 :as alias1]
 		   [other-namespace-2 :as alias2])
 (:import [package-symbol class-name-symbols*]))
```
The `(:require ...)` expression and `(:import ...)` expression are optional. If you are not sure what to require or import, you can leave them out or use our default namespace declaration:
```clojure
(ns juji-doc-random0.eng1.juji.web1
 (:require
  [juji.topics.fallback.chatflow.v1 :as fallback.chatflow]
  [juji.topics.fallback.exception.v1 :as fallback.exception]
  [juji.topics.fallback.qa.v1 :as fallback.qa]
  [juji.topics.fallback.request.v1 :as fallback.request]
  [juji.topics.fallback.social.v2 :as fallback.social]
  [juji.topics.interviewing.v4 :as interviewing]
  [juji.concept.basic :as concept]
  [juji.expressions.rep.basic :as rep]
  [juji-doc-random0.eng1.custom :as custom]
  [juji-doc-random0.eng1.faq :as faq]))
```

## Define Questions

Questions are essential to a conversation. Discussion on how they are defined can be found in the [question section of the Language page](reference.md#question).

Below is an example. You can choose any arbitrary name for each question as long as it is unique and easy to refer to from other parts of the script.
```clojure
(question
 [question_1
  {:kind :open-ended,
   :heading "What's your name?",
   :content
   [{:text "What's your name?"}
    {:text "Can you tell me your name?", :repeatable true}],
   :required true,
   :min-input-len 1}
  question_2
  {:kind :single-choice,
   :heading "What are you looking for?",
   :content
   [{:text
     ["What are you looking for?"
      (if
       (not= "facebook" (participation-release-type))
       "(FB buttons will show up in Facebook Messenger)")]}],
   :required true,
   :choices
   [{:text "Buy a game", :value 0}
    {:text "See new games", :value 1}
    {:text "Pricing", :value 2}],
   :elements
   [{:title "What are you looking for?",
     :buttons
     [{:type "postback", :title "Buy a game", :payload "0"}
      {:type "postback", :title "See new games", :payload "1"}
      {:type "postback", :title "Pricing", :payload "2"}],
     :subtitle "",
     :image-url ""}],
   :fb-display-type "generic-template-choice"}
  question_3
  {:kind :single-choice,
   :heading "What game do you play the most?",
   :content [{:text "What game do you play the most?"}],
   :required true,
   :choices [{:text "MHW", :value 0} {:text "The Witcher", :value 1}]}
  question_4
  {:kind :text,
   :heading "Collecting Facebook email",
   :fb-display-type "email",
   :content
   [{:text "Please click on the email to confirm.", :repeatable true}],
   :required true}])
```

## Define GUIs

GUIs are used for some special forms to be displayed in the conversation. Its definition is described in the [GUI section of the Language page](reference.md#gui).

Below is an example. You can use the same naming convention as questions.
```clojure
(gui
 [fb-media_5
  {:fb-display-type "generic-template",
   :type :raw,
   :data
   [{:title "The game shop is open now!!!",
     :buttons [{:url "juji.io", :title "First game"}],
     :subtitle "",
     :image-url ""}]}])
```

## Define Topics

Topic is the central part of Juji's REP Language. Before you start on defining topics, it would be helpful to have a [conceptual overview](concept.md) of its role. Topic is very powerful in terms of what it can do. Please refer to the [topic section of the Language page](reference.md#topic) regarding the details of its definition and capabilities.

Below are some examples.
```clojure
(deftopic ask-person-name_1
 [?q]
 {:pre-condition [],
  :pre-action [(<- skip-gibberish-detection true)],
  :post-action []}
 []
 [(ask-question ?q) (<- skip-gibberish-detection true)]
 (juji.topics.interviewing.v4/handle-person-name-response ?q))

(deftopic collect-basic-info-from-gui-w-attribute_2_3
 [?q]
 {:pre-condition [], :pre-action [], :post-action []}
 []
 [(ask-question-gui ?q)]
 (juji.topics.interviewing.v4/handle-gui-completion-w-attribute ?q))

(deftopic collect-fb-email_4
 [?q]
 {:pre-condition
  [(not
    (or
     (user-has-attribute? "opt-in email")
     (user-has-attribute? "opt-in email fb")))],
  :pre-action [],
  :post-action []}
 []
 [(ask-question-gui ?q)]
 (juji.topics.interviewing.v4/handle-email-gui-completion ?q))

(deftopic display-gui_5
 [?gui]
 {:pre-condition [], :pre-action [], :post-action []}
 [(has-participation?) (not= "facebook" (participation-release-type))]
 ["Facebook media: "
  (get-fb-media-gui-titles ?gui)
  " (the actual FB media card including images will show up"
  "in FB messenger after deployment)\n"
  (when
   (fb-media-button-without-valid-url? ?gui)
   "\nWARNING: Please ensure all buttons have valid url." 
   "Otherwise, the FB Media will not be displayed in Facebook Messenger.")]
 []
 [(display-gui ?gui "no question display") (agenda-topic-done)])

(deftopic rep-tell
 [?rep-msg]
 {:pre-condition [], :pre-action [], :post-action []}
 []
 [?rep-msg (agenda-topic-done)])

(deftopic final-closing-leave
 [?rep-msg]
 {:named-pattern [_default-rep-closing
   				  [(user-first-name)
    			   ", thanks for your time. Hope to chat with you again soon!"]],
  :pre-condition [],
  :pre-action [],
  :post-action []}
 []
 [(if (not (nil? ?rep-msg)) ?rep-msg _default-rep-closing)
  (agenda-topic-done)
  (end-chat (post-chat-url))])
```

These six topics are all auto generated from [Juji's library topics](topics.md). Juji provides numerous built-in topics for asking questions, handling responses and more. They cover huge varieties of common chatbot use cases. Please refer to the description for finding the topic that best suits your use case. 

The first three topic examples are used to ask questions, and each of them uses another Juji built-in topic to handle user's response (i.e., `juji.topics.interviewing.v4/handle-person-name-response`, `juji.topics.interviewing.v4/handle-gui-completion-w-attribute` and `juji.topics.interviewing.v4/handle-email-gui-completion`).  

The `display-gui_5` topic is defined to display a gui message, whereas the `rep-tell` topic is defined to show an regular text message. The last topic `final-closing-leave` is defined to end the chat.

However, Chatbot designers can write their own topics from scratch. That is actually one of the major benefits of editing the script. All topics can be directly defined inside the script or in other script namespace that the current script is depending on. In self-defined topics, designers can fully realize Juji REP language's potential. 

On the other hand, if a designer just wants to reuse Juji built-in topics, like the ones in the example above, the topics actually need not to be redefined in the script. We will discuss more about this when we configurate the chat.

## Configurate Chat

Config is a form that connects different parts of the script together along with some parameters that control the Chatbot's behavior. Please refer to the [config section in the Language page](reference.md#config) on details of how a config is defined.

Below is an example.
```clojure
(config
 {:name "Juji",
  :ad-lib
  [juji.topics.fallback.qa.v1/translate-how-about-you
   faq/uploaded-faqs
   juji.topics.fallback.chatflow.v1/handle-missed-user-answers
   juji.topics.fallback.chatflow.v1/handle-user-excuses
   juji.topics.fallback.chatflow.v1/handle-chat-flow
   juji.topics.fallback.chatflow.v1/handle-skip
   juji.topics.fallback.request.v1/handle-user-requests
   juji.topics.fallback.social.v2/echo-user-input
   juji.topics.fallback.qa.v1/handle-user-questions-engagement
   juji.topics.fallback.qa.v1/handle-user-questions-rep
   juji.topics.fallback.qa.v1/handle-user-questions-juji
   juji.topics.fallback.qa.v1/handle-user-questions-general
   juji.topics.fallback.chatflow.v1/handle-user-clarification
   juji.topics.fallback.chatflow.v1/handle-no-knowledge
   juji.topics.fallback.social.v2/comment-user-input
   (juji.topics.fallback.exception.v1/handle-user-questions-not-answered
    "")
   juji.topics.fallback.exception.v1/handle-gibberish],
  :pre-action [(<-| default-response-to-question "")],
  :agenda
  [(rep-tell
    [["Hello, "
      (user-first-name)
      ", thanks for connecting! I am your AI helper and cannot wait to chat w/ you."]])
   (ask-person-name_1 question_1)
   (collect-basic-info-from-gui-w-attribute_2_3 question_2)
   (collect-basic-info-from-gui-w-attribute_2_3 question_3)
   (collect-fb-email_4 question_4)
   (display-gui_5 fb-media_5)
   (final-closing-leave
    [[(user-first-name)
      ", thank you again for chatting w/ me! You can sign up to create your own version of me: https://juji.ai/signup. \n See u later!"]])],
  :turn-pace 0,
  :between-response-delay 1500,
  :bio
  "Hi, I'm Juji, the quintessential default REP. I'm known for my winning personality and great sense of humor.",
  :faq ["5edeb5f9-63d9-4467-a82e-2c2d6cb337bc"],
  :session-duration-max 60,
  :personality "default",
  :image-lg "/assets/img/content/juji-chat-profile-lg.png"
  :image "/assets/img/content/juji-profile.png"
  :image-sm "/assets/img/content/juji-chat-profile-sm.png"})
```

The `:ad-lib` vector declares a lot of built-in topics as fallbacks. The namespaces it uses are all required in the namespace declaration above. The `:agenda` vector specifies the topics we defined above in an implicit order to be presented in the chat.

Now, if you put everything together, you have a working script. If you copy the examples from each part of this article into a script file and upload it into your release, it can be compiled and you can try to chat with it. However, if you copy the examples directly into IDE, don't forget to update the imaginary namespace to be the same as your release's.

Last but not least, since we did not change any of the Juji built-in topics in our example, we can simplify the script significantly by skipping the entire topic definition and using namespaced topics directly inside the `:agenda`. Below is an example of the simplified script.

```clojure
(ns juji-doc-random0.eng1.juji.web1
 (:require
  [juji.topics.fallback.chatflow.v1 :as fallback.chatflow]
  [juji.topics.fallback.exception.v1 :as fallback.exception]
  [juji.topics.fallback.qa.v1 :as fallback.qa]
  [juji.topics.fallback.request.v1 :as fallback.request]
  [juji.topics.fallback.social.v2 :as fallback.social]
  [juji.topics.interviewing.v4 :as interviewing]
  [juji.concept.basic :as concept]
  [juji.expressions.rep.basic :as rep]
  [juji-doc-random0.eng1.custom :as custom]
  [juji-doc-random0.eng1.faq :as faq]))

(question
 [question_1
  {:kind :open-ended,
   :heading "What's your name?",
   :content
   [{:text "What's your name?"}
    {:text "Can you tell me your name?", :repeatable true}],
   :required true,
   :min-input-len 1}
  question_2
  {:kind :single-choice,
   :heading "What are you looking for?",
   :content
   [{:text
     ["What are you looking for?"
      (if
       (not= "facebook" (participation-release-type))
       "(FB buttons will show up in Facebook Messenger)")]}],
   :required true,
   :choices
   [{:text "Buy a game", :value 0}
    {:text "See new games", :value 1}
    {:text "Pricing", :value 2}],
   :elements
   [{:title "What are you looking for?",
     :buttons
     [{:type "postback", :title "Buy a game", :payload "0"}
      {:type "postback", :title "See new games", :payload "1"}
      {:type "postback", :title "Pricing", :payload "2"}],
     :subtitle "",
     :image-url ""}],
   :fb-display-type "generic-template-choice"}
  question_3
  {:kind :single-choice,
   :heading "What game do you play the most?",
   :content [{:text "What game do you play the most?"}],
   :required true,
   :choices [{:text "MHW", :value 0} {:text "The Witcher", :value 1}]}
  question_4
  {:kind :text,
   :heading "Collecting Facebook email",
   :fb-display-type "email",
   :content
   [{:text "Please click on the email to confirm.", :repeatable true}],
   :required true}])

(gui
 [fb-media_5
  {:fb-display-type "generic-template",
   :type :raw,
   :data
   [{:title "The game shop is open now!!!",
     :buttons [{:url "juji.io", :title "First game"}],
     :subtitle "",
     :image-url ""}]}])

(config
 {:name "Juji",
  :ad-lib
  [fallback.qa/translate-how-about-you
   faq/uploaded-faqs
   fallback.chatflow/handle-missed-user-answers
   fallback.chatflow/handle-user-excuses
   fallback.chatflow/handle-chat-flow
   fallback.chatflow/handle-skip
   fallback.request/handle-user-requests
   fallback.social/echo-user-input
   fallback.qa/handle-user-questions-engagement
   fallback.qa/handle-user-questions-rep
   fallback.qa/handle-user-questions-juji
   fallback.qa/handle-user-questions-general
   fallback.chatflow/handle-user-clarification
   fallback.chatflow/handle-no-knowledge
   fallback.social/comment-user-input
   (fallback.exception/handle-user-questions-not-answered
    "")
   fallback.exception/handle-gibberish],
  :pre-action [(<-| default-response-to-question "")],
  :agenda
  [(interviewing/rep-tell
    [["Hello, "
      (user-first-name)
      ", thanks for connecting! I am your AI helper and cannot wait to chat w/ you."]])
   (interviewing/ask-person-name question_1)
   (interviewing/collect-basic-info-from-gui-w-attribute question_2)
   (interviewing/collect-basic-info-from-gui-w-attribute question_3)
   (interviewing/collect-fb-email question_4)
   (interviewing/display-gui fb-media_5)
   (interviewing/final-closing-leave
    [[(user-first-name)
      ", thank you again for chatting w/ me! You can sign up to create your own version of me: https://juji.ai/signup. \n See u later!"]])],
  :turn-pace 0,
  :between-response-delay 1500,
  :bio
  "Hi, I'm Juji, the quintessential default REP. I'm known for my winning personality and great sense of humor.",
  :faq ["5edeb5f9-63d9-4467-a82e-2c2d6cb337bc"],
  :session-duration-max 60,
  :personality "default",
  :image-lg "/assets/img/content/juji-chat-profile-lg.png"
  :image "/assets/img/content/juji-profile.png"
  :image-sm "/assets/img/content/juji-chat-profile-sm.png"}) 
```

Here you have it - a working REP script from scratch. This opens up great possibilities for your next powerful chatbot.

## The Alternative

Even though writing REP scripts directly gives you access to potentially very powerful chatbots, it may still be an overkill in many use cases. The way our CTO described it is that the script language is like the machine code. In most cases, we don't need to play with such low level details. Luckily, we have introduced a more intuitive representation to define Juji chatbots, which grants designers full access to all capabilities of Juji chatbots that are available in the Juji Studio and more. Stay tuned for our upcoming tutorial of the Config-doc.