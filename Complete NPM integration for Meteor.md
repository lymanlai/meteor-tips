https://meteorhacks.com/complete-npm-integration-for-meteor

#1
meteor add meteorhacks:npm

#2
packages.json
{
  "redis": "0.8.2",
  "github": "0.1.8"
}

#3
var Github = Meteor.npmRequire('github');
var github = new Github();

github.gists.getFromUser({user: 'arunoda'}, function(err, gists) {
  console.log(gists);
});
