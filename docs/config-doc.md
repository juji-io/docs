# Config-doc Guide
A config-doc is a data structure that stores a chatflow from Juji Studio. Every chatflow's design has a corresponding config-doc. Designers can download their config-docs as backups of their chatflows. Any valid changes to a config-doc will be reflected in the corresponding chatflow in Juji Studio. Unlike [REP scripts](script.md), config-docs speak in higher level representation of the chatflow. So they are more intuitive to edit and easier to understant than scripts. These properties make config-docs the ideal first stop for designers who want to build Juji AI chatbots without Juji Studio. In other words, config-docs can be used for, not limited to, the following purposes:

* building Juji AI Chatbots using non-Juji UI/editor;
* converting to/from other chatflow designs;
* storing/transporting human readable Juji chatflow.

## The Abstraction of Items

The config-doc's representation is evolved around the abstraction of item. A chatflow is essentially some arrangement of such items. In Juji Studio, the items are shown as [topic blocks](design.md). 

<p align="center"><img src="../img/design-add-topic.png" alt="Juji topic blocks example" width="350"/></p>

In other platforms, items may have different names. For example, in both [ManyChat](https://support.manychat.com/support/solutions/articles/36000105060-flow-builder) and [Landbot](https://help.landbot.io/category/rysihgrn96-build-blocks), they are called blocks. 

<p align="center"><img src="../img/manychat-blocks.png" alt="ManyChat blocks example" width="650px"/></p>
<p align="center"><img src="../img/landbot-blocks.png" alt="Landbot blocks example" width="650px"/></p>

No matter how it is called, items define similar things - the message to be sent, some side effects on the system and possible handling of user inputs. We will discuss in detail how Juji items can be defined in the [agenda](#agenda) and [items](#items) section of the config-doc.

## How to access config-docs

Designers can find each engagement's config-doc in the [IDE](juji-ide.md) under the name "Config", where they can edit the content directly. Alternatively, designers can write their config-doc somewhere else and upload it through the IDE or API call.

## Overview of the Config-doc Structure
The config-doc can be written as a Clojure map or a JSON object. Since the IDE currently only supports Clojure format, we will start our guide in Clojure format. However, a designer can convert from one to another easily. The only difference between the JSON format and Clojure format is that the in the JSON format all key-value pair, a.k.a. field, keys are turned into string, whereas in the Clojure format they are either Clojure [keywords](https://clojure.org/reference/data_structures#Keywords) or integers.

In general, designers are free to add new fields in a config-doc, as long as they do not conflict with existing fields. Here are the six essential fields for a basic chatflow:

* requires: dependencies the chatbot is using;
* settings: general settings for the chatbot;
* items: definition of the items;
* agenda: items ordered implicitly to form the main flow;
* faq: Q&A data used by the chatbot;
* version: config-doc version.

We will look at each of these fields in detail.

## requires
The `:requires` field declares the dependencies of this chatbot. Its value is a string representing the require part of the namespace declaration. Usually designers don't need to change this. Below is an example of a typical value of requires.
```clojure
"[[juji.topics.fallback.chatflow.v1 :as fallback.chatflow] [juji.topics.fallback.exception.v1 :as fallback.exception] [juji.topics.fallback.qa.v1 :as fallback.qa] [juji.topics.fallback.request.v1 :as fallback.request] [juji.topics.fallback.social.v2 :as fallback.social] [juji.topics.interviewing.v4 :as interviewing] [juji.concept.basic :as concept] [juji.expressions.rep.basic :as rep]]"
```

## settings
The `:settings` field configures the chatbot's general behavior. Its value is a map. Below is an typical default settings map.
```clojure
{:turn-pace 0,
 :between-response-delay 1500,
 :session-duration-max 60,
 :thin-text-threshold 5,
 :task-completion-code false,
 :default-response-to-question "",
 :ad-lib [{:cid "juji.topics.fallback.chatflow.v1/handle-missed-user-answers",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.chatflow.v1/handle-missed-user-answers",
	           :description "Handles a chatbot missed user answers"}
	          {:cid "juji.topics.fallback.chatflow.v1/handle-user-excuses",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.chatflow.v1/handle-user-excuses",
	           :description "Handles a user's various \"excuses\" not answering a question"}
	          {:cid "juji.topics.fallback.chatflow.v1/handle-chat-flow",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.chatflow.v1/handle-chat-flow",
	           :description "Handles a user' input regarding the chat flow."}
	          {:cid "juji.topics.fallback.chatflow.v1/handle-skip",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.chatflow.v1/handle-skip",
	           :description "Handles a user's request to skip certain parts of a chat"}
	          {:cid "juji.topics.fallback.request.v1/handle-user-requests",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.request.v1/handle-user-requests",
	           :description "Handle a user's requests during a chat"}
	          {:cid "juji.topics.fallback.social.v2/echo-user-input",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.social.v2/echo-user-input",
	           :description "Handles users' chitchat input"}
	          {:cid "juji.topics.fallback.qa.v1/handle-user-questions-engagement",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.qa.v1/handle-user-questions-engagement",
	           :description "Answer a user's questions about the chat"}
	          {:cid "juji.topics.fallback.qa.v1/handle-user-questions-rep",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.qa.v1/handle-user-questions-rep",
	           :description "Answer a user's questions about the chatbot"}
	          {:cid "juji.topics.fallback.qa.v1/handle-user-questions-juji",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.qa.v1/handle-user-questions-juji",
	           :description "Answer a user's questions regarding Juji"}
	          {:cid "juji.topics.fallback.qa.v1/handle-user-questions-general",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.qa.v1/handle-user-questions-general",
	           :description "Answer a user's general questions"}
	          {:cid "juji.topics.fallback.chatflow.v1/handle-user-clarification",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.chatflow.v1/handle-user-clarification",
	           :description "Respond to a user's request for clarification"}
	          {:cid "juji.topics.fallback.chatflow.v1/handle-no-knowledge",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.chatflow.v1/handle-no-knowledge",
	           :description "Handles when a user claims that s/he has not knowledge"}
	          {:cid "juji.topics.fallback.social.v2/comment-user-input",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.social.v2/comment-user-input",
	           :description "Comment on a user's input"}
	          {:cid "juji.topics.fallback.exception.v1/handle-user-questions-not-answered",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.exception.v1/handle-user-questions-not-answered",
	           :needed true,
	           :parameters [{:name "default-response-to-question",
	                                  :value-path ["settings" "default-response-to-question"]}],
	           :description "Handles user questions that a chatbot cannot answer"}
	          {:cid "juji.topics.fallback.exception.v1/handle-gibberish",
	           :skip false,
	           :type "fallback",
	           :topic "juji.topics.fallback.exception.v1/handle-gibberish",
	           :description "Handle a user's gibberish input"}],
 :translations [{:cid "juji.topics.fallback.qa.v1/translate-how-about-you",
		                 :skip false,
			             :type "fallback",
			             :topic "juji.topics.fallback.qa.v1/translate-how-about-you",
			             :description "Handles a user's reciprocal question to the chatbot"}],
 :persona {:cid "juji",
		          :name "Juji",
		          :background "#8BDFCD",
		          :bio "Hi, I'm Juji, the quintessential default REP. I'm known for my winning personality and great sense of humor.",
		          :info "neutral stock persona",
		          :image-lg "/assets/img/content/juji-chat-profile-lg.png",
		          :personality "default",
		          :image "/assets/img/content/juji-profile.png",
		          :image-sm "/assets/img/content/juji-chat-profile-sm.png"}}
```
As we can see, there are quite a few sub-fields. Let's take a look at them one by one:

* turn-pace: Its value is an integer that defines the interval between system's proactive attempts to say something, in seconds.
* between-response-delay: Its value is an integer. When REP have multiple sentences to say in one turn, it's the delay in milliseconds between the sentences.
* session-duration-max: Its value is an integer that defines the maximum session duration in minutes. Once the duration has passed, the chatbot would leave the session.
* thin-text-threshold: Its value is an integer. If the user input's word count is less than the integer and the input is not matched to any existing triggers, the chatbot will ask for more input.
* task-completion-code: Its value is a boolean. If true, a random code will be generated upon chat completion and it will be given to the participant.
* default-response-to-question: Its value is a string. The chatbot will use this to respond if it does not understand a user's question. If the string is empty, a default response is used.
* ad-lib: Its value is an vector of maps, where each map represents a fallback topic. Currently only Juji's built-in fallback topics are supported. Designers can start with the default topics and remove the ones they don't want.
* translations: Its value is an vector of maps, where each map represents a translation topic. Currently only Juji's built-in translation topics are supported. The translation topics are applied after the main topic. In most cases, this field doesn't need to be changed.
* persona: Its value is a map that defines the chatbot persona. It does not need to be changed if the chat is not happening inside a [Juji web release](release.md#deploy-to-website) UI.

## items
The value of `:items` is a map where each key-value pair is an item as value and its id as key. An item's id is an unique non-negative integer. Below is an example of an items map that includes items of various types and sub-types. We will examine these concepts in detail.

```clojure
{;; remark items
 0 {:description "Display a plain text message",
     	:category "Provide user with information in general",
        :content ["Hello, `(user-first-name)`, thanks for connecting! I am your AI helper and cannot wait to chat w/ you."],
        :cid "juji.topics.interviewing.v4/rep-tell",
        :name "Welcome",
        :settings {:delay-start 0},
        :type "remark",
        :topic "juji.topics.interviewing.v4/rep-tell",
        :sub-type "plain-text",
        :id 0}
 1 {:description "Display a facebook media form",
        :name "T1",
        :settings {:delay-start 0},
        :type "remark",
        :topic "juji.topics.interviewing.v4/display-gui",
        :elements [{:title "We have two departments!",
                    :buttons
                    [{:url "https://www.facebook.com/Juji-AI-Chatbot-Demo-109315067094969",
                      :title "Books"}
                     {:url "https://en.wikipedia.org/wiki/Game",
                      :title "Games"}],
                    :subtitle "Please feel free to look around.",
                    :image-url "https://upload.wikimedia.org/wikipedia/commons/4/45/ChristmasMarketJena.jpg"}],
        :template-type "generic",
        :sub-type "facebook-media",
        :id 1},
 2 {:description "Display a web media form",
        :name "T2",
        :settings {:delay-start 0},
        :type "remark",
        :topic "juji.topics.interviewing.v4/web-media",
        :elements [{:link {:url "https://www.facebook.com/Juji-AI-Chatbot-Demo-109315067094969", :text "Books"},
                    :text "Or you can take a look at web media:",
                    :image-url "https://upload.wikimedia.org/wikipedia/commons/4/45/ChristmasMarketJena.jpg"}],
        :sub-type "web-media",
        :id 2}
 3 {:id 3,
	    :name "T3",
	    :type "remark",
	    :topic "juji.topics.interviewing.v4/display-personalized-message",
	    :traits [{:code "co400",
	               :name "smart shopper",
	               :skip false,
	               :message ["From your chat, you seem analytical and smart. You'd appreciate our product, which is backed by years of research and testing."],
	               :description "who are analytical and make informed economic decisions"}
	              {:code "co500",
	               :name "DIYer",
	               :skip false,
	               :message ["You seem a very capable individual and values the quality of a product. Check out ours that provides a high value and durability."],
	               :description "who are anti-materialistic and shop for value, durability, and comfort"}
	              {:code "co300",
	               :name "explorer",
	               :skip false,
	               :message ["From our chat, you seem very open-minded and having a unique taste. Check out our product for a fresh and unique experience."],
	               :description "who emphasize identity and enjoy new and unique experiences"}
	              {:code "co200",
	               :name "achiever",
	               :skip false,
	               :message ["You seem goal-oriented. Here are the product reviews that may help you evaluate how our product meets your needs."],
	               :description "who are goal-oriented and make economic decisions based on the needs of career and family"}
	              {:code "co100",
	               :name "sophisticated shopper",
	               :skip false,
	               :message ["You have a sophisticated taste and love finer things. We have an authentic product that will meet your standard."],
	               :description "who are successful and have a sophisticated taste"}
	              {:code "co600",
	               :name "value shopper",
	               :skip false,
	               :message ["From our chat, you seem a thoughtful person and stressing the real value of a product. Here are the reviews that would probably help you evaluate the value of our product."],
	               :description "who are cautious and prefer big, well-known brands"}
	              {:code "co700",
	               :name "aspiring shopper",
	               :skip false,
	               :message ["You seem loving fun and trendy stuff. What would be better to experience our fun product with style?"],
	               :description "who enjoy shopping as social activities, and love fun and trendy stuff"}],
	     :settings {:delay-start 0},
	     :sub-type "shopper-dna",
	     :description "Display a personalized plain text message"}
 4 {:description "Says goodbye and ends the chat",
        :category "General chitchat",
        :content ["`(user-first-name)`, thank you again for chatting w/ me! You can sign up to create your own version of me: https://juji.ai/signup. \n See u later!"],
        :cid "juji.topics.interviewing.v4/final-closing-leave",
        :name "Wrap-up",
        :end-type "regular",
        :settings {:delay-start 0},
        :type "remark",
        :topic "juji.topics.interviewing.v4/final-closing-leave",
        :sub-type "plain-text",
        :label "Chatbot says good bye",
        :id 4,
        :end true},

 ;; request items
 5 {:description "Ask how a user is doing",
        :category "General chitchat",
        :content [{:text "How are you doing?", :repeatable true}],
        :cid "juji.topics.interviewing.v4/ask-how-are-you-doing",
        :name "T5",
        :settings {:required true,
	                    :delay-start 0,
	                    :min-input-len 5,
	                    :allow-i-dont-know false,
	                    :gibberish-detection true},
        :type "request",
        :topic "juji.topics.interviewing.v4/ask-how-are-you-doing",
        :actions [],
        :sub-type "free-text",
        :label "How are you doing?",
        :id 5}
 6 {:description "Collect user input in a GUI",
        :scale "nominal",
        :content [{:text "What game do you play the most?"}],
        :name "T6",
        :settings {:required true, :delay-start 0},
        :type "request",
        :topic "juji.topics.interviewing.v4/collect-basic-info-from-gui-w-attribute",
        :choices [{:text "MHW", :value 0}
                  {:text "The Witcher", :value 1}],
        :actions [],
        :sub-type "single-choice",
        :label "What game do you play the most?",
        :id 6,
        :precondition [{:operand {:name 7,
                                  :trigger "trigger-1",
                                  :operator "triggered-by",
                                  :predicate-type "topic-specific"},
                        :operator "no-op",
                        :predicate-type "composite"}]}
 7 {:description "Collect user input in a GUI",
        :name "T7",
        :trigger-counter 3,
        :settings {:required true, :delay-start 0},
        :type "request",
        :topic "juji.topics.interviewing.v4/collect-basic-info-from-gui-w-attribute",
        :choices [{:text "Buy a product", :value 0}
                  {:text "See new collections", :value 1}
                  {:text "Pricing", :value 2}],
        :actions [{:trigger {:name "trigger-1",
                             :operands [{:operand {:value 1,
                                                   :operator "choice-is",
                                                   :operand-name "operand-1"},
                                         :operator "no-op"}],
                             :operator "and"},
                   :followups [6],
                   :quick-ack "Let me as you a quick question."}
                  {:trigger {:name "trigger-2",
                             :operands [{:operand {:value 2,
                                                   :operator "choice-is",
                                                   :operand-name "operand-1"},
                                         :operator "no-op"}],
                             :operator "and"},
                   :advanced {:jump true, :jump-to-topic 9},
                   :quick-ack "Books are $2 each; games are $5 each"}],
        :elements [{:title "What are you looking for?",
                    :buttons [{:type "postback",
                               :title "Buy a product",
                               :payload "0"}
                              {:type "postback",
                               :title "See new collections",
                               :payload "1"}
                              {:type "postback",
                               :title "Pricing",
                               :payload "2"}],
                    :subtitle "",
                    :image-url ""}],
        :template-type "generic",
        :sub-type "facebook-choice",
        :label "What are you looking for?",
        :id 7}
 8 {:description "Ask a yes-no question",
        :content [{:text "Do you have a coupon?"}],
        :name "T8",
        :settings {:required true, :delay-start 0},
        :type "request",
        :topic "juji.topics.interviewing.v4/ask-general-question-yes-no",
        :actions [],
        :sub-type "yes-or-no",
        :label "Do you have a coupon?",
        :id 8}
 9 {:description "Collect opt-in Facebook email",
        :content [{:text "Please click on the email to confirm.",
                   :repeatable true}],
        :name "T9",
        :settings {:required true, :delay-start 0},
        :type "request",
        :topic "juji.topics.interviewing.v4/collect-fb-email",
        :actions [],
        :sub-type "fb-email",
        :label "Collecting Facebook email",
        :id 9}
}
```

As shown in the example, each item in the items map is represented by another map. There are two types of item: "remark" and "request". When a chatbot is on a **remark** item, it typically presents the message and move on. In contrast, if a chatbot is on a **request** item, it does not only present the message, it also expects the user to respond to it. Thus, a request item would contain information on how to handle user's response. 

Each type has multiple sub-types. They are used in different situations and their fields are not entirely the same. A remark item can have the following sub-types:

* plain-text: It is used for a plain text message. When the item is presented in a Juji web release, it also support html tags.
* facebook-media: It is used for displaying a [facebook generic template](https://developers.facebook.com/docs/messenger-platform/send-messages/template/generic). When the item is presented in a Juji web release, the facebook template will be summarized in a plain text message.
* web-media: It is used for displaying a web template. The image in the template does not work in a facebook messenger.
* shopper-dna: It presents plain text messages conditioned on the current user's shopper personality.
* career-dna: It presents plain text messages conditioned on the current user's overall personality.

A request item can have the following sub-types:

* free-text: It is used for a plain text question.
* single-choice: It is used for a radio button choice question.
* multiple-choice: It is used for a check-box choice question.
* fb-email: It is used for asking email confirmation on facebook.
* facebook-choice: It is used for displaying a [facebook generic template](https://developers.facebook.com/docs/messenger-platform/send-messages/template/generic) as a choice question, such that the user's response will be processed for further actions.
* yes-or-no: It is used for a plain text yes or no question.

Most item fields are shared across sub-types. However, some fields are unique to certain sub-types. The item examples above include most of the sub-types. Thus, designers can refer to them when they are in doubt about which fields are needed for a given sub-type. The main fields are described below:

* description: Its value is a string description of the item.
* category: Its value is a string description of the category of the message the item contains.
* content: Its value is a vector that contains one or more utterances. The vector contains strings when the item has "remark" type and it contains maps of the format `{:text "question wording" :repeatable true/false}` when the item has "request" type. One exception is that when the item has the "facebook-media" sub-type, the content field is not used.
* elements: Its value is a vector that contains one or more maps representing a fecebook generic template's elements or a web media's elements.
* choices: Its value is a vector that contains one or more maps representing the choice options of a "single-choice", "multiple-choice" or "facebook-choice" question.
* name: Its value is a string name of the item.
* settings: Its value is a map representing the item settings. A remark item only has one parameter in the settings - delay-start, whereas a request item can have up to five parameters:
    * required: Its value is a boolean, if true, the user cannot skip this question.
    * delay-start: Its value is an integer indicating a delay in seconds before the message is presented to the user.
    * min-input-len: Its value is an integer. It has the same effect as thin-text-threshold in the overall config-doc settings except min-input-len only affects the current item.
    * allow-i-dont-know: Its value is a boolean, if false, when user say "I don't know" or similar expression the chatbot will not accept it as an valid answer and it will try to ask for a more definite answer.
    * gibberish-detection: Its value is a boolean, if true, user's input will be checked against an gibberish detector. If the input is classified as gibberish, the chatbot will try to ask for a different answer. We would suggest designers to put this to false if the item is asking about names, especially a foreign person's name, a company's name or names that can be arbitrary.
* type: Its value is a string indicating the type of the item. Two types are supported: "remark" and "request".
* sub-type: Its value is a string indicating the sub-type of the item. 
* topic: Its value is a string of a library or customized topic name with its namespace. Currently, only the "free-text" sub-type item supports a variety of topics. Items of other sub-types have their designated topics that should not be changed. Please refer to [built-in library topics](topics.md) if you would like to choose a built-in topic.
* label: Its value is a string summarizing what the item is asking. Only a request item uses this field. Its value is also used for identifying questions in chat reports and automatically matching a topic to a "free-text" sub-type item in Juji Studio.
* actions: Its value is a vector that contains one or more maps representing [customized actions](design.md#customizing-chatbot-actions). Customized actions can be used to define specific responses to different user answers, store attributes and dynamically change the chatflow.
* precondition: Its value is a vector that contains one or more maps representing preconditions. Only when the preconditions are satisfied, the item would be presented by the chatbot. This can be used to dynamically control the chatflow base on the user's attributes or/and the current context.
* id: Its value is an integer that is the id of this item.
* end: Its value is a boolean signaling whether this item will end the chat.

## agenda

The `:agenda` field lists out the item ids in certain order in a vector. Only the items in the vector will be presented by the chatbot. Here's an example:
```clojure
[0 5 1 2 7 8 6 9 3 4]
```
Chatbot will also follow the same order to present the items. However, designers can use jump and precondition to link one item to another. In the agenda and items example, item 7 is succeed by item 8 according to the agenda. But if the user chooses the "Pricing" option for item 7, the chatbot will jump to item 9 according to the second customized action. Below is a visualization of such chatflow.

<p align="center"><img src="../img/chatflow-with-jump.png" alt="Visualization of chatflow that includes an item with jump action" width="650px"/></p>

## version

The `:version` field indicates the version of the config-doc. Its value is a string. Currently, only the following versions are supported `"3.0.0"`, `"3.0.1"`, `"3.0.2"`, `"3.0.3"` and `"3.0.4"`. When in doubt, just use the latest version i.e., `"3.0.4"`.

## faq

The `:faq` field specifies the Q&A data the chatbot will use for question answering. Its value is a vector that contains indicies of Q&A data. Currently, only one index is supported. However, the index can contain thousands of questions and answers. By default, the index is the uuid of the engagement in string e.g, `"5edeb5f9-63d9-4467-a82e-2c2d6cb337bc"`. 

If you are copying or uploading a config-doc from somewhere else, remember to update the faq index. One way to find the uuid is by going into the IDE Config page of the engagement of choice, the uuid can then be found in its url.

## Put Everything Together

Combine all the examples from the different fields, we will get a working config-doc. A designer can do the following to validate the config-doc:

1. paste this to the Config of the engagement of choice in the IDE;
2. update faq index;
3. save the Config by click on "Save" (this also automatically sync Juji Studio with the new Config);
4. click on "Generate Script" to generate an "Preview";
5. navigate to the preview script in the IDE and click "Preview" to preview the chat.

```clojure
{:faq ["your-engagement-uuid-string"],
 :items {0 {:description "Display a plain text message",
            :category "Provide user with information in general",
            :content ["Hello, `(user-first-name)`, thanks for connecting! I am your AI helper and cannot wait to chat w/ you."],
            :cid "juji.topics.interviewing.v4/rep-tell",
            :name "Welcome",
            :settings {:delay-start 0},
            :type "remark",
            :topic "juji.topics.interviewing.v4/rep-tell",
            :sub-type "plain-text",
            :id 0},
         7 {:description "Collect user input in a GUI",
            :name "T7",
            :trigger-counter 3,
            :settings {:required true, :delay-start 0},
            :type "request",
            :topic "juji.topics.interviewing.v4/collect-basic-info-from-gui-w-attribute",
            :choices [{:text "Buy a product", :value 0}
                      {:text "See new collections", :value 1}
                      {:text "Pricing", :value 2}],
            :actions [{:trigger {:name "trigger-1",
                                 :operands [{:operand {:value 1,
                                                       :operator "choice-is",
                                                       :operand-name "operand-1"},
                                             :operator "no-op"}],
                                 :operator "and"},
                       :followups [6],
                       :quick-ack "Let me as you a quick question."}
                      {:trigger {:name "trigger-2",
                                 :operands [{:operand {:value 2,
                                                       :operator "choice-is",
                                                       :operand-name "operand-1"},
                                             :operator "no-op"}],
                                 :operator "and"},
                       :advanced {:jump true, :jump-to-topic 9},
                       :quick-ack "Books are $2 each; games are $5 each"}],
            :elements [{:title "What are you looking for?",
                        :buttons [{:type "postback",
                                   :title "Buy a product",
                                   :payload "0"}
                                  {:type "postback",
                                   :title "See new collections",
                                   :payload "1"}
                                  {:type "postback",
                                   :title "Pricing",
                                   :payload "2"}],
                        :subtitle "",
                        :image-url ""}],
            :template-type "generic",
            :sub-type "facebook-choice",
            :label "What are you looking for?",
            :id 7},
         1 {:description "Display a facebook media form",
            :name "T1",
            :settings {:delay-start 0},
            :type "remark",
            :topic "juji.topics.interviewing.v4/display-gui",
            :elements [{:title "We have two departments!",
                        :buttons [{:url "https://www.facebook.com/Juji-AI-Chatbot-Demo-109315067094969",
                                   :title "Books"}
                                  {:url "https://en.wikipedia.org/wiki/Game",
                                   :title "Games"}],
                        :subtitle "Please feel free to look around.",
                        :image-url "https://upload.wikimedia.org/wikipedia/commons/4/45/ChristmasMarketJena.jpg"}],
            :template-type "generic",
            :sub-type "facebook-media",
            :id 1},
         4 {:description "Says goodbye and ends the chat",
            :category "General chitchat",
            :content ["`(user-first-name)`, thank you again for chatting w/ me! You can sign up to create your own version of me: https://juji.ai/signup. \n See u later!"],
            :cid "juji.topics.interviewing.v4/final-closing-leave",
            :name "Wrap-up",
            :end-type "regular",
            :settings {:delay-start 0},
            :type "remark",
            :topic "juji.topics.interviewing.v4/final-closing-leave",
            :sub-type "plain-text",
            :label "Chatbot says good bye",
            :id 4,
            :end true},
         6 {:description "Collect user input in a GUI",
            :scale "nominal",
            :content [{:text "What game do you play the most?"}],
            :name "T6",
            :settings {:required true, :delay-start 0},
            :type "request",
            :topic "juji.topics.interviewing.v4/collect-basic-info-from-gui-w-attribute",
            :choices [{:text "MHW", :value 0}
                      {:text "The Witcher", :value 1}],
            :actions [],
            :sub-type "single-choice",
            :label "What game do you play the most?",
            :id 6,
            :precondition [{:operand {:name 7,
                                      :trigger "trigger-1",
                                      :operator "triggered-by",
                                      :predicate-type "topic-specific"},
                            :operator "no-op",
                            :predicate-type "composite"}]},
         3 {:id 3,
            :name "T3",
            :type "remark",
            :topic "juji.topics.interviewing.v4/display-personalized-message",
            :traits [{:code "co400",
                      :name "smart shopper",
                      :skip false,
                      :message ["From your chat, you seem analytical and smart. You'd appreciate our product, which is backed by years of research and testing."],
                      :description "who are analytical and make informed economic decisions"}
                     {:code "co500",
                      :name "DIYer",
                      :skip false,
                      :message ["You seem a very capable individual and values the quality of a product. Check out ours that provides a high value and durability."],
                      :description "who are anti-materialistic and shop for value, durability, and comfort"}
                     {:code "co300",
                      :name "explorer",
                      :skip false,
                      :message ["From our chat, you seem very open-minded and having a unique taste. Check out our product for a fresh and unique experience."],
                      :description "who emphasize identity and enjoy new and unique experiences"}
                     {:code "co200",
                      :name "achiever",
                      :skip false,
                      :message ["You seem goal-oriented. Here are the product reviews that may help you evaluate how our product meets your needs."],
                      :description "who are goal-oriented and make economic decisions based on the needs of career and family"}
                     {:code "co100",
                      :name "sophisticated shopper",
                      :skip false,
                      :message ["You have a sophisticated taste and love finer things. We have an authentic product that will meet your standard."],
                      :description "who are successful and have a sophisticated taste"}
                     {:code "co600",
                      :name "value shopper",
                      :skip false,
                      :message ["From our chat, you seem a thoughtful person and stressing the real value of a product. Here are the reviews that would probably help you evaluate the value of our product."],
                      :description "who are cautious and prefer big, well-known brands"}
                     {:code "co700",
                      :name "aspiring shopper",
                      :skip false,
                      :message ["You seem loving fun and trendy stuff. What would be better to experience our fun product with style?"],
                      :description "who enjoy shopping as social activities, and love fun and trendy stuff"}],
            :settings {:delay-start 0},
            :sub-type "shopper-dna",
            :description "Display a personalized plain text message"},
         2 {:id 2,
            :name "T2",
            :type "remark",
            :topic "juji.topics.interviewing.v4/web-media",
            :elements [{:link {:url "https://www.facebook.com/Juji-AI-Chatbot-Demo-109315067094969",
                               :text "Books"},
                        :text "Or you can take a look at web media:",
                        :image-url "https://upload.wikimedia.org/wikipedia/commons/4/45/ChristmasMarketJena.jpg"}],
            :settings {:delay-start 0},
            :sub-type "web-media",
            :description "Display a web media form"},
         9 {:description "Collect opt-in Facebook email",
            :content [{:text "Please click on the email to confirm.",
                       :repeatable true}],
            :name "T9",
            :settings {:required true, :delay-start 0},
            :type "request",
            :topic "juji.topics.interviewing.v4/collect-fb-email",
            :actions [],
            :sub-type "fb-email",
            :label "Collecting Facebook email",
            :id 9},
         5 {:description "Ask how a user is doing",
            :category "General chitchat",
            :content [{:text "How are you doing?", :repeatable true}],
            :cid "juji.topics.interviewing.v4/ask-how-are-you-doing",
            :name "T5",
            :settings {:required true,
                       :delay-start 0,
                       :min-input-len 5,
                       :allow-i-dont-know false,
                       :gibberish-detection true},
            :type "request",
            :topic "juji.topics.interviewing.v4/ask-how-are-you-doing",
            :actions [],
            :sub-type "free-text",
            :label "How are you doing?",
            :id 5},
         8 {:description "Ask a yes-no question",
            :content [{:text "Do you have a coupon?"}],
            :name "T8",
            :settings {:required true, :delay-start 0},
            :type "request",
            :topic "juji.topics.interviewing.v4/ask-general-question-yes-no",
            :actions [],
            :sub-type "yes-or-no",
            :label "Do you have a coupon?",
            :id 8}},
 :agenda [0 5 1 2 7 8 6 9 3 4],
 :version "3.0.4",
 :requires "[[juji.topics.fallback.chatflow.v1 :as fallback.chatflow] [juji.topics.fallback.exception.v1 :as fallback.exception] [juji.topics.fallback.qa.v1 :as fallback.qa] [juji.topics.fallback.request.v1 :as fallback.request] [juji.topics.fallback.social.v2 :as fallback.social] [juji.topics.interviewing.v4 :as interviewing] [juji.concept.basic :as concept] [juji.expressions.rep.basic :as rep]]",
 :settings {:default-response-to-question "",
            :thin-text-threshold 5,
            :ad-lib [{:cid "juji.topics.fallback.chatflow.v1/handle-missed-user-answers",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.chatflow.v1/handle-missed-user-answers",
                      :description "Handles a chatbot missed user answers"}
                     {:cid "juji.topics.fallback.chatflow.v1/handle-user-excuses",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.chatflow.v1/handle-user-excuses",
                      :description "Handles a user's various \"excuses\" not answering a question"}
                     {:cid "juji.topics.fallback.chatflow.v1/handle-chat-flow",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.chatflow.v1/handle-chat-flow",
                      :description "Handles a user' input regarding the chat flow."}
                     {:cid "juji.topics.fallback.chatflow.v1/handle-skip",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.chatflow.v1/handle-skip",
                      :description "Handles a user's request to skip certain parts of a chat"}
                     {:cid "juji.topics.fallback.request.v1/handle-user-requests",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.request.v1/handle-user-requests",
                      :description "Handle a user's requests during a chat"}
                     {:cid "juji.topics.fallback.social.v2/echo-user-input",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.social.v2/echo-user-input",
                      :description "Handles users' chitchat input"}
                     {:cid "juji.topics.fallback.qa.v1/handle-user-questions-engagement",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.qa.v1/handle-user-questions-engagement",
                      :description "Answer a user's questions about the chat"}
                     {:cid "juji.topics.fallback.qa.v1/handle-user-questions-rep",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.qa.v1/handle-user-questions-rep",
                      :description "Answer a user's questions about the chatbot"}
                     {:cid "juji.topics.fallback.qa.v1/handle-user-questions-juji",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.qa.v1/handle-user-questions-juji",
                      :description "Answer a user's questions regarding Juji"}
                     {:cid "juji.topics.fallback.qa.v1/handle-user-questions-general",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.qa.v1/handle-user-questions-general",
                      :description "Answer a user's general questions"}
                     {:cid "juji.topics.fallback.chatflow.v1/handle-user-clarification",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.chatflow.v1/handle-user-clarification",
                      :description "Respond to a user's request for clarification"}
                     {:cid "juji.topics.fallback.chatflow.v1/handle-no-knowledge",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.chatflow.v1/handle-no-knowledge",
                      :description "Handles when a user claims that s/he has not knowledge"}
                     {:cid "juji.topics.fallback.social.v2/comment-user-input",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.social.v2/comment-user-input",
                      :description "Comment on a user's input"}
                     {:cid "juji.topics.fallback.exception.v1/handle-user-questions-not-answered",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.exception.v1/handle-user-questions-not-answered",
                      :needed true,
                      :parameters [{:name "default-response-to-question",
                                    :value-path ["settings"
                                                 "default-response-to-question"]}],
                      :description "Handles user questions that a chatbot cannot answer"}
                     {:cid "juji.topics.fallback.exception.v1/handle-gibberish",
                      :skip false,
                      :type "fallback",
                      :topic "juji.topics.fallback.exception.v1/handle-gibberish",
                      :description "Handle a user's gibberish input"}],
            :turn-pace 0,
            :persona {:cid "juji",
                      :name "Juji",
                      :background "#8BDFCD",
                      :bio "Hi, I'm Juji, the quintessential default REP. I'm known for my winning personality and great sense of humor.",
                      :info "neutral stock persona",
                      :image-lg "/assets/img/content/juji-chat-profile-lg.png",
                      :personality "default",
                      :image "/assets/img/content/juji-profile.png",
                      :image-sm "/assets/img/content/juji-chat-profile-sm.png"},
            :between-response-delay 1500,
            :session-duration-max 60,
            :translations [{:cid "juji.topics.fallback.qa.v1/translate-how-about-you",
                            :skip false,
                            :type "fallback",
                            :topic "juji.topics.fallback.qa.v1/translate-how-about-you",
                            :description "Handles a user's reciprocal question to the chatbot"}],
            :task-completion-code false}}

```

## JSON Example

Below is the same example in JSON format.

```javascript
{"faq" ["your-engagement-uuid-string"],
 "items"
 {"9"
  {"sub-type" "fb-email",
   "settings" {"required" true, "delay-start" 0},
   "label" "Collecting Facebook email",
   "id" 9,
   "name" "T9",
   "content"
   [{"text" "Please click on the email to confirm.", "repeatable" true}],
   "type" "request",
   "description" "Collect opt-in Facebook email",
   "actions" [],
   "topic" "juji.topics.interviewing.v4/collect-fb-email"},
  "3"
  {"id" 3,
   "name" "T3",
   "type" "remark",
   "topic" "juji.topics.interviewing.v4/display-personalized-message",
   "traits"
   [{"code" "co400",
     "name" "smart shopper",
     "skip" false,
     "message"
     ["From your chat, you seem analytical and smart. You'd appreciate our product, which is backed by years of research and testing."],
     "description" "who are analytical and make informed economic decisions"}
    {"code" "co500",
     "name" "DIYer",
     "skip" false,
     "message"
     ["You seem a very capable individual and values the quality of a product. Check out ours that provides a high value and durability."],
     "description"
     "who are anti-materialistic and shop for value, durability, and comfort"}
    {"code" "co300",
     "name" "explorer",
     "skip" false,
     "message"
     ["From our chat, you seem very open-minded and having a unique taste. Check out our product for a fresh and unique experience."],
     "description"
     "who emphasize identity and enjoy new and unique experiences"}
    {"code" "co200",
     "name" "achiever",
     "skip" false,
     "message"
     ["You seem goal-oriented. Here are the product reviews that may help you evaluate how our product meets your needs."],
     "description"
     "who are goal-oriented and make economic decisions based on the needs of career and family"}
    {"code" "co100",
     "name" "sophisticated shopper",
     "skip" false,
     "message"
     ["You have a sophisticated taste and love finer things. We have an authentic product that will meet your standard."],
     "description" "who are successful and have a sophisticated taste"}
    {"code" "co600",
     "name" "value shopper",
     "skip" false,
     "message"
     ["From our chat, you seem a thoughtful person and stressing the real value of a product. Here are the reviews that would probably help you evaluate the value of our product."],
     "description" "who are cautious and prefer big, well-known brands"}
    {"code" "co700",
     "name" "aspiring shopper",
     "skip" false,
     "message"
     ["You seem loving fun and trendy stuff. What would be better to experience our fun product with style?"],
     "description"
     "who enjoy shopping as social activities, and love fun and trendy stuff"}],
   "settings" {"delay-start" 0},
   "sub-type" "shopper-dna",
   "description" "Display a personalized plain text message"},
  "4"
  {"sub-type" "plain-text",
   "settings" {"delay-start" 0},
   "label" "Chatbot says good bye",
   "end-type" "regular",
   "id" 4,
   "name" "Wrap-up",
   "content"
   ["`(user-first-name)`, thank you again for chatting w/ me! You can sign up to create your own version of me: https://juji.ai/signup. \n See u later!"],
   "type" "remark",
   "cid" "juji.topics.interviewing.v4/final-closing-leave",
   "category" "General chitchat",
   "end" true,
   "description" "Says goodbye and ends the chat",
   "topic" "juji.topics.interviewing.v4/final-closing-leave"},
  "8"
  {"sub-type" "yes-or-no",
   "settings" {"required" true, "delay-start" 0},
   "label" "Do you have a coupon?",
   "id" 8,
   "name" "T8",
   "content" [{"text" "Do you have a coupon?"}],
   "type" "request",
   "description" "Ask a yes-no question",
   "actions" [],
   "topic" "juji.topics.interviewing.v4/ask-general-question-yes-no"},
  "7"
  {"template-type" "generic",
   "sub-type" "facebook-choice",
   "settings" {"required" true, "delay-start" 0},
   "trigger-counter" 3,
   "label" "What are you looking for?",
   "id" 7,
   "name" "T7",
   "choices"
   [{"text" "Buy a product", "value" 0}
    {"text" "See new collections", "value" 1}
    {"text" "Pricing", "value" 2}],
   "type" "request",
   "elements"
   [{"title" "What are you looking for?",
     "buttons"
     [{"type" "postback", "title" "Buy a product", "payload" "0"}
      {"type" "postback", "title" "See new collections", "payload" "1"}
      {"type" "postback", "title" "Pricing", "payload" "2"}],
     "subtitle" "",
     "image-url" ""}],
   "description" "Collect user input in a GUI",
   "actions"
   [{"trigger"
     {"name" "trigger-1",
      "operands"
      [{"operand"
        {"value" 1, "operator" "choice-is", "operand-name" "operand-1"},
        "operator" "no-op"}],
      "operator" "and"},
     "followups" [6],
     "quick-ack" "Let me as you a quick question."}
    {"trigger"
     {"name" "trigger-2",
      "operands"
      [{"operand"
        {"value" 2, "operator" "choice-is", "operand-name" "operand-1"},
        "operator" "no-op"}],
      "operator" "and"},
     "advanced" {"jump" true, "jump-to-topic" 9},
     "quick-ack" "Books are $2 each; games are $5 each"}],
   "topic"
   "juji.topics.interviewing.v4/collect-basic-info-from-gui-w-attribute"},
  "5"
  {"sub-type" "free-text",
   "settings"
   {"required" true,
    "delay-start" 0,
    "min-input-len" 5,
    "allow-i-dont-know" false,
    "gibberish-detection" true},
   "label" "How are you doing?",
   "id" 5,
   "name" "T5",
   "content" [{"text" "How are you doing?", "repeatable" true}],
   "type" "request",
   "cid" "juji.topics.interviewing.v4/ask-how-are-you-doing",
   "category" "General chitchat",
   "description" "Ask how a user is doing",
   "actions" [],
   "topic" "juji.topics.interviewing.v4/ask-how-are-you-doing"},
  "6"
  {"sub-type" "single-choice",
   "scale" "nominal",
   "settings" {"required" true, "delay-start" 0},
   "label" "What game do you play the most?",
   "id" 6,
   "name" "T6",
   "content" [{"text" "What game do you play the most?"}],
   "choices" [{"text" "MHW", "value" 0} {"text" "The Witcher", "value" 1}],
   "type" "request",
   "precondition"
   [{"operand"
     {"name" 7,
      "trigger" "trigger-1",
      "operator" "triggered-by",
      "predicate-type" "topic-specific"},
     "operator" "no-op",
     "predicate-type" "composite"}],
   "description" "Collect user input in a GUI",
   "actions" [],
   "topic"
   "juji.topics.interviewing.v4/collect-basic-info-from-gui-w-attribute"},
  "1"
  {"template-type" "generic",
   "sub-type" "facebook-media",
   "settings" {"delay-start" 0},
   "id" 1,
   "name" "T1",
   "type" "remark",
   "elements"
   [{"title" "We have two departments!",
     "buttons"
     [{"url" "https://www.facebook.com/Juji-AI-Chatbot-Demo-109315067094969",
       "title" "Books"}
      {"url" "https://en.wikipedia.org/wiki/Game", "title" "Games"}],
     "subtitle" "Please feel free to look around.",
     "image-url"
     "https://upload.wikimedia.org/wikipedia/commons/4/45/ChristmasMarketJena.jpg"}],
   "description" "Display a facebook media form",
   "topic" "juji.topics.interviewing.v4/display-gui"},
  "0"
  {"sub-type" "plain-text",
   "settings" {"delay-start" 0},
   "id" 0,
   "name" "Welcome",
   "content"
   ["Hello, `(user-first-name)`, thanks for connecting! I am your AI helper and cannot wait to chat w/ you."],
   "type" "remark",
   "cid" "juji.topics.interviewing.v4/rep-tell",
   "category" "Provide user with information in general",
   "description" "Display a plain text message",
   "topic" "juji.topics.interviewing.v4/rep-tell"},
  "2"
  {"id" 2,
   "name" "T2",
   "type" "remark",
   "topic" "juji.topics.interviewing.v4/web-media",
   "elements"
   [{"link"
     {"url" "https://www.facebook.com/Juji-AI-Chatbot-Demo-109315067094969",
      "text" "Books"},
     "text" "Or you can take a look at web media:",
     "image-url"
     "https://upload.wikimedia.org/wikipedia/commons/4/45/ChristmasMarketJena.jpg"}],
   "settings" {"delay-start" 0},
   "sub-type" "web-media",
   "description" "Display a web media form"}},
 "agenda" [0 5 1 2 7 8 6 9 3 4],
 "version" "3.0.4",
 "requires"
 "[[juji.topics.fallback.chatflow.v1 :as fallback.chatflow] [juji.topics.fallback.exception.v1 :as fallback.exception] [juji.topics.fallback.qa.v1 :as fallback.qa] [juji.topics.fallback.request.v1 :as fallback.request] [juji.topics.fallback.social.v2 :as fallback.social] [juji.topics.interviewing.v4 :as interviewing] [juji.concept.basic :as concept] [juji.expressions.rep.basic :as rep]]",
 "settings"
 {"thin-text-threshold" 5,
  "translations"
  [{"cid" "juji.topics.fallback.qa.v1/translate-how-about-you",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.qa.v1/translate-how-about-you",
    "description" "Handles a user's reciprocal question to the chatbot"}],
  "task-completion-code" false,
  "between-response-delay" 1500,
  "session-duration-max" 60,
  "turn-pace" 0,
  "ad-lib"
  [{"cid" "juji.topics.fallback.chatflow.v1/handle-missed-user-answers",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.chatflow.v1/handle-missed-user-answers",
    "description" "Handles a chatbot missed user answers"}
   {"cid" "juji.topics.fallback.chatflow.v1/handle-user-excuses",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.chatflow.v1/handle-user-excuses",
    "description"
    "Handles a user's various \"excuses\" not answering a question"}
   {"cid" "juji.topics.fallback.chatflow.v1/handle-chat-flow",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.chatflow.v1/handle-chat-flow",
    "description" "Handles a user' input regarding the chat flow."}
   {"cid" "juji.topics.fallback.chatflow.v1/handle-skip",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.chatflow.v1/handle-skip",
    "description" "Handles a user's request to skip certain parts of a chat"}
   {"cid" "juji.topics.fallback.request.v1/handle-user-requests",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.request.v1/handle-user-requests",
    "description" "Handle a user's requests during a chat"}
   {"cid" "juji.topics.fallback.social.v2/echo-user-input",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.social.v2/echo-user-input",
    "description" "Handles users' chitchat input"}
   {"cid" "juji.topics.fallback.qa.v1/handle-user-questions-engagement",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.qa.v1/handle-user-questions-engagement",
    "description" "Answer a user's questions about the chat"}
   {"cid" "juji.topics.fallback.qa.v1/handle-user-questions-rep",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.qa.v1/handle-user-questions-rep",
    "description" "Answer a user's questions about the chatbot"}
   {"cid" "juji.topics.fallback.qa.v1/handle-user-questions-juji",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.qa.v1/handle-user-questions-juji",
    "description" "Answer a user's questions regarding Juji"}
   {"cid" "juji.topics.fallback.qa.v1/handle-user-questions-general",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.qa.v1/handle-user-questions-general",
    "description" "Answer a user's general questions"}
   {"cid" "juji.topics.fallback.chatflow.v1/handle-user-clarification",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.chatflow.v1/handle-user-clarification",
    "description" "Respond to a user's request for clarification"}
   {"cid" "juji.topics.fallback.chatflow.v1/handle-no-knowledge",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.chatflow.v1/handle-no-knowledge",
    "description" "Handles when a user claims that s/he has not knowledge"}
   {"cid" "juji.topics.fallback.social.v2/comment-user-input",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.social.v2/comment-user-input",
    "description" "Comment on a user's input"}
   {"cid"
    "juji.topics.fallback.exception.v1/handle-user-questions-not-answered",
    "skip" false,
    "type" "fallback",
    "topic"
    "juji.topics.fallback.exception.v1/handle-user-questions-not-answered",
    "needed" true,
    "parameters"
    [{"name" "default-response-to-question",
      "value-path" ["settings" "default-response-to-question"]}],
    "description" "Handles user questions that a chatbot cannot answer"}
   {"cid" "juji.topics.fallback.exception.v1/handle-gibberish",
    "skip" false,
    "type" "fallback",
    "topic" "juji.topics.fallback.exception.v1/handle-gibberish",
    "description" "Handle a user's gibberish input"}],
  "default-response-to-question" "",
  "persona"
  {"personality" "default",
   "bio"
   "Hi, I'm Juji, the quintessential default REP. I'm known for my winning personality and great sense of humor.",
   "image" "/assets/img/content/juji-profile.png",
   "info" "neutral stock persona",
   "name" "Juji",
   "image-sm" "/assets/img/content/juji-chat-profile-sm.png",
   "cid" "juji",
   "image-lg" "/assets/img/content/juji-chat-profile-lg.png",
   "background" "#8BDFCD"}}}
```