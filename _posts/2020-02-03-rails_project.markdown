---
layout: post
title:      "Rails Project"
date:       2020-02-03 08:25:56 +0000
permalink:  rails_project
---


Oh man, ActiveRecord associations, am I right?

Powerful, yes.  A pain in the behind?  Also true. 

Building an app from start to finish is a great way to learn.  It requires putting together everything we've learned so far, and maybe learning a few extra things as well.  Inevitably there will be bugs to solve, which is maybe one of the best ways to become familiar with how it all works.  

My project is a pet sitter tracker, designed to hold client information and track appointments.  It involved 5 models, each with a unique set of associations. As I started visualizing it initially, I realized it was going to be the biggest and gnarliest project I'd built to date.  So I laid it out in Excel.  There were a lot of associates to consider.

A User: has many appointments, and has many clients through appointments.

An Appointment: belongs to a User.  It belongs to a client, and has many pets through a Client.

A Client: has many appointments, has many pets.

A Pet: belongs to a Client, and has many Notes.

A Note: belongs to a pet. It's also created with a polymorphic association, it enable it to be set up for any model within the app.

That is a lot of associations.  Any one of those is not too tricky to establish, but once they start building upon each other, it can get kind of confusing in regards to which variable goes where. The fundamentals are the same as we've been learning so far, but making multiple associations can be tricky.  For example, below is the code for #create in my Appointments controller, which needs an association to both User and Client:

```
 def create
        @appointment = @user.appointments.build(appointment_params)
        @appointment.client_id = @client.id
        if @appointment.save
            redirect_to client_appointments_path(@client)
        else
            render :new
        end
    end

```

The appointment it built on the associated User, and then needs the client id set so it can belong to the correct client.  This took some messing with to get it right.

I also got to explore polymorphic associations.  Those are pretty neat, in that they can be set up to associate to any model while existing almost independently, in their own corner of the app.  I had a lot of fun creating those.

The form to create them is pretty simple, as it's just a text area field:

```

<%= form_with(model: [notable, Note.new], local: true) do |form| %>
    <div class="field">
    <%= form.submit class: "btn btn-primary" %>
    </div>
    <%= form.text_area :content %>
  
<% end %>
```

Then, in the view that you want to add it to, you simply make the association in the form:

```
<%= render partial: "notes/form", locals: {notable: @pet} %>
    <%= render partial: "notes/notes", locals: {notable: @pet} %>
</p>
```


which will set the note to that instance.

What an experience this has been!  There is so much to learn, and knowing what you CAN do is a lot different than knowing HOW to do it.  This project was a great exercise in putting some of those pieces together.


