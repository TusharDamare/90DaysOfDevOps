**Tasks:**

1.- Explain in your own words and with examples what Shell Scripting means for DevOps.

Shell scripting is writing a series of commands in a file named script to automate tasks or repitative tasks in Unix/Linux systems. 
As a devops engineer below are the fields where shell scripts mostly used :

-Deploying applications
-Monitoring servers
-Running backups
-Setting environment variables
-Configuring 

Example :
![example_1] (images/Image1.png)


2- What is `#!/bin/bash`? Can we write `#!/bin/sh` as well?

This line is called a shebang. It tells the system which interpreter to use to run the script.
#!/bin/bash: Uses the Bash shell (Bourne Again SHell)
#!/bin/sh: Uses the SH shell (older, simpler shell)

yes, we can use #!/bin/sh, but:
fers more features (like arrays, [[ ]], string manipulation).
/bin/sh is more portable across Unix systems but might lack Bash-specific features.


3- Write a Shell Script that prints `I will complete #90DaysOfDevOps challenge`.

#!/bin/bash

echo "I will complete #90DaysOfDevOps challenge."
~


4- Write a Shell Script that takes user input, input from arguments, and prints the variables.

! [example] (images/Image2.png)

5- Provide an example of an If-Else statement in Shell Scripting by comparing two numbers.

! [example_if-else] (images/image3.pnp)