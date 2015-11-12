http://blog.mongolab.com/2014/07/tutorial-scaling-meteor-with-mongodb-oplog-tailing/

1. meteor add facts
    if (Meteor.isServer) {
      // Set which users can see server metrics
      Facts.setUserIdFilter(function () {
        return true;
      });
    }
