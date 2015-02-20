FashionUnited Developers
========================

Documentation
-------------
The Fashionunited platform connects your website or application with the worldwide fashion conversation happening on Fashionunited.

Jobs API (push) - XML Feeds
---------------------------
Web Services To Post Jobs to FashionUnited Central Job-Board

### Introduction
FashionUnited uses API Post the job over http post, to post the job we prefer URL encoded XML format data (the structure of the XML is explained below). We use 2 Method in our API. to use this API username and password is mandatory, username and password is provided by Fashionunited so one can request Fashionunited to get a username and password, for a new username and password the client need to provide us an email address which will be associated with API call.

Create – to create single/multiple Jobs at a time.
Read - Not supported
Update - Not supported
Delete – to delete single/multiple jobs at a time.
Parameters :  The parameter are pre defined and must be sent on each request while requesting API call. 

xml – XML file in URL encoded format.
method – method to call defined function (add/delete).
submit – this parameter must have value as submit.

### XML structures

Adding a job:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<job>
    <username>info@fashionunited.com</username>
    <password>fashion123</password>
    <sender>name of sender</sender>
    <item>
   	 <cust_job_id>00001</cust_job_id>
   	 <published>1</published>
   	 <job_title><![CDATA[Design Assistant]]></job_title>
   	 <company_name><![CDATA[FashionUnited]]></company_name>
   	 <location><![CDATA[Amsterdam]]></location>
   	 <country>172</country>
   	 <cname><![CDATA[Dennis Houttuin]]></cname>
   	 <cemail><![CDATA[job_apply@yourcompany.com]]></cemail>
   	 <cphone>0031 2012345678</cphone>
   	 <description><![CDATA[Here you will have a description of the job]]></description>
   	 <htapply><![CDATA[Broadbean Job]]></htapply>
   	 <category>49</category>
   	 <expiry_date>2011-12-31 00:00:00</expiry_date>
   	 <salary_currency>EUR</salary_currency>
   	 <salary>25000</salary>
    </item>
    <item>
   	 <cust_job_id>00002</cust_job_id>
   	 <published>1</published>
   	 <job_title><![CDATA[Design Assistant]]></job_title>
   	 <company_name><![CDATA[FashionUnited]]></company_name>
   	 <location><![CDATA[Amsterdam]]></location>
   	 <country>172</country>
   	 <cname><![CDATA[Dennis Houttuin]]></cname>
   	 <cemail><![CDATA[job_apply@yourcompany.com]]></cemail>
   	 <cphone>0031 2012345678</cphone>
   	 <description><![CDATA[<a href="http://google.com"><img src="http://static.php.net/www.php.net/images/caret-l.gif" alt="&lt;" width="11" height="7">mysql_client_encoding</a>]]></description>
   	 <htapply><![CDATA[Broadbean Job]]></htapply>
   	 <category>49</category>
   	 <expiry_date>2011-12-31 00:00:00</expiry_date>
   	 <salary_currency>EUR</salary_currency>
   	 <salary>25000</salary>
    </item>
</job>
```


| XML Nodes       | Details                                                                 | Data Type                      | Data Size                                       |
|-----------------|-------------------------------------------------------------------------|--------------------------------|-------------------------------------------------|
| username        | Username provided by FashionUnited to API User                          | Character                      | 200 characters                                  |
| password        | Password Provided by FashionUnited to API User                          | Character & special Characters | 100 characters                                  |
| sender          | Sender Name                                                             | Characters                     | 150 Characters                                  |
| cust_job_id     | Customer job ID which must be unique                                    | Integer                        | 40                                              |
| published       | Status to publish or unpublish                                          | Enum                           | 1 or 0 (1 to publish and 0 to unpublish)        |
| job_title       | Title of the job                                                        | Characters                     | 255 Characters                                  |
| company_name    | Name of the company offering the job                                    | Characters                     | 255 characters                                  |
| location        | Job location (City or area)                                             | Character                      | 255 Characters                                  |
| country         | Country of job                                                          | Integer                        | As defined by fashionunited                     |
| cname           | Contact name of concern person for the job                              | Characters                     | 255 characters                                  |
| cemail          | Contact email                                                           | Characters                     | 255 characters                                  |
| cphone          | Contact phone number                                                    | Integers                       | 255 characters                                  |
| description     | Jobs description along with images if needed allowed in HTML format     | Text                           | 2500 Characters                                 |
| htapply         | Ho to apply for the job (any reference or any URL to apply for the job) | Characters                     | 255 Characters                                  |
| category        | Category of jobs                                                        | Integer                        | Id as per decided and declared by fashionunited |
| expiry_date     | Expiry date for the job if not set default is 8 weeks                   | Date time                      | 31/12/2011 00:00:00                             |
| salary_currency | Salary curreny                                                          | Characters                     | 10 characters                                   |
| salary          | Salary in numbers                                                       | Integer                        | 10 characters                                   |



Deleting a job(s)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<job>
    <username>info@fashionunited.com</username>
    <password>fashion123</password>
    <sender>Broadbean/logicmelon</sender>
    <item>
   	 <cust_job_id>00002</cust_job_id>
   	 <published>1</published>
    </item>
</job>
```


### Procedure

To post the XML file you need to post it on URL with above format

http://www.fashionunited.com/my/jobpost/index.php ⇒ production Url let us know before testing

I am attaching the job post form PHP coding which you can refer to understand the logic beside that 2 XLS sheets are attached for country table reference and category reference.



### Error Handling

