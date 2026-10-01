 # College-Management-System
1. Project Overview

The College Management System is a Salesforce Administration project
used to manage common college activities in one Salesforce application.

# Business Flow

Department → Students → Enrollments ← Courses → Attendance → Fee Payments

The project uses Salesforce relationships to connect the records and provides administration, validation, security, automation, data management, reporting, and dashboard capabilities.

# The project manages:

Students

Departments

Courses

Faculty

Enrollments

Attendance

Fee Payments

 Salesforce Admin Concepts Demonstrated

This project demonstrates:

Custom Objects

Custom Fields

Custom App

Lightning Experience

Console Navigation

Schema Builder

Lookup Relationship

Master-Detail Relationship

Roll-Up Summary

Formula Fields

Text Fields

Text Area

Rich Text Area

Picklists

Multi-Select Picklists

Global Value Sets

Dependent Picklists

Page Layouts

Record Types

Validation Rules

Duplicate Rules

Matching Rules

Users

Profiles

Permission Sets

Tasks

Events

Log a Call

Global Actions

Object-Specific Actions

Email Templates

Record-Triggered Flow

Data Import Wizard

Reports

Dashboards

# 2. Main Business Flow

Department
   |
   +---- Students
   |
   +---- Courses
   |
   +---- Faculty

Student ---- Enrollment ---- Course
   |
   +---- Attendance ---- Course / Faculty
   |
   +---- Fee Payment

3. Custom Objects

Object        Purpose

Department    Stores department information
Student       Stores student information
Course        Stores courses offered by the college
Faculty       Stores faculty information
Enrollment    Connects students with courses
Attendance    Records student attendance
Fee Payment   Records student fee payments

# 4. Department

Fields

Field                    

Department Name                 


Department Code          


HOD Name                 


Department Email         


Phone                    


Department Status   Picklist    Active / Inactive

# 5. Student

Fields

Field                   Data Type               Example

Student ID              Auto Number             STU-0001

First Name              Text                    Rahul

Last Name               Text                    Kumar

Email                   Email                   rahul@gmail.com

Phone                   Phone                   9876543210

Date of Birth           Date                    10-05-2005

Gender                  Picklist                Male / Female / Other

Department              Lookup                  Computer Science

Admission Year          Number                  2026

Student Status          Picklist                Active / Graduated /
Suspended /
Discontinued

Address                 Text Area               Nellore

# 6. Course

Fields

Field           Data Type   Example

Course Name     Text        Salesforce Administration
Course Code     Text        SF101
Department      Lookup      Computer Science
Credits         Number      4
Course Type     Picklist    Core / Elective / Practical / Project
Course Status   Picklist    Active / Inactive

# 7. Faculty

Fields

Field                   Data Type               Example

Faculty Name            Text                    Kumar

Employee ID             Text                    EMP001

Email                   Email                   kumar@college.com

Phone                   Phone                   9876543210

Department              Lookup                  Computer Science

Designation             Picklist                Professor / Associate
Professor / Assistant
Professor / Lecturer

Joining Date            Date                    01-06-2025

Faculty Status          Picklist                Active / Inactive

8. Enrollment

The Enrollment object records which courses a student has enrolled
in.

Fields

Field               Data Type       Example

Enrollment Number   Auto Number     ENR-0001
Student             Master-Detail   Rahul Kumar
Course              Lookup          Salesforce Administration
Enrollment Date     Date            01-07-2026
Semester            Picklist        1--6
Academic Year       Text            2026-27
Status              Picklist        Enrolled / Completed / Dropped
Marks               Number          75
Grade               Picklist        A / B / C / D / F
Result              Formula         Pass / Fail

Result Formula

IF(Marks__c >= 40, "Pass", "Fail")

Example:

Marks = 75 → Pass

Marks = 30 → Fail

9. Attendance

The Attendance object records attendance for a student in a course.

Fields

Field               Data Type     Example

Attendance Number   Auto Number   ATT-0001
Student             Lookup        Rahul Kumar
Course              Lookup        Salesforce Administration
Faculty             Lookup        Kumar
Attendance Date     Date          30-09-2026
Attendance Status   Picklist      Present / Absent / Leave
Remarks             Text Area     Attended full class

10. Fee Payment

The Fee Payment object records payments made by students.

Fields

Field                   Data Type               Example

Payment Number          Auto Number             PAY-0001

Student                 Master-Detail           Rahul Kumar

Payment Date            Date                    30-09-2026

Amount                  Currency                25000

Payment Type            Picklist                Tuition Fee / Exam Fee
/ Library Fee / Hostel
Fee / Other

Payment Status          Picklist                Paid / Pending / Failed

Academic Year           Text                    2026-27

Transaction ID          Text                    TXN12345

11. Relationships

Relationship            Type            Purpose

Department → Student    Lookup          Assign students to departments
Department → Course     Lookup          Assign courses to departments
Department → Faculty    Lookup          Assign faculty to departments
Student → Enrollment    Master-Detail   Store student enrollments
Course → Enrollment     Lookup          Connect enrollment to course
Student → Attendance    Lookup          Store student attendance
Course → Attendance     Lookup          Connect attendance to course
Faculty → Attendance    Lookup          Connect attendance to faculty
Student → Fee Payment   Master-Detail   Store student fee payments

