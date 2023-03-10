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
