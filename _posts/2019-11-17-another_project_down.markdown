---
layout: post
title:      "Another Project Down"
date:       2019-11-17 20:53:12 +0000
permalink:  another_project_down
---

# 
Here we are again at the end of another project.  I've come a lot farther and still feel the struggle as much as when I was just two months into this.  But that's ok, I've come to think of this journey like going to the gym - each time you go to the gym, you get a little stronger.  So each time you go, you increase the intensity or the weight of your workout.  It should never be easy or you're doing it wrong.  So it is with coding - there's so much to learn that it should always be somewhat of a challenge.  It's constant improvement, always learning more and adding to what you know.  It's not easy, but you're getting consistently stronger at it.  Effort in my mental workout is just as important, and just as rewarding, as my physical workout.

The prep for the Sinatra project introduced me to some new concepts, as well as solidifying a lot of material we had already covered.  But we had covered it with baby steps, and now we were taking big ol' adult steps with it.  I learned a lot more about Associations and how powerful they are.  I learned more about migrations and database management.  And once again, binding.pry was my best friend.

My project is a tracker where you can enter and keep track of your vehicle(s) and maintenance services. That way you can keep track of when you last bought new tires, or how much was spent on maintenance.


I learned about security and user authentication.  As the following well-known cartoon points out, it's important to only accept the params you want at any given time to avoid a hacker entering info that you don't want or didn't plan for.

![](https://xkcd.com/327/)

As an example, the following code would not be considered safe, or sanitized:

WRONG:
```post "/signup" do
    user = User.create(params)```
	
	Your form could request only the information needed to create your User instance, so it would work.  But you would leave yourself open to someone being able to pass in ANY params info and possibly use that to change a user ID, which shouldn't be accessible from here, or perhaps to send a command, such as in the cartoon above.
	
	RIGHT
	```post "/signup" do
    user = User.create(email: params[:email], password: params[:password], password_confirmation: params[:password_confirmation]) ```


Here, a user can only pass the information as you want it to be passed, and only used as you want it to be used.

Another important concept I learned also relates to params and passing information around.  My project uses multiple controllers to handle routes and requests.  Controllers can share variables with their views, but not with other controllers.  I ran into a problem in trying to assign the foreign key of a service instance with the corresponding vehicle.  To keep a separation of concerns, my services routes were in a separate controller from my vehicle routes.  But how to relate it to its vehicle?  

Post request in Services Controller:
```post "/services" do
        redirect_if_not_logged_in
        @service = Service.create(service_item: params[:service_item],date: params[:date],mechanic: params[:mechanic], cost: params[:cost],vehicle_id: params[:vehicle_id])
        redirect "/vehicles/#{@service[:vehicle_id]}"
    end```

 The vehicle controller route rendered the show.erb file which had a form to collect the info of the service.  On this form, the program knew what vehicle we wanted to add to, but once the form posted to the services controller, it no longer knew.  The answer was to use the form that collects the info (which become the params) to also collect a hidden param of the vehicle ID that I would set, not the user.  The params would then pass to the service controller and keep that information that we needed.  At that point we could create a Service instance with the foreign key of the vehicle that it belongs to.  And voila, the vehicle now has a service item, and the service item belongs to a vehicle.
 
 Another project down, more information acquired, on to the next challenge.

	
