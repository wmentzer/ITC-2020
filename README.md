# ITC-2020 - Web Applications Development - GoGoGnomes - Documentation

# Running Instructions
**Dependencies:** Docker community edition & Docker-compose  
> Install docker and docker-compose by following the instructions for your distribution here: https://docs.docker.com/install/  

to launch simply run `docker-compose build` & `docker-compose up` from the project directory.  
ensure port 80 is accessible on the host machine.  


<!-- DOCUMENTATION INSTRUCTIONS!
Documentation (10 points)
README file that describes the architecture/design of the systems, enumerate and explain
features of the system, show how different programs interact. If you implement new features,
clearly state them. This document also explains the database design and shows how tables are
related. Please follow this format for submission:
Web Applications Development – Team Name - Documentation
Application Deliverables and Documentation must be submitted by Sunday, April 5th @
11:59PM PST via Google Form. -->

# Documentation
## Docker/Containerization
Docker (with docker-compose) is used for containerizing all of the needed software for the site, namely the python(Django) web app and the mySQL database. This was chosen because it allows for us to quickly iterate on our code and run on multiple machines with minimal friction.  
We use docker-compose to orchestrate the software containers, creating a private network and limiting access to the containers through the docker network, with this setup the database is inaccessible to all (including the host machine) with the exception being the web application, reducing attack surface and increasing security.

## Database
### Table Relations: 
Holidays        |    | SampleCards 
----------------|----| --------------
HolidayName (PK)|    | Image_ID (PK)
HolidayID       | <- | HolidayID (FK)
|               |    | Image
|               |    | Image_Filename
|               |    | user_img_pos_x
|               |    | user_img_pos_y
|               |    | resize_img_len
|               |    | resize_img_wid

### Table Entities:
`Holidays Table` |                                       |
-----------------|---------------------------------------|
HolidayName (PK) | String identifying holiday names      |
HolidayID        | Integer identifier for holiday names  |

---

`SampleCards Table`|                                         |
-------------------|-----------------------------------------|
Image_ID (PK)  | Auto_Incrementing Integer identifier for sample Images |
HolidayID (FK) | Foreign Key pointing to `Holidays` table |
Image          | Blob holding raw image data |
Image_Filename | String for filename |
user_img_pos_x | Integer for X coordinate of template position |
user_img_pos_y | Integer for Y coordinate of template position |
resize_img_len | Integer for template image length in pixels |
resize_img_wid | Integer for template image width in pixels |
rotation       | Integer for rotating user image in degrees |
border_color    | String for image border color |


## Code:
### Django
Django is a free and open source python-based web framework that takes a lot of the hassle out of web app development, allowing for simple and fluid code development as well as rapid testing and prototyping. Django is well fleshed with featues that make for simple feature implementation such as user authentication, RSS feeds, and so much more. Along with it plentiful feature set, it is shockingly simple to create a secure site by using Django's built in protection against common vulnerabilities such as SQL Inejection, Cross-Site Scripting, Cross-Site Request Forgery, and Click-highjacking.

---

#### Django Architecture
Django's framework breaks each different page within the site into subsections called apps. These apps come preincluded with files such as models.py, urls.py, views.py, and a few others that all interact with one another to pass data across the site and determine which HTML template needs to be displayed depending on each request that is passed to the application. The views.py is where most of the processing happens such as handling POST requests from the user and making calls to the database. urls.py is a file that links the paths to each app within the site. models.py is an interesting feature that Django contains which handles all database interaction in a simple, easy to follow way. Each model is structured after a table within the database and can easily be synced and autogenerated to match the current state of the database.

---

### Bootstrap
Bootstrap is an open source toolkit for developing with HTML, CSS, and JS. A major focus of the framework is responsive, mobile-first front-end web development. Bootstrap is easy to use and speeds up the process of development by offering extensive prebuilt components, and powerful plugins built on jQuery.

---

### MySQL
We used MySQL for our database. We created two tables, one for the holidays and an ID to make them easier to search for within the database, and a second table to hold all of the images that we stored in BLOB format. BLOB format is a binary large object that can hold the variable amount, making it perfect for image files. Because of the size of the database we thought that BLOB format would be the best way to store the images because his approach means that images can be changed/added/removed without having to update multiple files and worry about broken links.

---
