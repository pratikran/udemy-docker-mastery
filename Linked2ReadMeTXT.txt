Assignment: Secure Docker Registry With TLS and Authentication
Section 7, Lecture 76

The default registry install is rather bare bones, and is open by default, meaning anyone can push and pull images.  You'll likely want to at least add TLS to it so you can work with it easily via HTTPS, and then also add some basic authentication.  

These aren't actually that hard to setup, but do require some commands.  You can learn the basics by creating a self-signed certificate for HTTPS, and then enabling htpasswd  auth, which you'll add users too with basic cli commands.

For this assignment you'll use Play With Docker, a great resource for web-based docker testing and also has a library of labs built by Docker Captains and others, and supported by Docker Inc. 

I'd like you to do the Part 2 and 3 of "Docker Registry for Linux" for this assignment. 
                       http://training.play-with-docker.com/linux-registry-part2/
                       
You can use their text to do this assignment on your own machine, or jump back to their Part 1 
                                                                                        http://training.play-with-docker.com/linux-registry-part1/

and run the container on their infrastructure using their web-based interface to a real docker engine and learn how "PWD" works!

For more extra credit labs, look through their growing list: http://training.play-with-docker.com/








Third Party Image Registries
Section 7, Lecture 78

I've mentioned Docker Hub, Docker Enterprise Edition DTR (Docker Trusted Registry), and Docker Registry as three options for storing your images, but there are many 3rd party options out there.

Quay.io
http://quay.io/
  is a popular choice, and is very comparable to Docker Hub as a cloud-based image registry.  Sysdig did a Docker Usage Report in April 2017 
  (https://sysdig.com/blog/sysdig-docker-usage-report-2017/)
  based off their users that shows Quay as the most popular cloud-based choice.

If you're on AWS, Azure, or Google Cloud, they all have their own registry options that are well integrated with their toolset.

If you want a self-hosted option, there's Docker EE (https://www.docker.com/enterprise-edition#/container_management), Quay Enterprise (https://quay.io/plans/?tab=enterprise), and also GitLab (https://about.gitlab.com/2016/05/23/gitlab-container-registry/), which comes with GitLab Container Registry, among others.

There's a much larger list of registries over at the Awesome Docker (https://github.com/veggiemonk/awesome-docker#hosting-images-registries) list.









Bonus Lecture: Bret's DockerCon 2017 Video: "Journey to Docker Production"
Section 8, Lecture 79

YouTube video of my talk (https://www.youtube.com/watch?v=ZdUcKtg84T8) at DockerCon17 in Austin. My largest audience ever (1k maybe) so I was excited and nervous at first. It turned into a well received talk to a packed room of people ready to go production Docker. Lots of Q&A at the end.

I talk about many of the decisions you need to make when taking your Docker containers from local dev/test to a production cluster. It covers decisions like:

    What host OS should I use?
    What base FROM images should I use?
    How should my Swarm node design look?
    What common issues do people have when starting a production docker project?
    How to limit the project from trying to change too much at once.
    How to speed up the project by outsourcing small pieces of solution to existing products.
    How Docker's Enterprise/Cloud products can help.

https://www.youtube.com/watch?v=ZdUcKtg84T8








Bonus Lecture: Swarm Quorum and Recovery (Laura Frank from DockerCon 2017)
Section 8, Lecture 80

Also from DockerCon 2017, fellow Docker Captain and friend Laura Frank (https://twitter.com/rhein_wein) had a great session on the internals of Swarm Managers and how quorum of their Raft log works, called "Everything You Thought You Already Knew About Orchestration" (https://www.youtube.com/watch?v=Qsv-q8WbIZY). She goes into the math of how you always need an odd number of Managers, and what happens when one or more fail.

She then shows various recovery options in case you "loose quorum" in your Swarm cluster. This video is demo heavy, so it's worth watching the whole thing!

Watch on YouTube: https://www.youtube.com/watch?v=Qsv-q8WbIZY







Bonus Lecture: Bret's Docker and DevOps Newsletter
Section 8, Lecture 81

I send out an email newsletter about once a week on new articles I've written, big news in the Docker ecosystem, and other things you might find useful around containers. You can signup at: 

www.bretfisher.com/newsletter







Bonus Lecture: Using Prune to Keep Your Docker System Clean (YouTube)
Section 8, Lecture 82

Docker has posted a short tip video (https://youtu.be/_4QzP7uwtvI) of me explaining the "prune" command in the docker cli and various ways you can use it. Enjoy!






Bonus Lecture: What's New In Docker 17.06 (YouTube)
Section 8, Lecture 83

It's June of 2017, which means Docker 17.06 (stable) is out!  New features that were in the edge releases the last two months (17.04 and 17.05) are also rolled into this quarterly stable release.  Watch a YouTube video of Mano at Docker HQ giving an overview of the new features (https://www.youtube.com/watch?v=-NeaXUGEK_g).

For a detailed list of changes, you can look through the Docker CE release notes on GitHub (https://github.com/docker/docker-ce/releases).





