# cit184
Oracle PL/SQL

/*-------------------------------------------------------------------------------
3.
For this question, you may have to run portions of the file SCOTT.SQL to create and populate SCOTT’s tables such as EMP. 

Create a trigger to fire 
    after an INSERT or UPDATE statement is issued on the EMP table owned by SCOTT. 
The trigger checks if the specified employee is making too much money! 
If the salary for this employee is $1000 or greater,   
    the trigger issues an error message stating that the salary is too high. 

Test your trigger and show the process.
-------------------------------------------------------------------------------*/

CREATE OR REPLACE TRIGGER t_emp_sal
    AFTER INSERT OR UPDATE
    ON EMP
    FOR EACH ROW
DECLARE
    lv_salary emp.sal%type;
BEGIN
    IF emp.sal < 1000
    THEN dbms_output.put_line('Salary is within accepted range');
    -- Predefined PL/SQL Exceptions
    ELSE RAISE_APPLICATION_ERROR(-20000, 'Salary is too high!');
    END IF;
END;
