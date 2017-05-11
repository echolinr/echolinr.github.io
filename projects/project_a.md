# HR Satisfaction Level Estimation System (HRSLES)

> This guide introduces how to use HRSLES.

## Visit the System

In your browser, visit the link https://dumbledorearmy.shinyapps.io/. 

## Get a satisfaction level

The system estimates an employee's satisfaction level based on that person's work information. 

To get a satisfaction level:

1. Select an answer for each item in the form. 
    - refer to [index](https://docsify.js.org/#/quickstart?id=loading-dialog) to see detailed description of each field.
2. Click `Caculate` to view the satisfacton level. The value is in a scale of 0 to 1.

## Add to database

If you wish to update the database with a new data, after selectiing all the answers, click `Add into the dataset`. Your input will be added into the database


## Provide feedback
The development team values your feedback. Please leave a comment. 

To provide feedback:
1. On the lower part of the page, enter your company name and your email address.
2. Rate the product on a scale of 0 to 10, 10 being the best score.
3. Type your comment on this product.
4. Click `Submit`.


## Index

- Name
    Name of the employee. value type: string.
- Last Evaluation
    Score of the employee in this last evaluation, on a scale of 0 to 1. value type: decimal.
- Number of Projects
    Number of projects the employeed has completed in the company. value tyep: integer.
- Average Monthly Hours
    Average number of working hours in one month of the employee. value type: integer.
- Time Spent in Company
    Number of years the employee has been working on this company, on a sclae of 0 to 12. value type: integer.
- Work Accident
    `yes` means there have beeen reported accident caused by the employee. `no` means there was not.
- Left
    `yes` means the employee has already left the compnay. `no` means the person is still a current employee.
- Promotion Within 5 Years
    `yes` means the employee has been promoted to higher position in the last five years. `no` mean not.
- Department
    Department to which the employee belongs.
- Salary
    Categroical value of the employee's salary. The categroy `low`, `medium`, `high` is defined by HR department's definition.

- Company Name
    the name of the company.

- Email Address
    Email address of HR staff who is using this system.
- Grade the product
    On a sclae of 0 to 10, how would you rate this system. 10 being the highest.
- Comment
    Comment for the system.