# 13. Picklists and Multi-Select Picklists

The project uses picklists for:

Gender

Student Status

Course Type

Course Status

Designation

Enrollment Status

Semester

Attendance Status

Payment Type

Payment Status

The Skills field on Student uses a Multi-Select Picklist.

Example values:

Java
Python
SQL
Salesforce
HTML
JavaScript

14. Global Value Sets

Global Value Sets can be used when the same picklist values need to be
reused.

Examples:

Student Status

Payment Status

This keeps picklist values consistent across objects.

16. Page Layouts

Page layouts organize fields so users can easily enter and view
information.

Student Page Layout Sections

Student Information

Academic Information

Address Information

17. Record Types

Two Student record types are used:

New Student

Existing student

Different page layouts can be assigned to these record types.

18. Validation Rules

Rule 1: Fee Amount must be greater than 0

Amount__c <= 0

Error message:

Payment Amount must be greater than 0.

Rule 2: Transaction ID required when payment is Paid

AND(
    ISPICKVAL(Payment_Status__c, "Paid"),
    ISBLANK(Transaction_ID__c)
)

Error message:

Transaction ID is required when Payment Status is Paid.

19. Duplicate and Matching Rules

A Student Matching Rule can be created using the Email field.

The Duplicate Rule can alert the user when a possible duplicate student
is entered.

Example:

Existing Student
Email: rahul@gmail.com

New Student
Email: rahul@gmail.com

→ Salesforce shows duplicate warning

# 20. Users, Profiles and Permission Sets

Users

The project can have users such as:

College Administrator

Finance Staff

# Profiles

Example profiles:

College Administrator

Faculty


Permission Set

A permission set such as Faculty Additional Access can provide extra
permissions to selected faculty users without changing their profile.

21. Activities

Salesforce Activities used in the project include:

Task

Example:

Call Susmitha Reddy regarding missing documents.

Event

Example:

Student Parent Meeting.

Log a Call

Example:

Called Rahul regarding fee payment.

22. Global Action

New Student Enquiry

A Global Action can allow staff to quickly create a new student enquiry
from a global Salesforce location.

Example fields:

First Name

Last Name

Email

Phone

Department

Admission Year

23. Object-Specific Action

Schedule Meeting

A Student object-specific action can be used to schedule a meeting
directly from a Student record.

24. Email Template

Fee Payment Confirmation

Subject:

Fee Payment Completed Successfully

Example message:

Dear Student,

Your fee payment has been successfully completed.

Payment Amount: ₹25,000
Payment Date: 30-09-2026
Payment Status: Paid
Transaction ID: TXN12345

Thank you.

Regards,
College Finance Department

25. Record-Triggered Flow

A Record-Triggered Flow is used for the fee payment confirmation.

Flow Name

Fee Payment Confirmation Flow

Trigger

Object:

Fee Payment

Condition:

Payment Status = Paid

Flow Process

Fee Payment
     ↓
Payment Status = Paid
     ↓
Record-Triggered Flow
     ↓
Send Email
     ↓
Student receives confirmation

This means that when a fee payment becomes Paid, Salesforce
automatically sends the payment confirmation email.

26. Reports

The project includes reports such as:

1. Students 

Shows students grouped by department.

2. Course Enrollment

Shows enrollment information for courses.

Shows student attendance information.

4. Fee Collection

Shows collected fee amounts.

5. Pending Fees

Shows fee payments whose status is Pending.

27. Dashboard

Dashboard Name

College Management Dashboard

Suggested components:

Total Students

Students by Department

Course Enrollment

Fee Collection

Pending Fees

Attendance Overview

Student Status

The dashboard gives college administrators a quick view of important
information.
 Schema Builder

Schema Builder is used to visually view the objects and relationships.

The main objects displayed are:

Department
Student
Course
Faculty
Enrollment
Attendance
Fee Payment

It helps administrators understand how the objects are connected.

30. Setup Audit Trail

Setup Audit Trail can be used to check Salesforce configuration changes.

Examples:

Custom object creation

Field creation

Page layout changes

Validation rule creation

Permission changes

31. Lightning Experience

The project is built using Salesforce Lightning Experience.

The College Management application can include navigation items such as:

Students

Departments

Courses

Faculty

Enrollments

Attendance

Fee Payments

Reports

Dashboards

32. Final Project Architecture

                 COLLEGE MANAGEMENT SYSTEM
                           |
       ---------------------------------------------
       |                    |                      |
   Department            Student                Course
       |                    |                      |
       |                    |                  Enrollment
       |                    |                      |
       |               Attendance <---------------+
       |                    |
       |               Fee Payment
       |
   Faculty

More specifically:

Department → Student
Department → Course
Department → Faculty

Student → Enrollment ← Course

Student → Attendance ← Course
                    ↑
                  Faculty

Student → Fee Payment

35. Conclusion

The College Management System combines Salesforce Administration
features into one practical project.

The system manages:

Students + Departments + Courses + Faculty + Enrollment + Attendance +
Fee Payments

It also demonstrates how Salesforce Admin features can be used to manage
data, control access, validate information, automate business processes,
and create reports and dashboards.
