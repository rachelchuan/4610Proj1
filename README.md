
# 4610Proj1
4610 Group Project 1: Gym Database

Team Members

Sophie Naustdal https://github.com/sophienaustdal/MIST4610GroupProject.git
Rachel Chuan https://github.com/rachelchuan/4610Proj1
Riley Cook https://github.com/rileyacook/4610Proj1.git
Chidera Nwosu
Coleman Vaughn

Scenario Description:

Our company, Dawg Fitness, is a large fitness enterprise with multiple gym locations across the United States, with each gym serving as the core of our operations. While all gyms operate under Dawg Fitness, each location offers tailored services to meet the diverse needs of its members. Our goal is to create a relational database that connects all relevant entities across the business. This database will manage key information such as gym details, member profiles, trainers, equipment inventory, class schedules, membership plans, payment history, and survey feedback. By leveraging this data, we aim to structure queries that provide valuable insights for improving and growing Dawg Fitness' operations.

Data Model Explanation: Our model's most center-based entity is our Gym entity. The Gym entity represents a unique identifier, location, phone number, and email. Since our gym table is our central point, we have multiple relationships stemming from the Gym entity: Equipment, Staff, and Members.

Equipment is directly related to Gyms, as equipment and resources are the main points of operation in gyms. A unique ID number is assigned to each piece of equipment, along with the name, status, and age of each piece. Equipment belongs to only one gym, so the gymID, which identifies the gym where the equipment is located, is present for each piece of equipment. Although equipment can only belong to one gym, a gym can have multiple pieces of equipment.

Our Staff entity tracks all non-trainer employees within our organization. To keep up with each individual staff member, we have assigned them a unique ID number. Other important information includes name, date of birth, contact information, position, salary, and the duration of their employment at Dawg Fitness. Each staff member is only able to work for one gym, hence the gymID being present for each row. Since gyms require many staff members to operate, this results in a one-to-many relationship.

Our Members table has a one-to-many relationship with Gym because our gym locations can be home to many members, but each member belongs to only one Dawg Fitness location. We assign a unique identifier to each member and track basic information such as name, personal details, contact information, and address. Although the Members table is not the central entity, it has the most relationships with other tables. There is a relationship with MembershipPlans that identifies which of our multiple membership options a member is under; a member can have one plan, while a plan can have multiple members. GymID is also present within the table to identify which gym our members are associated with. Members have the option to sign up for group classes taught by our trainers. Since members can sign up for multiple classes and classes can have multiple members, the associative entity "ClassRegistration" connects the two. Additionally, each member has their own payment information associated with their account.

Dawg Fitness offers a variety of membership plans to fit the different needs of our members. Each plan requires a unique identifier to differentiate between plans and their details. Each plan is named and assigned a monthly fee, along with a description of the accessibility offered by the plan.

Regarding the Payments entity, each payment method requires a unique identifier and tracks the associated fees a member needs to pay for gym access. Card information is recorded to finalize and authorize payments. MemberID is present within the table to associate each payment method with a single member, but members can have multiple forms of payment.

Though our trainers operate under the name "Dawg Fitness," they are a separate entity functioning independently. Like staff members, trainers have an ID number to track each individual trainer. Necessary details include name, salary, tenure at Dawg Fitness, and area of expertise. Trainers are associated with both Members and Classes in a many-to-many relationship. Trainers can have multiple one-on-one sessions with different members, recorded in the PrivateSessions table. Since trainers can teach multiple classes and each class type can have multiple trainers, we use the associative entity "TrainerSchedule."

Our Classes table is straightforward, tracking each class by its primary key, classID, the room where the class is taught, and the maximum number of members that can enroll. The Classes table is related to multiple tables: TrainerSchedule, ClassRegistration, and Surveys. Each class can have multiple Survey entries, registrations, and TrainerSchedule associations.

To track member satisfaction and their experience with classes, we created the Surveys table. Each survey requires a unique primary key, which is an ID number. To track recent trends in our classes, we include a date submitted attribute. To assess satisfaction, we implement a 1-5 rating system. The classID foreign key is present to attribute ratings and feedback to each class.

ClassRegistration is one of our three associative entities. The primary keys are also the foreign keys classID and memberID to track which classes and which members are associated with it. Another primary key, specific to ClassRegistration, registrationID, is present to allow multiple members to register for multiple classes instead of just one. We also believe naming each class is important.

TrainerSchedule is the associative entity linking trainers to the classes they teach. Similar to the ClassRegistration table, there are three primary keys, two of which originate from other tables. The trainerID is necessary to identify which trainer is teaching a class, and classID determines which class is within the trainer's schedule. The third primary key, scheduleID, ensures that trainers can teach multiple classes rather than just one.

PrivateSessions is designed for members interested in one-on-one training with a trainer. PrivateSessions is unique in that all attributes are primary keys. Two of the three primary keys originate from the Members table (memberID) and the Trainers table (trainerID), allowing each session to track which member is working with which trainer. The PrivateSessionID is a table-specific primary key that ensures multiple sessions can exist for each trainer and/or member.

Data Model: ![PNG image](https://github.com/user-attachments/assets/0ff63217-db8d-4775-9340-358eb8646225)

Data Dictionary: <img width="880" alt="Screenshot 2025-03-16 at 5 31 42 PM" src="https://github.com/user-attachments/assets/06af4589-d64b-431c-84ef-5fdb1719f4b7" />
<img width="879" alt="Screenshot 2025-03-16 at 5 35 22 PM" src="https://github.com/user-attachments/assets/62d0c915-16a4-41ed-81f0-544b8fb2d2d5" />

2 Complex Queries:
#1 #Retrieve the total number of members per membership plan and sort in descending order: CALL TP_Q5(); 
#2 #Retrieve trainers who have not conducted any private sessions or scheduled any classes: CALL TP_Q6();
1 Simple Query: 
#3 #Find all equipment in a specific gym: CALL TP_Q7();
