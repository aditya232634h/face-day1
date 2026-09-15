{
name:"Aditya Singhal",

age:21,

email:"fraud.com",

phone:98975xxxxx,
cgpa:9.0,

skills:\["C","Java","C++"],  ==> skills \["python","MYSQL","NOSQL"] ---> array objects

address:{                       address:{ --------------> embedded objects
city:"Jaipur",                     city;"vadodra",  DB name creation

zipcode: 317311,                   state:"Gujrat",  (1) use ("Poornima")

state:"Rajasthan",                 pincode:146711,  (2) Collesction creation/Tb creation

}                                   }                   db.createCollection("Student")
}

my sql       NO-SQL

database     Database

tables       collections

rows         document

colms        files

|**MY-*SQL***|**NO-*SQL***|
|-|-|
|Database|Database|
|Tables|Collections|
|Rows|Document|
|Colm's|Files|

&#x20;

**DB name creation** 



(1) use ("Poornima")

(2) Collesction creation/Tb creation
db.createCollection("Student")

(3). db.student.insertOne





Use("Ecommerce")



db.createCollection("Products")



db.Products.insertOne({



Name: "Aditya phone",



&#x20;

Category: "Smartphone",



Brand: "one plus",



Price: 29999,



Stock: 25,



Rating: 4.6,



Features: \["5G", "Face ID", "OLED Display", "Wireless Charging"],



Details: (



Color: "Black",



Storage: "256GB",



RAM: "8GB",



Warranty: "1 Year",



Country: "India"



})



}







\*\*use(”Ecommerce”);\*\*



\*\*db.createCollection(”Products”)\*\*



\*\*db.Products.insertone({\*\*



\*\*name: “Perfume”,\*\*



\*\*price: “2000”,\*\*



\*\*Rating: 3.5/5 ,\*\*



\*\*});\*\*

