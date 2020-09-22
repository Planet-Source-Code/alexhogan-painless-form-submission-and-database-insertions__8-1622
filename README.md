<div align="center">

## Painless Form submission and Database Insertions


</div>

### Description

How would you like to process a form and insert its data into a database with only a couple of lines of code?

With this tutorial I will show you how to process forms and insert data into databases with the least effort.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[AlexHogan](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/alexhogan.md)
**Level**          |Intermediate
**User Rating**    |5.0 (25 globes from 5 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Databases](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/databases__8-5.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/alexhogan-painless-form-submission-and-database-insertions__8-1622/archive/master.zip)





### Source Code

<style type="text/css">
<!--
.style3 {color: #006600}
.style4 {color: #0000FF}
.style5 {color: #FF0000}
-->
</style>
 <h2>Painless form submissions and Databases insertions..</h2>
 <p>If you are like me one of the things that you find most tedious is inserting data into databases. Having to name all the fields in the query and match them with all the values that you're inserting in to those fields. Every time you submit a form you have to go through this process.</p>
 <p><strong>Ever think.., <em>"There's got to be an easier way"</em>?</strong></p>
 <p>Well there is, and in this tutorial I'm going to show you how.</p>
 <p>First let's say that you have a form that allows visitors to your web site to register for things like free downloads, tutorials and added content that isn't available to non-registered visitors. We'll call this table "registration". This table contains the fields firstname, lastname, email, username and password.</p>
 <p>Your form would look something like this;</p>
 <table width="100%" border="0" cellspacing="0" cellpadding="3">
 <tr>
 <td colspan="2"><div align="center">My Form </div></td>
 </tr>
 <tr>
 <td width="44%"><div align="right">First Name: </div></td>
 <td width="56%"><table border="1" cellspacing="0" width="100%"><tr><td> </td></tr></table></td>
 </tr>
 <tr>
 <td><div align="right">Last Name:</div></td>
 <td><table border="1" cellspacing="0" width="100%"><tr><td> </td></tr></table></td>
 </tr>
 <tr>
 <td><div align="right">Email Address: </div></td>
 <td><table border="1" cellspacing="0" width="100%"><tr><td> </td></tr></table></td>
 </tr>
 <tr>
 <td><div align="right">Username:</div></td>
 <td><table border="1" cellspacing="0" width="100%"><tr><td> </td></tr></table></td>
 </tr>
 <tr>
 <td><div align="right">Password:</div></td>
 <td><table border="1" cellspacing="0" width="100%"><tr><td> </td></tr></table></td>
 </tr>
 <tr>
 <td colspan="2">
 <div align="center">
 Submit Reset
 </div></td>
 </tr>
 </table>
 <p>When the user presses the 'Submit' button you will need to process that request and enter the data into the database. You would probably use some code that looks like this;</p>
 <p>First you have to get the values from the form;</p>
 <p>$firstname <span class="style4">=</span> <span class="style4">$_POST</span>[<span class="style5">'firstname'</span>];<br>
 $lastname <span class="style4">= $_POST</span>[<span class="style5">'lastname'</span>];<br>
 $email <span class="style4">= $_POST</span>[<span class="style5">'email'</span>];<br>
 $username <span class="style4">= $_POST</span>[<span class="style5">'username'</span>];<br>
 $password <span class="style4">= $_POST</span>[<span class="style5">'password'</span>]; </p>
 <p>Then you have to insert those values into the database; </p>
 <table width="100%" border="0" cellspacing="0" cellpadding="3">
 <tr>
 <td width="13%" valign="top">$insert</td>
 <td width="7%" valign="top"><div align="center" class="style4">=</div></td>
 <td width="80%" valign="top"><p><span class="style5">"INSERT INTO registration<br>
 (firstname, lastname, email, username, password)<br>
 VALUES<br>
 ($firstname, $lastname, $email, $username, $password)
 "</span>;<br>
 </p> </td>
 </tr>
 </table>
 <p>Let's not forget that you'll want to see if there is anything in the $_POST array before trying to assign a variable to the value. </p>
 <p>All in all not a whole lot of code to write. But, what if your form contained 30 or 40 items with values, or if you have a dozen forms on your site, or if you have an application that makes 10 or 20 database inserts during the course of the users session. Multiply the above code by 20 or 30 times with 10 to 20 more fields in the form and you can see how this can become a tedious and taxing task.</p>
 <p> </p>
 <p><strong>So, how are we going to make our lives easier?</strong></p>
 <p>Let's start by looking at the $_POST array. Yes I said $_POST array! All of the data that is posted from your forms is transferred from the form page to the functionality page as an array. So why not use PHPs array manipulation functions to our advantage to help us process our forms and insert data into our databases?</p>
 <p>Let's create a class called, "dbinsert" and while we're at it declare some variables.</p>
 <p><span class="style3">class</span> dbinsert{<br>
   <span class="style3">var</span> $i;<br>
   <span class="style3">var</span> $n;<br>
   <span class="style3">var</span> $fld;<br>
   <span class="style3">var</span> $val;</p>
 <p>
 }</p>
 <p>The variable $i and $n will simply be counters, while $fld and $val will represent field names and field values respectively. </p>
 <p>The next thing we'll want to do is to create a method that will parse through the $_POST data. We'll call this "gotcha" and we'll pass it two parameters $arr, which will be the $_POST array, and $table, which will be the name of our table in our database. We will also initialize $i. </p>
 <p><span class="style4">function</span> gotcha($arr, $table){<br>
  <span class="style4">$this-></span>i <span class="style4">=</span> <span class="style5">0</span>;</p>
 <p>} </p>
 <p>Now we'll want to cycle through the $_POST array with a foreach loop and seperate the array keys and values into temp variables using $key => $value. We then assign the values to our variables $fld and $val. You may notice at this point that the name of the form object is going to be the same as the name in the $fld variable. What we are going to do is insure that we name the form objects the EXACT same names as we have named our fields in our database. In the above example we have named the textbox that will contain the users first name, "firstname", just the same as we've named our field in the database. You'll also notice that we're escaping quotes in our assignment of the $val variable. This is because we want to allow the user to be free to add apostrophes and quotes to any field that would be approapreate to have them. </p>
 <p><span class="style3">foreach</span>($arr <span class="style3">as</span> $key <span class="style4">=></span> $value){<br>
  <span class="style4">$this-></span>fld[<span class="style4">$this-></span>i] <span class="style4">=</span> $key;<br>
  <span class="style4">$this-></span>val[<span class="style4">$this-></span>i] <span class="style4">=</span> <span class="style5">"\"$value\""</span>;<br>
<br>
  <span class="style4">$this-></span>i<span class="style4">++</span>;<br>
} </p>
 <p>The last thing we want to do is to increment the variable $i before we start the loop over again.</p>
 <p>Now if you think about what we are getting in the $_POST you should see that we have a little bit of a problem. Our post array will look like this;<br>
 [firstname]=>John, [lastname]=>Smith, [email]=>mymail@mydomain.com, [username]=>myusername, [password]=>mypassword, [Submit]=>Submit</p>
 <p>We've also picked up the name and value of the button on the form. Obviously we don't and won't have a field in the database named "Submit" so we'll need to make sure we get rid of that key and value. To do that we use an if statement. We'll check to see if any of the $key(s) are equal to "Submit". In this case we are saying that if $key is not equal to Submit then assign the values to the variables $fld and $val, and when $key does equal Submit then break out of this loop. </p>
 <p><span class="style3">foreach</span>($arr <span class="style3">as</span> $key <span class="style4">=></span> $value){</p>
 <p> <span class="style3"> if</span>($key <span class="style4">!=</span> <span class="style5">'Submit'</span>){<br>
    <span class="style4">$this-></span>fld[<span class="style4">$this-></span>i] = $key;<br>
    <span class="style4">$this-></span>val[<span class="style4">$this-></span>i] = <span class="style5">"\"$value\""</span>;<br>
   }<br>
  <span class="style3"> else</span>{<br>
     <span class="style3">break</span>;<br>
    }<br>
  <span class="style4"><br>
  $this-></span>i<span class="style4">++</span>;<br>
<br>
} </p>
 <p>We now have two arrays. The first being the $fld array that contains the names of the fields that we are going to insert data into, and the $val array that contains the values or data for each of those fields. </p>
 <p>The last line in our method is;<br>
 <span class="style4">$this-></span>insert($table, <span class="style4">$this-></span>fld, <span class="style4">$this-></span>val);</p>
 <p>Here we are calling another method that will actually insert the values into the database in the appropreiate fields. </p>
 <p>So the entire gotcha method looks like this;<br>
 <br>
 <span class="style4">function</span> gotcha($arr, $table){<br>
  <span class="style4">$this-></span>i <span class="style4">=</span> <span class="style5">0</span>;</p>
 <p><span class="style3">  foreach</span>($arr <span class="style3">as</span> $key <span class="style4">=></span> $value){<br>
 <span class="style3">    if</span>($key <span class="style4">!=</span> <span class="style5">'Submit'</span>){<br>
        <span class="style4">$this-></span>fld[<span class="style4">$this-></span>i] = $key;<br>
        <span class="style4">$this-></span>val[<span class="style4">$this-></span>i] = <span class="style5">"\"$value\""</span>;<br>
      }<br>
     <span class="style3">else</span>{<br>
       <span class="style3">break</span>;<br>
      }<br>
<br>
    <span class="style4">$this-></span>i<span class="style4">++</span>;<br>
<br>
    }  </p>
 <p><span class="style4">  $this-></span>insert($table, <span class="style4">$this-></span>fld, <span class="style4">$this-></span>val);</p>
 <p>} </p>
 <p>All thats left now is the actual function, or method that will insert the data into our database. We'll call this method "insert" just like we called it in our gotcha method. In this method we'll pass in the table name, $table, the fields, $fld and the field values, $val. </p>
 <p><span class="style4">function</span> insert($table, $fld, $val){<br>
<br>
} </p>
<p>Next we have to build our SQL statement that will insert the data to our database. Here we are assigning the variable $query with the insert statement. At first it looks like what we've done above with the normal insert statement with the exception that we have used $table for the table name and (%s) for both the field names and the field values. </p>
 <p> $query <span class="style4">=</span> <span class="style5">"INSERT INTO $table (%s) VALUES (%s)"</span>;<br>
 $query <span class="style4">=</span> <span class="style4">sprintf</span>($query, <span class="style4">implode</span>(<span class="style5">","</span>, $fld), <span class="style4">implode</span>(<span class="style5">","</span>, $val));</p>
 <p>On the next line we're letting PHP break apart the arrays that we created in the "gotcha" method and using the "implode" function we are creating a string that has all the field names seperated by a comma and using the sprintf() function then replacing the %s after $table with the string. The same is done with the $val array and all the values are broken into a string and replace the %s after values.</p>
 <p>The next line passes the $query to the function mysql_query() just like normal. <br>
<br>
$result <span class="style4">=</span> <span class="style4">mysql_query</span>($query) <span class="style3">or</span> <span class="style4">die</span>;</p>
 <p>The completed method looks like this;</p>
 <p><span class="style4">function</span> insert($table, $fld, $val){<br>
  $query <span class="style4">=</span> <span class="style5">"INSERT INTO $table (%s) VALUES (%s)"</span>;<br>
  $query <span class="style4">=</span> <span class="style4">sprintf</span>($query, <span class="style4">implode</span>(<span class="style5">","</span>, $fld), <span class="style4">implode</span>(<span class="style5">","</span>, $val));<br>
  $result <span class="style4">=</span> <span class="style4">mssql_query</span>($query) <span class="style3">or</span> <span class="style4">die</span>;<br>
<br>
} </p>
 <p>Put it all together and the finished class looks like this;</p>
 <p><span class="style3">class</span> dbinsert{<br>
  <span class="style3">var</span> $i;<br>
  <span class="style3">var</span> $n;<br>
  <span class="style3">var</span> $fld;<br>
  <span class="style3">var</span> $val;</p>
 <p><span class="style4">  function</span> gotcha($arr, $table){<br>
    <span class="style4">$this-></span>i <span class="style4">=</span> <span class="style5">0</span>;</p>
 <p><span class="style3">    foreach</span>($arr <span class="style3">as</span> $key <span class="style4">=></span> $value){<br>
 <span class="style3">      if</span>($key <span class="style4">!=</span> <span class="style5">'Submit'</span>){<br>
          <span class="style4">$this-></span>fld[<span class="style4">$this-></span>i] = $key;<br>
          <span class="style4">$this-></span>val[<span class="style4">$this-></span>i] = <span class="style5">"\"$value\""</span>;<br>
        }<br>
       <span class="style3">else</span>{<br>
         <span class="style3">break</span>;<br>
        }<br>
 <br>
      <span class="style4">$this-></span>i<span class="style4">++</span>;<br>
 <br>
      }  </p>
 <p><span class="style4">    $this-></span>insert($table, <span class="style4">$this-></span>fld, <span class="style4">$this-></span>val);</p>
 <p>  } </p>
 <p><span class="style4">  function</span> insert($table, $fld, $val){<br>
    $query <span class="style4">=</span> <span class="style5">"INSERT INTO $table (%s) VALUES (%s)"</span>;<br>
    $query <span class="style4">=</span> <span class="style4">sprintf</span>($query, <span class="style4">implode</span>(<span class="style5">","</span>, $fld), <span class="style4">implode</span>(<span class="style5">","</span>, $val));<br>
    $result <span class="style4">=</span> <span class="style4">mssql_query</span>($query) <span class="style3">or</span> <span class="style4">die</span>;<br>
<br>
  } </p>
 <p> }</p>
 <p>Now save this off as "class_one.php" or what ever you like. </p>
 <p> </p>
 <p><strong>We've got our class now how do we access it? </strong></p>
 <p>In order to make this as streamlined and maintenance free as possible we're going to create another file called, "submit_forms.php". This is the file that we'll call from our form action.</p>
 <p>At the top of this page we have to include our class_one.php file so we'll use the requier_once() to add it to our page.</p>
 <p><span class="style4">require_once</span>(<span class="style5">'class_one.php'</span>); </p>
 <p>We now have to find out where this page is being called from. Since we are going to use this for all of our form processing we need to know where the information came from.</p>
 <p>$from <span class="style4">=</span> <span class="style4">substr</span>(<span class="style4">strrchr</span>(<span class="style4">$_SERVER</span>[<span class="style5">'HTTP_REFERER'</span>],<span class="style5">'/'</span>),<span class="style5">1</span>); </p>
 <p>Here we are using the substr(), strrchr() and $_SERVER['HTTP_REFERER'] functions to find out what the page name is that called this "submit_forms.php" page and we are going to use that to route the user after we've inserted the data to the database. Just in case you haven't noticed we still need to identify what table in the database we're going to insert our data into. Since we'll want to make this as expandable as possible we're going to use a switch statement. </p>
 <p><span class="style3">switch</span> ($from){<br>
  <span class="style3">case</span> 'myform.php':<br>
    $table <span class="style4">=</span> <span class="style5">'registration'</span>;<br>
    $location <span class="style4">=</span> <span class="style5">'thankyou.php'</span>;<br>
   <span class="style3"> break</span>;<br>
<br>
} </p>
 <p>In this case we have identified $from to have the value of the name of our form file, "myform.php", and we've identified the table as being "registration" and now we have a location to go after the data has been entered into the database as "thankyou.php" where the user will be thanked for registering on our web site.'</p>
 <p>Now we have to call our class. First we'll create a new instance of the class.</p>
 <p>$dbinsert <span class="style4">= </span><span class="style3">new</span> dbinsert;</p>
 <p>Now we'll call our method "gotcha", and pass it the $_POST array and $table variable. </p>
 <p>$rs <span class="style4">=</span> $dbinsert<span class="style4">-></span>gotcha(<span class="style4">$_POST</span>, $table);</p>
 <p>The last thing we need to do is to actually redirect the user after their data has been entered.</p>
 <p> <span class="style4">header</span>(<span class="style5">"location:"</span>.$location); </p>
 <p>The completed file will look like this;</p>
 <p><span class="style4">require_once</span>(<span class="style5">'class_one.php'</span>); </p>
 <p>$from <span class="style4">=</span> <span class="style4">substr</span>(<span class="style4">strrchr</span>(<span class="style4">$_SERVER</span>[<span class="style5">'HTTP_REFERER'</span>],<span class="style5">'/'</span>),<span class="style5">1</span>); </p>
 <p><span class="style3">switch</span> ($from){<br>
  <span class="style3">case</span> 'myform.php':<br>
    $table <span class="style4">=</span> <span class="style5">'registration'</span>;<br>
    $location <span class="style4">=</span> <span class="style5">'thankyou.php'</span>;<br>
   <span class="style3"> break</span>;<br>
<br>
} </p>
 <p>$dbinsert <span class="style4">= </span><span class="style3">new</span> dbinsert;<br>
 $rs <span class="style4">=</span> $dbinsert<span class="style4">-></span>gotcha(<span class="style4">$_POST</span>, $table);</p>
 <p><span class="style4">header</span>(<span class="style5">"location:"</span>.$location); </p>
 <p> </p>
 <p><strong>Recap... </strong></p>
 <p>You're going to find that life is going to be much easier when you are processing your forms and entering data into a database now. All you will have to do is:</p>
 <ul>
 <li>Name your form object the same as your fields in your database</li>
 <li>Set the action of your form to "submit_forms.php"</li>
 <li>Add a case to the switch statement that names your table and give a location to send the users after their data has been entered into the database</li>
 </ul>
 <p>And that's it!!!</p>
 <p>This is a beginning to what you will need for a full production version, but it gets you going in the right direction. You will want to add datatype checking to the class so you can validate the data from the forms and check that against the datatype of the fields.., </p>
 <p>But that's a different tutorial...</p>

