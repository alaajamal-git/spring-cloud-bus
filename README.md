# spring-cloud-bus

In this project, we set up spring-bus to make our config-server update properties on demand and its clients(services) update dynamically.

Configuration steps:

setup spring-cloud-starter-bus-amqp and spring-boot-starter-actuator maven dependencies and setup AMQP server (to send and schedule messages between Config-Server and its clients). AMQP runs on port 5672 and graphical interface on port 15672.

spring-boot-starter-actuator used to get the post request to make the Config-Server re-read the remote properties file. spring-bus to send updated properties to the clients throughout the AMQP server. All clients should have spring-cloud-starter-bus-amqp dependency.

Run example steps:

1. post : http://10.3.14.48:8011/users-ws/users
   body : 
   <UserResposeModel>
    <firatname>Ziad</firatname>
    <lastname>Jamal</lastname>
    <email>alaajamal470@gmail.com</email>
    <userId>2eeaec6f-4092-46d1-ba23-b84ce1006d97</userId>
   </UserResposeModel>
   
2. post : http://10.3.14.48:8011/users-ws/users/login
   body :
    {
    "email":"alaajamal470@gmail.com",
    "password":"154454588"
    }
3. get : http://localhost:8011/users-ws/users/status/check
   Header :
   Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIyZWVhZWM2Zi00MDkyLTQ2ZDEtYmEyMy1iODRjZTEwMDZkOTciLCJleHAiOjE1OTUyNjk5ODN9.cIZOTV8gfZtQTa0_odhkrN2TFPvbYCTD8WbwyIPQKmg
   this header was taken from the successful login request in step2.
   
4. change the "token.date.expired" on your private git account and send the refresh request to Config-Server:
post : http://localhost:8012/actuator/bus-refresh. Re-do the step 2 and 3 you will see the new value of your property.
    
