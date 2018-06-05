---
layout: post
title: How to sort Array List based on Custom Order
author: Ekansh Rastogi
tags: Java Arrays Collections API
redirect_from: "/2016/02/how-to-sort-array-list-based-on-custom-order-java.html"
---
## How to sort Array List using Custom Order
On many occasions we need to sort an array list or linked list based on custom logic. Suppose you have a Quiz 
application and you want to return questions based on a custom question id.

e.g Request : `ids = [ 88, 21, 43, 15, 64, 35 ]`

When you will fetch the Questions from Database you will be using a query something like below

```sql
select * from question where id in (?)
```

This will give you questions ordered by id by default. So to covert it in same order as requested order you can use

```java
// ids = [ 88, 21, 43, 15, 64, 35 ]  
// questions = new ArrayList<Question>();   
Collections.sort(questions, new Comparator<Question>() {  
     @Override  
     public int compare(QuestionDto q1, QuestionDto q2) {  
         // compare based on the index of id in list **ids  
         return ids.indexOf(q1.getId()) - ids.indexOf(q2.getId());  
     }  
 });
```

The above code will give you questions in order of ids requested.