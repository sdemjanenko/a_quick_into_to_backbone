A Quick Into To Backbone
============

Backbone is one of the most popular MVC frameworks for JavaScript.
Backbone has two main components: Models and Views.

Models
======

In Backbone, models store data and worry about communicating with the server.

    var User = Backbone.Model.extend({
      defaults: {
        name: '',
        email: '',
        sex: 'male'
      },
      isMale: function() {
        return this.get('sex') == 'male';
      }
    });

    var user = new User({name: 'Stephen', email: 'stephen@somecompany.com'});

In the above example the isMale function is a helper method which I will use in a View later.


Sync
----

Backbone.sync lets your models talk to your server. Sync by default is set up to talk
with a RESTful API. If you would like more control over your API, you can override sync.

When working with a model you can use the .fetch() and .save() methods. These methods delegate
out to Backbone.Sync.

    var my_user = new User({url: '/my_user'});
    my_user.fetch(); // makes a GET request with type application/json


    var new_user = new User({url: '/users', name: 'Ben', email: 'ben@somecompany.com', sex: 'male'});
    new_user.save(); // makes a POST request


Views
=====

Backbone views manage rendering UI elements as well as handling user interactions.


    var UserView = Backbone.View.extend({
      events: {
        "click span.name": "nameClicked"
      },
      initialize: function() {
        this.$el.html("<span class='name'></span> (<span class='email'></span>)");
        this.renderName().renderEmail();
      },
      renderName: function() {
        var title = this.model.isMale() ? 'Sir' : 'Madamme';
        this.$('.name').text(title + " " + this.model.get('name'));
        return this;
      },
      renderEmail: function() {
        this.$('.email').text(this.model.get('email'));
        return this;
      },
      nameClicked: function() {
        alert("Hello, " + this.model.get('name'));
      }
    });

    var userProfile = new UserView({el: "#userProfile", model: user });


Summary
=======

Backbone is a great way to give structures to your applications.  Data goes in Models.
User interactions & rendering logic goes in the Views.

When interacting with a server your Models serve as the data cache from which your views read.
You can then let Backbone.Sync talk to your server when prompted by .fetch() or .save()