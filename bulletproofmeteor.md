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

8. Meteor.defer 与 this.unblock 区别在于defer内的代码运行时间不计入该method的运行时间，
    unblock则是告诉meteor来pick下一个method执行不用等该方法执行完

9. SubsManager：Subscriptions Manager caches your subscriptions and runs all the subscriptions that have been cached when a route is changed.
  https://github.com/kadirahq/subs-manager
  meteor add meteorhacks:subs-manager
  Usage with Iron Router: just replace Meteor.subscribe() calls with subs.subscribe(), where subs is a new SubsManager().
  var subs = new SubsManager();
  // later in some other place
  subs.reset();
  var subs = new SubsManager({
    // maximum number of cache subscriptions
    cacheLimit: 10,
    // any subscription will be expire after 5 minute, if it's not subscribed again
    expireIn: 5
  });
  1). Using separate Subscription Managers
  2). Cache subscriptions you only need
  3). Using global ready checking
  var subs = new SubsManager();
  subs.subscribe('postList');
  subs.subscribe('singlePost', 'id1');

  Tracker.autorun(function() {
    if(subs.ready()) {
      // all the subscriptions are ready to use.
    }
  });
