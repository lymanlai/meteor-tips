https://bulletproofmeteor.com/basics/introduction

1. https://kadira.io/

2. https://kadira.io/platform/kadira-debug/overview
    1) meteor add kadira:debug
    2) go to http://debug.kadiraio.com/debug and connect to the app

3. To take a client side profile, you need to use Google Chrome's CPU profiling tool. Watch this [video](https://kadira.io/platform/kadira-debug/cpu-profiling/taking-a-client-profile) on how to take a CPU profile.

4. You can also learn how to use Chrome CPU profile with [this article](https://developer.chrome.com/devtools/docs/cpu-profiling).

5. Analyzing a CPU Profile with Kadira Debug

Watch the following video to learn how to analyze a CPU profile:

You can also refer to [this](https://kadira.io/academy/analyze-meteor-cpu-profile/) Kadira Academy article for the same information.

6. Monitor Performance in Production
  1). visit ui.kadira.io
  2). meteor add meteorhacks:kadira
  3). In server/kadira.js file
          Kadira.connect("<appId>", "<appSecret>");

7. send email stuff should wrap into Meteor.defer()
    Meteor.methods({
      addTodo: function(title) {
        check(title, String);

        // sending emails to followers for this todo list
        followers.forEach(function(follower) {
          Meteor.defer(function(){
            Email.send({
              from: "hello@todoapp.com",
              to: follower,
              subject: "New todo added",
              text: "here's the todo item: " + title
            });
          }, 0);
        });

        var a =  Todos.insert({'title': title});
      }
    });

    send email service:
      [mailgun](http://documentation.mailgun.com/api-sending.html#sending),
      [gmail](https://developers.google.com/gmail/api/overview),
      [sendgrid](https://sendgrid.com/docs/API_Reference/Web_API/index.html),
      [http://customer.io/](http://customer.io/)
