---
layout: post
exclude: true
title: How to create Nested Custom Exceptions in Java
author: Ekansh Rastogi
tags:
- Java
- Exceptions
- Exception Handling
modified_time: '2015-02-15T21:26:36.215+05:30'
blogger_id: tag:blogger.com,1999:blog-5485242750509374114.post-2187478208760689910
blogger_orig_url: http://ekiras.blogspot.com/2015/02/how-to-create-nested-custom-exceptions-in-java.html
redirect_from: "/2015/02/how-to-create-nested-custom-exceptions-in-java.html"
---

<div dir="ltr" style="text-align: left;" trbidi="on">
    <div style="text-align: left;"><h2 style="text-align: left;">Points To Rememeber</h2>When you have to create a
        nested or a group of similar Exceptions in your application then&nbsp;</div>
    <div style="text-align: left;"></div>
    <ul style="text-align: left;">
        <li>First create a <b>ParentException</b> class and this class should either extend <b>Exception</b>&nbsp;class
            or <b>RuntimeException</b> class.&nbsp;</li>
        <li>All the nested Exceptions will extend the ParentException and thus will lie in a hierarchy.</li>
    </ul>
    <br/>
    <h2>Scenario</h2>There may be times when you want to have your own hierarchy of Custom Exception so that you can
    manage your application in a better way.<br/><br/>Suppose we have a <b>Quiz application</b> where we want to show
    questions based on a Topic and display questions<br/>
    <h2>Creating Nested Custom Exceptions&nbsp;</h2>So we have created three exception classes here.<br/><br/>
    <ol style="text-align: left;">
        <li>QuixException</li>
        <li>InvalidQuestionIdException</li>
        <li>InvalidAnswerException</li>
    </ol>
    <div>Here Quiz Exception is the Parent of all the other Exceptions. QuizException can catch all the nested
        Exceptions so that we do not have to catch each of them separately. &nbsp;</div>


```java
class QuizException extends Exception {

 public QuizException(String message) {
  super(message);
 }

}

class InvalidQuestionIdException extends QuizException {

 public InvalidQuestionIdException() {
  super("invalid question id provided");
 }

}

class InvalidAnswerException extends QuizException {

 public InvalidAnswerException() {
  super("invalid answer is provided");
 }

}
class Question {
 public String getQuestion(Integer id) throws InvalidQuestionIdException{
  switch (id) {
  case 1:
   return "This is question 1";
  case 2:
   return "This is question 2";
  default:
   throw new InvalidQuestionIdException();
  }
 }
}


class Answer{
 public String getAnswer(Integer ans)throws InvalidAnswerException{
  switch(ans){
  case 1:
   return "right answer";
  case 2:
   return "wrong answer";
  default:
   throw new InvalidAnswerException();
  }
  }
 }
 
public class Test {
 public static void main(String args[]) {
  try {
   System.out.println(new Question().getQuestion(1));
   System.out.println(new Question().getQuestion(5));
  } catch (QuizException e) {
   e.printStackTrace();
  }
  try {
   System.out.println(new Answer().getAnswer(1));
   System.out.println(new Answer().getAnswer(3));
  } catch (QuizException e) {
   e.printStackTrace();
  }
 }

}
```
    Output of the above example is as follows<br/>
    <div class="output">This is question 1<br/>InvalidQuestionIdException: invalid question id provided<br/><span
            class="Apple-tab-span" style="white-space: pre;"> </span>at Question.getQuestion(Test.java:32)<br/><span
            class="Apple-tab-span" style="white-space: pre;"> </span>at Test.main(Test.java:59)<br/>right answer<br/>InvalidAnswerException:
        invalid answer is provided<br/><span class="Apple-tab-span" style="white-space: pre;"> </span>at
        Answer.getAnswer(Test.java:47)<br/><span class="Apple-tab-span" style="white-space: pre;"> </span>at
        Test.main(Test.java:65)
    </div>
    This is how you create Nested Custom Exceptions in java. When you want to create hierarchy of Exception you can keep
    extending the QuizException or any other Exception that extend Quiz Exception.<br/><br/></div>
