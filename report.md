# EEC174AY Lab 1 Report


**Name:** Sukhman Cheema


## 1. SSH


**(a) What is the purpose of port forwarding between your laptop, the course server, and the Docker container?**


We use the course server and Docker so I don't have to rely on my laptop's compute or install libraries myself. But Jupyter then runs inside a container on the server, while my browser is on my laptop. Port forwarding connects the two: the path is laptop → SSH tunnel → server → container → Jupyter. The SSH tunnel sends my laptop's localhost:<port> to the server, and Docker's -p flag passes that port into the container where Jupyter is listening. Because the port is bound to 127.0.0.1, Jupyter is only reachable from the server itself, not the whole network, so the encrypted SSH tunnel is the only way in.


## 2. Git and GitHub


**(a) What is a Git repository? Explain specifically why you would track your code in a repository.**




A Git repository is a place where your code is saved so others can view it. The reason we track our code in Git is that, along with saving every version of the code, each commit includes a message explaining the changes that were made. This also makes it easy to find which commit introduced a mistake.


**(b) Explain what a branch is in Git. Why are branches useful when a team works on one project?**
A branch is basically a way to work on different versions of the code in the same Git repository. It can represent a new feature or any changes you want to test when you are not sure if you want them on the main branch yet. Branches are useful for teams because they allow multiple people to work on one project at the same time. For example, Branch A goes to Robert and Branch B goes to Joe; after both are done, they can merge their work and resolve any conflicts.
**(c) What is the default branch (commonly named `main`)? What is its role in a software project?**


The default branch is the main line of the project. It is the branch you get when you clone a repo, and the branch other branches are usually merged into. Its role is to hold the stable, working version of the code.


**(d) Explain what a pull request is and why it is important. Briefly explain a typical collaborative software-development cycle using Git and GitHub.**


A pull request (PR) is a request on GitHub to merge one branch into another, usually a feature branch into main. It shows the exact changes and lets teammates review, comment, and run tests before the code is merged.


Typical cycle:


1. Pull the latest `main`.
2. Create a new branch for the feature or fix.
3. Write code and make commits.
4. Push the branch to GitHub.
5. Open a pull request.
6. Teammates review it; make changes if requested.
7. Merge into `main`, then delete the branch and start again for the next task.


## 3. Docker


**(a) In your own words, explain why Docker is useful for programmers. Discuss the ways Docker can save development time.**


Docker is useful because it eliminates dependency conflicts and package mismatches, where a single incorrect library out of hundreds can prevent an application from running. It saves development time by providing an isolated environment that can be quickly reset or re-created if something breaks, allowing developers to test changes safely without disrupting their local machine.


**(b) Explain the difference between a Docker image and a Docker container.**


An **image** is the read-only template, the packaged environment (OS, tools, libraries). Example: `eec174lab1-2:latest`. A **container** is a running instance of an image. You can start, stop, and delete it, and you can run many containers from the same image.


**(c) Explain how Docker can resolve a dependency conflict between a computer-vision program and a control program being developed on the same machine.**


If the computer-vision program requires a newer version of a shared library (such as OpenCV or NumPy) while the control program relies on an older, incompatible version, installing them globally on the host operating system would cause a conflict. Docker resolves this by packaging each application with its specific dependencies into independent images. Because each application runs inside an isolated container, their runtimes do not interfere with each other, allowing both conflicting versions to execute on the same machine seamlessly.


**(d) Can Docker be used to support Linux software on a Windows computer? Explain the role of the Linux environment used by Docker Desktop.**


Yes. Docker containers share the host's operating system kernel, and Linux containers require a Linux kernel, which Windows lacks natively. Docker Desktop solves this by running a lightweight Linux virtual machine in the background. This virtual environment provides the necessary Linux kernel that the containers run on, allowing Linux software to work on a Windows machine.


**(e) Can Docker support development of the same project on different machines? Explain.**


Yes. Because the image contains the full environment, anyone who pulls the same image gets the exact same setup on their own machine: my laptop, a teammate's computer, or the course server.


**(f) In one to three sentences, explain how to build a new Docker image from scratch.**


Write a `Dockerfile` that starts from a base image (`FROM`), installs dependencies (`RUN`), copies in files (`COPY`), and sets the default command (`CMD`). Then run `docker build -t <image-name> .` in that folder to build the image.


## 4. Python


**(a) Compare interpreted and compiled languages. In what situations might Python be more advantageous than C++?**
Python is better when development speed matters more than execution speed. It allows for quick scripting and rapid testing because it runs line by line with an interpreter, whereas C++ requires you to recompile the code after every change. Python is also far better suited for machine learning and computer vision, offering libraries like NumPy, PyTorch, and OpenCV to handle heavy computational workloads, while in C++ its a lot harder to do.


From NOTES:
- A **compiled** language like C++ is translated into machine code by a compiler before it runs. This makes it very fast, but you must recompile after every change.
- An **interpreted** language like Python is run line by line by an interpreter. It runs slower, but you can run code right away without a build step.




**(b) Explain what lists, dictionaries, and tuples are in Python. Give one example scenario where you would use each.**


**List:**A list is an ordered changeable collection of things. You can add, remove or reorder them. In terms of a scenario I used them in lab 1 to build the queue as I added to the back and removed from the front.
- e.g. `[1, 2, 3]`. You can add, remove, and reorder items.
  
**Dictionary:** is a collection of key-value pairs, e.g. `{'a': 2, 'b': 1}`. Values are looked up by key instead of by position.
  *Example:* In the anagram question, I used a dictionary to count how many times each letter appears in each string, then compared the two dictionaries.


**Tuple:** An ordered collection that cannot be changed after it is created, e.g. `(3, 4)`.
  *Example:* Storing fixed values that belong together, like an (x, y) coordinate or an image size `(width, height)`.



