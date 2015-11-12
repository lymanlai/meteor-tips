https://github.com/phusion/passenger/wiki/Phusion-Passenger:-Meteor-tutorial

How’s this any different from putting Meteor behind an Nginx reverse proxy yourself?

1. Using Phusion Passenger is much easier. If you do it yourself, you’ll have to write reverse proxy rules, write init scripts, setup process supervision, etc. The result probably does not even handle corner cases properly. Phusion Passenger takes care of all this for you and handles virtually all the corner cases. This reduces the number of moving parts and reduces complexity.
2. Phusion Passenger integrates much deeper into Nginx than a straight reverse proxy does, and as such can leverage Nginx features much better. For example, the load balancing and response buffering in Phusion Passenger is much better than the one you get with manual reverse proxying.
3. By using Nginx’s proxy module, it’s very hard to see what’s going on with the system right now. Are all connections ok? Are all processes ok? Phusion Passenger provides simple and powerful administration tools that can help you with that.
