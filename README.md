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


Views
=====

Backbone views manage rendering UI elements as well as handling user interactions.


    var UserView = Backbone.View.extend({
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
      }
    });

    var userProfile = new UserView({el: "#userProfile", model: user });
