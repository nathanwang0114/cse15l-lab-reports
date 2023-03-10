# Lab Report 5
## Writing a Bash Script to Run the Commands in Lab Report 4 ##

For my final lab report, I decided to go back and visit one of my favorite labs/lab reports which was the lab we used to write Lab Report 4. I am going to do the task in a different way then in lab, instead of typing in the commands in the terminal and doing terminal shortcuts to make the process faster, I am deciding to instead write a bash script instead, which will definitely be faster then I can manually achieve. 

** Bash Scripts to Run the Same Commands I Did Manually in Lab Report 4**

*lab9.sh*
```
ssh cs15lwi23ahp@ieng6.ucsd.edu << EOF
git clone https://github.com/nathanwang0114/lab9.git
cd lab9
bash commands.sh
EOF
```

*commands.sh*
```
git clone git@github.com:nathanwang0114/lab7.git
cd lab7
junit1="javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java"
junit2="java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests"
${junit1}
${junit2}
sed -i '43 s/index1/index2/' ListExamples.java
${junit1}
${junit2}
git add ListExamples.java
git commit -m "Fixed"
git push
```

** Explanatation of My Process Writing These Bash Scripts **

I had to create two seperate bash scripts in order to complete all the terminal steps from Lab Report 4 since after ssh-ing into ieng6, it kept logging me out of the remote server right after logging in, so the rest of my bash script commands just ran on the local server. I looked up and tried many different ways of resolving this issue, and these two bash scripts is the best implementation I could come up with. Firstly, I tried using ssh -t which allocates a terminal for me from the terminal to help me stay in the remote server after logging in to run my commands, but that didn't work. Then, I tried using scp which we learned in class to copy a second bash script I made named commands.sh which has all the commands I need to run after ssh-ing into the remote server, but the scp command never terminated. This was the step that made me split my script into two scripts, one being lab9.sh which would login to ieng6, copy the bash script by git cloning it(I made a repository for commands.sh to achieve this), and then execute it, and the other script being commands.sh which I explainned in the previous sentence. However, I was unable to get scp to work as it never terminated even though I tried my best to use the proper syntax. I kept looking for solutions that would keep me logged into ssh and run multiple commands. I could run all the commands in the same line I ssh-ed into the remote server with, but that was not easy to read. So, I searched up ways to do this but in a more clean way, which lead me to << EOF ... EOF, which was supposed to run the commands between the two EOFs(End of File) while keeping me logged into ieng6. I ran my bash script this way and I was able to stay logged in to ieng6 and terminate my commands from comands.sh. However, I ran into a problem after opening up nano to edit ListExamples.java. My comamands in my bash script of navigating through nano using for loops, escape characters for certain keys, and echo/printf would not run. I looked up workarounds to edit a file using a bash script, and found the command sed, which allowed me to replace an exisitng string in the file with my given string. This was exactly what I needed since I only needed to edit one line of the code, changing index1 into index2. After swapping out all my for loops and echo/printf statements for just the sed command, I ran the bash script again and every command I needed to execute was run, the bug got fixed, and I was able to successfully able to commit and push  the edited ListExamples.java file into my GitHub repository. Since everything worked, I tried again using only one bash script by having all the commands in commands.sh inside EOF, but for some reason, the JUnit commands never ran, or at least the terminal didn't show the tests being tested. I went back to what worked originally and the bash scripts above is the end result. Overall, writing the bash script for the commands in the terminal was not too bad, as most of it was just the exact same thing I put in the terminal but instead it was now put into a bash script. There were only a few commands specific to bash script like EOF and sed, and I also made string variables for the lines that compiled and ran the tester since I had to use them twice. 

** Screenshots of me Running lab9.sh and Running all the Commands from Lap Report 4 **

![image](lab9-pic1.png)

![image](lab9-pic2.png)

