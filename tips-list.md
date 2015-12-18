# Basics
## Meteor.defer()
## this.unblock()
## meteor add meteorhacks:fast-render
## meteor add meteorhacks:kadira-profiler
https://bulletproofmeteor.com/basics/cpu-profiling-basics/2
## subscriptions caching
  meteor add meteorhacks:subs-manager
## Server-Side Transformation
https://bulletproofmeteor.com/basics/send-less-data/3
```
// function that transform the document and create the summary field
function transform(wiki) {
  var newWiki = {
    topic: wiki.topic,
    summary: wiki.content.substring(0, 100)
  };

  return newWiki;
}

Meteor.publish('getRecentWikis', function () {
  var sub = this;
  var options = {
    sort: {date: -1},
    limit: 50,
    fields: {topic:1, content: 1},
  };

  // creates the cursor
  var cursor = Wiki.find({}, options);

  // observe the cursor and send changes manually
  cursor.observeChanges({
    added: function (id, doc) {
      // wikis is the collection name (in mongodb)
      sub.added('wikis', id, transform(doc));
    },
    changed: function (id, doc) {
      sub.changed('wikis', id, transform(doc));
    },
    removed: function (id) {
      sub.removed(id);
    }
  });

  // making sure to mark subscription as ready
  sub.ready();
});
```
## Pagination
https://bulletproofmeteor.com/basics/send-less-data/4
```
Meteor.publish('getRecentWikis', function (limit) {
  limit = limit || 10;

  var options = {
    sort: {date: -1},
    limit: limit,
    fields: {topic:1, content: 1},
    transform: function (wiki) {
      var newWiki = {
        topic: wiki.topic,
        summary: wiki.content.substring(0, 100)
      };

      return newWiki;
    }
  };
  return Wiki.find({}, options);
});
```

# Database Modeling
## Using Indexs
https://bulletproofmeteor.com/database-modeling/using-indexes/7
```Mongodb
db.articles.ensureIndex({author: 1, category: 1, createdAt: 1});
db.posts.find({author: "Author-89"}).explain();
```
```Meteor
var Posts = new Mongo.Collection('posts');
Posts._ensureIndex({category: 1});
```
## Counting Documents
```
meteor add tmeasday:publish-counts
Meteor.publish('posts', function (author) {
  var cursor = Posts.find({author: author});
  Counts.publish(this, 'posts-count', cursor);
});
Meteor.publish('posts', function (author) {
  var cursor = Posts.find({author: author});
  Counts.publish(this, 'posts-count', cursor, {nonReactive: true});
});
Template.dashboard.helpers({
  counter: function () {
    return {
      postCount: Counts.get('posts-count'),
      author: author
    };
  }
});
```
## One-to-Many Relationships
https://github.com/arunoda/meteor-ddp-analyzer
make Comments as seperate collection out of posts collection
```
Meteor.subscribe('getSinglePost', 'one');
Meteor.publish('getSinglePost', function (id) {
  return [
    Posts.find(id),
    Comments.find({postId: id})
  ];
});
```
## Many-to-Many Relationships
