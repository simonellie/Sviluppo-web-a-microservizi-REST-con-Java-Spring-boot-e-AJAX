# Sviluppo-web-a-microservizi-REST-con-Java-Spring-boot-e-AJAX
Materiale del corso UDEMY : Sviluppo web a microservizi REST con Java Spring boot e AJAX

Snippet e risorse per il corso

-----------------------------------------

## Documentazioni e tutorial ##

Istruzioni installazione JRE 1.8
https://www.java.com/it/download/help/download_options.xml

Istruzioni installazione Maven
https://maven.apache.org/install.html

Istruzioni installazione Git
https://git-scm.com/book/it/v1/Per-Iniziare-Installare-Git

Istruzioni installazione IntelliJIDEA Community Edition
https://www.jetbrains.com/idea/documentation/

Documentazione Spring Framework
https://docs.spring.io/spring/docs/current/spring-framework-reference/pdf/spring-framework-reference.pdf

Documentazione Spring Boot
https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/

Documentazione JPA
https://docs.spring.io/spring-data/jpa/docs/current/reference/pdf/spring-data-jpa-reference.pdf

Ottimo tutorial JPA
https://www.petrikainulainen.net/spring-data-jpa-tutorial/

Strategie per definire i metodi-query
https://www.petrikainulainen.net/programming/spring-framework/spring-data-jpa-tutorial-creating-database-queries-from-method-names/
https://www.petrikainulainen.net/programming/spring-framework/spring-data-jpa-tutorial-introduction-to-query-methods/

Documentazione JWT
https://stormpath.com/blog/jwt-java-create-verify
https://stormpath.com/blog/beginners-guide-jwts-in-java
https://github.com/jwtk/jjwt

Documentazione JSR-303
http://beanvalidation.org/1.0/spec/

Project Lombok
https://projectlombok.org/

Libreria criptaggio password
http://www.jasypt.org/

------------------------------------------

# Snippets o link utili: #

## Spring Initializer ##
<https://start.spring.io/>

## Struttura del DB ##

 ### nome DB: accountdb (H2 - in Memory DB) il nome non è importante ###
  
    TABLE users      (String ID, String USERNAME, String PASSWORD, String PERMISSION) 
  
    TABLE accounts   (String ID, String FK_USER, Double TOTAL) 
  
    TABLE operations (String ID, Date DATE, Double VALUE, String DESCRIPTION, String FK_ACCOUNT1, String FK_ACCOUNT2)

  ### nome DB: coupondb (in MySQL) ###
  
    TABLE coupon      ( (autogenerated int) couponid, String couponcode, String account)
  

------------------------------------------

## pom.xml di AccountMicroservice ##

    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.quicktutorials.learnmicroservices</groupId>
	<artifactId>AccountMicroservice</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>AccountMicroservice</name>
	<description>First Microservice in SpringBoot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.7.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
	    <dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-data-jpa</artifactId>
	    </dependency>
	    <dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	    </dependency>

	    <dependency>
		<groupId>com.h2database</groupId>
		<artifactId>h2</artifactId>
		<scope>runtime</scope>
	    </dependency>
	    <dependency>
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
		<optional>true</optional>
		<version>1.16.10</version>
	    </dependency>
	    <dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	    </dependency>
	    <dependency>
		<groupId>org.jasypt</groupId>
		<artifactId>jasypt</artifactId>
		<version>1.9.2</version>
	    </dependency>
	    <dependency>
		<groupId>io.jsonwebtoken</groupId>
		<artifactId>jjwt</artifactId>
		<version>0.7.0</version>
	    </dependency>
 	 </dependencies>

	 <build>
	    <plugins>
		<plugin>
	   	   <groupId>org.springframework.boot</groupId>
		   <artifactId>spring-boot-maven-plugin</artifactId>
		</plugin>
	   </plugins>
	</build>
     </project>

------------------------------------------

## pom.xml di CouponMicroservice ##

    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.quicktutorialz.learnmicroservices</groupId>
	<artifactId>CouponMicroservice</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>CouponMicroservice</name>
	<description>It consumes the rest message of account microservice</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.7.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<scope>runtime</scope>
			<version>5.1.39</version> <!-- without it gives errors-->
		</dependency>
		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
			<version>1.16.10</version>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
    </project>

------------------------------------------

## Metodi dei due Service di AccountMicroservice: ##

### LoginService: ###
	
  ```Optional(User) getUserFromDbAndVerifyPassword(String id, String password)```
  #### Richiama al suo interno: ####
       * userDao.findById(id), encryptionUtils.decrypt(pwd) 
  #### che possono entrambe lanciare: ####
       * UserNotLoggedException
	
  ```String createJwt(String subject, String name, String permission, Date date) ```    
   #### Richiama al suo interno: ####
       * JwtUtils.generateJwt(...) 	
   #### che può lanciare: ####
       * UnsupportedEncodingException
	    
   ```Map<String, Object> verifyJwtAndGetData(HttpServletRequest request)```
   #### Richiama al suo interno: ####
      * JwtUtils.getJwtFromHttpRequest(request)
   #### che può lanciare: ####
      * UserNotLoggedException
   #### Richiama anche:####
      * JwtUtils.jwt2Map(jwt)
   #### che può lanciare: ####
      * UnsupportedEncodingException 
      * ExpiredJwtException 

