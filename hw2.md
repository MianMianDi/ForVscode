2.9
1. The primary keys of the various relation schemas are as follows:
   + For branch:branch_name
   + For customer: customer_name,customer_street,customer_city
   + For loan:loan_number
   + For borrower:customer_name,loan_number
   + For account:account_number
   + For depositor:customer_name,account_number
2.  
   + For loan:branch_name referencing branch
   + For borrower:loan_number referencing loan
   + For account:branch_name referencing branch
   + For depositor:account_number referencing account



![hw2](C:\Users\Dell\Desktop\DatabaseSystem_2020\Homework\hw2\IMG_8599.JPG "IMG_8599.JPG")