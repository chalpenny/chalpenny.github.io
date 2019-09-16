---
layout: post
title:      "CLI Project"
date:       2019-09-16 00:38:52 +0000
permalink:  cli_project
---

Harder than it should have been, or maybe just as hard as it was meant to be.

For my CLI Project at the end of the Ruby module, I created a quick recipe finder using an API provided by RecipePuppy.  When you run it, it returns a list of recipes that you can choose from to see its ingredients and get a link to the full recipe.  I unfortuantely wasn't able to add as much functionality as I was hoping to - more about that later.

The fun part of this project was seeing the methods and pieces of Ruby come together to create a program specified by me, and as I made changes or decided to add steps, the program would morph along with my ideas.  Additionally, I learned that taking time to plan and properly organize the steps of your program is as important as actually writing the code.  Some very cool programs are abstracted down to be very clean and simple.  Those programs didn't happen that way by accident, it took a lot of planning to make them that way.  I spent a good amount of time starting at my screen, thinking through how the program should run step-by-step, then how to put that in a method, then how to build the appropriate methods to make it happen.  

My code went through multiple iterations to come up with just this one step:

```   elsif @input == "1"
            print_recipes
            @input = gets.chomp
            return_recipe(@input)```
						
Having built a CLI now, the process would probably be a lot quicker for me the next time.  I was on one hand surprised by how simple the program turned out to be to build, and at the same time, surprised by how long it took me to build it.  It involved about 16 missteps for every 1 step in the right direction.  I didn't use Test Driven Development to create this, as I have been for the other labs in this course, so a lot of time was spent making a change, running the program, and figuring out the error, then repeating the process until it was working.  Binding.pry proved it's worth 100 times over, as it gave me the chance to figure out why something wasn't working when I thought it should be, by checking values partway through the process of calling a method.

One method I wish I'd been able to get working was a search-by-ingredient option.  I worked on the code for quite a while before finally scrapping the idea due to time constraints.  

```def self.find_by_ingredient(input)      
           recipe = self.all.collect {|recipe| recipe.ingredients}
           recipe.each do |string|         
           string.split(", ").uniq.each do |word|         
                      if word == input         
                                 puts "#{recipe.name}   <- THIS LINE DOESN'T WORK     
                      end       
                 end      
           end    
     end```

Besides the fact that this method is in need of some good abstraction, it was very disappointing to get so close and not get it working.  I'm sure it's something another head and/or some experience will help me work out in the future.

This was a good trial by fire.  I've learned a lot about how to build a program, and looking back to my past, three-weeks ago, self, I can see that even in that short amount of time, I've progressed in my coding skills.  Looking forward to the next project, with the hope that the skills I've learned this time will make the next project easier!