Method Cannot be blank (if add or delete method is missing from post).
submit Cannot be blank (if submit is blank).
xml string Cannot be blank (if XML string posted is blank).
!! A job has been posted successfully !! (success message after job post with job id,  country, name of sender as in json string)
XML is in incorrect format (if XML is not formated like explained in documentation)
Problem in connection (general failure like server not responding etc our developer will receive information automatically and they will take care of it)
Username not found (if the XML is posted without Username)
Password does not match our records (if wrong password is entered)
!! This country code is not supported by FashionUnited yet supported countries codes are (GBR, USA, RUS, ITA, CHE, IND, FRA, ESP, NLD, DEU, BEL, AUT) !! (if country code other then these countries are sent)
!! Job ID must be Integer !! (the cust_job_id sent by client must be integer type data)
!! expiry_date field is not in proper format please have dates in 0000-00-00 00:00:00 format !! (if expiry_date format send is wrong).
!! Please enter a valid email address !! (if wrong email id entered in cemail field)
!! salary field must be Integer !! (if salary field is not numerical).
Problem in deleting the job at (portal name), this shows delete request is not gone well so contact fashionunited.


Jobs non-API (pull) - XML Feeds
-------------------------------
### Introduction

FashionUnited’s Non API service provides a full suite of real-time, highly available Jobboard transactions. This service opens the door to FashionUnited’s infrastructure and enables you to execute a wide variety of jobboard transactions empowering you to make the best decisions and interact with FashionUnited. We are constantly reviewing our suite of services for completeness, accuracy and usefulness.




FashionUnited for Websites
--------------------------
Fashionunited for Websites is a suite of embeddable widgets, buttons, and client-side scripting tools to integrate Fashionunited and display jobs on your website or JavaScript application, including the Universal Job Apply Button, Embedded Jobs, and Embedded Job Timelines.

###Embedded Job API

With this API one can easily display jobs on ones own website while the jobs are being hosted by us. This saves people from having to setup an infrastructure to handle vacancies and also generates far more traffic than publishing jobs on their own website. 

Some examples: [Hugo Boss](http://www.fashionunited.com/jobs/hugoboss/), [Gerry Weber](http://www.fashionunited.com/jobs/gerryweber/), [GAB](http://www.fashionunited.com/jobs/gab/), [Men at Work](http://www.fashionunited.com/jobs/menatwork/), [JD Sports NL](http://www.fashionunited.com/jobs/jdsportsnl/), [IKKS](http://www.fashionunited.com/jobs/ikks/), [Witteveen](http://www.fashionunited.com/jobs/witteveen/), [Sergent Major](http://www.fashionunited.com/jobs/sergentmajor/), [Derhy](http://www.fashionunited.com/jobs/derhy/), [Eric Bompard](http://www.fashionunited.com/jobs/ericbompard/)

To place this API in your own website, all you need to do is paste one single line of code on any page or site you want for it to display. It's in fact easier than embedding a YouTube video.


###Employer Branding Page

In order to signify a brand name from a company, we developed the Employer Branding Page. Here you can show people what it is like working for a company, without interfering with the marketing for collections for that company. Also other information about the company, such as its different labels, statistics, history, video or images, it's all possible.

Examples: [Adidas](http://www.fashionunited.co.uk/adidas), [Veldhoven](http://www.fashionunited.nl/veldhovengroup/), [Peek & Cloppenburg](http://www.fashionunited.de/pc%11Peek%11Cloppenburg/), [Grupo Cortefiel](http://www.fashionunited.es/grupo-cortefiel).

Images supplied need to be high resolution 300dpi and can be supplied in JPG, PDF, TIFF, GIF or BMP format. 


###Banners
We deploy banners in various image and file sizes. Here's an overview:

| banner name      | format (px)        | max. file size (kB)  | 
|------------------|--------------------|----------------------|
| Work for Brands  | 150 x 50           | 20                   |
| Calendar         | 234 x 60           | 30                   |
| Top Half         | 468 x 90           | 60                   |
| Leaderboard      | 728 x 90           | 60                   |
| Top Full         | 970 x 90           | 60                   |
| Medium Rectangle | 300 x 250          | 60                   |
| Half Page        | 300 x 600          | 60                   |
| Wallpaper   	   | 260 x 1200         | 60                   |

File types supported for primary files: GIF, HTML5, HTML, JPEG, JPG, PDF, PNG, and TXT. A destination URL must also be provided.

###Sponsored Messages
Sponsored Message texts need to be supplied in a .txt or Word file. Please mark the TITLE and, if applicable, LINKS clearly (including target URL). Image size: at least 800 x 500 px, 72 dpi, but preferably larger than that. Definitely NOT smaller.

[aantal  / aantal images / aanlever deadlines (evt. nieuwsbrief?)]

###Logo
The logo makes the link between fashion and uniting everyone working within the industry, which of course the name FashionUnited embodies. It is displayed in a stylish and modern font, with an emphasis on the word United by making that bold.

The normal logo with FASHIONUNITED spelled together is preferred. But in terms of size, this is sometimes suboptimal, 
therefore the square version created. It must always be accompanied by the circular logo with the F in it, or favicon.

In principle, the logo will only be used in black or in white. The background color or the image the logo is placed upon may vary in color, so obviously it depends on that whether the white or black logo is to be used. 

(logo placement, fonts used, download link?)








<!---


OAuth
=====
Use our OAuth endpoints to connect users to Fashionunited and send secure, authorized requests to the Fashionunited API.

REST APIs
=========
The REST APIs provides programmatic access to read and write Fashionunited data. Author a new Job, read job data, and more. The REST API identifies Fashionunited applications and users using OAuth; responses are available in XML.

-->
