# 本リポジトリの概要
本リポジトリは以下リポジトリをベースとして作成している。  
https://github.com/howdyai/botkit.git

legacyブランチの以下バージョンで動作確認済み

| Date       | コミットID                                     |
|------------|--------------------------------------------|
| 2020/12/02 | `8e91473651276f28bb72715295b19a3f07dc09da` |


# 新規追加ファイル
- [anonymous_bot.js](anonymous_bot.js)・・・実行中、ユーザは指定のチャンネルで匿名での投稿をすることができる
  - 前準備　　：
    - （作成者側の動き）コード本文に`トークン`、`チャンネルID`の設定ができていること
    - （作成者側の動き）Slackアプリ側で`anonymous`をAppとして追加できていること
      - 以下URLにアクセスし、作成する（このさい、Tokenを記録しておくこと）
        - https://my.slack.com/services/new/bot
      - 以下サイトの手順1～3あたりを参考
        - https://qiita.com/prime300th/items/a2fcdbccd42804153ff5
    - （ユーザごとの動き）Appの追加でBotを追加する
  - 実行方法：`node anonymous_bot.js`
  - 投稿方法：App->anonymousに対してメッセージを送信する
  - 注意点　：直接対象のチャンネルに投稿しても匿名化されない


# Botkit Legacy Version

This is the maintenance branch for the legacy version of Botkit (< 0.7.4).

Only security and bug fix updates will be made to this branch!

## New Project?

If you are starting a new project, use the [4+ version found here](https://github.com/howdyai/botkit).

### **Start from Scratch**

You can also add Botkit into an existing Node application.

First, add it to your project:

```
npm install --save botkit@0.7.4
```

Then, add Botkit to your application code:

```
var Botkit = require('botkit');

var controller = Botkit.anywhere(configuration);

controller.hears('hello','direct_message', function(bot, message) {
    bot.reply(message,'Hello yourself!');
});
```

[Review the documentation](https://botkit.ai/docs/v0) to learn how to configure Botkit's controller to work with the messaging platform of your choice.

## Build Your Bot

The goal of Botkit is to make it easier and more fun to build software that talks and works like a robot! Building a bot should feel cool, and not too technically complicated.

Botkit handles all the nitty gritty details like
API calls, session management and authentication,
allowing you to focus on building COOL FEATURES for your
bot using middleware and event handlers.

The toolkit is designed to provide meaningful building blocks for creating conversational user interfaces - with functions like `hears()`, `ask()`, and `reply()` that do what they say they do.

### Hearing Keywords

Most bots do their thing by listening for keywords, phrases or patterns in messages from users. Botkit has a special event handler called `hears()` that makes it easy to configure your bot to listen for this type of trigger.

```
controller.hears(['string','pattern .*',new RegExp('.*','i')],'message_received,other_event',function(bot, message) {

  // do something!
  bot.reply(message, 'I heard a message.')

});
```

[Read more about hearing things &rsaquo;](https://botkit.ai/docs/v0/core.html#matching-patterns-and-keywords-with-hears)

### Responding to Events

Bots can respond to non-verbal events as well, like when a new user joins a channel, a file gets uploaded, or a button gets clicked. These events are handled using an event handling pattern that should look familiar. Most events in Botkit can be replied to like normal messages.

```
controller.on('channel_join', function(bot, message) {

  bot.reply(message,'Welcome to the channel!');

});
```

[See a full list of events and more information about handling them &rsaquo;](https://botkit.ai/docs/v0/core.html#receiving-messages-and-events)

### Middleware

In addition to taking direct action in response to a certain message or type of event, Botkit can also take passive action on messages as they move through the application using middlewares. Middleware functions work by changing messages, adding new fields, firing alternate events, and modifying or overriding the behavior of Botkit's core features.

Middleware can be used to adjust how Botkit receives, processes, and sends messages. [Here is a list of available middleware endpoints](https://botkit.ai/docs/readme-pipeline.html).

```
// Log every message received
controller.middleware.receive.use(function(bot, message, next) {

  // log it
  console.log('RECEIVED: ', message);

  // modify the message
  message.logged = true;

  // continue processing the message
  next();

});

// Log every message sent
controller.middleware.send.use(function(bot, message, next) {

  // log it
  console.log('SENT: ', message);

  // modify the message
  message.logged = true;

  // continue processing the message
  next();

});
```
## [Change Log](https://github.com/howdyai/botkit/blob/master/changelog.md)

## Full Documentation

* [Get Started](https://botkit.ai/getstarted.html)
* [Introduction](https://botkit.ai/docs/v0)
* [Core Features](https://botkit.ai/docs/v0/core.html)
* [Botkit Studio API](https://botkit.ai/docs/v0/readme-studio.html)
* Platforms
  * [Web and Apps](https://botkit.ai/docs/v0/readme-web.html)
  * [Slack](https://botkit.ai/docs/v0/readme-slack.html)
  * [Cisco Webex](https://botkit.ai/docs/v0/readme-webex.html)
  * [Cisco Jabber](https://botkit.ai/docs/v0/readme-ciscojabber.html)
  * [Microsoft Teams](https://botkit.ai/docs/v0/readme-teams.html)
  * [Facebook Messenger](https://botkit.ai/docs/v0/readme-facebook.html)
  * [Twilio SMS](https://botkit.ai/docs/v0/readme-twiliosms.html)
  * [Twilio IPM](https://botkit.ai/docs/v0/readme-twilioipm.html)
  * [Microsoft Bot Framework](https://botkit.ai/docs/v0/readme-botframework.html)
  * [Google Hangouts Chat](https://botkit.ai/docs/v0/readme-google-hangouts.html)
* [Extending Botkit with Plugins and Middleware](https://botkit.ai/docs/v0/middleware.html)
  * [Message Pipeline](https://botkit.ai/docs/v0/readme-pipeline.html)
  * [List of current plugins](https://botkit.ai/docs/v0/readme-middlewares.html)
* [Storing Information](https://botkit.ai/docs/v0/storage.html)
* [Logging](https://botkit.ai/docs/v0/logging.html)
* Contributing to Botkit
  * [Contributing to Botkit Core](CONTRIBUTING.md)
  * [Building platform connectors](https://botkit.ai/docs/howto/build_connector.html)

## Community & Support

Join our thriving community of Botkit developers and bot enthusiasts at large.
Over 6500 members strong, [our open Slack group](https://community.botkit.ai) is
_the place_ for people interested in the art and science of making bots.
Come to ask questions, share your progress, and commune with your peers!

You can also find help from members of the Botkit team [in our dedicated Cisco Spark room](https://eurl.io/#SyNZuomKx)!

We also host a [regular meetup and annual conference called TALKABOT.](https://talkabot.ai)
Come meet and learn from other bot developers! [Full video of our 2016 event is available on Youtube.](https://www.youtube.com/playlist?list=PLD3JNfKLDs7WsEHSal2cfwG0Fex7A6aok)

## About Botkit

Botkit is a product of [Howdy.ai](https://howdy.ai).

Want to contribute? [Read the contributor guide](CONTRIBUTING.md)

Botkit is released under the [MIT Open Source license](LICENSE.md)
