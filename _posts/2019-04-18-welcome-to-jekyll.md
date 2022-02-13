---
title: Welcome to Jekyll!
date: {}
categories:
  - blog
tags:
  - Jekyll
  - update
published: true
---

Nemesis is a hybrid ROS1/ROS2 skid-steer UVG which grew out of an effort to primarily familiaze my self with integrating an exising ground vehicle into the ROS ecosystem.

I started  by implementing a ROS1 Hardware Interface for the  [Monsterborg mobile base](https://www.piborg.org/robots-1/monsterborg) from PiBorg.  
[IMAGE https://www.piborg.org/image/cache/catalog/freeburn/BURN-0047/main-image-1024x780.jpg]

After its succesfull completion I went on to extend the resulting system by adding a more powerfull processor and sensors for SLAM. Since then I have been using the system as an outdoor mapping and a mobile compute edge platform for drone navigation experiments including the [TUM ARDrone ROS stack](http://wiki.ros.org/tum_ardrone "TUM ARDrone ROS Wiki").

Very recently I have began making inroads into adding experimental autonomous navigation support with move_base. After a rudimentary setup of move_base on ROS Melodic, I decided to switch to ROS2 to leveradge the nav2 package for greater flexibility using ROS1 bridge to communicate with the base hardware interface.  This is currently current work in progress.


The following describes my stable setup on ROS1.

[SYSTEM DIAGRAM IMAGE]

The System architecture is logically into two system components with corresponding code repositories:
1.  A mobile base with an internal ARM based (ARM Cortex-A53 1.2GHz) motor controller computer running ROS Kinetic.
2.  Upper chassis housing an i7 Intel 2 core processor ( i7-6600U CPU @ 2.60GHz processor) computer running ROS Melodic and D435i & T256 Intel Realsense depth and tracking cameras positioned relative to each other with a dedicated mount.

Both computers are connected via ethernet network with an onboard router. The robot can be driven via multiplexed input from a PS4 controller, rqt steering plugins or cmd_vel input from move_base.

Software Architecture
The software stack running on the mobile base is largely based on an adaptation of the [Clearpath Husky Kinetic](https://github.com/husky/husky/tree/kinetic-devel "Husky Kinetic github branch ") stack's base, control, description and navigation packages. 

The ROS hardware interface implementation wraps the motor controller driver that came with the mobile base, which I ported to Cython from Python to reduce latency in the main ROS control loop.  For perception and SLAM, I use Rtabmap [LINK] which I build from source with Apriltag, g2o features support.

[ROS GRAPH IMAGE]

Below is an example of an outdoor mapping session.

[Outdoor Gif]
======================================================================
You'll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

```ruby
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