### OperationService: ###

   ```List<Operation> getAllOperationPerAccount(String accountId)```
   ```List<Account> getAllAccountsPerUser(String userId)```
   ```Operation saveOperation(Operation operation)```



------------------------------------------
 # Interfaccia FRONT-END #
 
 ```
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Single Page App</title>
    <!-- import of jQuery library "write less do more" -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
    <!-- import of Stackoverflow CSS -->
    <link rel="stylesheet" type="text/css" href="https://cdn.sstatic.net/Sites/stackoverflow/all.css?v=5df92b6be7e1"/>
    <!-- address: http://localhost:8094/signin.html-->
</head>
<body style="margin: 20px">

<!-- Sign in div: it will be hidden when user signs in-->
<div id="signin_section">
    <h2><b>Sign in</b></h2>
    <hr align=”left” size=”1″ width=”300″ noshade/>
    <form>
        USER ID CODE:<br />
        <input type="text" id="id" /><br />
        PASSWORD:<br />
        <input type="password" id="password" /><br />
    </form>
    <button id="submit">SUBMIT</button>
</div>


<!-- operations div: it will be activated when user signs in-->
<div id="operation_section">

    <a id="signout" style="float: right">Sign out</a>

    <h2><b>You're logged in!</b></h2>
    <hr align=”left” size=”1″ width=”300″ noshade/>
    <button id="getAccounts">GET YOUR ACCOUNTS</button>
    <br /><br />
    <hr align=”left” size=”1″ width=”300″ noshade/>

    <section id="showCoupon"> <!-- subsection for CouponMicroservice -->
        <h2>Coupons</h2>
        <p id="coupons"></p> <!-- this paragraph will be filled with the result of Ajax Call to Coupon Microservice (after login) -->
        <hr align=”left” size=”1″ width=”300″ noshade/>
    </section>

    <ul id="accountsList"></ul> <!-- list of all accounts found for the user logged. Filled with Ajax call to AccountMicroservice -->

    <!-- subsection for all the operations of the selected account-->
    <div id="operations">
        <hr align=”left” size=”1″ width=”300″ noshade/>

        <b><h3 id="operationsTitle"></h3></b>            <!-- filled with js-->
        <ul id="operationsList"></ul>                    <!-- filled with js-->

        <hr align=”left” size=”1″ width=”300″ noshade/>

        <!-- form and button to save a new Operation in H2 database through AccountMicroservice -->
        <b><h3>New Operation</h3></b>
        <form>
            <input type="text"   name="id"          id="codeInput"      placeholder="insert operation code"/>
            <input type="hidden" name="date"        id="dateInput"/>
            <input type="text"   name="description" id="descrInput"      placeholder="insert description"/>
            <input type="number" name="value"       id="valueInput"      placeholder="insert value"/>
            <input type="hidden" name="fkAccount1"  id="fkAccount1Input" value=""/>
            <input type="text"   name="fkAccount2"  id="fkAccount2Input" placeholder="insert beneficiary account"/>
        </form>
        <button id="submitNewOperation">Submit Operation</button>

    </div>

</div>

<script>
     $(document).ready(function(){
            $("#signin_section").show();         /* it shows the sign in and hide the operation sections */
            $("#operation_section").hide();
            ChangeUrl("Signin","/signin.html");  /* it sets the new url when the page is loaded */
     });
      /* --------  functions  --------- */
       /* function used to get the jwt from cookies after having saved it, for later async ajax calls to microservices */
       function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2)
                return parts.pop().split(";").shift();
       }
        /* function used to change the text of the url giving the impression we're changing page */
        function ChangeUrl(title, url) {
            if (typeof (history.pushState) != "undefined") {
               var obj = { Title: title, Url: url };
               history.pushState(obj, obj.Title, obj.Url);
            } else {
               alert("Browser does not support HTML5.");
            }
        }
         /* --------  on click events  -------- */
         /* sign in submit function */
        $("#submit").click(function(e) {
            e.preventDefault();
            $.ajax({                                                        /* Ajax call to AccountMicroservice for login */
               url: 'http://localhost:8094/login',
               type: "POST",
               data: {
                  id: $("#id").val(),
                  password: $("#password").val()
               },
               success: function (data, status, xhr) {
                  $("#signin_section").hide();                              /* it hides sign in section and shows operation section */
                  $("#operation_section").show();
                  $("#showCoupon").hide();
                  $("#operations").hide();
                  console.log(data);
                  ChangeUrl("Operations","/operations.html");               /* it changes url after sign in */
                  document.cookie = "jwt=" + xhr.getResponseHeader("jwt");  /* it saves in cookies the received token */
               },
               error: function(result) {
                  alert("Sign in failed!");
                  console.log(result);
               }
            });
        });
        /* sign out submit function */
        $("#signout").click(function(e) {
            e.preventDefault();
            document.cookie = "jwt=;expires=Thu, 01 Jan 1970 00:00:01 GMT;";        /* it cancels jwt from cookies */
            $("#accountsList").empty();
            $("#operationsTitle").empty();                                          /* it empties all lists and info */
            $("#operationsList").empty();
            $("#operations").hide();
            $("#signin_section").show();                                            /* it hides operations and shows sign in section */
            $("#operation_section").hide();
            alert("You're logged out!");
            ChangeUrl("Signin","/signin.html");                                     /* it changes url again to signin.html */
        });
        /* on click of #getAllAccounts button */
        $("#getAccounts").click(function(e) {
            e.preventDefault();
            /* first Ajax call */
            $.ajax({                                                                /* Ajax call to AccountMicroservice for accouns */
               url: 'http://localhost:8094/accounts/user',
               type: "POST",
               success: function (data, status, xhr) {
                  console.log(data);
                  $("#accountsList").empty();                                       /* Reset info */
                  $("#operationsTitle").empty();
                  $("#operationsList").empty();
                  $("#showCoupon").show();
                  $("#operations").hide();
                  jQuery.each(data.response, function(i, val) {
                     /* with the response it fills #accountList */
                     $("#accountsList").append("<li><h3><a id='" + val.id + "' class='accountButton' title='Go to operations'>Account " + val.id+ "</a></h3></li>");
                  });
               },
               error: function(result) {
                  alert("Error accessing accounts!");
                  console.log(result);
               }
            });
            /* second Ajax call */
            $.ajax({                                                                /* Ajax call to CouponMicroservice for coupons */
               url: 'http://localhost:8095/findCoupon',
               type: "POST",
               data: {
                  jwt: getCookie("jwt")                                             /* it gets jwt from cookies and send as body POST */
               },
               success: function (data, status, xhr) {
                  console.log(data);
                  $("#coupons").empty();
                  $("#coupons").append(data.response);                              /* it resets and fills #coupons section with result */
                  console.log("Data.response: " + data.response);
               },
               error: function(result) {
                  alert("Error accessing CouponMicroservice!");
                  console.log(result);
               }
            });
        });
        /* onclick on the choosen Account */
        //get operation for one account
        $(document).on('click', '.accountButton', function (e) {
            e.preventDefault();
            $("#operationsTitle").text("Operations for account number " + e.target.id);     /* it sets the title of the section */
            $.ajax({                                                                        /* Ajax call to AccountMicroservice */
               url: 'http://localhost:8094/operations/account/' + e.target.id,
               type: "GET",
               success: function (data, status, xhr) {
                  console.log(data);
                  $("#operationsList").empty();
                  jQuery.each(data.response, function(i, val) {
                     /* with the response it fills #operationsList */
                     $("#operationsList").append("<li><h4>COD: " + val.id + ", DESCR: " + val.description + ", VALUE: " + val.value + "</h3></li>");
                  });
               },
               error: function(result) {
                  alert("Error!");
                  console.log(result);
               }
            });
            $("#operations").show();                        /* it shows the sub section of the operations */
            $("#codeInput").val("");                        /* it empties the form to save a new operation */
            $("#descrInput").val("");
            $("#valueInput").val("");
            $("#fkAccount1Input").val(e.target.id);
            $("#fkAccount2Input").val("");
        });
        /* onclick to save a new operation in database */
        $("#submitNewOperation").click(function(e) {
            e.preventDefault();
            if($("#codeInput").val() != "" && $("#valueInput").val() != ""){      /* having a valid value to submit */
               $.ajax({
                  url: 'http://localhost:8094/operations/add',                  /* Ajax call to AccountMicroservice to save operation */
                  type: "POST",
                  data: {
                     id:          $("#codeInput").val(),                        /* it gets the values from the HTML5 form to send in req. */
                     value:       $("#valueInput").val(),
                     description: $("#descrInput").val(),
                     fkAccount1:  $("#fkAccount1Input").val(),
                     fkAccount2:  $("#fkAccount2Input").val()
                  },
                  success: function (data, status, xhr) {
                     alert("Success!");
                     $("#codeInput").val("");                        /* it empties the form to save a new operation */
                     $("#descrInput").val("");
                     $("#valueInput").val("");
                     $("#fkAccount1Input").val(e.target.id);
                     $("#fkAccount2Input").val("");
                     $("#operations").hide();
                  },
                  error: function(result) {
                     alert("Error!");
                     console.log(result);
                  }
               });
            }else{
                alert("Insert a valid operation!");
            }
        });
</script>


</body>
</html>
 
 ```



