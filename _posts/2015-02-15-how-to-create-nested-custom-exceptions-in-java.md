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

## Points To Remember

When you have to create a nested or a group of similar Exceptions in your application then
* First create a **ParentException** class and this class should either extend ***Exception*** class or ***RuntimeException*** class.
* All the nested Exceptions will extend the ParentException and thus will lie in a hierarchy.

There may be times when you want to have your own hierarchy of Custom Exception so that you can manage your application in a better way.
Suppose we have a **Quiz application** where we want to show questions based on a Topic and display questions.
So we can have following exceptionss for our application.

1. QuizException
2. InvalidQuestionIdException
3. InvalidAnswerException

> Here Quiz Exception is the Parent of all the other Exceptions.
> QuizException can catch all the nested Exceptions so that we do not have to catch each of them separately.

Following is teh example of how we can implement nested exceptions.

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
```

Now our business logic could be as follows

```java
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

Output of the above example is as follows

```
This is question 1
InvalidQuestionIdException: invalid question id provided
 at Question.getQuestion(Test.java:32)
 at Test.main(Test.java:59)
right answer
InvalidAnswerException: invalid answer is provided
 at Answer.getAnswer(Test.java:47)
 at Test.main(Test.java:65)
```
This is how you create Nested Custom Exceptions in java. 
When you want to create hierarchy of Exception you can keep extending the QuizException or any other Exception that extend Quiz Exception.
