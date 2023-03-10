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

I had to create two seperate bash scripts in order to complete all the terminal steps from Lab Report 4 since after ssh-ing into ieng6, it kept logging me out of the remote server right after logging in, so the rest of my bash script commands just ran on the local server. I looked up and tried many different ways of resolving this issue, and these two bash scripts is the best implementation I could come up with. Firstly, I tried using ssh -t which allocates a terminal for me from the terminal to help me stay in the remote server after logging in to run my commands, but that didn't work. Then, I tried using scp which we learned in class to copy a second bash script I made named commands.sh which has all the commands I need to run after ssh-ing into the remote server, but the scp command never terminated. This was the step that made me split my script into two scripts, one being lab9.sh which would login to ieng6, copy the bash script, and then execute it, and the other script being commands.sh which I explainned in the previous sentence. However, I was unable to get scp to work as it never terminated even though I tried my best to use the proper syntax.
