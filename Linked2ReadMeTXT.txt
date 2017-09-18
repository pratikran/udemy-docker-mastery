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

