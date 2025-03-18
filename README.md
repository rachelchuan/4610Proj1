
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

Data Model Explanation: Our model's most center-based entity is our Gym entity. The Gym entity represents each of Dawg Fitness's distinct gym locations across the United States. Its attributes include a unique identifier, location, phone number, and email. Since our gym table is our central point, we have multiple relationships stemming from the Gym entity: Equipment, Staff, and Members.

Equipment is directly related to Gyms, as equipment and resources are the main points of operation in gyms. A unique ID number is assigned to each piece of equipment, along with the name, status, and age of each piece. Equipment belongs to only one gym, so the gymID, which identifies the gym where the equipment is located, is present for each piece of equipment. Although equipment can only belong to one gym, a gym can have multiple pieces of equipment representing a one-to-many relationship.

Our Staff entity tracks all non-trainer employees within our organization. To keep up with each individual staff member, we have assigned them a unique ID number. Other important information includes name, date of birth, contact information, position, salary, and the duration of their employment at Dawg Fitness. Each staff member is only able to work for one gym, hence the gymID being present for each row of staff members. Since gyms require many staff members to operate, this results in a one-to-many relationship.

Our Members table has a one-to-many relationship with the Gym table because our gym locations can be home to many members, but each member belongs to only one Dawg Fitness location. We assign a unique identifier to each member and track basic information such as name, personal details, contact information, and address. Although the Members table is not the central entity, it has the most relationships with other tables. There is a relationship with MembershipPlans that identifies which of our multiple membership options a member is under; a member can have one plan, while a plan can have multiple members. GymID is also present within the table to identify which gym our members are associated with. Members have the option to sign up for group classes taught by our trainers. Since members can sign up for multiple classes and classes can have multiple members, the associative entity "ClassRegistration" connects the two. Additionally, each member has their own payment information associated with their account.

Dawg Fitness offers a variety of membership plans to fit the different needs of our members. Each plan requires a unique identifier to differentiate between plans and their details. Each plan is named and assigned a monthly fee, along with a description of the accessibility offered by the plan.

Regarding the Payments entity, each payment requires a unique identifier and tracks the associated fee a member has paid for gym access on that date. The member's payment method used is also recorded in this table along with the date they submitted the payment. MemberID is present within the table to associate each payment with a single member, but members make multiple payments, as there are monthly dues.

Though our trainers operate under the name "Dawg Fitness," they are a separate entity functioning independently. Like staff members, trainers have an ID number to track each individual trainer. Necessary details include name, salary, tenure at Dawg Fitness, area of expertise, and contact information. Trainers are associated with both Members and Classes in a many-to-many relationship. Trainers can have multiple one-on-one sessions with different members, recorded in the PrivateSessions table. Since trainers can teach multiple classes and each class type can have multiple trainers, we use the associative entity "TrainerSchedule."

Our Classes table is straightforward, tracking each class by classID, class name, the room where the class is taught, and the maximum number of members that can enroll. The Classes table is related to multiple tables: TrainerSchedule, ClassRegistration, and Surveys. Each class can have multiple Survey entries, registrations, and TrainerSchedule associations.

To track member satisfaction and their experience with classes, we created the Surveys table. Each survey requires a unique primary key, which is a survey ID number. To track recent trends in our classes, we include a date-submitted attribute. To assess satisfaction, we implement a 1-5 rating system. The classID foreign key is present to attribute ratings and feedback to each class.

ClassRegistration is one of our three associative entities. Many members can take many different classes, thus this many-to-many relationship results in an associative entity. The composite primary key is made up of classID and memberID as primary keys to track which classes and members are associated with one another. ClassID is also a foreign key in that it references the Class table, to store classes taken by members, and memberID is also a foreign key that references the Member table, to store members who take classes. RegistrationID is the final primary key, to represent each unique case of a member signing up for a class. The class name is also present in this table to easily signify which class a member has been registered for. The date of the class is also present as members can take the same class many times over various dates.

TrainerSchedule is the associative entity linking trainers to the classes they teach. Many trainers can teach many classes. Similar to the ClassRegistration table, there are three primary keys, two of which originate from other tables. The trainerID and classID make up the composite primary key to match trainers with the classes that they teach. These two attributes are also foreign keys in which trainerID references the Trainer table to identify which trainer is teaching a class, and classID references the Class table to determine which class is within the trainer's schedule. The third primary key, scheduleID, represents each unique case of a trainer teaching a class. The date of a class they teach is also represented as trainers can teach the same class many times over many dates.

PrivateSessions is designed for members interested in one-on-one training with a trainer. Many members can have many private sessions with trainers. The composite primary key originates from the Members table with memberID and the Trainers table with trainerID, allowing each session to track which member is working with which trainer. Again, these two attributes are foreign keys that reference the Members table and the Trainers table. The PrivateSessionID is a table-specific primary key that represents each unique pairing of a member and the trainer they are to have a one-on-one session with. Lastly, the date of the private session is included, as members can have many different private sessions with the same trainer.

Data Model: ![PNG image](https://github.com/user-attachments/assets/0ff63217-db8d-4775-9340-358eb8646225)

Data Dictionary: <img width="880" alt="Screenshot 2025-03-18 at 3 13 55 PM" src="https://github.com/user-attachments/assets/e884bd6c-43aa-4198-a2cc-ab6b9f2b3f62" />
<img width="878" alt="Screenshot 2025-03-18 at 3 14 20 PM" src="https://github.com/user-attachments/assets/4a1d623c-aefb-4879-9b49-b1565d722005" />


Query 5: Retrieves the total number of members per membership plan and sorts in descending order. This query organizes the number of members in each membership plan and can be used to send emails that specifically cater to the type of membership they have.
<img width="807" alt="423557637-7cba7469-c76b-4a49-a9be-178404da4726" src="https://github.com/user-attachments/assets/e7ecf9b8-40fa-45a9-939e-bb78e6df916f" />

Query 6: Finds members who have never signed up for a class or a private session. This query finds gym members that have not signed up for a class or session, this informaton can be used to send emails to members to encourage them to sign-up.
<img width="704" alt="423557732-c1f994ce-d061-417d-a8e7-0d02e233b5f8" src="https://github.com/user-attachments/assets/73c32b06-6c0b-43c5-bb0f-ff5232d63248" />

Query 7: Find all the equipment in a specific gym. This query organizes the equipment for gym 6, which can be used to keep track of the equipment.
<img width="456" alt="423557791-ff74a3b9-5a39-47f3-8ab8-ae328bc468ec" src="https://github.com/user-attachments/assets/ad9cef66-90fd-4cf8-89f7-fa9a9224a911" />



